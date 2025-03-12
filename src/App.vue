/* eslint-disable */
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <my-header :addTodo="addTodo"></my-header>
        <my-list :todos="todos" :handleTodo="handleTodo"></my-list>
        <my-footer :todos="todos" :checkAll="checkAll" :clearAllDone="clearAllDone"></my-footer>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyFooter from './components/MyFooter.vue';
import MyList from './components/MyList.vue';

export default {
  name: 'App',
  components: {
    MyHeader,MyFooter,MyList
  },
  data() {
    return {
        todos:[
            {
                id:'001',
                title:'吃饭',
                isDone:true
            },{
                id:'002',
                title:'睡觉',
                isDone:false
            },{
                id:'003',
                title:'学习',
                isDone:true
            },
        ]
    }
  },
  methods:{
    //添加 todo
    addTodo(todoObj){
        // console.log("@@",todoObj)
        this.todos.unshift(todoObj)
    },
    //已完成或未完成
    handleTodo(id,x){
      // console.log(id)
      this.todos.forEach((todoObj)=>{
        if(todoObj.id === id){
          if(x === 1){
            // console.log("删除")
            this.todos = this.todos.filter((todoObj)=>{
              return todoObj.id !== id
            })
          }else
            todoObj.isDone = !todoObj.isDone
        }
      })
    },
    //全选or全不选
    checkAll(isDone){
      this.todos.forEach((todoObj)=>{
        todoObj.isDone = isDone
      })
    },
    //删除已完成 todo
    clearAllDone(){
      this.todos = this.todos.filter((todoObj)=>{
        return !todoObj.isDone
      })
    }
  }
}
</script>

<style>
  /*base*/
  body {
    background: #fff;
  }
  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }
  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }
  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }
  .btn:focus {
    outline: none;
  }
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
