<template>
  <ul class="todo-main">
    <Item v-for="(todo,index) in todos" :key="index" :todo="todo" :index = index :deleteTodo='deleteTodo' />
  </ul>
</template>

<script>
import Item from "./todoItem";
export default {
    props:{
        todos:Array,
        deleteTodo:Function
    },
    components:{    //渲染一个组件为动态组件
        Item
    }
};
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>