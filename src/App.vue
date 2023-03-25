<script>
import { ref } from "vue";

export default {
  data() {
    return {
      todos: [],
      content: "",
    };
  },
  methods: {
    addTodo() {
      if (this.content.trim() === "") {
        return;
      }
      this.todos.push({
        name: this.content,
        createdAt: new Date().getTime(),
        done: false,
      });
      this.content = "";
    },
    taskDoneSwitch(index) {
      this.todos[index].done = !this.todos[index].done;
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },
  watch: {
    todos: {
      handler(newQuestion, oldQuestion) {
        console.log("essa");
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
      deep: true,
    },
  },
};
</script>

<template>
  <section id="appContent">
    <h1 id="logo">Todo list VUE</h1>
    <section class="createTodoForm">
      <form @submit.prevent="addTodo">
        <input
          class="input_text"
          type="text"
          v-model="content"
          placeholder="Wpisz co masz zrobić"
        />
      </form>
    </section>
    <section class="todos">
      <div class="todo" v-for="(todo, index) in todos" :key="index">
        <p>{{ todo.name }}</p>
        <div class="todoOptions">
          <input
            type="checkbox"
            name=""
            :checked="todo.done"
            @change="taskDoneSwitch(index)"
          />
          <span href="#" @click="deleteTodo(index)">usuń</span>
        </div>
      </div>
    </section>
  </section>
  <footer>
    <i>Created by <b>squishfunk</b></i>
  </footer>
</template>

<style>
* {
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: Century Gothic, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: justify;
  text-align: center;
  height: 100vh;
  background: linear-gradient(#0f0061, #3a0000);
  color: whitesmoke;
}

#appContent {
  display: flex;
  flex-direction: column;
  width: 80%;
  margin: auto;
  gap: 1rem;
}

#logo {
  font-size: 3rem;
  letter-spacing: 0.3rem;
  margin: 2rem;
  text-shadow: 1px 1px 10px rgb(255, 116, 116);
}

.input_text {
  width: 100%;
  padding: 10px;
  border: 1px solid whitesmoke;
  border-radius: 0.7rem;
  background: transparent;
  color: whitesmoke;
}

.todos {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

/* .todo {
  display: flex;
  padding: 1rem;
  background-color: rgb(95, 67, 60);
  border-radius: 10px;
  box-shadow: 0px 0px 7px rgb(255, 205, 205);
  justify-content: space-between;
} */

.todo {
  display: grid;
  grid-template-columns: 80% 20%;
  gap: 1rem;
  padding: 1rem;
  background-color: rgb(95, 67, 60);
  border-radius: 10px;
  box-shadow: 0px 0px 7px rgb(255, 205, 205);
}

.todo p {
  padding: 0.2rem;
  overflow: hidden;
}

.todoOptions {
}

span {
  cursor: pointer;
  background-color: red;
  border: 1px solid rgb(255, 255, 255);
  border-radius: 10px;
  padding: 0.5rem;
  vertical-align: middle;
  text-align: center;
}

footer {
  background-color: rgb(48, 2, 0);
  margin-top: auto;
  opacity: 0.7;
  padding: 0.5rem;
  font-size: 0.5rem;
  text-align: center;
}
</style>
