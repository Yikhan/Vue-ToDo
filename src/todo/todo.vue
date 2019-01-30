<template>
    <section class="real-app">
      <input 
        type = "text"
        class = "add-input"
        autofocus = "autofocus"
        placeholder = "What to do next?"
        @keyup.enter = "addTodo"
      />
    <vItem 
      :todo="todo"
      v-for="todo in filterTodos"
      :key="todo.id"
      @del="deleteTodo"
    />
    <vTabs 
      :tabSelected="tabSelected" 
      :todos="todos"
      @toggle="toggleTab"
      @clearCompleted='clearCompleted'
    />
    </section>
</template>

<script>
import vItem from './item.vue'
import vTabs from './tabs.vue'
let id = 0;
export default {
  components: {
    vItem, vTabs
  },
  data() {
    return {
      todos: [],
      tabSelected: 'all'
    }
  },
  computed: {
    filterTodos() {
      if (this.tabSelected === 'all') {
        return this.todos
      }
      const isSelectCompleted = this.tabSelected === 'completed'
      return this.todos.filter(todo => todo.completed === isSelectCompleted)
    }
  },
  methods: {
    addTodo(e) {
      this.todos.unshift({
        id: id++,
        content: e.target.value.trim(),
        completed: false,
      })
      // clear field after each input
      e.target.value = ""
    },
    deleteTodo(id) {
      console.log("try delete index ", id)
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    toggleTab(state) {
      this.tabSelected = state
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed)
    },
  }
}
</script>

<style lang="stylus" scoped>
.real-app
  width 600px
  margin auto
  box-shadow 0 0 5px #666
.add-input 
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  outline: none;
  color: inherit;
  padding: 6px;
  border: 1px solid #999;
  box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  font-smoothing: antialiased;
  padding: 16px 16px 16px 60px;
  border: none;
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
</style>


