<template lang="pug">
.movie-content
  .movie-info
    .sides
      .left-side(:class='{seen: data.seen}', @click='detail = !detail')
        .movie-title {{data.title}} ({{data.year}})
        .movie-director {{data.director}}
      .right-side(@click='data.seen = !data.seen')
        i.mdi.mdi-check(v-if='!data.seen')
        i.mdi.mdi-plus(v-if='data.seen')
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

  .left-side.seen
    text-decoration: line-through

  .right-side
    width: 50px
    text-align: right
    padding-right: 16px
    font-size: 1.2em

.movie-detail
  margin-top: 15px

</style>
