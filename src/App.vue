<template>
  <div id="app">
    <comment v-for="item in items" v-bind="item" v-bind:key="item.id"></comment>
    <observer v-on:intersect="intersected"/>
  </div>
</template>

<script>
import Observer from './components/Observer'
import Comment from './components/Comment'
export default {
  name: 'App',
  components: {
    Comment,
    Observer
  },
  data(){
    return{
      items:[],
      page: 1
    }
  },
  methods: {
    async intersected(){
      const res = await fetch(`https://jsonplaceholder.typicode.com/comments?_page=${this.page++}`);
      const items= await res.json();
      this.items= [...this.items, ...items];
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
