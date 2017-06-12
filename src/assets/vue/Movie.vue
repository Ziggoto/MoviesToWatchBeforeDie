<template lang="pug">
.movie-content
  .movie-info(@click='detail = !detail')
    .sides
      .left-side
        .movie-title {{data.title}} ({{data.year}})
        .movie-director {{data.director}}
      .right-side
        //- | Opa
  .movie-detail(v-if='detail')
    span Em breve... desculpa D:
</template>

<script>
export default {
  props: ['data'],
  data () {
    return {
      detail: false
    }
  }
}
</script>

<style lang="stylus" scoped>
.movie-content
  width: 100%

  .sides
    display: flex
    justify-content: space-between

.movie-detail
  margin-top: 5px
</style>
