<script lang="ts">
  import '../app.css';
  import Header from '$lib/components/Header.svelte';
  import { onMount } from 'svelte';
  
  let vantaContainer: HTMLDivElement;
  
  onMount(() => {
    // @ts-ignore
    const effect = window.VANTA.FOG({
      el: vantaContainer,
      mouseControls: true,
      touchControls: true,
      gyroControls: false,
      minHeight: 200.00,
      minWidth: 200.00,
      highlightColor: 0xEB0D7A,
      midtoneColor: 0xDA5FAB,
      lowlightColor: 0x3010c3,
      baseColor: 0xffffff,
      blurFactor: 0.35,
      speed: 1.7,
      zoom: 1.20
    });
  
    return () => effect?.destroy?.();
  });
</script>

<style>
  .vanta-bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: -1;
  }
</style>

<div  bind:this={vantaContainer} class="vanta-bg"></div>

<Header />
<slot />
