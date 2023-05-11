<script>
  export let isChecked;
  export let title;
  export let changeValue;
  export let deleteTodo;
</script>

<div class="todo">
  <input class="checkbox" type=checkbox checked={isChecked} on:click={changeValue}>
  <div class="todo-body" on:click={changeValue}>{title}</div>
  <div class="todo-delete" on:click={deleteTodo}/>
</div>

<style>
  .checkbox {
    height: 1.5em;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 1.5em;
    white-space: nowrap;
  }
  .todo {
    align-items: center;;
    background-color: #404040;
    border-radius: 0.5em;
    cursor: pointer;
    display: flex;
    padding: 0.5em;
  }
  .todo-body {
    cursor: pointer;
    margin-left: 10px;
  }
  .todo-delete {
    background-image: url(https://cdn-icons-png.flaticon.com/512/860/860778.png);
    background-size: 1.5em 1.5em;
    cursor: pointer;
    height: 1.5em;
    margin-left: auto;
    width: 1.5em;
  }
</style>