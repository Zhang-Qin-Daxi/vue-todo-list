<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <!-- 第三种方式 -->
        <TodoHeader ref="header" />

        <!-- 第二种方式 -->
        <!-- 给TodoHeader标签对象绑定addTodo事件监听 -->
        <!-- <TodoHeader @addTodo="addTodo" /> -->

        <!-- 第一种方式 -->
        <!-- <TodoHeader :addTodo="addTodo" /> -->
        <TodoList :deleteTodo="deleteTodo" :todos = "todos" />
        <TodoFooter :todos="todos" :deleteCompleteTodos="deleteCompleteTodos" :selectAllTodo="selectAllTodo" />
        <!-- 另一种写法
        <todo-footer/>-->
      </div>
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/todoHeader.vue";
import TodoList from "./components/todoList.vue";
import TodoFooter from "./components/todoFooter.vue";

export default {
  data() {
    return {
      //从localStorage读取todos
      todos: JSON.parse(window.localStorage.getItem('todos_key') || '[]')
    };
  },
  // 第三种方式
  mounted(){  //执行异步代码
    // 给<TodoHeader /> 绑定addTodo事件监听
    this.$refs.header.$on('addTodo',this.addTodo)
  },
  methods:{
        //删除所有选中的todo
    deleteCompleteTodos(){
      this.todos = this.todos.filter(todo => !todo.complete)
    },
    //全选/全不选
    selectAllTodo(check){
      this.todos.forEach(todo => todo.complete = check)
    },
    deleteTodo(index){
      this.todos.splice(index,1)
    },
    addTodo(todo){
      this.todos.unshift(todo);
    },
  },
  watch:{ //监视
    todos:{
      deep:true,  //深度监视
      handler:function(value){
        //将todos最新的值的json数据，保存到localstorage
        window.localStorage.setItem('todos_key',JSON.stringify(value))
      }
    }
  },
  components: {
    TodoHeader,
    TodoList,
    TodoFooter
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
