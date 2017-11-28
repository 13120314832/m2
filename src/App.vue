// import Header from './Header'
// import Footer from './Footer'

// new Vue({
//   el: '#app',
//   data:{

//   },
//   //注册
//   components: [
//     // {Header},
//     // {Footer}
//     Header,Footer
//   ]
// })
<template>
  <div id="app">
    <!-- <h1>{{title}}</h1>
    <h1 v-text="title"></h1> -->
    <h1 v-html="title"></h1>
    <input placeholder="请输入事项..." v-model="newItem" v-on:keyup.enter="addNew">
    <ol>
      <!-- <li v-for="item in items" v-bind:class="{finishen:item.isFinshed}"> -->
      <!-- <li v-for="item in items" v-bind:class="{finishen:item.isFinshed}" v-on:click="toggleFinish(item)">         -->
      <li v-for="(item,index) in items" :key="index" v-bind:class="{finishen:item.isFinshed}" v-on:click="toggleFinish(item)">        
        {{item.label}}
        <button v-on:click="Delete(index)">删除</button>
        <!-- <span>{{Data}}</span> -->
      </li>
    </ol>
    <header msg='someting interesting'>{{header}}</header>
    <!-- <footer>{{footer}}</footer> -->
    <!-- <components-a msgfromfather='you die!'></components-a> -->
  </div>
</template>
<script>
import Store from './store'
import componentsA from './components/componentsA'
// console.log(Store);
export default {
  data: function() {
    return {
      title:'<span>*</span>this is a todo list',
      items:Store.fetch(),
      newItem:'',
      header:'注：删除线表示该项已完成',
      footer:'这里是footer',
      msgfromfather:''
      // liClass:'thisisLiClass'
    }
  },
  components:{componentsA},//注册 儿子
  watch:{
    items:{
      handler:function(items){//存到localStorage
        Store.save(items)
      },
      deep:true
    }
  },
  methods:{
    toggleFinish:function(item){//点击失去class
      item.isFinshed = !item.isFinshed        
    },
    addNew:function(){
      this.items.push({
        label:this.newItem,
        isFinshed:false
      })
      this.newItem = ''//输入input后清除input框中的文字
    },
    Delete:function(index){//点击button按钮 删除li
      this.items.splice(index,1) 
    }
  }
}
</script>
<style>
button{
  float: right;
  border-style: none;
}
button:hover{
  color: red;
}
li{
  /* list-style-type:none; */
  margin: 10px 35px 10px 0;
  color:black;
  /* padding: 0 0 1px 0; */
  border: 1px solid black;  
}
span{
  color: red;
}
.finishen{
  text-decoration: line-through;/*删除线*/
  color: #aaa;
  background: #ddd;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 400px;
  margin: 60px auto 0;
  border: 1px solid black;
}
</style>
