<template>
  <div id="app">
    
    <AddTodo v-on:add-Todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteObject"/>
    
  </div>
</template>

<script>
import Todos from '../components/Todos'

import AddTodo from '../components/AddTodo'
import axios from'axios';
// Load the full build.
var _ = require('lodash');
export default {
  
  name: 'Home',
  components: {
   Todos,
   
   AddTodo
  
  },


  data(){
    return {
      todos:[
        
      ]
    }
  },
  methods:{
    deleteObject(id){
       // this.todos = this.todos.filter(todo => todo.id !== id);
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res=> 
       {this.todos= _.remove(this.todos, (todo)=> todo.id!==id);
       console.log(res);
      })
      .catch(err=> console.log(err));

      
    },
    addTodo(newTodo){
      const{title, completed}=newTodo;
       axios.post("https://jsonplaceholder.typicode.com/todos",{title,completed})
       .then(res=> this.todos= [...this.todos, res.data])
       .catch( err=> console.log(err));

      
    },
   
  },
  created(){
     axios.get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res=> this.todos=res.data)
      .catch(err=>console.log(err));
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

btn:hover{
  background: #666;
}

</style>
