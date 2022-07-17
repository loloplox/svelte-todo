<script>
    import Card from "./lib/Card.svelte";

    document.title = "Todo Svelte"

    let todos = []
    let todo = {id: '', name: '', state: false}

    function addTodo() {
        let newTodos

        if (!todo.name.trim()) {
            return
        }

        todo.id = Date.now()
        todos = [...todos, todo]
        todo = {id: '', name: '', state: false}

        setLocalStorage(newTodos)
    }

    function getAllTodo() {
        let allTodos = localStorage.getItem('todos')
        allTodos = JSON.parse(allTodos)

        if (allTodos !== null) {
            todos = allTodos
        } else {
            todos = []
        }
    }

    function removeTodo(id) {
        todos = todos.filter(todo => todo.id !== id)

        setLocalStorage(todos)
    }

    function editTodo(id) {
        todos = todos.map(item => item.id === id ? {...item, state: !item.state} : item)

        setLocalStorage(todos)
    }

    function setLocalStorage(arrayTodos) {
        let newTodos = JSON.stringify(todos)
        localStorage.setItem('todos', newTodos)
    }

    getAllTodo()

</script>

<main>
    <div class="container">
        <h1 class="display-5 text-center mb-5">CRUD</h1>
        <div class="row">
            <div class="col-sm-12 col-md-5 p-4">
                <form on:submit|preventDefault={addTodo} class="d-grid gap-3">
                    <div class="">
                        <label for="Name" class="form-label">Name:</label>
                        <input bind:value={todo.name} type="text" id="Name" placeholder="Name Todo" class="form-control" />
                    </div>
                    <div>
                        <input bind:checked={todo.state} type="checkbox" id="state" class="form-check-input">
                        <label for="state">Complete</label>
                    </div>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
            <div class="col-sm-12 col-md-7 d-grid gap-2">
                {#each todos as item}
                    <Card
                        id={item.id}
                        name={item.name}
                        state={item.state}
                        editTodo={editTodo}
                        removeTodo={removeTodo}
                    />
                {/each}
            </div>
        </div>
    </div>
</main>


