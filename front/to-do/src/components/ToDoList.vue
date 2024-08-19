<template>
    <div>
        <h2>To-Do List</h2>
        <input v-model="newTodo" placeholder="Add a new to-do" @keyup.enter="addTodo" type="text">
        <button @click="addTodo">Add</button>

        <ul>
            <li v-for="(todo, index) in todos" :key="index">
                <input type="checkbox" v-model="todo.complted">
                <span :class="{complted: todo.complted}">{{todo.text}}</span>
                <button @click="removeTodo">remove</button>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'ToDoList',

        data() {
            return{
                newTodo: '',
                todos: []
            }
        },
        methods:{
            addTodo(){
                if(this.newTodo.trim()){
                    this.todos.push({text : this.newTodo, complted: false})
                    this.newTodo = ''
                }
            },
            removeTodo(index){
                this.todos.splice(index, 1);
            }
        }
    }
</script>

<style>
.complted{
    text-decoration: line-through;
    color: grey;
}
</style>