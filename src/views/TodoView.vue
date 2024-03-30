<template>
  <div class="todo">
    <div class="add">
      <form @submit="addTodo">
        <input
          type="text"
          v-model="newTodo"
          class="todo-input"
          placeholder="what is in your mind ?"
        />
        <input type="submit" value="Add" />
      </form>
    </div>

    <div v-for="todo in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" class="todo-item-label" :class="{ completed : todo.completed }" >
          {{ todo.title }}
        </div>
        <input v-else class="todo-item-edit" type="text" v-model="todo.title"  @blur="doneEdit(todo)" 
        @keyup.enter="doneEdit(todo)" 
        @keyup.esc="cancelEdit(todo)"/>
      </div>
      <div>
        <div class="fa fa-trash control-item" @click="removeTodo(index)"></div>
        <div class="fa fa-edit control-item" @click="editTodo(todo)"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-view",
  data() {
    return {
      newTodo: "",
      beforeEditCache: '',
      todos: [
        {
          id: 1,
          title: "Finish Vue task",
          completed: false,
          editing: false,
          description:
            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
        },
        {
          id: 2,
          title: "Take over world",
          completed: false,
          editing: false,
        },
      ],
    };
  },
  methods: {
    addTodo: function (todo) {
      todo.preventDefault();
      if (this.newTodo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.todoId,
        title: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
      this.todoId++;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
    },
  },
};
</script>

<style lang="scss">
.todo-input {
  flex: 10;
  padding: 15px;
  border: 1px solid #d74b76;
  border-radius: 10px 0px 0px 10px;
  outline: 0;
}
.todo-item {
  margin-top: 12px;
  margin-bottom: 12px;
  display: flex;
  font-size: 23px;
  align-items: center;
  justify-content: space-between;
  animation-duration: 0.3s;
}

.control-item {
  margin-left: 14px;
  cursor: pointer;
  &:hover {
    color: #2c3e50;
  }
}

form {
  display: flex;
}

input[type="submit"] {
  flex: 2;
  background: #d74b76;
  color: #fff;
  border-radius: 0px 10px 10px 0px;
  border: 1px #d74b76 solid;
  cursor: pointer;
}
input[type="checkbox"]{
  font: inherit;
  width: 1.15em;
  height: 1.15em;
  transform: translateY(0.075em);
}

.todo-item-left {
  display: flex;
  align-items: center;
}

.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  margin-left: 12px;
}

.todo-item-edit {
  font-size: 20px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  font-family:  Helvetica, Arial, sans-serif;
  border-radius: 5px;
  &:focus {
    outline: none;
  }
}
.completed {
    text-decoration: line-through;
    color: grey;
  }
</style>