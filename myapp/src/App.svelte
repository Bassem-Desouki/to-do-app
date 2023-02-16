<script>
import Header from "./UI/Header.svelte";
import TaskItem from "./Tasks/TaskItem.svelte";

	let taskName = "";
	let tasks = [];
	let validInputVal = true;

	function addTaskHandler (){

		if(taskName.trim() !== ''){
			validInputVal = true;

			let newTask = {
			id: Math.random(),
			taskName : taskName,
			accomplished: false
			}

			tasks = [...tasks, newTask];
			taskName = "";
		}else{
			validInputVal = false;
		}
	} 

	function removeTaskHandler(index){
		tasks = tasks.filter(task => task !== tasks[index]);
	}

	function accomplishTaskHandler(index){
		 tasks[index].accomplished = true;
	}

</script>

<style>
</style>


<Header/>
<main class=" mt-4">
	<form class="d-flex justify-content-center" on:submit|preventDefault={addTaskHandler}>
		<input 
		 id="myInput"
		 class="w-25"
		 type="text"
		 placeholder="Create new task"
		 bind:value={taskName}
		 />
		<button class="btn btn-primary ms-2" type="submit">Add</button>
	</form>

	{#if !validInputVal}
		<p class="text-danger text-center">Please enter a task name first!</p>
	{/if}
	
	<section class="tasks-container mt-5">
		<h1 class="text-center">Your tasks</h1>
		{#each tasks as task, index (task.id)}
			<div class="d-flex justify-content-center align-items-center">
				<TaskItem taskName = {task.taskName} {index} accomplishedTask={task.accomplished} />
				<div class="buttons">
					<button class="btn btn btn-primary" on:click={() => accomplishTaskHandler(index)}>Done</button>
					<button class="btn btn btn-danger" on:click={() => removeTaskHandler(index)}>Remove</button>
				</div>
			</div>
		{:else}
			<p class=" text-center text-danger">There are no tasks for you!</p>
		{/each}
	</section>
</main>

