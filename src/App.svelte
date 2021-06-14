<script>
	import { _todos } from './stores/store';

	let todos;

	_todos.subscribe((data) => {
		todos = data;
	});

	import Header from './component/Header.svelte';
	import Footer from './component/Footer.svelte';
	import Form from './component/Form.svelte';

	const addTodo = (e) => {
		 const todo = e.detail;
		 todos = [todo, ...todos];
	};

	const deleteItem = (id) => {
		todos = todos.filter ((todo) => todo.id != id)
	};	

</script>

<Header />
{#key todos}
	<Form on:addTodo={addTodo}/>
{/key}
<main>
	<div class='form'>
		{#each todos.filter(t => !t.done) as todo (todo.id)}
			<label class='board'>
				<input type=checkbox >
				<input id='plh1' type='text' contenteditable="true" placeholder={todo.title} autoComplete="off">
				<input id='plh2' type='text' contenteditable="true" placeholder={todo.description} autoComplete="off">
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
		display: flex;
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