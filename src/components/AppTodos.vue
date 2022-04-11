<template>
  <TodoItem 
  v-for="todo in todos" 
  v-bind:key = "todo.id" 
  v-bind:todoProps = "todo"
  v-on:item-completed = "markCompleted"
  v-on:item-deleted = "deleteTodo"
  />
</template>

<script>    
import { ref } from "vue";
import TodoItem from "./TodoItem";

export default {
    name: "AppTodos",
    components: {
        TodoItem,
    },
    setup () {
        const todos = ref([
            {
                id: 1,
                title: 'Việc 01',
                completed: false,
            },
            {
                id: 2,
                title: 'Việc 02',
                completed: false,
            },
            {
                id: 3,
                title: 'Việc 03',
                completed: false,
            }
            ]);
        const markCompleted = (id) => {
            todos.value = todos.value.map(todo => {
                if(todo.id === id) todo.completed = !todo.completed;
                return todo;
            });
        }
        const deleteTodo = (id) => {
            todos.value = todos.value.filter(todo => todo.id !== id);
        }
        return {
            todos,
            markCompleted,
            deleteTodo,
        }
    }
}
</script>

<style>

</style>