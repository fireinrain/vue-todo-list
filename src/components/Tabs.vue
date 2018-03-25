<template>
    <div class="filterStates">
        <span class="left">{{unFinishedTodoLength}}&nbsp&nbsp<span>{{changeMessageByState}}</span></span>
        <span class="tabs">
            
            <span
                v-for="state in states"
                :key="state"
                :class="[state,filter=== state ? 'actived':'']"
                @click="toggleFilter(state)"
                @cilck=""
            >{{state}}</span>
        </span>
        <span class="clear" @click="chirldClearAllCompleted()">
            Clear All Done!
        </span>
    </div>
</template>


<script>
export default {
  //props 从父组件接受值
  props: {
    filter: {
      type: String,
      required: true
    },
    todos: {
      type: Array,
      required: true
    }
  },
  data: function() {
    return {
      states: ["All", "Active", "Completed"]
    };
  },
  computed: {
    unFinishedTodoLength() {
      if (this.filter === "All") {
        return this.todos.length;
      }
      if (this.filter === "Active") {
        return this.todos.filter(todo => !todo.completed).length;
      }
      if (this.filter === "Completed") {
        return this.todos.filter(todo => todo.completed === true).length;
      }
    },
    changeMessageByState: function() {
      if (this.filter === "All") {
        return "Items";
      }
      if (this.filter === "Active") {
        return "Items Doing";
      }
      if (this.filter === "Completed") {
        return "Items Done";
      }
    }
  },
  methods: {
    toggleFilter: function(state) {
      // console.log(state);
      this.$emit("toggle", state);
    },
    chirldClearAllCompleted: function() {
      this.$emit("removeAllCompleted");
    }
  }
};
</script>


<style scoped>
.filterStates {
  font-weight: 100px;
  font-family: inherit;
  display: flex;
  justify-content: space-between;
  padding: 5px 0;
  line-height: 30px;
  background-color: #fff;
  font-size: 14px;
  border-radius: 0 0 10px 10px;
}

.left,
.clear,
.tabs {
  padding: 0 10px;
  box-sizing: border-box;
}

.left,
.clear {
  width: 150px;
}
.left {
  text-align: left;
}

.clear {
  text-align: right;
  cursor: pointer;
}
.tabs {
  width: 200px;
  display: flex;
  justify-content: space-around;
}

.tabs * {
  display: inline-block;
  padding: 0 10px;
  cursor: pointer;
  border: 1px solid rgba(175, 47, 47, 0);
}

.tabs *.actived {
  border-color: rgba(175, 47, 47, 0.4);
  border-radius: 5px;
}
</style>
