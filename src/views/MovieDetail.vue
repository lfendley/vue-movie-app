<template>
  <div class="loader"><i class="fas fa-circle-notch fa-spin"></i></div>
  <div class="movie-detail">
    <div class="container">
      <router-link to="/"
        ><i class="fas fa-arrow-alt-circle-left"
          ><span id="back-btn">Back to search</span></i
        ></router-link
      >
      <div class="movie-details--wrapper">
        <div class="poster--ratings">
          <img
            width="300"
            height="440"
            class="movie-poster"
            :src="movie.Poster"
            :alt="movie.Title"
          />
          <div class="ratings">
            <div>{{ movie.imdbRating }}</div>
          </div>
        </div>
        <div class="movie-detail--title">
          <div>
            <h2>{{ movie.Title }}</h2>
            <p>
              Genre: <span>{{ movie.Genre }}</span>
            </p>
            <p>
              Rated: <span>{{ movie.Rated }}</span>
            </p>
            <p>
              Runtime: <span>{{ movie.Runtime }}</span>
            </p>
          </div>
          <div class="movie-detail--details">
            <p>{{ movie.Plot }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `https://omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
          document.querySelector('.loader').style.display = "none";
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style lang="scss" scoped>
.loader {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  top: 0;
  left: 0;
  color: #fff;
  font-size: 4em;
  background: #282931;
  z-index: 2;
}
.movie-detail {
  color: #f5f5f5;

  i,
  #back-btn {
    font-size: 14px;
    color: #f5f5f5;
  }

  #back-btn {
    display: inline-block;
    padding: 5px;
  }

  .movie-details--wrapper {
    @media screen and (min-width: 768px) {
      display: flex;
      gap: 1em;
    }
  }

  .poster--ratings {
    position: relative;

    .movie-poster {
      width: 100%;
      height: fit-content;
      max-height: 350px;

      @media screen and (min-width: 768px) {
        width: auto;
      }
    }

    .ratings {
      position: absolute;
      bottom: 10px;
      right: 10px;
      padding: 12px;
      font-size: 30px;
      background-color: #d64f55;
    }
  }

  .movie-detail--title {
    & div:first-of-type {
      background-color: #d64f55;
      padding: 4px;

      h2 {
        font-size: 18px;
      }
      p {
        font-size: 12px;
      }
    }
    .movie-detail--details {
      margin: 10px 0;

      p {
        font-size: 13px;
        line-height: 16px;
      }
    }
  }
}
</style>