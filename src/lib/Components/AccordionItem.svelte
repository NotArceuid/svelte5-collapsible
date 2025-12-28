<script lang="ts">
  import { getContext, type Snippet } from "svelte";
  import type { TransitionParams } from "./TransitionParams.ts";
  import type { SvelteMap } from "svelte/reactivity";

  let {
    params,
    key,
    header,
    body,
  }: { params: TransitionParams; key: string; header: Snippet; body: Snippet } =
    $props();

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
</li>
