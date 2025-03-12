/* eslint-disable */
<template>
    <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keydown.enter="addObj"/>
    </div>
</template>

<script>
    import {nanoid} from 'nanoid';
    export default {
        name:'MyHeader',
        props:['addTodo'],
        data() {
            return {
                title:''
            }
        },
        methods:{
            addObj(){
                //处理输入
                if(!this.title) 
                    return alert("输入不能为空")
                // console.log(this.title)
                //将输入包装为对象
                const todoObj ={
                    id:nanoid(),
                    title:this.title,
                    isDone:false
                }
                // console.log(todoObj)
                //将包装袋的对象传给 App
                this.addTodo(todoObj)
                //清空输入框
                this.title=''
            }
        }
    }
</script>

<style scoped>
    /*header*/
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
        box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
    }
</style>