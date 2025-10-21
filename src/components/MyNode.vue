<template>
<h1 class="title">考拉记事本</h1>
<center>
    <ul class="table">
      <li>
        <input class="addli" v-model="taskInput" @keyup.enter="addTask" placeholder="请输入任务..."/>
        
        <button class="addbtn" @click="addTask">添加任务</button>
        </li>
      <li class="line" v-for="(item,index) in tasks" :key='index' @mouseenter="showDel(index)" @mouseleave="hideDel(index)">
        <div>
          {{ index+1 }} . {{ item }}
        </div>
        <button class="delIndex" @click="delTask(index)" :style="{display:delBtn[index]?'block':'none'}">
          ×
        </button>
      </li>
      
      <li v-if="tasks.length>0">
        <div class="total">合计：{{ tasks.length }}</div>
        <button class="clearAll" @click="clearAll">清空任务</button>
      </li>
    </ul>
</center>
</template>
<script setup>
import { ref } from 'vue'
const taskInput = ref('')
// console.log(taskInput)
const tasks = ref(['吃饭', '睡觉', '敲代码', '学习数学1', '学习408', '背单词'])
const addTask=()=> {
  if (taskInput.value.trim()) {
    tasks.value.unshift(taskInput.value.trim())
  }
  taskInput.value=''
}
//定义一个鼠标移入、移出的状态监听器
const delBtn=ref({})
const showDel = (index) => {
  delBtn.value[index]=true
}
const hideDel = (index) => {
  delBtn.value[index]=false
}
// 删除
const delTask = (index) => {
  tasks.value.splice(index,1)
}

const clearAll = () => {
  tasks.value=[]
}
</script>
<style>
body {
  background-color: #f5f5f5;
  margin: 0;
  background: #f5f5f5 url('https://s21.ax1x.com/2025/10/17/pVqq77D.jpg') no-repeat fixed center / cover;
  min-height: 100vh;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style: none;
  color: #666;
  border: none;
}
.title{
  color: #fa6e6e;
  font-size: 30px;
  text-align: center;
  margin: 20px;
  margin-top: 60px;
}
.table{
  width: 600px;
  background-color: white;
  
  padding: 20px;
  border-radius: 8px;
  box-shadow: 2px 3px 4px rgba(0, 0, 0, 0.1); 
}
li{
  height: 40px;
}
li:first-child{
  display: flex;
  align-items: center;
  border: 2px solid #fa6e6e;
  border-radius: 5px;
  margin-bottom: -8px;
}
.addli{
  flex:1;
  background-color: transparent;
  outline: none;
  padding-left:5px ;
}
.addbtn{
  background-color: #fa6e6e;
  font-size: 16px;
  padding: 8px 15px;
  height: 100%;
  color: white;
  cursor: pointer;
}

ul li:not(:first-child):not(:last-child){
  display: flex;
  border-bottom: 1px dashed #eee;
  margin-top: 10px;
  padding-top: 10px;
  padding-left: 10px;
}

.line div{
  text-align: left;
  flex: 1;
}
.delIndex{
  display: none;
  background-color: transparent;
  font-weight: bolder;
  vertical-align: middle;
  font-size: 18px;
  height: 100%;
  padding-right:10px ;
  cursor: pointer;
}

li:last-child{
  text-align: left;
  height: 40px;
  line-height: 40px;
  margin-bottom: -10px;
 display: flex;
}
.total{
font-size: 12px;
 flex: 1;
}
.clearAll{
font-size: 12px;
  background-color: transparent;
  cursor: pointer;
}
</style>