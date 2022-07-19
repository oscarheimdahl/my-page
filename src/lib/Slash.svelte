<script lang="ts">
  import { onMount } from 'svelte';
  export let flipped: boolean;
  export let showDelay: number;
  export let width: number;

  const viewBox = '0 0 10 10';
  let opacity = 0;

  onMount(() => {
    setTimeout(() => {
      opacity = 1;
      setTimeout(() => {
        opacity = 0.1;
      }, 2000);
    }, showDelay);
  });
</script>

<section style="--width-as: {width}px; --opacity: {opacity};">
  {#if flipped}
    <svg {viewBox}>
      <path d="M0 0 l10 10" />
    </svg>
  {:else}
    <svg {viewBox}>
      <path d="M10 0 l-10 10" />
    </svg>
  {/if}
</section>

<style lang="scss">
  section {
    height: var(--width-as);
    width: var(--width-as);
    opacity: var(--opacity);
    transition: opacity 1000ms;
  }
  svg {
    stroke: var(--dark-accent-1);
    stroke-width: 0.4;
    width: 100%;
    height: 100%;
    transition: stroke 6000ms;
  }
</style>
