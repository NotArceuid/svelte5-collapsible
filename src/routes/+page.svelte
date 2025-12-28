<script>
  import Accordion from "$lib/Accordion/Accordion.svelte";
  import AccordionItem from "$lib/Accordion/AccordionItem.svelte";
  import CollapsibleCard from "$lib/Card/CollapsibleCard.svelte";
  import { fade } from "svelte/transition";
</script>

<div>
  <CollapsibleCard transition={fade}>
    {#snippet header()}
      <div>Hello World!</div>
    {/snippet}
    {#snippet body()}
      <div>Lorem ipsum dolor sit amet</div>
    {/snippet}
  </CollapsibleCard>

  <Accordion>
    {#snippet item1(key)}
      <AccordionItem {key}>
        {#snippet header()}
          <div>First Item!</div>
        {/snippet}
        {#snippet body()}
          <div>Lorem ipsum!</div>
        {/snippet}
      </AccordionItem>
    {/snippet}
    {#snippet item2(key)}
      <AccordionItem {key}>
        {#snippet header()}
          <div>First Item!</div>
        {/snippet}
        {#snippet body()}
          <div>Lorem ipsum!</div>
        {/snippet}
      </AccordionItem>
    {/snippet}
  </Accordion>
</div>
