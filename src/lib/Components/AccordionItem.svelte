<script lang="ts">
  import { type Snippet } from "svelte";
  import { AccordionItemState } from "./Accordion.svelte.ts";
  import type { TransitionParams } from "./TransitionParams.ts";

  let {
    params,
    key,
    header,
    body,
  }: { params: TransitionParams; key: string; header: Snippet; body: Snippet } =
    $props();

  function handleToggle(): void {
    const newMap = new Map(AccordionItemState);
    newMap.set(key, !newMap.get(key));

    for (const [k] of newMap) {
      if (k !== key) {
        newMap.set(k, false);
      }
    }

    newMap.forEach((v, k) => {
      AccordionItemState.set(k, v);
    });
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
  {#if AccordionItemState.get(key)}
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
