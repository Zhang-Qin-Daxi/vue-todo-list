<template>
  <li
    @mouseenter="handleEnter(true)"
    @mouseleave="handleEnter(false)"
    :style="{background:bgColor}"
    :class="isActive? 'active': ''"
  >
    <label>
      <input type="checkbox" v-model="todo.complete" />
      <span>{{todo.title}}</span>
    </label>
    <button @click="deleteItem" class="btn btn-danger" v-show="isShow">删除</button>
  </li>
</template>

<script>
export default {
  name: 'Item',
  props: {
    todo: Object,
    index: Number,
    deleteTodo: Function
  },
  data() {
    return {
      bgColor: "#fff",
      isShow: false,
      isActive: false
    };
  },
  methods: {
    activeFun () {
      this.isActive = true
    },
    defaultFun () {
      this.isActive = false
    },
    deleteItem() {
      const { index } = this;
      this.deleteTodo(index);
    },
    handleEnter(isMouse) {
      if (isMouse) {
        this.bgColor = "#555";
        this.isShow = true;
      } else {
        this.bgColor = "#fff";
        this.isShow = false;
      }
    }
  }
};
</script>

<style scoped>
.active {
  width: 100px;
  height: 100px;
  float: left;
  border: 1px solid #ddd;
}
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>