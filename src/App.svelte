<script>
  import ToDo from './lib/ToDo.svelte'

  let audio, 
      name = "", 
      toDos = [{title: "An old to do", isChecked: true}, {title: "Pick up clothes from cleaners", isChecked: true}, {title: "Wash car", isChecked: false}];

  const addToDo = () => {
    if (!name) {
      alert("Please enter a value");
    } else {
      toDos = [...toDos, {title: name, isChecked: false}];
      name = "";
    }
  }
  const toggleToDo = (key) => {
    toDos = toDos.map((todo, index) => {
      const isChecked = todo.isChecked;
      if (key === index) {
        !isChecked && audio.play();
        return {...todo, isChecked: !isChecked};
      }
      return todo;
    });
  }
  const deleteTodo = (key) => (toDos = toDos.filter((_, index) => key !== index));
  const deleteAllToDos = () => confirm("Delete all to dos?") && (toDos = []);
</script>

<main>
  <h1>Side Hustle ToDos</h1>
  <div class="card">
    {#each toDos as toDo, key}
      {#if !toDo.isChecked}
      <ToDo deleteTodo={deleteTodo.bind(this, key)} isChecked={toDo.isChecked} title={toDo.title} changeValue={toggleToDo.bind(this, key)}/>
      {/if}
    {/each}
    <input class="input" type="text" bind:value={name} placeholder="Add a to do"/>
    <button class="button" on:click={addToDo}>Add {name || "to do"}</button>
    {#if toDos.length > 0}
    <button class="button" on:click={deleteAllToDos}>Delete All ToDos</button>
    {/if}
    <div>Completed</div>
    {#each toDos as toDo, key}
      {#if toDo.isChecked}
      <ToDo deleteTodo={deleteTodo.bind(this, key)} isChecked={toDo.isChecked} title={toDo.title} changeValue={toggleToDo.bind(this, key)}/>
      {/if}
    {/each}
  </div>
</main>

<style>
  .button {
    align-self: center;
    background-color: purple;
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 50%;
  }
  .input {
    padding: 10px;
  }
</style>

<audio src="https://cdn.freesound.org/previews/484/484344_5121236-lq.mp3" bind:this={audio}></audio>
