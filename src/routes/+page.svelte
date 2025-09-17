<script lang="ts">
  import { Button } from '$lib/components/ui/button';
  import github from '$lib/images/github.svg';
  import svelteLogo from '$lib/images/svelte-logo.svg';
  import { Cpu, Eye, Settings, Code, BookOpen, Monitor, Play, Github } from '@lucide/svelte';
</script>

<!-- Header Section -->
<header
  class="w-full border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60"
>
  <div class="container mx-auto px-4 py-4">
    <div class="flex items-center justify-between">
      <!-- Logo -->
      <div class="flex items-center space-x-2">
        <!-- <img src={svelteLogo} alt="HackLab" class="h-8 w-8" /> -->
        <span class="font-mono text-xl font-bold text-foreground">HackLab</span>
      </div>

      <!-- Navigation -->
      <nav class="flex items-center space-x-4">
        <Button variant="outline" href="/lab">Enter Lab</Button>
        <Button variant="outline" size="icon" href="https://github.com/your-username/hack-lab">
          <Github class="h-5 w-5" />
        </Button>
      </nav>
    </div>
  </div>
</header>

<!-- Hero Section -->
<section class="px-4 py-20">
  <div class="container mx-auto max-w-6xl">
    <div class="grid grid-cols-1 items-center gap-12 lg:grid-cols-2">
      <!-- Hero Content -->
      <div class="space-y-8">
        <div class="space-y-4">
          <h1 class="text-5xl leading-snug font-bold tracking-tight text-foreground">
            Build Computers from
            <span class="text-primary">Scratch</span>
          </h1>
          <p class="text-xl leading-relaxed text-muted-foreground">
            HackLab is an interactive computer simulation inspired by <em>Nand to Tetris</em>. Learn
            how computers work by building them from the ground up, starting with simple NAND gates
            all the way to a complete machine capable of running high-level programs.
          </p>
        </div>

        <div class="flex flex-col gap-4 sm:flex-row">
          <Button size="lg" href="/lab">Start Building</Button>
          <Button variant="outline" size="lg" href="#features">Learn More</Button>
        </div>
      </div>

      <!-- Hero Image -->
      <div class="relative">
        <div
          class="flex aspect-square items-center justify-center rounded-2xl bg-gradient-to-br from-primary/20 to-primary/5 p-8"
        >
          <div class="space-y-4 text-center">
            <div
              class="mx-auto flex h-32 w-32 items-center justify-center rounded-full bg-primary/10"
            >
              <Cpu class="h-16 w-16 text-primary" />
            </div>
            <h3 class="text-2xl font-semibold text-foreground">Interactive Lab</h3>
            <p class="text-muted-foreground">Explore, build, and simulate</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
<!-- Video Section -->
<section id="video" class="px-4 py-20">
  <div class="container mx-auto max-w-6xl">
    <div class="overflow-hidden rounded-2xl border bg-card shadow-sm">
      <div class="flex aspect-video items-center justify-center bg-muted/50">
        <div class="space-y-4 p-8 text-center">
          <div
            class="mx-auto flex h-20 w-20 items-center justify-center rounded-full bg-primary/10"
          >
            <Play class="h-10 w-10 text-primary" />
          </div>
          <h3 class="text-2xl font-semibold text-foreground">See HackLab in Action</h3>
          <p class="mx-auto max-w-md text-muted-foreground">
            Watch how students learn computer architecture through interactive simulation and
            hands-on building.
          </p>
          <Button size="lg" class="mt-4">Watch Demo Video</Button>
        </div>
      </div>
    </div>
  </div>
</section>
<!-- Features Section -->
<section id="features" class="bg-muted/30 px-4 py-20">
  <div class="container mx-auto max-w-6xl">
    <div class="mb-16 space-y-4 text-center">
      <h2 class="text-4xl font-bold text-foreground">Why HackLab?</h2>
      <p class="mx-auto max-w-3xl text-xl text-muted-foreground">
        Experience computer architecture like never before through hands-on exploration and
        interactive visualization.
      </p>
    </div>

    <div class="mb-16 grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
      <!-- Feature 1 -->
      <div class="rounded-lg border bg-card p-6 shadow-sm transition-shadow hover:shadow-md">
        <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-lg bg-primary/10">
          <Cpu class="h-6 w-6 text-primary" />
        </div>
        <h3 class="mb-2 text-xl font-semibold">Hierarchical Visualization</h3>
        <p class="text-muted-foreground">
          Explore the complete structure from NAND gates, flip-flops, registers, ALU, CPU, RAM, up
          to the complete Hack computer.
        </p>
      </div>

      <!-- Feature 2 -->
      <div class="rounded-lg border bg-card p-6 shadow-sm transition-shadow hover:shadow-md">
        <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-lg bg-primary/10">
          <Eye class="h-6 w-6 text-primary" />
        </div>
        <h3 class="mb-2 text-xl font-semibold">Exploration Mode</h3>
        <p class="text-muted-foreground">
          Click on any block to reveal its implementation, either in HDL (Hardware Description
          Language) or basic logic composition.
        </p>
      </div>

      <!-- Feature 3 -->
      <div class="rounded-lg border bg-card p-6 shadow-sm transition-shadow hover:shadow-md">
        <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-lg bg-primary/10">
          <Settings class="h-6 w-6 text-primary" />
        </div>
        <h3 class="mb-2 text-xl font-semibold">Interactive Simulation</h3>
        <p class="text-muted-foreground">
          Design or replicate components, run them, and verify against specifications in real-time.
        </p>
      </div>

      <!-- Feature 4 -->
      <div class="rounded-lg border bg-card p-6 shadow-sm transition-shadow hover:shadow-md">
        <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-lg bg-primary/10">
          <Code class="h-6 w-6 text-primary" />
        </div>
        <h3 class="mb-2 text-xl font-semibold">Hack Language Support</h3>
        <p class="text-muted-foreground">
          Load and execute programs written in Hack assembly, and run higher-level Jack code on your
          simulated computer.
        </p>
      </div>

      <!-- Feature 5 -->
      <div class="rounded-lg border bg-card p-6 shadow-sm transition-shadow hover:shadow-md">
        <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-lg bg-primary/10">
          <BookOpen class="h-6 w-6 text-primary" />
        </div>
        <h3 class="mb-2 text-xl font-semibold">Educational Focus</h3>
        <p class="text-muted-foreground">
          Bridges theoretical computer science with hands-on practice, showing the full path from
          bit to operating system.
        </p>
      </div>

      <!-- Feature 6 -->
      <div class="rounded-lg border bg-card p-6 shadow-sm transition-shadow hover:shadow-md">
        <div class="mb-4 flex h-12 w-12 items-center justify-center rounded-lg bg-primary/10">
          <Monitor class="h-6 w-6 text-primary" />
        </div>
        <h3 class="mb-2 text-xl font-semibold">Visual Learning</h3>
        <p class="text-muted-foreground">
          Make learning computer architecture tangible through direct exploration, experimentation,
          and visualization.
        </p>
      </div>
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="px-4 py-20">
  <div class="container mx-auto max-w-4xl text-center">
    <div class="space-y-8">
      <h2 class="text-4xl font-bold text-foreground">Ready to Build Your First Computer?</h2>
      <p class="text-xl text-muted-foreground">
        Join thousands of students learning computer architecture through interactive simulation.
      </p>
      <div class="flex flex-col justify-center gap-4 sm:flex-row">
        <Button size="lg" href="/lab">Start Building Now</Button>
      </div>
    </div>
  </div>
</section>
