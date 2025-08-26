<script lang="ts">
    import TournamentShowcase from "$lib/components/TournamentShowcase.svelte";
    import { players, matches, depth } from "$lib/global";

    // Firebase Functions
    import { loadGame, pushGame } from "$lib/global";

    import { onMount } from "svelte";
    onMount(async () => {
        await loadGame();
    });
</script>
<div class="w-full mt-12">
        <div
            class="flex w-[90%] max-w-[500px] h-20 mx-auto items-center justify-center mb-6 bg-white/70 shadow-md px-6 py-4 border-0 border-primary-200 rounded"
        >
            <h1>Open Style</h1>
        </div>
</div>

<TournamentShowcase></TournamentShowcase>