<template>
  <div id="app">
   <h1>{{title}}</h1>

   <input type="text" name="" v-model="newItem" @keyup.enter="addNew">

   <ul>
     <li v-for='item in lists' :class={isF:item.isF} @click="toggleMenu(item)">
       {{item.label}}
     </li>
   </ul>
   <p>child:{{childwords}}</p>
   <component-a v-on:child-tell='listen' msgfromfather='我来自父亲'></component-a>
 </div>
</template>

<script>
  import Store from './store';
  import ComponentA from './components/componentA'

  export default {
    data(){
      return {
        title:'This is a todo list!',
        lists:Store.fetch(),
        newItem:' ',
        childwords:''
      }
    },
    components:{ComponentA},
    methods: {
      toggleMenu:function(item){
        item.isF=!item.isF;
      },
      addNew:function(){
        this.lists.push({label:this.newItem,isF:false});
        this.newItem='';
      },
      listen:function(msg){
        this.childwords=msg; 
      }
    },
    watch:{
      lists:{
        handler:function(lists){
          Store.save(lists);
        },
        deep:true
      }
    }
  }
</script>

<style>
  .isF{
    color:red;
  }
</style>
