<script lang="ts">
  import { Handle, Position, type NodeProps } from '@xyflow/svelte';
  let { data }: NodeProps = $props();
</script>

<div class="triangle-node">
  <svg width="120" height="100" viewBox="0 0 120 100">
    <!-- Triangle shape -->
    <polygon points="60,10 10,90 110,90" fill="#4caf50" stroke="#2e7d32" stroke-width="3" />

    <!-- Text label centered inside the triangle -->
    <text
      x="60"
      y="60"
      fill="white"
      font-weight="bold"
      font-size="16"
      text-anchor="middle"
      dominant-baseline="middle"
    >
      {data.label}
    </text>
  </svg>
</div>

<!-- Connection handles -->
<Handle type="target" position={Position.Top} style="top: 0; left: 50%;" />
<Handle type="source" position={Position.Bottom} style="bottom: 0; left: 50%;" />

<style>
  .triangle-node {
    user-select: none;
    cursor: move;
  }
</style>
