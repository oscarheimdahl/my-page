<script lang="ts">
  import Slash from './lib/Slash.svelte';
  let gridWidth = 0;
  if (window.innerWidth < 600) gridWidth = 30;
  else gridWidth = 50;
  const x = Math.floor(window.innerWidth / gridWidth);
  const y = Math.floor(window.innerHeight / gridWidth);

  const distanceFromCenter = (i: number) => {
    const dx = (i % x) * gridWidth + gridWidth;
    const dy = Math.floor((i / x) * gridWidth);
    return Math.hypot(dx - window.innerWidth / 2, dy - window.innerHeight / 2);
  };
</script>

<main style="--grid-width: {gridWidth}px">
  {#each Array(x * y) as _, i}
    {#if Math.random() > 0.8}
      <div class="spacer" />
    {:else}
      <Slash width={gridWidth} showDelay={2 * distanceFromCenter(i) + 1000} flipped={Math.random() > 0.5} />
    {/if}
  {/each}
</main>

<style lang="scss">
  main {
    display: flex;
    justify-content: center;
    width: 100%;
    height: 100%;
    flex-wrap: wrap;
    align-content: flex-start;
    overflow-y: hidden;
    background-color: var(--dark-main-1);

    .spacer {
      width: var(--grid-width);
    }
  }
</style>
