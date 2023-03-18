<script>
import { ref } from 'vue';
import env from "../env";

export default {

  //Search bar functionality
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data =>{
          movies.value = data.Search;
          search.value = '';
        });// To call searches from the omdb api
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<template>
  <div class="home">
    <div class="main-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://www.smartprix.com/bytes/wp-content/uploads/2022/11/Naruto.jpg"
          alt="Naruto"
          class="main-img"
        />

        <div class="detail">
          <h3>Naruto</h3>
          <p>
            Naruto Uzumaki, a mischievous adolescent ninja, struggles as he searches for recognition
            and dreams of becoming the Hokage, the village's leader and strongest ninja
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="Search here" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movie-list">
      <div class="movie-screen" v-for="movie in movies" :key="movie.imdbID">
        <router-link v-bind:to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="movie-product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>

          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div> <!--To display the movies called out -->
  </div>
</template>

<style lang="scss">
.home {
  .main-card {
    position: relative;

    .main-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
    }

    h3 {
      color: #ffff;
      margin-bottom: 16px;
    }

    p {
      color: #ffff;
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type='text'] {
        width: 100%;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 10px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type='submit'] {
        width: 100%;
        max-width: 300px;
        background-color: #8b0a0a;
        padding: 16px;
        border-radius: 10px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: rgb(77, 6, 6);
        }
      }
    }
  }

  .movie-list{
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
  }

  .movie-screen{
    max-width: 50%;
    flex: 1 1 50%;
    padding: 16px 8px;

    .movie-link{
      display: flex;
      height: 100%;
      flex-direction: column;

      .movie-product-image{
        position: relative;
        display: block;

        img{
          display: block;
          width: 100%;
          height: 275px;
          object-fit: cover;
        }

        .type{
          position: absolute;
          padding: 8px 16px;
          background-color: #8b0a0a;
          color: #fff;
          bottom: 16px;
          left: 0px;
          text-transform: capitalize;
        }
      }
    }
  }
}
</style>
