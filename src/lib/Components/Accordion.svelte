<script lang="ts">
  import { setContext, type Snippet } from "svelte";
  import { SvelteMap } from "svelte/reactivity";

  export type AccordionProps = {
    [key: string]: Snippet<[string]>;
  };

  let props: AccordionProps = $props();

  let itemsNames = Object.keys(props).filter((key) => {
    const pattern = new RegExp(`^item\\d+$`);
    return pattern.test(key);
  });

  let elements: Array<Snippet<[string]>> = itemsNames.map(
    (key: string) => props[key],
  );

  let accordionMap = new SvelteMap<string, boolean>();
  itemsNames.forEach((x) => {
    accordionMap.set(x, false);
  });

  setContext("accordion", accordionMap);
</script>

<div class="accordion">
  {#each elements as element, idx}
    {@render element(itemsNames[idx])}
  {/each}
</div>
