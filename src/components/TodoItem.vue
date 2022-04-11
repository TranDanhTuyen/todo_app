<template>
    <p :class = "['todo-item', todoProps.completed ? 'is-completed' : '']">
      <input type="checkbox" :checked = "todoProps.completed" v-on:change = "markItemCompleted"/>
      {{todoProps.title}}
      <button class="del-btn" @click="deleteItem">Delete</button>
    </p>
</template>

<script>
export default {
    name: "TodoItem",
    props: ['todoProps'],
    setup(props, context) {
        const markItemCompleted = () => {
            //console.log(props.todoProps.id);
            context.emit("item-completed", props.todoProps.id);
        }
        const deleteItem = () => {
            //console.log(props.todoProps.id);
            context.emit("item-deleted", props.todoProps.id);
        }
        return {
            markItemCompleted,
            deleteItem
        }
    }
}
</script>

<style>
.todo-item {
    background: #f4f4f4;
    padding: 10px;
    margin: 0;
    border-bottom: 1px #ccc dotted;
}
.del-btn {
    background: #ff0000;
    color: #fff;
    border: none;
    float: right;
    cursor: pointer;
}
.is-completed {
    text-decoration: line-through;
}
</style>