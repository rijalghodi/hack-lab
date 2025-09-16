<script module lang="ts">
  import '@xyflow/svelte/dist/base.css';
  import Circuit from '@/lib/components/flow/circuuit/circuit.svelte';
  import { SvelteFlowProvider } from '@xyflow/svelte';
</script>

<script lang="ts">
</script>

<div style:width="100vw" style:height="100vh">
  <SvelteFlowProvider>
    <Circuit />
  </SvelteFlowProvider>
</div>
