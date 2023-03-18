<template>
    <div class="movie-detail">
        <h2>{{ movie.Title }}</h2>
        <p>{{ movie.Year }}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="main-img" />
        <p>{{ movie.Plot }}</p>
        <p>{{ movie.Actors }}</p>
    </div>
</template>


<script>
    import {ref, onBeforeMount} from 'vue'
    import { useRoute } from 'vue-router';
    import env from '../env';

    export default{
        setup () {
            const movie = ref({});
            const route = useRoute();

            onBeforeMount(() => {
                fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
                .then(response => response.json())
                .then(data => {
                    movie.value = data;
                });
            });

            return{
                movie
            }
        }
    }
</script>

<style lang="scss">
    .movie-detail{
        padding: 16px;
        h2{
            color: #000;
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 16px;
        }

        .main-img{
            display: block;
            max-width: 200px;
            margin-bottom: 16px;
        }

        p{
            color: #000;
            font-size: 20px;
            font-weight: 600;
            margin-bottom: 16px;
        }
    }
</style>