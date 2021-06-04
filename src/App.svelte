<script>
	import Header from './component/Header.svelte';
	import Footer from './component/Footer.svelte';
	import Form from './component/Form.svelte';
	

	let todos = [
		{title: 'Shop', description: 'Buy some milk', done: false, id:0},
		{title: 'Work', description: 'Write some codes', done: false, id:1},
	]

	const addTodo = (e) => {
		 const todo = e.detail;
		 todos = [todo, ...todos];
	}

	const markItem = (todo, done) => {
		todo.done = done;
		remove(todo);
		todos = todos.concat(todo);
	}

	const deleteItem = (id) => {
		todos = todos.filter ((todo) => todo.id != id)
	}

	
</script>

<Header />
<Form on:addTodo={addTodo}/>
<main>
	<div class='board-left'>
		<h2>TODO</h2>
		{#each todos.filter(t =>!t.done) as todo (todo.id)}
			<div class='left'>
				<input type=checkbox on:change={() => markItem(todo, true)}>
				<h3>{todo.title}</h3> 
				<input type='text' placeholder={todo.description}>
				<button on:click={() => deleteItem(todo.id)}>Delete</button>
			</div>
		{/each}	
	</div>

	
	<div class='board-right'>
		<h2>DONE</h2>
		{#each todos.filter(i => i.done) as todo (todo.id)}
			<div class='right'>
				<input type=checkbox checked on:change={() => markItem(todo, false)}>
				<h3>{todo.title}</h3> 
				<input type='text' placeholder={todo.description}>
				<button on:click={() => deleteItem(todo.id)}>Delete</button>
			</div>
		{/each}	
	</div>
</main>
<Footer />


<style>
	.board-left {
		display: flex;
		flex-flow: row wrap;
		justify-content: space-around;
		border: 1px solid white;
		border-radius: 8px;
		width: 450px;
	}
	.board-right {
		display: flex;
		flex-flow: row wrap;
		justify-content: space-around;
		border: 1px solid white;
		border-radius: 8px;
		width: 450px;
	}
	.left {
		display: flex;
		border: 1px solid white;
		border-radius: 8px;
		padding: 8px;
		margin: 10px;
		max-width: 450px;
		background-color: #b9abae;	
	}
	.right {
		display: flex;
		border: 1px solid white;
		border-radius: 8px;
		padding: 8px;
		margin: 10px;
		max-width: 500px;	
		background-color: #b9abae;
	}
	main {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 20px;
		max-width: 1000px;
		margin: 40px auto;
	}
	button {
		background-color: #527b88;
		width: 70px;
		height: 50px;
		display: flex;
		flex-direction: column;
		align-self: center;
		margin: 10px ;
		padding: 10px;
	}
	button:hover {
		opacity: 0.8;
		border-radius: 10px;
		box-shadow: 0 2px #85363dab;
	}
	h2, h3 {
		color: #225564;
		padding: 10px;
		display: flex;
		align-items: center;
	}
	input[type="text"] { 
		overflow: hidden;
	}
	input:hover {
		opacity: 0.8;
		border-radius: 10px;
		box-shadow: 0 2px #838383ab;
	}	
    input[type="checkbox"] {
		display:flex;
		flex-direction: column;
		align-self: center;
		width: 25px;
		height: 25px;
		background:url(check_radio_sheet.png) left top no-repeat;
	}
	
</style>