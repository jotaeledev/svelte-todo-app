<script>
	import { createEventDispatcher } from 'svelte';
	
	export let name;
	export let index;

	const dispatch = createEventDispatcher();

	const remove = () => { dispatch('remove', {"name": name, "index": index}) }

	const edit = () => { dispatch('edit', {"name": name, "index": index}) }

</script>
<style>
	.task{
			display:flex;
			justify-content: space-between;
			align-items:center;
			padding:10px;
			margin: 0px 10px;
		}
</style>
<div class="task">
	<span>{index + 1}. {name}</span>
	<div>
		<button on:click={edit}>Editar</button>
		<button on:click={remove}>Borrar</button>
	</div>
</div>