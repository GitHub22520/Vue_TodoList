/* eslint-disable */
<template>
    <div class="todo-footer" v-show="todoTotal">
        <label>
            <!-- <input type="checkbox" :checked="isAll" @change="AllDone"/> -->
            <input type="checkbox" v-model="isAll"/>
        </label>
        <span>
            <span>已完成{{ DoneTotal }}</span> / 全部{{ todoTotal }}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div>
</template>

<script>
    export default {
        name:'MyFooter',
        props:['todos','checkAll','clearAllDone'],
        computed:{
            DoneTotal(){
                return this.todos.reduce((pre,todoObj)=>{
                    return pre + (todoObj.isDone ? 1 : 0)
                },0)
                // let DoneCount = 0
                // this.todos.forEach((todoObj)=>{
                //     if(todoObj.isDone)
                //         DoneCount++
                // })
                // return DoneCount
            },
            todoTotal(){
                return this.todos.length
            },
            isAll:{
                // return this.DoneTotal === this.todoTotal && this.todoTotal > 0
                get(){
                    return this.DoneTotal === this.todoTotal && this.todoTotal > 0
                },
                set(val){
                    this.checkAll(val)
                }
            }
        },
        methods:{
            AllDone(e){
                // console.log("全选",e.target.checked)
                this.checkAll(e.target.checked)
            },
            clearAll(){
                if(this.DoneTotal === 0)
                    return alert("没有已完成任务")
                if(confirm("确定清除已完成任务吗？"))
                    this.clearAllDone()
            }
        }
    }
</script>

<style scoped>
    /*footer*/
    .todo-footer {
        height: 40px;
        line-height: 40px;
        padding-left: 6px;
        margin-top: 5px;
    }

    .todo-footer label {
        display: inline-block;
        margin-right: 20px;
        cursor: pointer;
    }

    .todo-footer label input {
        position: relative;
        top: -1px;
        vertical-align: middle;
        margin-right: 5px;
    }

    .todo-footer button {
        float: right;
        margin-top: 5px;
    }
</style>