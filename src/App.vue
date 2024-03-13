<template>
  <h1 class="Title">TodoList</h1>
  <div class="TodoEnter">
    <input
      v-model="todoEnter"
      placeholder="What need to be done"
      @keyup.enter="addTodo(todoEnter)"
    />
    <button @click="addTodo(todoEnter)">Enter</button>
  </div>
  <div class="TodoList">
    <ol v-if="todos.length">
      <li
        v-for="(item, index) of todos"
        :key="item.id"
        v-show="item.show === true"
      >
        <input
          type="checkbox"
          id="checkbox"
          v-model="todos[index].todoCheck"
          @click="checkTodo(index)"
        />
        {{ item.todoItem }}
        <button @click="deleteTodo(index)">x</button>
      </li>
    </ol>
  </div>
  <div class="TodoFilter">
    <button @click="All">All</button>
    <button @click="Done">Done</button>
    <button @click="Undone">Undone</button>
  </div>
</template>

<script>
export default {
  //初始化資料
  data() {
    return {
      todos: [],
      todoEnter: "",
    };
  },

  methods: {
    addTodo(todo) {
      if (todo) {
        this.todos.push({ todoItem: todo, todoCheck: false, show: true });
        this.todoEnter = "";
      }
    },

    deleteTodo(todoIndex) {
      this.todos.splice(todoIndex, 1);
    },

    checkTodo(todoIndex) {
      this.todos[todoIndex].todoCheck = !this.todos[todoIndex].todoCheck;
    },

    All() {
      for (var i = 0; i < this.todos.length; i++) {
        this.todos[i].show = true;
      }
    },

    Done() {
      for (var i = 0; i < this.todos.length; i++) {
        if (!this.todos[i].todoCheck) {
          this.todos[i].show = false;
        } else {
          this.todos[i].show = true;
        }
      }
    },

    Undone() {
      for (var i = 0; i < this.todos.length; i++) {
        if (this.todos[i].todoCheck) {
          this.todos[i].show = false;
        } else {
          this.todos[i].show = true;
        }
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
