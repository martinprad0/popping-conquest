<script lang="ts">
    import * as utils from "$lib/tournamentUtils.js";
    import { SvelteFlow, Controls, Panel, Background } from "@xyflow/svelte";
    import MatchNode from "./MatchNode.svelte";
    import "@xyflow/svelte/dist/style.css";
    import { Item } from "$lib/types/Item";
    import { players, matches, depth } from "$lib/global";

    const nodeTypes = { matchNode: MatchNode };

    let nodes = $derived(utils.nodesGenerator($depth, $matches));

    let edges = $derived(utils.edgesGenerator($depth, $matches));

    import { onMount } from "svelte";
    import { loadGame } from "$lib/global";

    onMount(() => {
        const interval = setInterval( async () => {
            await loadGame();
        }, 5000);

        return () => {clearInterval(interval);
        }
    });

    $inspect($matches)
</script>

<div style="width: 100%; height: 40vh">
    <SvelteFlow
        bind:nodes
        bind:edges
        {nodeTypes}
        proOptions={{ hideAttribution: true }}
        fitView
    >
        <Controls />
    </SvelteFlow>
</div>

<style>
  :global(.svelte-flow) {
    background: transparent !important;
  }
</style>
