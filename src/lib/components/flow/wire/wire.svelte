<script lang="ts">
  import { BaseEdge, getSmoothStepPath, type EdgeProps, Position } from '@xyflow/svelte';
  let {
    sourceX,
    sourceY,
    targetX,
    targetY,
    sourcePosition = Position.Right,
    targetPosition = Position.Left
  }: EdgeProps = $props();

  // 20px radius for the corners
  let [edgePath] = getSmoothStepPath({
    sourceX,
    sourceY,
    sourcePosition,
    targetX,
    targetY,
    targetPosition,
    borderRadius: 20 // Adjust for more or less rounded corners
  });
</script>

<BaseEdge path={edgePath} />
