/* eslint-disable */
<template>
    <li>
        <label>
            <input type="checkbox" :checked="todoObj.isDone" @change="isCheck(todoObj.id)"/>
            <span>{{todoObj.title}}</span>
        </label>
        <button class="btn btn-danger" @click="delTodo(todoObj.id)">删除</button>
    </li>
</template>

<script>
    export default {
        name:'MyItem',
        props:['todoObj','handleTodo'],
        methods:{
            //勾选or 取消勾选
            isCheck(id){
                // console.log(id)
                this.handleTodo(id,0)
            },
            //删除 todo
            delTodo(id){
                // console.log(id)
                if(confirm("确定删除吗？")){
                    this.handleTodo(id,1)
                }
            }
        }
    }
</script>

<style scoped>
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
        display: none;
        margin-top: 3px;
    }

    li:before {
        content: initial;
    }

    li:last-child {
        border-bottom: none;
    }
    li:hover{
        background-color: #ddd;
    }
    li:hover button{
        display: block;
    }
</style>