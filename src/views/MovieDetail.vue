<template>
  <div class="movie-detail">
     <h2>{{movie.Title}}</h2> 
      <p>{{movie.Year}}</p>
        <img :src="movie.Poster" alt="poster image" class="featured-image">
        <p>{{movie.Plot}}</p> 
  </div>
</template>

<script>
import {ref,onBeforeMount} from 'vue';
import {useRoute} from 'vue-router';
import env from '@/env';

export default {
    setup(){
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
                .then(response=>response.json())
                .then(data=>{
                    movie.value=data;
              });
        });

        return{
            movie
        }
    }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;
  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p {
      margin-top: 15px;
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
  }
}

</style>