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
          <h4>Recipes name :</h4>  {{item.title}} <br>
          <h4>Ready in minutes :</h4>  {{item.readyInMinutes}}
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
      axios.get(`https://api.spoonacular.com/recipes/search?query=${this.query}&number=9&apiKey=89ec3200076941aea9df44b9e1820f7c`)
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
  width:100%;
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
  width:350px;
  height:350px;
  margin:0px 50px;
  background: #fff;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  color:#000;
  margin:30px 45px;
}
img{
  width:200px;
  height: 200px;
}
@media only screen and (max-width: 600px) {
  .output{
    display: grid;
    grid-template-columns: 1fr;
  }
  .card{
    margin: 30px 80px;
  }
  .container{
    position: relative;
    top:150px;
  }
  .search{
    width:100vw;
  }
}

</style>
