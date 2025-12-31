<script lang="ts">
  import type { Snippet } from "svelte";
  import type { TransitionParams } from "./TransitionParams.d.ts";
  let {
    transition,
    transitionIn = transition,
    transitionOut = transition,
    isOpen,
    header,
    body,
  }: {
    transition: TransitionParams;
    transitionIn?: TransitionParams;
    transitionOut?: TransitionParams;
    isOpen?: boolean;
    header: Snippet;
    body: Snippet;
  } = $props();

  function handleToggle(): void {
    isOpen = !isOpen;
  }
</script>

<div>
  <div
    tabindex="0"
    role="button"
    onkeydown={handleToggle}
    class="card-header"
    onclick={handleToggle}
  >
    {@render header()}
  </div>

  {#if isOpen}
    <div
      class="card-body"
      in:transitionIn.transition={{
        delay: transitionIn.delay,
        duration: transitionIn.duration,
        easing: transitionIn.easing,
      }}
      out:transitionOut.transition={{
        delay: transitionOut.delay,
        duration: transitionOut.duration,
        easing: transitionOut.easing,
      }}
    >
      {@render body()}
    </div>
  {/if}
</div>
