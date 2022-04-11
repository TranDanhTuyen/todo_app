<template>
  <TodoItem v-for="todo in todos" v-bind:key = "todo.id" v-bind:todoProps = "todo"/>
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
                completed: true,
            },
            {
                id: 2,
                title: 'Việc 02',
                completed: false,
            },
            {
                id: 3,
                title: 'Việc 03',
                completed: true,
            }
            ]);
        return {
            todos,
        }
    }
}
</script>

<style>

</style>