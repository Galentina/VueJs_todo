<template>
  <div >
    <h2>To application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
        @add-todo="addTodo"/>
    <hr/>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr/>
    <Loader v-if="loading"/>
    <TodoList
        v-else-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: 'App',
  data(){
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(responce => responce.json())
        .then(json => {setTimeout(()=>{
          this.todos = json
          this.loading = false
        }, 1000)
        })
  },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    filteredTodos() {
      if(this.filter==='all'){
        return this.todos
      }
      if(this.filter==='completed'){
        return this.todos.filter(el=> el.complete===true)
      }
      if(this.filter==='not-completed'){
        return this.todos.filter(el=> !el.complete)
      }
      return this.todos
    }
  },
  components: {
    AddTodo,
    TodoList,
    Loader
  },
  methods: {
    removeTodo(id) {
      this.todos=this.todos.filter(el=> el.id!==id)
    },
    addTodo(item) {
      this.todos.push(item)
    }
  }
}
</script>

<style scoped>

</style>
