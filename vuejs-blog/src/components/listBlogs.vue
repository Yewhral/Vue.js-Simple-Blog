<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>List Blog title</h1>
    <input type="text" v-model="search" placeholder="search blogs"/>
        <div v-for="blog in filteredBlogs" class="single-blog">
            <h2 v-rainbow> {{ blog.title | to-uppercase}} </h2>
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
    this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
        console.log(data);
        this.blogs = data.body.slice(0,10);
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
