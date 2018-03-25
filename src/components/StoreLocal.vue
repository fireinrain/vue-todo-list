<template>
  
</template>

<script>
    const STORE_TODO_KEY = "todo_key";

    // 将todo-list列表存储在localstoreage
    export default{
        //保存todo-lists对象列表
        store: function(items){
            window.localStorage.setItem(STORE_TODO_KEY,JSON.stringify(items));
        },

        //获取
        fetchAll:function(){
            return JSON.parse(window.localStorage.getItem(STORE_TODO_KEY))||[];
        }




    }
</script>

<style scoped>

</style>
