<script lang="ts">
  import '../app.css';

  let { children } = $props();
</script>

<svelte:head>
  <title>HackLab - Interactive Computer Architecture Learning</title>
  <meta
    name="description"
    content="Learn computer architecture from NAND gates to complete computers through interactive simulation and visualization."
  />
</svelte:head>

<div class="app dark">
  <main>
    {@render children()}
  </main>

  <footer class="py-4">
    <p class="text-center text-sm text-muted-foreground">Made by Rijal Ghodi</p>
  </footer>
</div>
