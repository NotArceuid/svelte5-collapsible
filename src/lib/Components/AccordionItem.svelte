<script lang="ts">
  import { getContext, type Snippet } from "svelte";
  import type { TransitionParams } from "./TransitionParams.d.ts";
  import type { SvelteMap } from "svelte/reactivity";

  let {
    transition,
    transitionIn = transition,
    transitionOut = transition,
    key,
    header,
    body,
  }: {
    transition: TransitionParams;
    transitionIn?: TransitionParams;
    transitionOut?: TransitionParams;
    key: string;
    header: Snippet;
    body: Snippet;
  } = $props();

  const store: SvelteMap<string, boolean> = getContext("accordion");
  function handleToggle(): void {
    store.forEach((_, k) => {
      if (k != key) {
        store.set(k, false);
      }
    });
    store.set(key, !store.get(key));
  }
</script>

<li>
  <div
    role="button"
    onkeydown={handleToggle}
    tabindex="0"
    onclick={handleToggle}
  >
    {@render header()}
  </div>
  {#if store.get(key)}
    <div
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
</li>
