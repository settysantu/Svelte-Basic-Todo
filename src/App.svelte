<script>
	let todoitems = [];
	let newtodoitem;
	let updatetodoitem;
	let edit = false;

	const addItem = () => {
		if(newtodoitem !== "" && newtodoitem !== undefined) {
			const todo = {
				id: Math.random(),
				name: newtodoitem
			}
			todoitems = [...todoitems, todo];
			newtodoitem = "";
		}
	}

	const deleteItem = (id) => {
		todoitems = todoitems.filter( (item) => item.id !== id );
	}

	const editItem = (id, name) => {
		edit = id;
		updatetodoitem = name;
	}

	const saveItem = (index) => {
		edit = false;
		todoitems[index].name = updatetodoitem;
	}

</script>

<div class="container">
	<h4 class="mt-5 mb-4 font-weight-bold">TO-DO APP</h4>
	<div class="input-group pt-3">
		<input type="text" class="form-control" placeholder="Add To Do List" bind:value={newtodoitem} required>
		<button class="btn btn-primary rounded-0" on:click={addItem}>Add</button>
	</div>
	<hr>
	{#if todoitems}
		<ul class="list-unstyled">
		{#each todoitems as {id, name}, index}
			<li class="d-flex justify-content-between">
				<strong class="mr-2">
					{(index + 1) <= 9 ? "0" + (index + 1) : (index + 1)}.
				</strong>
				<strong>{name}</strong>
				<div class="btn-group">
					<button class="btn btn-info" on:click={() => editItem(id, name)}>Edit</button>
					<button class="btn btn-danger" on:click={() => deleteItem(id)}>Delete</button>
				</div>
			</li>
			{#if edit === id}
				<div class="input-group">
					<input type="text" class="form-control" bind:value={updatetodoitem}>
					<button class="btn btn-success rounded-0" on:click={() => saveItem(index)}>Save</button>
				</div>
			{/if}
			<hr>
		{/each}
		</ul>
	{/if}
</div>

<style>

</style>