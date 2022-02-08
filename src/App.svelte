<script>
	import Header from './component/Header.svelte';
	import Footer from './component/Footer.svelte';
	import Form from './component/Form.svelte';

	let todos = [
		{checked: false, title: 'Shop', description: 'Buy some milk', id:123123},
		{checked: false, title: 'Work', description: 'Write some codes', id:1456456},
		{checked: false, title: 'Fix', description: 'Feed the turtle', id:789789},
	];

	todos = JSON.parse(localStorage.getItem("localTodo")) || [];
   
    const updateStorage = () => {
		console.log(todos);
        localStorage.setItem("localTodo", JSON.stringify(todos));
    }

	const updateTodo = (todo) => {
		//console.dir(todo)
		 todos = todos.map(t => { 
			 if(t.id == todo.id) {
				 return todo;
			 }
			return t;
		 })
		 updateStorage();
	};

	const addTodo = (e) => {
		 const todo = e.detail;
		 todos = [todo, ...todos];
		 updateStorage();
	};

	const deleteItem = (id) => {
		todos = todos.filter ((todo) => todo.id != id);
		updateStorage();
	};	

</script>

<Header />
{#key todos}
	<Form on:addTodo={addTodo}/>
{/key}
<main>
	<div class='form'>
		{#each todos as todo (todo.id)}
			<label class='board'>
				<input type=checkbox bind:value={todo.checked} on:input={() => updateTodo(todo)}>
				<input id='plh1' type='text' contenteditable="true" bind:value={todo.title} autoComplete="off" on:input={() => updateTodo(todo)}>
				<input id='plh2' type='text' contenteditable="true" bind:value={todo.description} autoComplete="off" on:input={() => updateTodo(todo)}>
				<button on:click={() => deleteItem(todo.id)}>Delete</button>	
			</label>
		{/each}	
	</div>
</main>
<Footer />


<style>
	.form {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.board {
		display: flex;
		align-items: stretch;
		border: 1px solid white;
		border-radius: 8px;
		padding: 8px;
		margin: 20px;
		height: 50px;
		width: 800px;
		padding: 10px;	
	}
	button {
		background-color: #527b88;
		display: flex;
		align-self: center;
		width: 70px;
		height: 40px;
		margin: 10px ;
		padding: 10px;
	}
	button:hover {
		opacity: 0.8;
		border-radius: 10px;
		box-shadow: 0 2px #2a3f46;
	}
	#plh1 {
		overflow: hidden;
		display: flex;
		align-items: center;
		width: 150px;
		margin: 5px;
        font-weight: bolder;
		font-size: large;
	}
	#plh2 { 
		overflow: hidden;
		display:flex;
		align-self: center;
		width: 500px;
		margin: 5px;
	}
	input:hover {
		opacity: 0.8;
		border-radius: 5px;
		box-shadow: 0 2px #838383ab;
	}	
    input[type="checkbox"]{
		width: 25px ;
		height: 25px ;
		background:url(check_radio_sheet.png) left top no-repeat;
		margin: 12px;
	}
</style>