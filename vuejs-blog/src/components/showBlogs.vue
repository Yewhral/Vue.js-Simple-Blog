<template>
  <div id="show-blogs">
    <h1>All Blog Articles</h1>
        <div v-for="blog in blogs" class="single-blog">
            <h2> {{ blog.title}} </h2>
            <h3> {{ blog.body }} </h3>
        </div>
  </div>
</template>



<script>


export default {
  data () {
    return {
        blogs:[]
    }
  },
  methods: {

  },
  created(){
    this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
        console.log(data);
        this.blogs = data.body.slice(0,10);
    });
    }
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
