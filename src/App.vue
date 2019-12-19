<template>
    <div id="app">
        <Header/>
        <AddTodo v-on:add-todo="addTodo"/>
        <!-- Here we catch 'del-todo' that is created in "TodoItem.vue" -->
        <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    </div>
</template>
<script>
import Todos from './components/Todos.vue';
import Header from './components/layouts/Header.vue';
import AddTodo from './components/AddTodo.vue';
import axios from 'axios';

export default {
    name: 'app',
    components: {
        Todos,
        Header,
        AddTodo
    },
    data(){
        return{
            todos: []
        }
    },
    methods: {
        deleteTodo(id){
            console.log("deleteTodo");
            this.todos = this.todos.filter(todo => todo.id !== id);
        },
        addTodo(newTodo){
            console.log("addTodo");
            this.todos = [...this.todos, newTodo];
        }
    },
    created(){
            axios.get('https://jsonplaceholder.typicode.com/todos?')
            .then(res => this.todos = res.data)
            .catch(err => console.log(err));
    }
}
</script>
<style>
    body{
        font-family: Arial, Helvetica, sans-serif;
        line-height: 1.4;
        margin: 0;
        padding: 0;
    }
    .btn{
        display: inline-block;
        border: none;
        background: #555;
        color: #fff;
        padding: 7px 20px;
        cursor: pointer;
    }
    .btn:hover{
        background: #666; 
    }
</style>