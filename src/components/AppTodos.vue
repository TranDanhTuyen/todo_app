<template>
    <AddTodo @add-todo = "addTodo"/>
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
import AddTodo from "./AddTodo";
import {v4 as uuidv4} from "uuid";

export default {
    name: "AppTodos",
    components: {
        TodoItem,
        AddTodo,
    },
    setup () {
        const todos = ref([
            {
                id: uuidv4(),
                title: 'Việc 01',
                completed: false,
            },
            {
                id: uuidv4(),
                title: 'Việc 02',
                completed: false,
            },
            {
                id: uuidv4(),
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
        const addTodo = (newTodo) => {
            console.log(newTodo.id);
            todos.value.push(newTodo);
        } 
        return {
            todos,
            markCompleted,
            deleteTodo,
            addTodo,
        }
    }
}
</script>

<style>

</style>