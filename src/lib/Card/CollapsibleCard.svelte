<script lang="ts">
  import type { Snippet } from "svelte";
  import {
    type EasingFunction,
    type TransitionConfig,
  } from "svelte/transition";

  let {
    transition,
    easing,
    duration,
    delay,
    isOpen,
    header,
    body,
  }: {
    transition: (node: Element, params?: any) => TransitionConfig;
    easing?: EasingFunction;
    duration?: number;
    delay?: number;
    isOpen?: boolean;
    header: Snippet;
    body: Snippet;
  } = $props();

  function handleToggle(): void {
    isOpen = !isOpen;
  }
</script>

<div>
  <button type="button" class="card-header" onclick={handleToggle}>
    {@render header()}
  </button>

  {#if isOpen}
    <div
      class="card-body"
      in:transition={{
        delay: delay,
        duration: duration,
        easing: easing,
      }}
      out:transition={{
        delay: delay,
        duration: duration,
        easing: easing,
      }}
    >
      {@render body()}
    </div>
  {/if}
</div>
