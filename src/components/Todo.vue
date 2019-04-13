<script>
// import TodoInput from "./TodoInput.vue";

export default {
  name: "Todo",
  components: {
    // TodoInput
  },
  data() {
    return {
      inputText: null,
      edit: null,
      editText: null
    };
  },
  props: ["todos"],
  methods: {
    onInputText() {},
    onSubmit() {
      let todo = { desc: this.inputText };
      if (this.inputText) this.$emit("add-todo", todo);
      this.counter++;
      this.inputText = "";
    },
    onEdit(index) {
      this.edit = index;
    },
    onEditText(id, event) {
      event.stopPropagation();
      let data = { id, desc: this.editText };
      this.$emit("edit-todo", data);
      this.edit = null;
      this.editText = null;
    },
    onCancelEdit() {
      this.edit = null;
      this.editText = null;
    }
  }
};
</script>


<template>
  <div>
    <!-- <TodoInput v-on:add-todo="$emit('add-todo',text)"/> -->
    <div class="input-group mb-3">
      <input
        v-model="inputText"
        type="text"
        class="form-control"
        placeholder="type todo's here..."
        aria-describedby="button-addon2"
      >
      <div class="input-group-append">
        <button
          v-on:click="onSubmit"
          class="btn btn-outline-secondary btn-warning"
          type="button"
          id="button-addon2"
        >+</button>
      </div>
    </div>
    <div class="todo-list">
      <ol>
        <div v-bind:key="index" v-for="(todo,index) in todos">
          <div class="edit-bottom" v-if="edit === index">
            <input
              type="text"
              v-model="editText"
              v-on:change="onEditText"
              class="form-control btm"
              placeholder="type here..."
              aria-describedby="button-addon2"
            >
            <p
              v-on:click="onEditText(todo._id,$event)"
              class="btn btm bottom delete left btn-outline-secondary btn-danger"
              type="button"
              id="button-addon2"
            >done</p>
            <p
              v-on:click="onCancelEdit()"
              class="btn mar btm bottom delete left btn-outline-secondary btn-danger"
              type="button"
              id="button-addon2"
            >cancel</p>
          </div>
          <div v-else class="bottom">
            <li
              v-on:click="$emit('finish-todo' , todo._id)"
              v-bind:class="{ completed: todo.completed }"
            >{{todo.desc}}</li>
            <div>
              <button
                v-on:click="$emit('del-todo' , todo._id)"
                class="btn delete left btn-outline-secondary btn-danger"
                type="button"
                id="button-addon2"
              >remove</button>
              <button
                v-on:click="onEdit(index)"
                class="btn mar delete left btn-outline-secondary btn-danger"
                type="button"
                id="button-addon2"
              >edit</button>
              <small>created - on : {{todo.date}}</small>
              <br>
            </div>
          </div>
        </div>
      </ol>
    </div>
  </div>
</template>

<style scoped>
ol {
  padding-inline-start: 0px;
}

li {
  padding: 10px;
  border: 1px solid black;
  border-radius: 3px;
  background-color: #ffc107;
  font-size: 20px;
  list-style: none;
  cursor: pointer;
  margin: 0 0 15px 0;
  transition: background-color 0.2s;
}

.todo-list {
  padding: 0 600px;
}

.group {
  border: 1px solid black;
}

.checkbox {
  display: flex;
  float: left;
}

.input-group {
  padding: 50px 600px;
}

.left {
  float: right;
}

.completed {
  background-color: rgb(41, 211, 41);
  text-decoration: line-through;
}

.bottom {
  margin-bottom: 30px;
}

.edit-bottom {
  margin-bottom: 50px;
}

.mar {
  margin-right: 20px;
}

.btm {
  margin-bottom: 10px;
}
</style>
