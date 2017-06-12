<template lang="pug">
.movie-content
  .movie-info
    span.movie-title {{data.title}}
    span.movie-director {{data.director}}
  .movie-detail(v-if='detail')
    span Besteira
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
</style>
