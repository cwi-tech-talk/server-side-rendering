<template>
  <el-card class="movie">
    <el-row
      :gutter="20"
      class="movie__row"
      type="flex"
      align="middle">
      <el-col
        :md="6"
        :sm="8"
        :xs="24">
        <img
          :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
          class="movie__poster">
      </el-col>
      <el-col
        :md="18"
        :sm="16"
        :xs="24">
        <h1>{{ movie.title }}</h1>
        <p>{{ movie.tagline }}</p>
        <el-rate
          v-if="rating"
          v-model="rating"
          disabled
          show-score
          text-color="#ff9900"
          score-template="{value} pontos"/>
        <p class="movie__overview">{{ movie.overview }}</p>
        <div
          class="movie__links">
          <nuxt-link
            v-if="link"
            :to="{ name: 'movies-id', params: { id: movie.id }}">
            <el-button type="text">Detalhes <i class="el-icon-arrow-right el-icon-right"/></el-button>
          </nuxt-link>
          <a
            v-if="movie.homepage"
            :href="movie.homepage"
            target="_blank">
            <el-button type="text">Site oficial <i class="el-icon-arrow-right el-icon-right"/></el-button>
          </a>
        </div>
      </el-col>
    </el-row>
  </el-card>
</template>

<script>
export default {
  props: {
    movie: {
      type: Object,
      default: null,
      required: true
    },
    rating: {
      type: Number,
      default: null,
      required: false
    },
    link: {
      type: Boolean,
      default: false,
      required: false
    }
  }
}
</script>

<style scoped>
.movie__row {
  flex-wrap: wrap;
}

.movie__poster {
  width: 100%;
  height: auto;
}

.movie__overview {
  margin-top: 20px;
  text-align: justify;
  text-indent: 20px;
}

.movie__links {
  text-align: right;
}
</style>
