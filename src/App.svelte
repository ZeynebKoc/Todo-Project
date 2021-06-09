<script>
	import Header from './component/Header.svelte';
	import Footer from './component/Footer.svelte';
	import Form from './component/Form.svelte';

	let todos = [
		{title: 'Shop', description: 'Buy some milk', done: false, id:0},
		{title: 'Work', description: 'Write some codes', done: false, id:1},
		{title: 'Fix', description: 'Feed the turtle', done: true, id:3},
	];

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
	<form>
		{#each todos.filter(t => !t.done) as todo (todo.id)}
			<label class='board'>
				<input type=checkbox >
				<h3 contenteditable="true">{todo.title}</h3>
				<input type='text' contenteditable="true" placeholder={todo.description}>
				<button on:click|once={() => deleteItem(todo.id)}>Delete</button>
			</label>
		{/each}	
	</form>	
</main>
<Footer />


<style>
	form {
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
		max-height: 50px;
		min-width: 700px;
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
	h3 {
		color: #225564;
		padding: 10px;
		display: flex;
		align-items: center;
		min-width: 50px;
	}
	input[type="text"] { 
		overflow: hidden;
		display:flex;
		align-self: center;
		min-width: 500px;
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