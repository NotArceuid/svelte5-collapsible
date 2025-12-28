<script lang="ts">
  import type { Snippet } from "svelte";
  import type { TransitionParams } from "./TransitionParams.ts";
  let {
    params,
    isOpen,
    header,
    body,
  }: {
    params: TransitionParams;
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
      in:params.transition={{
        delay: params.delay,
        duration: params.duration,
        easing: params.easing,
      }}
      out:params.transition={{
        delay: params.delay,
        duration: params.duration,
        easing: params.easing,
      }}
    >
      {@render body()}
    </div>
  {/if}
</div>
