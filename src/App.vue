<template>
  <div id="app">
    <div id="cover"></div>
    <TODO_Header/>
    <TODO_Todos/>
    <TODO_Footer/>

  </div>
</template>

<script>
//引入header 组件
import TODO_Header from "./components/Header.vue";

//引入footer组件
import TODO_Footer from "./components/Footer.vue";

//引入todos 组件
import TODO_Todos from "./components/Todos.vue";

export default {
  name: "App",
  //声明该组件下挂载了那些组件
  components: {
    TODO_Header,
    TODO_Footer,
    TODO_Todos
  }
};
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

#app {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}

#cover {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: #555;
  opacity: 0.5;
  z-index: -1;
}
</style>
