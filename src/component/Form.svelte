<script>
    import { createEventDispatcher } from 'svelte';

    let dispatch = createEventDispatcher();

    let title;
    let description;

    const handleSubmit = () => {
        const todo = {
            title: title,
            description: description,
            id: Math.random()
        }
        dispatch('addTodo', todo);
    };
</script>

<form on:submit|preventDefault={handleSubmit}>
    <input type='text' placeholder='Title' bind:value={title}>
    <input type='text' placeholder='What needs to be done?' bind:value={description}>
    <button>Add To Do</button>
</form>

<style>
    form {
        border: 1px solid white;
        border-radius: 8px;
		text-align: center;
		padding: 10px;
		max-width: 600px;
		margin: 50px auto;
        background-color: #b9abae;
    } 
    input[type="text"] { 
		overflow: hidden;
	}
	input:hover {
		opacity: 0.8;
		border-radius: 10px;
		box-shadow: 0 2px #838383ab;
	} 
    button {
		background-color: #527b88;
		width: 110px;
		height: 50px;
		margin: 10px ;
		padding: 10px;
	}
	button:hover {
		opacity: 0.8;
		border-radius: 10px;
		box-shadow: 0 2px #85363dab;
	} 
</style>