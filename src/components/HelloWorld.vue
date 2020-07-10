<template>
  <div>
    <div class="header">
      <div class="container">
        <div class="logo">toDoList</div>
        <div class="input-area">
          <input type="text" v-model="inpVal">
          <button @click="addEvent">添加</button>
        </div>
      </div>
    </div>
    <div class="container">
      <h2>
        <span>正在进行</span>
        <span class="mask-num">{{ progressList.length }}</span>
      </h2>
      <ul class="mask-list">
        <li v-for="(item,index) in progressList" :key="index">
          <div>
            <input type="checkbox" @click="check(index)">
            <span>{{ item }}</span>
          </div>
          <button @click="deleteProgress(index)">删除</button>
        </li>
      </ul>
    </div>
    <div class="container">
      <h2>
        <span>已经完成</span>
        <span class="mask-num">{{ completeList.length }}</span>
      </h2>
      <ul class="mask-list complete-list">
        <li v-for="(item,index) in completeList" :key="index">
          <div>
            <input type="checkbox">
            <span>{{ item }}</span>
          </div>
          <button @click="deleteComplete(index)">删除</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      inpVal: '',
      progressList: [],
      completeList: []
    }
  },
  methods: {
    addEvent(){
      console.log(this.inpVal)
      this.inpVal && this.progressList.push(this.inpVal)
      this.inpVal = '';
    },
    check(index){
      const content = this.progressList.splice(index,1);
      console.log(content)
      this.completeList.push(...content);
    },
    deleteProgress(index){
      this.progressList.splice(index,1);
    },
    deleteComplete(index){
      this.completeList.splice(index,1);
    }
  }
}
</script>


<style>
* {
  padding: 0;
  margin: 0;
  list-style: none;
}

h2 {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 10px 0;
}

h2 .mask-num {
  height: 20px;
  padding: 0 5px;
  border-radius: 20px;
  background-color: #e6e6fa;
  color: #666;
  font-size: 14px;
}

body {
  background-color: #cdcdcd;
}

.container {
  width: 600px;
  margin: 0 auto;
  padding: 0 10px;
}

.header {
  height: 50px;
  background-color: #333;
}

.header .container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header .container .logo {
  width: 100px;
  line-height: 50px;
  color: #ddd;
  font-size: 24px;
  cursor: pointer;
}

.header .container .input-area {
  width: 60%;
}

.header .container .input-area input {
  width: 80%;
  height: 24px;
  text-indent: 10px;
  border-radius: 5px;
  box-shadow: 0 1px 0 rgba(255, 255, 255, 0.24), 0 1px 6px rgba(0, 0, 0, 0.45) inset;
  border: none;
  outline: none;
}

.header .container .input-area button {
  width: 15%;
  height: 24px;
  vertical-align: center;
}

.mask-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 32px;
  line-height: 32px;
  margin-bottom: 10px;
  padding: 0 15px;
  border-radius: 3px;
  border-left: 5px solid #629A9C;
  background-color: #fff;
}

.mask-list.complete-list li {
  border-left-color: #999;
  opacity: .5;
}

</style>