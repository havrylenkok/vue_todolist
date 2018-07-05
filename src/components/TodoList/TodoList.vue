<template>
  <div class="todolist-component">
    <h1>Super mega huge todo list</h1>
    <BaseInputText v-model="newTodoText" placeholder="New todo" @keydown.enter="addTodo"/>
    <ul v-if="todos.length">
      <TodoListItem v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo"/>
    </ul>
    <p v-else>You've done every task! Add more</p>
  </div>
</template>

<script>
import BaseInputText from '../Base/BaseInputText'
import TodoListItem from './TodoListItem'

let nextTodoId = 1
export default {
  name: 'TodoList',
  components: {TodoListItem, BaseInputText},
  data () {
    return {
      newTodoText: '',
      todos: [
        {
          id: nextTodoId++,
          text: 'Find a question for that 42 answer'
        },
        {
          id: nextTodoId++,
          text: 'Push this to github so everyone know you are into Vue now'
        },
        {
          id: nextTodoId++,
          text: 'Idk lol'
        }
      ]
    }
  },

  methods: {
    addTodo () {
      const trimmedText = this.newTodoText.trim()
      if (trimmedText) {
        this.todos.push({id: nextTodoId++, text: trimmedText})
        this.newTodoText = ''
      }
    },
    removeTodo (idToRemove) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== idToRemove
      })
    }
  }
}
</script>

<style scoped>

</style>
