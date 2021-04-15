<template>
  <!-- featured banner -->
  <div class="home">
    <div class="featured-card">
      <router-link to="/movie/tt0758746">
        <img
          class="featured-img"
          src="http://1.bp.blogspot.com/-x2rl9cZxrw0/VFvMkW7XfCI/AAAAAAAAOSM/CFSO7Tzh_Og/w680/motionposter.gif"
        />
        <div class="detail">
          <div class="container">
            <h3>Friday the 13th</h3>
            <p>
              A group of young adults set up tent near the abandoned summer camp
              where a series of gruesome murders are said to have taken place
              back in 1980.
            </p>
          </div>
        </div>
      </router-link>
    </div>

    <!-- search & results -->
    <div class="container">
      <form @submit.prevent="searchMovies()" class="search-box">
        <input type="text" placeholder="Search movies..." v-model="search" />
        <input type="submit" value="search" />
      </form>

      <div class="movies-list">
        <div class="movie" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="`/movie/${movie.imdbID}`" class="movie-link">
            <div class="product-image">
              <img :src="movie.Poster" alt="Movie Poster" />
              <div class="type">{{ movie.Type }}</div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";
import env from "@/env.js";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if (search.value != "") {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            console.log(data.Search);
            movies.value = data.Search;

            //debug
            console.log(movies.value);
            search.value = "";
          });
      }
    };

    // Populate homepage movies by IIFE
    (function () {
      fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=jason`)
        .then((response) => response.json())
        .then((data) => {
          movies.value = data.Search;
          console.log(movies.value);
        });
    })();

    return {
      search,
      movies,
      searchMovies,
      hover: false
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  .featured-card {
    position: relative;
    background-color: currentColor;

    .featured-img {
      display: block;
      width: 100%;
      height: 250px;
      object-fit: contain;

      @media screen and (min-width: 768px) {
        height: 375px;
      }

      @media screen and (min-width: 1200px) {
        height: 500px;
        // object-position: center -200px;
        object-position: center;
        object-fit: none;
      }

      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 8px 6px;
      z-index: 1;

      h3 {
        font-size: 16px;
        color: #fff;
        margin-bottom: 8px;

        @media screen and (min-width: 768px) {
          font-size: 28px;
        }
      }

      p {
        font-size: 10px;
        color: #fff;

        @media screen and (min-width: 768px) {
          font-size: 13px;
        }
      }
    }
  }

  .movies-list {
    padding-bottom: 10px;
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    @media screen and (min-width: 768px) {
      flex-direction: row;
    }

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #282931;
        padding: 8px 10px;
        border-radius: 5px;
        margin-bottom: 15px;
        background-color: #fff;

        @media screen and (min-width: 768px) {
          margin-bottom: 0;
          border-radius: 0;
        }

        &::placeholder {
          color: #65688091;
        }
        &:focus {
          box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 100px;
        color: #fff;
        text-transform: uppercase;
        background-color: #d64f55;
        padding: 8px;
        cursor: pointer;

        &:active {
          background-color: #d82f38;
        }
      }
    }
  }
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0 8px;

    .movie {
      flex: 1 1 50%;
      max-width: 50%;
      padding: 12px 5px;
      justify-content: center;

      @media screen and (min-width: 640px) {
        flex: 1 1 33%;
        max-width: 33%;
      }
      @media screen and (min-width: 900px) {
        flex: 1 1 20%;
        max-width: 20%;
      }

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 250px;
            border: 2px solid #42b883;
          }

          .type {
            position: absolute;
            font-size: 12px;
            padding: 8px 10px;
            background-color: #42b883;
            color: #fff;
            bottom: 7px;
            left: 0;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: #496583;
          padding: 15px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 6px 6px;

          .year {
            font-size: 12px;
            color: #b9b9b9;
          }

          h3 {
            color: #fff;
            font-size: 12px;
          }
        }
      }
    }
  }
}
</style>
