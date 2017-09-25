<template>
  <div id="app">
    <img src="./assets/logo.png">

    <h1>{{message}}</h1>
    <input v-model="newItems" v-on:keyup.enter="addItems">
    <ol>
      <li v-for="item in items" v-bind:class="{Finished:item.isFinished}" v-on:click="tagleFinished(item)">{{item.label}}</li>
    </ol>
  </div>
</template>

<script>
import Store from './store.js'
console.log(Store)
export default {
  name: 'app',
  data:function(){
    return{
      message:"hello",
      items:Store.fetch(),
      newItems:" "
    }
  },
  watch:{
items:{
  handler:function(items)
  {
    Store.save(items)
  },
  deep:true
}
  },
  methods:{
    tagleFinished:function(item)
    {
      item.isFinished=!item.isFinished
      alert(item.label+" is "+((item.isFinished==true)?"finished":"unfinished"))
    },
    addItems:function()
    {
      this.items.push(
                {
                    label:this.newItems,
                    isFinished:false
                }),
      this.newItems=" "
      Store.save(this.newItems)
    }
  }
}
</script>

<style>
.Finished{
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
