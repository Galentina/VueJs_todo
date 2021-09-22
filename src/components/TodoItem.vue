<template>
  <li> <span v-bind:class="{done:todo.complete}">
    <input type="checkbox"
           v-on:change="todo.complete=!todo.complete"/>
    <strong>{{index+1}}</strong>
    {{todo.title | uppercase}}
  </span>
    <button class="rm" v-on:click="$emit('remove-todo', todo.id)"
    >&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: Object,
    index: Number,
  },
  filters: {
    uppercase(value) {
      console.log(value)
      return value.toUpperCase()
    }
  },
  name: "TodoItem",

}
</script>

<style scoped>
li{
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin: 1rem;
}
.rm{
  background-color: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
}
input{
  margin-right: 1rem;
}
.done{
  text-decoration: line-through;
}
</style>
