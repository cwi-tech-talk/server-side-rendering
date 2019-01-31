<template>
  <el-container>
    <el-row
      v-if="movie"
      class="movie__row"
      type="flex"
      justify="center">
      <el-col
        :xl="14"
        :lg="16"
        :sm="20">
        <Movie
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
  validate({ params }) {
    // Must be a number
    return /^\d+$/.test(params.id)
  },
  head() {
    return {
      title: this.movie
        ? `${this.movie.title} - ${this.movie.tagline}`
        : undefined,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.movie ? this.movie.tagline : undefined
        },
        {
          hid: 'og:title',
          name: 'og:title',
          content: this.movie ? this.movie.title : undefined
        },
        {
          hid: 'og:description',
          name: 'og:description',
          content: this.movie ? this.movie.tagline : undefined
        },
        {
          hid: 'og:type',
          name: 'og:type',
          content: 'video.movie'
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: this.movie
            ? `https://image.tmdb.org/t/p/w500${this.movie.backdrop_path}`
            : undefined
        },
        {
          hid: 'twitter:card',
          name: 'twitter:card',
          content: 'summary_large_image'
        }
      ]
    }
  },
  async asyncData({ $axios, params }) {
    const movie = await $axios.$get(
      `https://api.themoviedb.org/3/movie/${params.id}`,
      {
        params: {
          api_key: 'API_KEY_HERE',
          language: 'pt-BR'
        }
      }
    )
    return { movie }
  }
}
</script>

<style scoped>
.movie__row {
  width: 100%;
}
</style>
