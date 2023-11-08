---
title: '⚡ Svelte: Export a "class" Property'
description: How to export a property called "class"
date: 2023-11-07T20:55:23-05:00
publishDate: 2023-11-07T20:55:23-05:00
tags: [Svelte]
showReadingTime: true
showToc: false
tocOpen: false
---

## Svelte

I recently started contributing to an Open Source Project, [Immich][immich], which uses a [Svelte](svelte) frontend. Svelte has been great to work with so far. I especially like the easy, intuitive way it handles binding properties and events for Svelte Components.

### Props

For example, pass data to a component via a property:

```svelte
<MyComponent enabled={true} />
```

```svelte
// my-component.svelte
<script lang="ts">
  export let enabled: boolean;
</script>

{#if !enabled}
 <span>I'm enabled! 😂</span>
{:else}
 <span>I'm not enabled. 😢</span>
{/if}
```

### Problem

Eventually, I wanted to export a property called `class`, hoping to allow class names to pass through to the underlying element. Something like this:

```svelte
<MyComponent class="custom-class" />
```

```svelte
// my-component.svelte
<script lang="ts">
  export let class = '';
</script>

<span {class}>Hello</span>
```

Well, it turns out, as you might have guessed, `export let class` is _invalid_ because `class` is a [reserved word][reserved].

### Solution

Luckily there is a solution to this, which takes advantage of an export _alias_. Basically this works just fine:

```svelte
// my-component.svelte
<script lang="ts">
  let className = '';
  export { className as class }
</script>

 <span class={className}>Hello</span>
{/if}
```

So there you have it! A way to use the `class` prop, even though it is a reserved word in the language.

[immich]: https://immich.app/
[svelte]: https://svelte.dev/
[reserved]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#reserved_words
