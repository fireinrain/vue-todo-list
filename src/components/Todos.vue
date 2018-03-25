<template>
    <section class="todos-container">
        <input type="text" 
                class="add_item"
                autofocus="autofocus"
                placeholder="亲 ~(@^_^@)~,不做点什么吗?"
                v-on:keyup.enter="addTodoItem">

        <!-- items 事项列表-->
        <TODO_Items :todo="todo"
                    v-for="todo in filteredTodos"
                    :key="todo.id"
                    @removeItem="deleteTodo" />

        <!-- tabs 选择 -->
        <TODO_Tabs :filter="filter"
                    :todos="todos"
                    @toggle="toggleFilter"
                    @removeAllCompleted="clearAllCompleted"/>
        
    </section>
</template>


<script>
// 导入子组件 Item
import TODO_Items from "./Items.vue";
import TODO_Tabs from "./Tabs.vue";
import TODO_Store_Local from "./StoreLocal.vue";

let item_id=0;

export default {
  data: function() {
    return {
      todos: TODO_Store_Local.fetchAll(),
      filter: "All", //所有的
      
      
    };
  },
  //当实例被创建时加载数据
  
  

  // 计算属性
  computed: {
    filteredTodos() {
      if (this.filter === "All") {
        return this.todos;
      }
      if (this.filter === "Active") {
        return this.todos.filter(todo => !todo.completed);
      }
      if (this.filter === "Completed") {
        return this.todos.filter(todo => todo.completed === true);
      }
    }
  },
  beforeCreate:function(){
      let length = TODO_Store_Local.fetchAll().length;
      item_id = length-1;
  },

  //watch监视data中数据变化
  watch: {
    todos: {
      handler: function(todos) {
        TODO_Store_Local.store(todos);
      },
      deep: true
    }
  },
  methods: {
    addTodoItem(item) {
      // 内容不能为空
      if (item.target.value.trim()) {
        let new_push = {
          id: item_id++,
          content: item.target.value.trim(),
          completed: false
        };
        this.todos.unshift(new_push);
        TODO_Store_Local.store(this.todos);
        item.target.value = "";
      } else {
        alert("输入为空，你是不是想偷懒?（*>.<*）");
      }
    },
    deleteTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1);
    },
    // 依据状态显示符合 状态的项
    toggleFilter(state) {
      this.filter = state;
      //console.log("fater"+state);
    },

    clearAllCompleted() {
      this.todos = this.todos.filter(todo => todo.completed === false);
    }
  },

  // 声明子组件
  components: {
    TODO_Items,
    TODO_Tabs
  }
};
</script>


<style scoped>
.todos-container {
  width: 600px;
  margin: 0 auto;
  box-shadow: 0 0 5px #666;
  /* 与add_item 圆角重合 */
  border-radius: 10px 10px 10px 10px;
}
.add_item {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  outline: none;
  color: inherit;
  box-sizing: border-box;
  padding: 16px 16px 16px 36px;
  border: none;
  box-shadow: inset 0 -2 1px rgba(0, 0, 0, 0.03);

  border-radius: 10px 10px 0 0;
}
</style>
