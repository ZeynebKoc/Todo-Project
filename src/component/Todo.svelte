<script> 
    import { createEventDispatcher } from 'svelte';

    let dispatch = createEventDispatcher();

    let title;
    let description;
</script>    

{#each todos as todo (todo.id)}
<div class='left'> 
    <h2>TO DO</h2> 
	<input type='checkbox'>
	<input type='text' placeholder={todo.title}>
	<input type='text' placeholder={todo.description}>	
</div>
{/each}



<style>

</style>   