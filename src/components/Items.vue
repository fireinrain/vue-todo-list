<template>
    <div v-bind:class="['todo-item',todo.completed ? 'completed':'']">
        <input type="checkbox" 
                class="toggle"
                v-model="todo.completed">

        <label>{{todo.content}}</label>
        <button class="deleteItem" v-on:click="chirldemoveItem"></button>
    </div>
</template>


<script>
    export default{
        data: function(){
            return{
                //数据来自于父组件
            }
        },
        props:{
            todo:{
                type:Object,        //props验证
                require:true,       //props验证
            }
        },
        methods:{
            chirldemoveItem:function(){
                //向父组件 提交一个函数 并请求父组件处理  传入参数
                this.$emit('removeItem',this.todo.id);
            }
        }
    }
</script>


<style scoped>
    .todo-item{
        position: relative;;
        background-color: #fff;
        font-size: 24px;
        border-bottom: 1px solid rgba(0, 0, 0, 0.06);
        
        
    }
    .todo-item:hover .deleteItem:after{
        content: url('../assets/images/delete.svg')
    }

    .todo-item label{
        white-space: pre-line;
        word-break: break-all;
        padding: 15px 60px 15px 15px;
        margin-left: 45px;
        display: block;
        line-height: 1.2;
        -webkit-transition: color 0.4s;
        -o-transition: color 0.4s;
        transition: color 0.4s;
    }
    .todo-item.completed label{
        color: #d9d9d9;
        text-decoration: line-through;
    }

    .toggle{
            text-align: center;
            width: 28px;
            height: 28px;
            line-height: 40px;
            position: absolute;
            top: 0;
            bottom: 0;
            left: 10px;
            margin: auto 0;
            border: none;
            /* checkbox 默认样式设置为无 */
            appearance: none;
            outline: none;
            padding-left: 5px;
            cursor:pointer;
    }

    .toggle:after{  
        content: url('../assets/images/init.svg');
    }

    .toggle:checked:after{
        content: url('../assets/images/finished.svg');
    }
         
    .deleteItem{
        position: absolute;
        top: 0;
        right: 10px;
        bottom: 0;
        width: 40px;
        height: 40px;
        margin: auto 0;
        font-size: 30px;
        color: #cc9a9a;
        margin-bottom: 6px;
        transition: color 0.2s ease-out;
        background-color:transparent;
        /* appearance:none; */
        border-width: 0;
        cursor:pointer;
        outline: none;
    }

</style>
