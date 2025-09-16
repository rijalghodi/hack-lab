<script module lang="ts">
  import {
    Background,
    Controls,
    MiniMap,
    Panel,
    Position,
    SvelteFlow,
    type Edge,
    type Node
  } from '@xyflow/svelte';
  import { ChipNode } from '@/lib/components/flow/chip';
  import { WireEdge } from '@/lib/components/flow/wire';
  import '@xyflow/svelte/dist/style.css';
  import type { Chip } from '@/lib/components/flow/type';
  const nodeTypes = { chip: ChipNode };
  const edgeTypes = { wire: WireEdge };
</script>

<script lang="ts">
  import { useSvelteFlow, type OnConnectEnd } from '@xyflow/svelte';

  let nodes = $state.raw<Node<Omit<Chip, 'id'>>[]>([
    {
      id: '0',
      position: { x: 0, y: 100 },
      data: {
        name: 'ABC',
        ports: [
          { id: 'in', name: 'in', type: 'input' },
          { id: 'out', name: 'out', type: 'output' }
        ]
      },
      type: 'chip'
    }
  ]);
  let edges = $state.raw<Edge[]>([
    // {
    //   id: 'e1-2',
    //   source: '0',
    //   target: '2',
    //   type: 'smoothstep',
    //   label: 'to'
    //   // style: 'stroke: #f00; stroke-dasharray: 5 5;'
    // }
  ]);

  const { screenToFlowPosition } = useSvelteFlow();

  const handleConnectEnd: OnConnectEnd = (event, connectionState) => {
    if (connectionState.isValid) return;

    const sourceNodeId = connectionState.fromNode?.id ?? '0';

    const id = crypto.randomUUID();
    const { clientX, clientY } = 'changedTouches' in event ? event.changedTouches[0] : event;

    const newNode: Node<Omit<Chip, 'id'>> = {
      id,
      data: {
        name: `Node ${id.slice(0, 5)}`,
        ports: [
          { id: 'in', name: 'in', type: 'input' },
          { id: 'out', name: 'out', type: 'output' }
        ]
      },
      // project the screen coordinates to pane coordinates
      position: screenToFlowPosition({
        x: clientX,
        y: clientY
      }),
      // set the origin of the new node so it is centered
      origin: [0.0, 0.5],
      type: 'chip'
    };
    nodes = [...nodes, newNode];
    edges = [
      ...edges,
      {
        source: sourceNodeId,
        target: id,
        id: `${sourceNodeId}--${id}`,
        type: 'smoothstep'
      }
    ];
  };
</script>

<SvelteFlow
  bind:nodes
  bind:edges
  fitView
  {nodeTypes}
  {edgeTypes}
  onconnectend={handleConnectEnd}
  colorMode="dark"
  defaultEdgeOptions={{
    type: 'smoothstep'
  }}
>
  <Background />
  <MiniMap />
  <Controls />
  <Panel position="top-left">
    <h1>My Flow</h1>
  </Panel>
</SvelteFlow>
