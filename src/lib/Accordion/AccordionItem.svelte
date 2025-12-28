<!-- AccordionItem.svelte -->
<script lang="ts">
  import { type Snippet } from "svelte";
  import { fade } from "svelte/transition";
  import { AccordionItemState } from "./Accordion.svelte.ts";

  let { key, header, body }: { key: string; header: Snippet; body: Snippet } =
    $props();

  function handleToggle(): void {
    const newMap = new Map(AccordionItemState);
    newMap.set(key, !newMap.get(key));

    // Close all other items
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

<li transition:fade>
  <button onclick={handleToggle}>
    {@render header()}
  </button>
  {#if AccordionItemState.get(key)}
    {@render body()}
  {/if}
</li>
