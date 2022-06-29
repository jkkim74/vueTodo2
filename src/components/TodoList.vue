<template>
  <div>
   <ul>
    <li v-for="(todoItem, index) in todoItems " v-bind:key="todoItem" class="shadow">
    <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem,index)"></i>
    <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
    <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
      <i class="removeBtn fas fa-trash-alt"></i>
    </span>
    </li>
   </ul>
  </div>
</template>

<script>
export default {
  data: function(){
    return {
      todoItems: []
    }
  },
  methods:{ 
    removeTodo: function(todoItem, index){
      console.log(todoItem, index);
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    },
    toggleComplete: function(todoItem,index){
      console.log(todoItem,index);
      todoItem.completed = !todoItem.completed;
      // localStorage는 업데이트가 없으므로 해당 ITEM을 삭제 후, 재정의하여 업데이트 처리를 한다..
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item,JSON.stringify(todoItem));
    }
  },
  created:function(){
      if(localStorage.length >= 0){
        for(var i = 0 ; i < localStorage.length ; i ++){
          if(localStorage.key(i) !== "loglevel:webpack-dev-server"){
            //this.todoItems.push(localStorage.key(i));
            // console.log(localStorage.key(i));
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          }
        }
      }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  /* color: black; */
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  /* color: #62acde; */
  color: black;
}
.textCompleted {
  text-decoration: line-through;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>