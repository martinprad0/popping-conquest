<script lang="ts">
    import { ButtonGroup, Button } from "flowbite-svelte";
    let navVisible = true;
    import { EyeOutline, EyeSlashOutline } from "flowbite-svelte-icons";
</script>

<header class="sticky top-0 left-0 right-0 z-50 h-32">
    <div
        class="flex justify-center items-center w-full h-full py-2 backdrop-blur-md bg-white/40 shadow-md"
    >
        <!-- Hamburger Button -->
        <div class="absolute left-4 top-1/2 -translate-y-1/2">
            <Button
                onclick={() => (navVisible = !navVisible)}
                class="p-2 bg-white/20 hover:bg-primary-500"
            >
                {#if navVisible}
                    <EyeOutline />
                {:else}
                    <EyeSlashOutline />
                {/if}
            </Button>
        </div>

        <!-- Logo -->
        <div
            class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2"
        >
            <img
                src="assets/banner.svg"
                alt="Banner"
                class="h-24 object-contain"
            />
        </div>
    </div>
    {#if navVisible}
        <ButtonGroup
            class="bg-white/40 shadow-md *:ring-primary-700! *:rounded-t-none *:rounded-b-md *:border-2 *:border-primary-200"
        >
            <Button href="/">Inicio</Button>
            <Button href="/live">Transmisión</Button>
            <Button href="/sevenToSmoke">7-To-Smoke</Button>
            <Button href="/openStyle">Open Style</Button>
        </ButtonGroup>
    {/if}
</header>
