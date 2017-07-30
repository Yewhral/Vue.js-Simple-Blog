<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="search blogs"/>
        <div v-for="blog in filteredBlogs" class="single-blog">
            <router-link v-bind:to="'/blog/'+ blog.id"><h2 v-rainbow> {{ blog.title | to-uppercase}} </h2></router-link>
            <h3> {{ blog.content | snippet}} </h3>
        </div>
  </div>
</template>



<script>

import searchMixin from '../mixins/searchMixins';

export default {
  data () {
    return {
        blogs:[],
        search: ''
    }
  },
  methods: {

  },
  created(){
    this.$http.get('https://fir-for-vue-blog.firebaseio.com/posts.json').then(function(data){
        return data.json();
    }).then(function(data){
        var blogsArray = [];
        for (let key in data){
            data[key].id = key;
            blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;

    });
   },

    filters:{
      toUppercase(value){
        return value.toUpperCase();
      }
    },
    mixins: [searchMixin]
}
</script>



<style>
#show-blogs{
    margin: 0 auto;
}
.single-blog{
    padding:20px;
    margin:20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>
