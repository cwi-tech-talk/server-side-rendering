<template>
  <el-container class="movies__container">
    <el-row
      v-for="movie in movies"
      :key="movie.id"
      class="movies__row"
      type="flex"
      justify="center">
      <el-col
        :xl="14"
        :lg="16"
        :sm="20">
        <Movie
          :link="true"
          :movie="movie"
          :rating="movie.vote_average/2"/>
      </el-col>
    </el-row>
  </el-container>
</template>

<script>
import Movie from '~/components/Movie'

export default {
  components: {
    Movie
  },
  head() {
    return {
      title: 'Filmes populares'
    }
  },
  async asyncData({ $axios }) {
    const response = await $axios.$get(
      `https://api.themoviedb.org/3/movie/popular`,
      {
        params: {
          api_key: 'API_KEY_HERE',
          language: 'pt-BR'
        }
      }
    )
    return { movies: response.results.slice(0, 5) }
  }
}
</script>

<style scoped>
.movies__container {
  flex-wrap: wrap;
}

.movies__row {
  margin-bottom: 20px;
  width: 100%;
}

.movies__row:last-of-type {
  margin-bottom: 0;
}
</style>
