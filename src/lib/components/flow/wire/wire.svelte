<script lang="ts">
  import { BaseEdge, getBezierPath, type EdgeProps } from '@xyflow/svelte';

  let { sourceX, sourceY, targetX, targetY, ...props }: EdgeProps = $props();

  const [edgePath] = $derived(
    getBezierPath({
      sourceX,
      sourceY,
      targetX,
      targetY
    })
  );

  $inspect(edgePath);

  const { markerStart, markerEnd, interactionWidth, label, labelStyle } = props;
</script>

<BaseEdge path={edgePath} {markerStart} {markerEnd} {interactionWidth} {label} {labelStyle} />
