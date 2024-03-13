<template>
  <h1 class="Title">TodoList</h1>
  <!-- 代辦事項輸入框 -->
  <div class="TodoEnter">
    <input
      v-model="todoEnter"
      placeholder="What need to be done"
      @keyup.enter="addTodo(todoEnter)"
    />
    <button @click="addTodo(todoEnter)">Enter</button>
  </div>
  <!-- 顯示代辦事項 -->
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
  <!-- 分類代辦事項 全部All已完成Done未完成Undone -->
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
    // 新增代辦事項
    addTodo(todo) {
      if (todo) {
        this.todos.push({ todoItem: todo, todoCheck: false, show: true });
        this.todoEnter = "";
      }
    },
    // 刪除代辦事項
    deleteTodo(todoIndex) {
      this.todos.splice(todoIndex, 1);
    },
    // 代辦事項確認框
    checkTodo(todoIndex) {
      this.todos[todoIndex].todoCheck = !this.todos[todoIndex].todoCheck;
    },
    // filter-All 全部代辦事項
    All() {
      for (var i = 0; i < this.todos.length; i++) {
        this.todos[i].show = true;
      }
    },
    // filter-Done 已完成代辦事項
    Done() {
      for (var i = 0; i < this.todos.length; i++) {
        if (!this.todos[i].todoCheck) {
          this.todos[i].show = false;
        } else {
          this.todos[i].show = true;
        }
      }
    },
    // filter-Undone 未完成代辦事項
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
