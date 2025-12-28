<script lang="ts" module>
  import type { Snippet } from "svelte";
  import { AccordionItemState } from "./Accordion.svelte.ts";

  export type AccordionProps = {
    [key in `item${number}`]: Snippet<[string]>;
  };
</script>

<script lang="ts">
  let props: AccordionProps = $props();
  let prefix = "item";

  let itemsNames = Object.keys(props).filter((key) =>
    key.match(new RegExp(`^${prefix}\\d+$`)),
  );

  let elements: Array<Snippet<[string]>> = itemsNames.map(
    (key: any) => props[key],
  );

  for (let i = 0; i < itemsNames.length; i++) {
    AccordionItemState.set(itemsNames[i], false);
  }
</script>

<div class="accordion">
  {#each elements as element, idx}
    {@render element(itemsNames[idx])}
  {/each}
</div>
