<script>
    export let id
    export let name
    export let state
    export let editTodo = () => {}
    export let removeTodo = () => {}

</script>


<div class="border border-opacity-10 border-dark rounded todo-container">
    <div class="col-sm-8">
        <p class="lead p-2 text-wrap {state && 'text-decoration-line-through'}">{name}</p>
    </div>
    <div class="col-sm4 p-1 gap-2 d-flex align-items-center justify-content-center">
        <button class="btn {state ? 'btn-outline-warning' : 'btn-outline-success'}" on:click={editTodo(id)}>
            <i class={state ? 'bi-x' : 'bi-check'}></i>
        </button>
        <button class="btn btn-outline-danger" on:click={removeTodo(id)}>
            <i class="bi-trash"></i>
        </button>
    </div>
</div>


<style>
    .todo-container {
        max-width: 100vw;
        min-height: 50px;
        display: flex;
        justify-content: space-between;
    }
</style>