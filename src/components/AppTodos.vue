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
//import {v4 as uuidv4} from "uuid";
import axios from "axios";

import TodoItem from "./TodoItem";
import AddTodo from "./AddTodo";


export default {
    name: "AppTodos",
    components: {
        TodoItem,
        AddTodo,
    },
    setup () {
        const todos = ref([]);
        const getAllTodos = async () => {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
                console.log(res.data);
                todos.value = res.data;
            } catch (error) {
                console.log(error);
            }
        }
        getAllTodos();

        const markCompleted = (id) => {
            todos.value = todos.value.map(todo => {
                if(todo.id === id) todo.completed = !todo.completed;
                return todo;
            });
        }
        //Delete phần 4
        // const deleteTodo = (id) => {
        //     todos.value = todos.value.filter(todo => todo.id !== id);
        // }

        const deleteTodo = async (id) => {
            try {
                await axios.delete('https://jsonplaceholder.typicode.com/todos/${id}');
                todos.value = todos.value.filter(todo => todo.id !== id);
            } catch (error) {
                console.log(error);
            }
        }
        //Phần 4
        // const addTodo = (newTodo) => {
        //     console.log(newTodo.id);
        //     todos.value.push(newTodo);
        // }
        
        const addTodo = async (newTodo) => {
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo);
                //console.log(newTodo.id);
                todos.value.push(res.data);
            } catch (error) {
                console.log(error);
            }
        }

        return {
            todos,
            markCompleted,
            deleteTodo,
            addTodo,
            getAllTodos
        }
    }
}
</script>

<style>

</style>