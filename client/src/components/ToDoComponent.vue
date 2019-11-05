<template>
  <div class="container" >
    <h1>ToDo List</h1>
    <div class="create-post">
      <input v-on:keyup.enter="createPost" type="text" id="create-post" v-model="text" placeholder="Create a ToDo">
    </div>
    <hr>
    <p class="error" v-if="error">{{ error }}</p>
    <div class="post-container">
      <div class = "post"
        v-for="(post, index) in posts"
        v-bind:item="post"
        v-bind:index="index"
        v-bind:key="post._id"
        
      >
      {{ `${post.createdAt.getDate()}/${post.createdAt.getMonth()}/${post.createdAt.getFullYear()}` }}s
      <div class="row">
          <p class="text col-90">{{ post.text }}</p> 
          <button class="delete col-10" v-on:click="deletePost(post._id)">x</button>
      </div>
        
        
      </div> 
    </div>
  </div>

</template>

<script>
import PostService from '../PostService'
export default {
  name: 'ToDoComponent',
  data() {
    return {
      posts: [],
      error: '',
      text: ''
    }
  },
  async created() {
    try {
      this.posts = await PostService.getPosts()
    } catch(err) {
      this.error = err.message
    }
  },
  methods: {
    async createPost() {
      await PostService.insertPost(this.text)
      this.text = ""
      this.posts = await PostService.getPosts()
    },
    async deletePost(id) {
      await PostService.deletePost(id)
      this.posts = await PostService.getPosts()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row { 
  
	display: flex;
	align-items: center;
	justify-content: center;
	overflow: hidden;
	margin-bottom: 5px; 
	border-radius: 5px; 
  z-index: 3;

}
.col-5 { width: 5%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-10 { width: 10%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-15 { width: 15%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-20 { width: 20%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-25 { width: 24%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-30 { width: 30%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-33 { width: 33.33%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-35 { width: 35%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-40 { width: 40%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-45 { width: 45%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-50 { width: 50%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-55 { width: 55%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-60 { width: 60%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-65 { width: 65%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-70 { width: 70%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-75 { width: 75%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-80 { width: 80%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-85 { width: 85%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-90 { width: 90%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-95 { width: 95%; min-height: 10px; display: block; float: left; box-sizing: border-box; }
.col-100 { width: 100%; min-height: 10px; display: block; box-sizing: border-box; }

button.delete {
  width: 30px;
  height: 30px;
  font-size: 29px;
  text-align: center;
  line-height: 1px;
}
input {
  width: 95%;
  height: 30px;
}
div.container {
  max-width: 800px;
  margin: 0 auto;
}

p.error {
  border: 1px solid #ff5b5f;
  background-color: #ffc5c1;
  padding:  10px;
  margin-bottom: 15px;
}

div.post {
  position: relative;
  border: 1px solid grey;
  background-color:  white;
  padding: 10px 10px 30px 10px;
  margin-bottom: 15px;
  height: auto;
}

div.created-at {
  position: absolute;
  top: 0;
  left: 0;
  padding: 5px 15px 5px 15px;
  background-color: darkgreen;
  color: white;
  font-size: 13px;
}

p.text {
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 0;

}
</style>