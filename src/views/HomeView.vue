<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://cdn.pixabay.com/photo/2023/09/04/03/36/ai-generated-8231894_640.png" class="featured-img">

        <div class="detail">
          <h3>Naruto</h3>
          <p>Naruto Uzumaki, a mischievous adolescent ninja, struggles as he searches for recognition and dreams of
            becoming the Hokage, the village's leader and strongest ninja.</p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search">
      <input type="submit" value="Search">
    </form>
   
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' +movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail2">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
     
      </div>
    </div>
 
  </div>
</template>


<script setup>
import { ref } from 'vue'
import env from '@/env';

const search = ref('');
const movies = ref([]);

const SearchMovies = () => {
  if (search.value != '') {
    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
      .then(response => response.json())
      .then(data => {
       movies.value = data.Search;
       search.value = '';
       
       
      });
  }
}

</script>


<style scoped>

.feature-card {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;
}

.featured-img {
  width: 400px;
  height: 500px;
  object-fit: cover;
  position: relative;
  z-index: 0;
}

.detail {
  position: absolute;

  bottom: 4px;
  background-color: rgba(0, 0, 0, 0.6);
  padding: 16px;
  z-index: 1;
  width: 400px;


}

.detail h3 {
  color: #FFF;
  margin-bottom: 16px;
}

.detail p {
  color: #FFF;
}

.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
}

input {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none
}

input[type="text"] {
  width: 400px;
  color: #FFF;
  background-color: #496583;
  font-size: 20px;
  padding: 10px 16px;
  border-radius: 8px;
  margin-bottom: 15px;
  transition: 0.4s;

}

input::placeholder {
  color: #afafaf;
}

input:focus {
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}

input[type="submit"] {
  width: 100%;
  max-width: 300px;
  background-color: #42B883;
  padding: 16px;
  border-radius: 8px;
  color: #FFF;
  text-transform: uppercase;
  font-size: 20px;
  transition: 0.4s;
  cursor: pointer;


  &:active {
    background-color: #3B8070;
  }
}

.movies-list{
  display: flex;
  flex-wrap: wrap;
  margin: 0px 8px;
}

.movie{
  max-width: 25%;
  flex: 1 1 50%;
  padding: 16px 8px;
  

}

.movie-link{
  display: flex;
  flex-direction: column;
  height: 100%;

}

.product-image{
  position: relative;
  display: block;
  transition: 0.4s ease-in;
 
}

.product-image:hover{
  opacity: 0.2;
}

.product-image img {
  display: block;
  width: 100%;
  height: 275px;
  object-fit: cover;
}
.product-image .type{
  position: absolute;
  padding: 8px 16px;
  background-color: #42B883;
  color: #FFF;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}

.detail2{
  background-color: #496583;
  padding: 16px 8px;
  flex:1 1 100%;
  border-radius: 0px 0px 8px 8px;
}

.year{
  color: #AAA;
  font-size: 14px;
}

.detail2 h3{
  color:#FFF;
  font-weight: 600;
  font-size: 18px;
}
</style>