<script>
    import { createEventDispatcher } from "svelte";

    let dispatch = createEventDispatcher();

    let title;
    let description;

    const handleSubmit = () => {
        const todo = {
            title,
            description,
            id: Math.random(),
        };
        console.log(todo);
        dispatch("addTodo", todo);
        title = "";
        description = "";
    };
</script>

<form on:submit|preventDefault={handleSubmit}>
    <input class="plh1" type="text" placeholder="Title" bind:value={title} />
    <input
        class="plh2"
        type="text"
        placeholder="What needs to be done?"
        bind:value={description}
    />
    <button>Add To Do</button>
</form>

<style>
    form {
        border: 1px solid white;
        border-radius: 8px;
        text-align: center;
        padding: 10px;
        width: 650px;
        margin: 30px auto;
        background-color: #b9abae;
    }
    .plh1 {
        overflow: hidden;
        width: 120px;
        margin: 5px;
        font-weight: bolder;
        font-size: large;
        height: 40px;
    }
    .plh2 {
        overflow: hidden;
        width: 350px;
        margin: 5px;
    }
    input:hover {
        opacity: 0.8;
        border-radius: 10px;
        box-shadow: 0 2px #838383ab;
    }
    button {
        background-color: #527b88;
        width: 120px;
        height: 60px;
        margin: 10px;
        padding: 5px;
    }
    button:hover {
        opacity: 0.8;
        border-radius: 10px;
        box-shadow: 0 2px #2a3f46;
    }
</style>
