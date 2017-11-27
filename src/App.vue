<template>
  <div id="app">
    <!-- <h1>{{title}}</h1>
    <h1 v-text="title"></h1> -->
    <h1 v-html="title"></h1>
    <ul>
      <!-- <li v-for="item in items" v-bind:class="{finishen:item.isFinshed}"> -->
      <li v-for="item in items" 
      v-bind:class="{finishen:item.isFinshed}" 
      v-on:click="toggleFinish(item)">        
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      title:'<span>??</span>this is a todo list',
      items:[
        {
          label:'codeing',
          isFinshed:true
        },
        {
          label:'walking',
          isFinshed:true
        }
      ]
      // liClass:'thisisLiClass'
     
    }
  },
  methods:{
    toggleFinish:function(item){
      item.isFinshed = !item.isFinshed        
    }
  }
}
</script>

<style>
.finishen{
  text-decoration: underline;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
