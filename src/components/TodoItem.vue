<template>
    <!-- We are binding a class 'is-completed' to the property "todo.completed" (if it's true the class will be asigned) -->
    <div class="todo-item" v-bind:class="{'is-completed': todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markCompleted">
            {{ todo.title }}
            <!-- This emits a event with name 'del-todo' -->
            <button @click="$emit('del-todo', todo.id)" class="del">x</button>
        </p>
    </div>
</template>
<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods: {
        markCompleted(){
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>
<style scoped>
    .todo-item{
        background: azure;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }
    .is-completed{
        text-decoration: line-through;
    }
    .del{
        background: red;
    }
</style>