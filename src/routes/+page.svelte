<script lang="ts">
  import Accordion from "$lib/Components/Accordion.svelte";
  import AccordionItem from "$lib/Components/AccordionItem.svelte";
  import CollapsibleCard from "$lib/Components/CollapsibleCard.svelte";
  import type { TransitionParams } from "$lib/Components/TransitionParams.js";
  import { fade, slide } from "svelte/transition";

  let accordionParams: TransitionParams = {
    transition: slide,
  };
</script>

<div>
  <CollapsibleCard params={{ transition: fade }}>
    {#snippet header()}
      <div>Card</div>
    {/snippet}
    {#snippet body()}
      <div>This is a card</div>
    {/snippet}
  </CollapsibleCard>
  <Accordion>
    {#snippet item1(key)}
      <AccordionItem {key} params={accordionParams}>
        {#snippet header()}
          <div>First Item!</div>
        {/snippet}
        {#snippet body()}
          <div>Lorem ipsum!</div>
        {/snippet}
      </AccordionItem>
    {/snippet}
    {#snippet item2(key)}
      <AccordionItem {key} params={accordionParams}>
        {#snippet header()}
          <div>Second Item!</div>
        {/snippet}
        {#snippet body()}
          <div>Lorem ipsum!</div>
        {/snippet}
      </AccordionItem>
    {/snippet}
    {#snippet item3(key)}
      <AccordionItem {key} params={accordionParams}>
        {#snippet header()}
          <div>Third Item!</div>
        {/snippet}
        {#snippet body()}
          <div>Lorem ipsum!</div>
        {/snippet}
      </AccordionItem>
    {/snippet}
  </Accordion>
</div>
