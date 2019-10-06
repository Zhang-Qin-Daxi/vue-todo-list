<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" @keyup.enter="addItem" v-model="title" />
  </div>
</template>

<script>
export default {
  props: {
    addTodo: Function
  },
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addItem() {
      const title = this.title;
      if (!title) {
        alert("请输入内容名称");
        return false;
      }
      const todo = {
        title,
        complete: false
      };
      // 第一种方式
      //  添加到addTodos
      // this.addTodo(todo);

      // 第二种 方式
      //触发自定义事件（@）: addTodo
      this.$emit('addTodo',todo);

      this.title = "";
    }
  }
};
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>