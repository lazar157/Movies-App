<template>
    <div class="overlay">
        <div class="movie-detail">
            <h2>{{ movie.Title }}</h2>
            <h3>{{ movie.imdbRating }} <i class="fa-solid fa-star"></i></h3>
            <p>{{ movie.Year }}</p>
            <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
            <div class="text">
                <p>{{ movie.Plot }}</p>
            </div>

        </div>
    </div>
</template>


<script setup>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env'

const movie = ref({});
const route = useRoute();

onBeforeMount(() => {
    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
            movie.value = data;
            console.log(movie.value)
        });
});
</script>


<style scoped>
.overlay {
    position: fixed;
    top: 20%;
    left: 0;
  
    z-index: 9999;
    display: flex;
    justify-content: center;
    align-items: center;
}


.movie-detail {
    background-color: #496583;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
    max-width: 80%;
}

.movie-detail i{
    color: yellow;
}

.movie-detail h3{
    color: #FFF;
    font-weight: 300;
    font-size: 20px;
}

.movie-detail h2{
    font-size: 30px;
    font-weight: bold;
    color: white;
}

.close-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
    padding: 5px 10px;
}

.featured-img {
    max-width: 100%;
    height: auto;
    margin-bottom: 10px;
}

.text {
    margin-top: 10px;
}

.text p{
    color: #CCC;
}
</style>