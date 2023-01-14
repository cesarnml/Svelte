# SvelteKitTutorial Notes

- [SvelteKitTutorial Notes](#sveltekittutorial-notes)
  - [Sections](#sections)
  - [Notes](#notes)
    - [Part 1: Welcome to Svelte](#part-1-welcome-to-svelte)
      - [Introduction](#introduction)
      - [Reactivity](#reactivity)
      - [Props](#props)
      - [Logic](#logic)

## Sections

- Part 1: Welcome to Svelte

* [x] ~~_Introduction_~~ [2023-01-14]
* [x] ~~_Reactivity_~~ [2023-01-14]
* [x] ~~_Props_~~ [2023-01-14]
* [x] ~~_Logic_~~ [2023-01-14]
* [ ] Events
* [ ] Bindings
* [ ] Lifecycle
* [ ] Stores

- Part 2: Introduction to SvelteKit

* [ ] Concepts
* [ ] Routing
* [ ] Loading data
* [ ] Forms
* [ ] API routes
* [ ] Errors and redirects
* [ ] Page options

- Part 3: Advanced Svelte

* [ ] Motion
* [ ] Transitions
* [ ] Animations
* [ ] Actions
* [ ] Advanced Bindings
* [ ] Classes
* [ ] Component composition
* [ ] Context API
* [ ] Special elements
* [ ] Module context
* [ ] Debugging
* [ ] Next steps

- Part 4: Advanced SvelteKit

* [ ] Hooks
* [ ] Stores
* [ ] Advanced routing
* [ ] Advanced loading
* [ ] Environment variables

## Notes

### Part 1: Welcome to Svelte

#### Introduction

- `Svelte` is a tool for building web apps via a declarative, component-based paradigm.
- A `component` is a self-contained block of code that encapsulates `HTML`, `CSS` and `JavaScript` that belong together.
- [[Shorthand attributes]] ... i.e. `<img src={src} />` becomes `<img {src} />`
- In Svelte, components are imported within a `<script>` tag

```jsx
<script>
  import Nested from './Nested.svelte'
</script>

<p>This is a paragraph.</p>
<Nested/>

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

- Component names are always capitalized, to distinguish them from HTML elements.
- To enable parsing HTML strings use `<p>{@html string}</p>`

#### Reactivity

- `Reactivity` is how Svelte keeps the DOM in sync with application state

```jsx
<script>
	let count = 0;

	function increment() {
    count += 1
	}
</script>

<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
```

- `reactive declarations` , `$: [expression or value]` are Svelte's version of computed properties. Multiple statements can be encased in a block-scope

```jsx
<script>
	let count = 0;

  $: doubled = count * 2;

	function handleClick() {
		count += 1;
	}
</script>

<button on:click={handleClick}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

<p>{count} doubled is {doubled}</p>
```

- Note: `Reactivity` is triggered via `assignments` (i.e. mutating methods won't trigger DOM updates)

#### Props

- `Props` are declared in components by via the `export` keyword in the `<script>`. An optional defaultValue can also be passed to exported props

```jsx
<script>
export let answer = [defaultValue];
<script>
```

- `Prop spreading` is possible via <Component {...object} /> syntax
- Within the template portion of a Svelte component,`$$props` can be referenced to access all props that were passed to a component
  - _Avoid do to poor optimization_

#### Logic

- `If/else if/else` block syntax:

```jsx
{#if [expression]}
// if conditional html
{:if else [expression]}
// else if conditional html
{:else}
// else conditional html
{/if}
```

- `Each` blocks:

```jsx
<ul>
{#each cats as cat, index}
<li key={cat.id}>#{index + 1} - {cat.name}</li>
{/each}
</ul>
```

- Of course, it's possible for a list to change order then we must use a `Keyed each` block:

```jsx
<ul>
{#each cats as cat, index (cat.id)}
<li key={cat.id}>#{index + 1} - {cat.name}</li>
{/each}
</ul>
```

- `Await` blocks

```jsx
{#await promise}
// render something while promise is resolved
{:then response}
// do something with response
{:catch error}
// do something with error
{/await}
```

- No loading state? No error handling? Then a shorthand version of the above Await block syntax is possible:

```jsx
{#await promise then response}
// do something with response
{/await}
```
