<script lang="ts">
  import { BaseEdge, EdgeLabel, getBezierPath, type EdgeProps } from '@xyflow/svelte';
  import { getSmoothStepPath } from '../utils/smooth-step-edge';

  let { sourceX, sourceY, targetX, targetY, sourcePosition, targetPosition, ...props }: EdgeProps =
    $props();

  const [edgePath, labelX, labelY, offsetX, offsetY] = $derived(
    getSmoothStepPath({
      sourceX,
      sourceY,
      targetX,
      targetY,
      targetPosition,
      sourcePosition,
      borderRadius: 10,
      offset: 10
    })
  );

  $inspect(labelX, labelY, offsetX, offsetY);

  const { markerStart, markerEnd, interactionWidth, label, labelStyle } = props;
</script>

<BaseEdge
  path={edgePath}
  {markerStart}
  {markerEnd}
  {interactionWidth}
  {label}
  {labelStyle}
  style="stroke-width: 2;"
/>

<EdgeLabel x={labelX} y={labelY} class="absolute">
  {label}
</EdgeLabel>
