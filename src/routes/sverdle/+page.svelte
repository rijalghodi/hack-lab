<script lang="ts">
  import { enhance } from '$app/forms';
  import { confetti } from '@neoconfetti/svelte';
  import type { ActionData, PageData } from './$types';
  import { MediaQuery } from 'svelte/reactivity';

  interface Props {
    data: PageData;
    form: ActionData;
  }
  let { data, form = $bindable() }: Props = $props();

  /** Whether the user prefers reduced motion */
  const reducedMotion = new MediaQuery('(prefers-reduced-motion: reduce)');

  /** Whether or not the user has won */
  let won = $derived(data.answers.at(-1) === 'xxxxx');

  /** The index of the current guess */
  let i = $derived(won ? -1 : data.answers.length);

  /** The current guess */
  let currentGuess = $derived(data.guesses[i] || '');

  /** Whether the current guess can be submitted */
  let submittable = $derived(currentGuess.length === 5);

  const { classnames, description } = $derived.by(() => {
    /**
     * A map of classnames for all letters that have been guessed,
     * used for styling the keyboard
     */
    let classnames: Record<string, 'exact' | 'close' | 'missing'> = {};
    /**
     * A map of descriptions for all letters that have been guessed,
     * used for adding text for assistive technology (e.g. screen readers)
     */
    let description: Record<string, string> = {};
    data.answers.forEach((answer, i) => {
      const guess = data.guesses[i];
      for (let i = 0; i < 5; i += 1) {
        const letter = guess[i];
        if (answer[i] === 'x') {
          classnames[letter] = 'exact';
          description[letter] = 'correct';
        } else if (!classnames[letter]) {
          classnames[letter] = answer[i] === 'c' ? 'close' : 'missing';
          description[letter] = answer[i] === 'c' ? 'present' : 'absent';
        }
      }
    });
    return { classnames, description };
  });

  /**
   * Modify the game state without making a trip to the server,
   * if client-side JavaScript is enabled
   */
  function update(event: MouseEvent) {
    event.preventDefault();
    const key = (event.target as HTMLButtonElement).getAttribute('data-key');

    if (key === 'backspace') {
      currentGuess = currentGuess.slice(0, -1);
      if (form?.badGuess) form.badGuess = false;
    } else if (currentGuess.length < 5) {
      currentGuess += key;
    }
  }

  /**
   * Trigger form logic in response to a keydown event, so that
   * desktop users can use the keyboard to play the game
   */
  function keydown(event: KeyboardEvent) {
    if (event.metaKey) return;

    if (event.key === 'Enter' && !submittable) return;

    document
      .querySelector(`[data-key="${event.key}" i]`)
      ?.dispatchEvent(new MouseEvent('click', { cancelable: true, bubbles: true }));
  }
</script>

<svelte:window onkeydown={keydown} />

<svelte:head>
  <title>Sverdle</title>
  <meta name="description" content="A Wordle clone written in SvelteKit" />
</svelte:head>

<h1 class="visually-hidden">Sverdle</h1>

<form
  method="post"
  action="?/enter"
  use:enhance={() => {
    // prevent default callback from resetting the form
    return ({ update }) => {
      update({ reset: false });
    };
  }}
>
  <a class="how-to-play" href="/sverdle/how-to-play">How to play</a>

  <div class="grid" class:playing={!won} class:bad-guess={form?.badGuess}>
    {#each Array.from(Array(6).keys()) as row (row)}
      {@const current = row === i}
      <h2 class="visually-hidden">Row {row + 1}</h2>
      <div class="row" class:current>
        {#each Array.from(Array(5).keys()) as column (column)}
          {@const guess = current ? currentGuess : data.guesses[row]}
          {@const answer = data.answers[row]?.[column]}
          {@const value = guess?.[column] ?? ''}
          {@const selected = current && column === guess.length}
          {@const exact = answer === 'x'}
          {@const close = answer === 'c'}
          {@const missing = answer === '_'}
          <div class="letter" class:exact class:close class:missing class:selected>
            {value}
            <span class="visually-hidden">
              {#if exact}
                (correct)
              {:else if close}
                (present)
              {:else if missing}
                (absent)
              {:else}
                empty
              {/if}
            </span>
            <input name="guess" disabled={!current} type="hidden" {value} />
          </div>
        {/each}
      </div>
    {/each}
  </div>

  <div class="controls">
    {#if won || data.answers.length >= 6}
      {#if !won && data.answer}
        <p>the answer was "{data.answer}"</p>
      {/if}
      <button data-key="enter" class="restart selected" formaction="?/restart">
        {won ? 'you won :)' : `game over :(`} play again?
      </button>
    {:else}
      <div class="keyboard">
        <button data-key="enter" class:selected={submittable} disabled={!submittable}>enter</button>

        <button
          onclick={update}
          data-key="backspace"
          formaction="?/update"
          name="key"
          value="backspace"
        >
          back
        </button>

        {#each ['qwertyuiop', 'asdfghjkl', 'zxcvbnm'] as row (row)}
          <div class="row">
            {#each row as letter, index (index)}
              <button
                onclick={update}
                data-key={letter}
                class={classnames[letter]}
                disabled={submittable}
                formaction="?/update"
                name="key"
                value={letter}
                aria-label="{letter} {description[letter] || ''}"
              >
                {letter}
              </button>
            {/each}
          </div>
        {/each}
      </div>
    {/if}
  </div>
</form>

{#if won}
  <div
    style="position: absolute; left: 50%; top: 30%"
    use:confetti={{
      particleCount: reducedMotion.current ? 0 : undefined,
      force: 0.7,
      stageWidth: window.innerWidth,
      stageHeight: window.innerHeight,
      colors: ['#ff3e00', '#40b3ff', '#676778']
    }}
  ></div>
{/if}
