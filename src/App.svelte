<script>
	let todos = []
	function addTodo () {
		todos = [...todos, '']
	}
	function removeSelf (index) {
		todos = [...todos.slice(0, index), ...todos.slice(index+1)]
	}
</script>

<main>
	{#each todos as todo, index}
		<input bind:value={todos[index]}>
		<button on:click={()=>removeSelf(index)}>X</button>
		<br>
	{/each}
	<button on:click={addTodo}>Add</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
