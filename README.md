### Learning svelte

- define props :

```
<script>
    export let prop // Need to export prop value
</script>  
```

- default value for prop
```
export let prop = 'its default value'
```

- spread props:
```
<script>
	import Info from './Info.svelte';

	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};
</script>

<Info name={pkg.name} version={pkg.version} speed={pkg.speed} website={pkg.website}/>
<Info {...pkg}/>
```

## Logic

- conditions:
```
<script>
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}
</script>

{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{/if}

{#if !user.loggedIn}
	<button on:click={toggle}>
		Log in
	</button>
{/if}
```

- if else:
```
<script>
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}
</script>

{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}
```
- if else elseif:
```
<script>
	let x = 7;
</script>

{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}
```

### LOOPS

```
{#each cats as cat}
    <li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
        {cat.name}
    </a></li>
{/each}
{#each cats as cat, i}
	<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
		{i + 1}: {cat.name}
	</a></li>
{/each}
```

### Keys
```
{#each things as thing (thing.id)}
	<Thing current={thing.color}/>
{/each}
```

### Await blocks
```
{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
```

### DOM events
```
<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>
```

## Inline handlers
```
<div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m.x} x {m.y}
</div>
```

## handler modifiers
```
<script>
	function handleClick() {
		alert('no more alerts')
	}
</script>

<button on:click|once={handleClick}>
	Click me
</button>
```
- preventDefault — calls event.preventDefault() before running the handler. Useful for client-side form handling, for example.
- stopPropagation — calls event.stopPropagation(), preventing the event reaching the next element
- passive — improves scrolling performance on touch/wheel events (Svelte will add it automatically where it's safe to do so)
- nonpassive — explicitly set passive: false
- capture — fires the handler during the capture phase instead of the bubbling phase ()
- once — remove the handler after the first time it runs
- self — only trigger handler if event.target is the element itself


## Events
```
<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function sayHello() {
		dispatch('message', {
			text: 'Hello!'
		});
	}
</script>
```

## Forward events up
- Inner.svelte
```
<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function sayHello() {
		dispatch('message', {
			text: 'Hello!'
		});
	}
</script>

<button on:click={sayHello}>
	Click to say hello
</button>
```

- Outer.svelte
```
<script>
	import Inner from './Inner.svelte';
</script>

<Inner on:message/>
```

- App.svelte
```
<script>
	import Outer from './Outer.svelte';

	function handleMessage(event) {
		alert(event.detail.text);
	}
</script>

<Outer on:message={handleMessage}/>
```

## some more events forward
- App.svelte
```
<script>
	import CustomButton from './CustomButton.svelte';

	function handleClick() {
		alert('clicked');
	}
</script>

<CustomButton on:click={handleClick}/>
```

- CustomButton.svelte
```
<button>
	Click me
</button>
```

### Data bindings
```
<script>
	let name = 'worl2d';
</script>

<input bind:value={name}>

<h1>Hello {name}!</h1>
```

- inputs
```
<input type=number bind:value={a} min=0 max=10>
<input type=range bind:value={a} min=0 max=10>
<input type=checkbox bind:checked={yes}>
```

## bind array
```
{#each menu as flavour}
	<label>
		<input type=checkbox bind:group={flavours} value={flavour}>
		{flavour}
	</label>
{/each}
```
- LAST TIME I END TUTORIAL ON THIS LINK https://svelte.dev/tutorial/multiple-select-bindings 

