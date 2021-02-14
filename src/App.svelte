
<script>
	import Task from './Task.svelte';
	
	const task = { 
		name:'' 
	};

	let newTask = true;
	let updatingIndex = null;

	let tasks = [];
	
	const addToDo = () => { 
		if(newTask){
			tasks = [...tasks, {...task}];
		}else{
			updateToDo();
			newTask = true;
		}
		task.name = '';
	};
	const removeToDo = (data) => { 
		tasks.splice(data.detail.index, 1);
		tasks = [...tasks]
	};
	const updateToDo = () => {
		tasks[updatingIndex].name = task.name;
	}
	const loadSelectedToDo = (data) => {
		newTask = false;
		updatingIndex = data.detail.index;
		task.name = data.detail.name;
	};
</script>
<style>
	.center{
		text-align:center;
	}
	ul{
		list-style: none;
	}
	li{
		border: 1px solid black;
		margin:10px 0px;
	}
</style>
<div>
	<div class="center">
		<h1>
			ToDo App
		</h1>
		<input placeholder="New ToDo" bind:value={task.name}/>
		<button on:click="{addToDo}">
			{newTask ? 'Add' : 'Edit'}
		</button>
	</div>
	<div>
		<h2 class="center">ToDo List</h2>
		<ul>
			{#each tasks as task, i}
				<li>
					<Task name={task.name} index={i} on:remove="{removeToDo}" on:edit="{loadSelectedToDo}"/>
				</li>
			{/each}
		</ul>
	</div>
</div>