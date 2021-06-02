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
        border-radius: 5px;
		text-align: center;
		padding: 10px;
		max-width: 900px;
		margin: 40px auto;
    }   
</style>