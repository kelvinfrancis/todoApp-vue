<script setup>
import { ref, computed, watch, onMounted } from "vue";
import Greeting from "./components/Greeting.vue";
import CreateTodo from "./components/CreateTodo.vue";
import TodoList from "./components/TodoList.vue";

const name = ref("");
const todos = ref([]);
const input_content = ref("");
const input_category = ref(null);

const todos_ascending = computed(() =>
  [...todos.value].sort((a, b) => b.createAt - a.createAt)
);

const addTodo = () => {
  if (input_content.value.trim() === "" || input_category.value === null)
    return;
  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    done: false,
    createAt: new Date().getTime(),
  });
  input_content.value = "";
  input_category.value = null;
};

const updateTodo = (index, newTodo) => {
  todos.value[index] = newTodo;
};

const removeTodo = (index) => {
  todos.value.splice(index, 1);
};

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
);

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});
</script>

<template>
  <main class="app">
    <Greeting v-model:name="name" />
    <CreateTodo
      :inputContent="input_content"
      :inputCategory="input_category"
      @update:inputContent="input_content = $event"
      @update:inputCategory="input_category = $event"
      @add-todo="addTodo"
    />
    <TodoList
      :todos="todos_ascending"
      @update-todo="updateTodo"
      @remove-todo="removeTodo"
    />
  </main>
</template>

<!-- <script setup>
  import { ref, onMounted, computed, watch } from "vue";

  const todos = ref([]);
  const name = ref('');

  const input_content = ref('');
  const input_category = ref(null);

  const todos_ascending = computed(() => todos.value.sort((a,b) => {
    return b.createAt - a.createAt
  }));

  const addTodo = () => {
    // Validar que no se agregen tareas vacías o sin categoría.
    if (input_content.value.trim() === '' || input_category.value === null) {
      return
    }
    // agregar la tarea a la lista
    todos.value.push({
      content: input_content.value,
      categoy: input_category.value,
      done: false,
      createAt: new Date().getTime()
    })

    input_category.value = null
    input_content.value = ''
  }

  // Elimitar tarea
  const removeTodo = todo => {
    todos.value = todos.value.filter(t => t !== todo)
  }

  // Agregar la terea al local Storage
  watch(todos, (newVal) => {
    localStorage.setItem('todos', JSON.stringify(newVal))
  }, { deep: true})

  // Guardamos el nombre ingresado en la variable 'name' y esta la guardamos en el local Storage.
  watch(name, (newVal) => {
    localStorage.setItem('name', newVal)
  });

  // Visualizamos el valor que tiene 'name' en el local storage cada vez que actualice la página.
  // Si no tiene valor guardado, devuelve un string vacío.
  onMounted(() => {
    name.value = localStorage.getItem('name') || ''
    todos.value = JSON.parse(localStorage.getItem('todos')) || []
  })
</script>

<template>

  <main class="app">

    <section class="greeting">
      <h2 class="title">
        Hola!, <input type="text" placeholder="Ingresa tu nombre" v-model="name"/>
      </h2>
    </section>

    <section class="create-todo">
      <h3>AGREGA UNA TAREA</h3>

      <form @submit.prevent="addTodo">
        <h4>Qué necesitas agregar a tus tareas?</h4>
        <input 
          type="text" 
          placeholder="ej. Terminar la actividad final" 
          v-model="input_content" 
        />
        <h4>Elige una categoría</h4>
        <div class="options">
          <label>
            <input 
              type="radio"
              name="category" 
              value="Estudios" 
              v-model="input_category"/>
              <span class="bubble business"></span>
              <div>Estudios</div>
          </label>
          <label>
            <input 
              type="radio"
              name="category" 
              value="Personal" 
              v-model="input_category"/>
              <span class="bubble personal"></span>
              <div>Personal</div>
          </label>
        </div>
        
        <input type="submit" value="Agregar tarea" />
      </form>
    </section>

    <section class="todo-list">
      <h3>TAREAS</h3>
      <div class="list">
        <div v-for="todo in todos_ascending" :class="`todo-item ${todo.done && 'done'}`">

          <label>
            <input type="checkbox" v-model="todo.done" />
            <span :class="`bubble ${todo.category}`"></span>
          </label>

          <div class="todo-content">
            <input type="text" v-model="todo.content" />
          </div>

          <div class="actions">
            <button class="delete" @click="removeTodo(todo)">Delete</button>
          </div>

        </div>
      </div>
    </section>

  </main>

</template> -->
