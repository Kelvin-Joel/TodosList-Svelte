<script>
  let TaskInitial = {
    id: null,
    name: "",
    description: "",
  };
  let ListTask = [
    {
      id: 1,
      name: "programar",
      description: "programar",
    },
    {
      id: 2,
      name: "limpiar la caza",
      description: "temprano",
    },
  ];

  const HandleSubmit = () => {
    if (TaskInitial.name !== "") {
      TaskInitial.id = Date.now();
      ListTask = [...ListTask, TaskInitial];
      Clear();
      return;
    }
    alert("Campos Vacios!");
  };

  const Clear = () => {
    TaskInitial = {
      id: null,
      name: "",
    };
  };

  const DeleteTask = (taskId) => {
    const FilterTask = ListTask.filter((task) => task.id !== taskId);
    ListTask = FilterTask;
  };

  const EdiTask = (IdTask) => {
    const updateTask = ListTask.map((task) =>
      task.id === IdTask ? TaskInitial : task
    );
    ListTask = updateTask;
    Clear();
  };
</script>

<div class="conteiner">
  <h1 class="conteiner__title">Tasks</h1>
  <form class="form" on:submit|preventDefault={HandleSubmit}>
    <label for="">Name :</label>
    <input class="form__input" type="text" bind:value={TaskInitial.name} />
    <label for="">Description :</label>
    <input
      class="form__input"
      type="text"
      bind:value={TaskInitial.description}
    />
    <button class="form__button btn">Save Task</button>
  </form>

  {#each ListTask as task}
    <ul class="list-task">
      <li class="tasks">
        {task.name} - {task.description}
        <button class="task__btn" on:click={EdiTask(task.id)}>edit</button>
        <button class="task__btn" on:click={DeleteTask(task.id)}>Delete</button>
      </li>
    </ul>
  {/each}
</div>

<style>
  :root {
    --border-radius: 0.2em;
    --border: 1px solid #ccc;
    --colorWhite:#fff;
  }
  button {
    outline: none;
    border: none;
    cursor: pointer;
  }
  .conteiner {
    width: 50%;
    margin: 50px auto;
  }
  .conteiner__title {
    text-align: center;
  }
  .form {
    width: 100%;
    border: var(--border);
    border-radius: 0.2em;

    padding: 0.5em;
  }
  label {
    margin-bottom: 0.4em;
  }
  .form__input {
    margin-bottom: 1em;
    display: block;
    width: 100%;
    outline: none;
    border: var(--border);
    padding: 0.7em 0;
    border-radius: var(--border-radius);
  }
  .form__button {
    border-radius: var(--border-radius);
    background-color: orangered;
    color: var(--colorWhite);
    padding: 0.7em 1.5em;
    cursor: pointer;
  }
  .list-task {
    width: 100%;
    padding: 0;
  }
  .tasks {
    background-color: rgb(66, 66, 255);
    color: var(--colorWhite);
    padding: 0.8em 0.5em;
    border-radius: var(--border-radius);
  }
  .task__btn {
    padding: 0.7em 1em;
    border-radius: 0.2em;
    background-color: var(--colorWhite);
    font-weight: bold;
  }
</style>
