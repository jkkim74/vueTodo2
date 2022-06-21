<template>
    <div>
        <input type="text" v-model="newTodoItem">
        <button v-on:click="addTodo">add</button>
    </div>
</template>

<script>
export default {
    data: function(){
        return {
            newTodoItem: ""
        }
    },
    methods:{
        addTodo: function(){
            console.log(this.newTodoItem);
            //저장로직수행
            localStorage.setItem(this.newTodoItem,this.newTodoItem);
            this.newTodoItem = "";
        }
    }
}
</script>

<style>
</style>