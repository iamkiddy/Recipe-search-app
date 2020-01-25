<template>
  <div id="app">
    <div class="receipe-container">
      <div class="container">
        <h1 class="text">Recipe Search App</h1>
        <div class="search-bar">
          <form class="form" v-on:submit.prevent="onSubmit">
            <input type="text" v-model="query" class="search" placeholder="Search for your favourite recipe">
          </form>
          </div>
        </div>
        <div class="output">
          <div class="card" v-for="(item,index) in results" :key="index">
          <img :src="`https://spoonacular.com/recipeimages/${item.id}90x90.jpg&${item.image}`" alt="receipe image"><br>
          Recipes name : {{item.title}} <br>
          Ready in minutes : {{item.readyInMinutes}}
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data(){
    return {
      query:'',
      results:[]
    }
  },
  methods:{
    onSubmit(){
      axios.get(`https://api.spoonacular.com/recipes/search?query=${this.query}&number=3&apiKey=89ec3200076941aea9df44b9e1820f7c`)
      .then((response)=>{
        this.results = response.data.results;
        this.query = '';
      })
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Poppins|Roboto&display=swap');

*{
  margin:0px;
  padding:0px;
  box-sizing: border-box;
}
#app {
  font-family: "poppins", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:#000;
  
}
body{
  background: #c4c4c4;
  overflow-x: hidden;
}
.receipe-container{
  background: linear-gradient(rgba(0,0,0,0.5),rgba(0,0,0,0.5)),url("./assets/food.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height:50vh;
  color:#fff;
}
.container{
  position: relative;
  top:180px;
}
.text{
  font-size:30px;
  position: relative;
  top:-30px;
}
.search{
  width:600px;
  height:60px;
  font-size: 20px;
  border-radius: 4px;
  border: 1px solid #c4c4c4;
  background: #c4c4c4;
  padding: 6px 30px;
}
.output{
  position: relative;
  top:300px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
.card{
  width:400px;
  height:400px;
  margin-left:50px;
  background: #fff;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  color:#000;
}
img{
  width:200px;
  height: 200px;
}
</style>
