<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            
                <mti_todo v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem';
export default {
    name: "Todos",
    
    components:{
      mti_todo: TodoItem
},
    props: ["todos"],
    
}
</script>

<style lang="stylus" scoped>

</style>