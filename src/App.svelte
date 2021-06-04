<script>
	import Header from './component/Header.svelte';
	import Footer from './component/Footer.svelte';
	import Form from './component/Form.svelte';
	

	let todos = [
		{title: 'Shop', description: 'Buy some milk', id:0},
		{title: 'Work', description: 'Write some codes', id:1},
	]

	const addTodo = (e) => {
		 const todo = e.detail;
		 todos = [todo, ...todos];
	}

	let yes = false;
	
</script>

<Header />
<main>
	<Form on:addTodo={addTodo}/>

	{#each todos as todo (todo.id)}
		<div class='left'>
			<h2>{todo.title}</h2> 
	<input type='checkbox' bind:checked={yes}>
	
	<input type='text' placeholder={todo.description}>
		</div>
	{/each}	
</main>
<Footer />


<style>
	.left {
		border: 1px solid white;
		border-radius: 5px;
		text-align: left;
		padding: 8px;
		margin-top: 20px;
	}

	
	main {
		display:flex;
		flex-direction: column;
		align-items: flex-start;
		text-align: center;
		max-width: 900px;
		margin: 40px auto;
	}
	
</style>