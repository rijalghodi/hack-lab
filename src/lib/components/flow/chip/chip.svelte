<script lang="ts">
  import { Handle, Position, type Node, type NodeProps } from '@xyflow/svelte';
  import type { Chip } from '@/lib/components/flow/type';

  const { data }: NodeProps<Node<Omit<Chip, 'id'>>> = $props();
  const { name, label, ports } = data;
</script>

<div
  class="chip-node relative w-20 rounded-md border border-gray-300 bg-background p-2 hover:border-white hover:shadow-md"
>
  <div class="text-center font-mono text-sm text-foreground">
    {label ?? name.toUpperCase()}
  </div>
</div>

<!-- Connection handles -->
{#each ports as port}
  <Handle
    type={port.type === 'input' ? 'target' : 'source'}
    position={port.type === 'input' ? Position.Left : Position.Right}
    style="width: 8px; height: 8px;"
    class="hover:bg-red-500"
  />
{/each}

<!-- <style>
  .chip-node {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    position: relative;
    display: flex;
    width: 100px;
    align-items: center;
    justify-content: center;
    border-radius: 0.375rem;
    border: 1px solid #d1d5db;
    background: #fff;
    padding: 0.5rem;
  }
  .label {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style> -->
