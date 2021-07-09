<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>

  <div class="container">
    <div class="row">
      <div class="col-12 col-md-6 offset-md-3">
        <div class="row my-3" v-for="(todo, index) in todos" v-bind:key="todo.id">
          <div class="col-md-8">
            <div class="card my-3">
              <div class="card-body">
                <div class="card-title" :class="{ done: todo.done }">
                  {{ todo.content }}
                </div>
              </div>
            </div>
          </div>
          <div class="col-md-4 d-flex align-items-center">
            <button @click="toggleDown(todo)" class="btn btn-success">
              Hecho
            </button>


            <button @click="removeTodo(index)" class="btn ">Eliminar</button>

          </div>
        </div>
        <div class="card">
          <div class="card-body">
            <div class="card-title">
              <p>{{ newTodo }}</p>
            </div>
          </div>
        </div>

        <form @submit.prevent="addNewTodo">
          <div class="input-group">
            <input
              v-model="newTodo"
              type="text"
              name="newTodo"
              class="form-control"
              placeholder="Insertar tarea"
            />
          </div>
          <div class="input-group-append" id="button-addon4">
            <button class="btn btn-dark my-3" type="submit">Insertar</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDown(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    return {
      newTodo,
      todos,
      addNewTodo,
      toggleDown,
      removeTodo
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
