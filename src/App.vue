<script>
import Navbar from "./components/Navbar.vue";
import Todo from "./components/Todo.vue";
import Signin from "./components/Signin.vue";
import Register from "./components/Register.vue";
import axios from "axios";

export default {
  name: "app",
  components: {
    Navbar,
    Todo,
    Signin,
    Register
  },
  data() {
    return {
      currentUser: null,
      currentAuth: "signin",
      todos: []
    };
  },
  methods: {
    addTodo(data) {
      const todo = { desc: data.desc, userId: this.currentUser._id };
      axios
        .post("http://localhost:5000/api/todos", todo)
        .then(res => (this.todos = res.data.todos))
        .catch(err => console.log(err));
    },
    deleteTodo(id) {
      axios
        .delete(`http://localhost:5000/api/todos/${this.currentUser._id}/${id}`)
        .then(res => (this.todos = res.data.todos))
        .catch(err => console.log(err));
    },
    finishTodo(id) {
      const todo = { userId: this.currentUser._id, msg: "completedEdit" };
      axios
        .put(`http://localhost:5000/api/todos/${id}`, todo)
        .then(res => (this.todos = res.data.todos))
        .catch(err => console.log(err));
    },
    editTodo(data) {
      const todo = {
        userId: this.currentUser._id,
        desc: data.desc,
        msg: "descEdit"
      };
      axios
        .put(`http://localhost:5000/api/todos/${data.id}`, todo)
        .then(res => (this.todos = res.data.todos))
        .catch(err => console.log(err));
    },
    changeAuth(msg) {
      this.currentAuth = msg;
    },
    onAuth(data) {
      console.log(data);
      this.currentUser = data.user;
      this.todos = data.todo.todos;
    },
    onLogOut() {
      this.currentUser = null;
      this.currentAuth = "signin";
    }
  }
};
</script>

<template>
  <div id="app">
    <Navbar
      v-bind:currentUser="currentUser"
      v-on:change-auth="changeAuth($event)"
      v-on:on-logout="onLogOut()"
    />
    <div v-if="currentUser">
      <Todo
        v-bind:todos="todos"
        v-on:add-todo="addTodo($event)"
        v-on:del-todo="deleteTodo($event)"
        v-on:finish-todo="finishTodo($event)"
        v-on:edit-todo="editTodo($event)"
      />
    </div>
    <div v-else-if="currentAuth === 'signin'">
      <Signin v-on:on-auth="onAuth($event)"/>
    </div>
    <div v-else>
      <Register v-on:change-auth="changeAuth($event)"/>
    </div>
  </div>
</template>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
