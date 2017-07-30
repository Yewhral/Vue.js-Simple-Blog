<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form v-if="!submitted">
        <label>Blog Title:</label>
        <input type="text" v-model="blog.title" required/>
        <label>Blog Content:</label>
        <textarea v-model="blog.content"></textarea>
        <div id ="checkboxes">
        <p> Periods/tags: </p>
            <label>Nara</label>
            <input type="checkbox" value="Nara" v-model="blog.categories"/>
            <label>Heian </label>
            <input type="checkbox" value="Heian" v-model="blog.categories"/>
            <label>Kamakura </label>
            <input type="checkbox" value="Kamakura" v-model="blog.categories"/>
            <label>Nanboku-cho</label>
             <input type="checkbox" value="Nanboku" v-model="blog.categories"/>
        </div>
        <label>Author:</label>
        <select v-model="blog.author">
            <option v-for="author in authors"> {{author}} </option>
        </select>
        <button v-on:click.prevent="post">Add blog</button>
    </form>
    <div v-if="submitted">
        <p>Thanks for posting!</p>
    </div>
    <div id="preview">
        <h3>Preview Blog</h3>
        <p>Blog title: {{blog.title}} </p>
        <p>Blog content: </p>
        <p>  {{blog.content}} </p>
        <p> Blog Categories: </p>
        <ul>
            <li v-for="category in blog.categories"> {{category}} </li>
        </ul>
        <p> By: {{blog.author}} </p>
    </div>
  </div>
</template>



<script>
export default {
    data () {
        return {
            blog: {
                title: '',
                content: '',
                categories: [],
                author: ''
            },
            authors: ['Yewhral', 'Doethe', 'Lady P'],
            submitted: false
        }
    },
    methods: {
        post: function(){
            this.$http.post('https://fir-for-vue-blog.firebaseio.com/posts.json', this.blog).then(function(data){
                console.log(data);
                this.submitted = true;
            });
        }
    }
}
</script>



<style>
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}

#checkboxes input{
    display: inline-block;
    margin-right: 10px;
}
#checkboxes label{
    display:inline-block;
}
</style>