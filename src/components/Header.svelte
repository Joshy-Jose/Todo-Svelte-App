<script>
    export let totalTodos;
    export let remainTodos;

</script>
	<div class="app-header">
		<div>{totalTodos} Total</div>
		<div class="task-count">{remainTodos} Remaining</div>
	</div>

    <style>
        .app-header {
            padding: 10px;
            display: flex;
            justify-content: space-between;
        }
        
        .task-count {
            align-self: center;
        }
    </style>