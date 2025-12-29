# svelte5-collapsible

Rewrite of [svelte-collapsible](https://github.com/rsdavis/svelte-collapsible/) to support svelte5 syntax. 

## Installation

```bash
npm install svelte5-collapse
```

## Components

### CollapsibleCard

Standalone collapsible card with transitions.

```svelte
<script>
	import { CollapsibleCard } from 'svelte5-collapse';
	import { fade } from 'svelte/transition';
</script>

<CollapsibleCard transition={{ transition: fade }}>
  {#snippet header()}
    <div>Card Header</div>
  {/snippet}
  {#snippet body()}
    <div>Card content here</div>
  {/snippet}
</CollapsibleCard>
```

### Accordion

Collection where only one item is open at a time.

```svelte
<script>
import { Accordion, AccordionItem } from 'svelte5-collapse';
</script>


<Accordion>
  {#snippet item1(key)}
    <AccordionItem {key} transition={accordionParams}>
      {#snippet header()}
        <div>First Item</div>
      {/snippet}
      {#snippet body()}
        <div>Hello from first item</div>
      {/snippet}
    </AccordionItem>
  {/snippet}
  {#snippet item2(key)}
    <AccordionItem {key} transition={accordionParams}>
      {#snippet header()}
        <div>Second Item</div>
      {/snippet}
      {#snippet body()}
        <div>Hello from second item</div>
      {/snippet}
    </AccordionItem>
  {/snippet}
</Accordion>
```

## Api

**CollapsibleCard:**
- `transition`: `TransitionParams`
- `transitionIn?`: `TransitionParams`
- `transitionOut?`: `TransitionParams`
- `isOpen?`: boolean (default: false)
- `header`: Snippet
- `body`: Snippet

**Accordion**
- `itemN`: Snippet function (e.g., `item1`, `item2`, etc.)
> Support for changing the item name will come soon™

**AccordionItem:**
- `transition`: `TransitionParams`
- `transitionIn?`: `TransitionParams`
- `transitionOut?`: `TransitionParams` 
-  `header`: Snippet
- `body`: Snippet

**TransitionParams:**
- `transition`: Transition type (svelte/transition)
-  `easing`: EasingFunction (svelte/transition)
- `duration`: Duration of the animation in ms
-  `delay`: Time before the animation starts in ms

