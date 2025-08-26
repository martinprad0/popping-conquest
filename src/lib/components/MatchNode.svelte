<script lang="ts">
    import { Handle, Position, type NodeProps } from "@xyflow/svelte";

    // Variable props
    import { players, matches } from "$lib/global";
    import { Item } from "$lib/types/Item";
    import { Match } from "$lib/types/Match";
    let { data }: NodeProps = $props();
    let dlevel = data.dlevel;
    let j = data.j;
    // @ts-ignore:
    let id = `${j + 2 ** dlevel - 1}`;
    // Match logic function
    function matchIndex(id) {
        let idx = $matches.findIndex((match) => match.id === id);
        if (idx === -1) {
            // no existing match → append a new one
            const items: Item[] = [];
            $matches = [...$matches, new Match(id, items, 0)];
            idx = $matches.length - 1;
        }
        return idx;
    }
    function playerIndex(player_id) {
        return $players.findIndex((player) => player.id === player_id);
    }

    // Constants
    const matchWidth = "200px";
    const playerHeight = "50px";
    const flipDurationMs = 100;
    let i = matchIndex(id);

    // Animation
    import { fade } from "svelte/transition";
    import { flip } from "svelte/animate";

    // Drag and Drop Components
    import { dndzone } from "svelte-dnd-action";

    // Flowbite UI Components
    import { Button } from "flowbite-svelte";
    import { StarOutline } from "flowbite-svelte-icons";

    //
    let emptyStyle = $derived(
        $matches[i].items.length > 0
            ? ""
            : "box-sizing: border-box; border: 1px dashed gray; background-color: lightgray",
    );

    $effect(() => {
        if ($matches[i].id != id) {
            i = matchIndex(id);
        }

    });
</script>
<div class="flex flex-col items-center justify-center space-y-2 h-full w-full border-1 background-red">
<Handle type="target" position={Position.Left}  />
<Handle type="source" position={Position.Right} />
    
    {#each $matches[i].items as item (item.id)}
        {@const k = playerIndex(item.player_id)}

        <div class="flex items-center justify-center w-full">
            <p class="text-center player">{$players[k].name}</p>
        </div>
    {/each}
</div>
<style>
    .match {
        min-height: var(--player-height);
        width: var(--container-width);
        gap: 0em;
        padding: calc(var(--player-height) * 0.5) 0
            calc(var(--player-height) * 0.5) 0;
        /* border: 1px solid blue; */
    }
    .player {
        border-bottom: 1px solid black;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        z-index: 1;
        /* border: 1px solid red; */
        width: 100%;
        height: var(--player-height);
        background-color: var(--color-primary-800);
    }
    .winner {
        background-color: var(--color-primary-500);
    }
</style>
