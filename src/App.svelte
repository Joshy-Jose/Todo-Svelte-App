<script>
    import Header from "./components/Header.svelte";
    import Form from "./components/Form.svelte";
    import Todos from "./components/Todos.svelte";
import { text } from "svelte/internal";

    let todos = [
        { id: 1, text: "First", completed: true },
        { id: 2, text: "Second", completed: false },
        { id: 3, text: "Third", completed: false },
    ];

    let remainTodos;
    let totalTodos;
    let newText ;

    $:totalTodos = todos.length;
    $:remainTodos = todos.reduce((n, todos) => {
        return n + (todos.completed ? 0 : 1)

    },0)                                   //n = count//zero initailly,find completed increment n else 0;
                                                                       
    function onComplete(event) {
        let updateId = event.detail.id;
        todos.map((todo) => {
            if(todo.id === updateId) todo.completed = !todo.completed;
        });
        todos = todos;
    }
    function createdTodo() {
        newText = newText.trim();
        if(newText != "") {
            let newId = Math.max(...todos.map((e) =>e.id)) + 1;
            todos = [...todos, {
                id:newId,
                text: newText,
                completed:false
            }]
            newText = "";
        }
        
    }
</script>

<div id="app-container" class="app-container">
    <Header {totalTodos} {remainTodos}/>
    <Todos {todos} on:completed={onComplete}/>
    <Form on:created={createdTodo} bind:newText/>
</div>

<style>
    .app-container {
        width: 400px;
        min-height: 500px;
        background-color: #282c34;
        box-shadow: 0 20px 80px rgba(0, 0, 0, 0.6);
        background: radial-gradient(
            circle,
            #282c34 0%,
            rgba(40, 48, 56, 1) 100%
        );
        position: relative;
        border-radius: 1em;
        padding: 20px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
</style>
