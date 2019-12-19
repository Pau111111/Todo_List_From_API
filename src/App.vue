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
        //This funcion is called in <template>: v-on:del-todo="deleteTodo"
        deleteTodo(id){
            console.log("deleteTodo");
            axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
            .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
            .catch(err => console.log(err));
        },
        //This funcion is called in <template>: v-on:add-todo="addTodo"
        addTodo(newTodo){
            console.log("addTodo");
            const {title, completed} = newTodo;

            axios.post('https://jsonplaceholder.typicode.com/todos', {
                title,
                completed
            })
            .then(res => this.todos = [...this.todos, res.data])
            .catch(err => console.log(err));
        }
    },
    //This is called once all the app is created
    created(){
            axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
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