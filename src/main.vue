<template lang="pug">
// App
#app
  // Statusbar
  f7-statusbar
  // Left Panel
  f7-panel(left='', reveal='', layout='dark')
    f7-view#left-panel-view(navbar-through='', :dynamic-navbar='true')
      f7-navbar(title='Categorias')
      f7-pages
        f7-page(style='background-color: #35373c')
          #panel-content(style='height: 100%; display: flex; flex-direction: column; justify-content: space-between')
            f7-list
              f7-list-item.close-panel(v-for='(category, index) in dataset.categories', :title='category.title', @click='changeView(index)', link-view='#main-view', link-close-panel='')
            #credits
              div Feito com ♥ por Fábio Theophilo
              div(style='color: #ffd9a6') Feliz dia dos namorados #[b Victória]!
  // Main Views
  f7-views
    f7-view#main-view(navbar-through='', :dynamic-navbar='true', main='')
      // Navbar
      f7-navbar
        f7-nav-left
          f7-link(icon='icon-bars', open-panel='left')
        //- f7-nav-center(sliding='') Lista de Filmes
        | {{movies.title}}
      // Pages
      f7-pages
        f7-page
          // Comeca aqui...
          //- f7-list
          //-   f7-list-group(v-for='value in movies.values')
          //-     f7-list-item(:title='value.subtitle', group-title='')
          //-     f7-list-item(v-for='movie in value.movies', :title='movie.title')

          //- f7-block-title Welcome to my App
          f7-searchbar(cancel-link='Cancel', search-list='#search-list')
          // This block will become visible when there is nothing found
          f7-list.searchbar-not-found
            f7-list-item(title='Nothing found')
          // Search through this list
          //- f7-list#search-list.searchbar-found(media-list='', virtual='', :virtual-items='movies.values[0].movies', :virtual-height='63', :virtual-search-all='searchAll')
          f7-list#search-list.searchbar-found
            f7-list-group(v-for='value in movies.values')
              f7-list-item(:title='value.subtitle', group-title='')
              f7-list-item(v-for='movie in value.movies')
                movie(:data='movie')
          //-   // Templte 7 Virtual List Item Template
          //-   t7-template
          //-     f7-list-item(media-item='', link='#', :title="'{{title}}'", :subtitle="'{{director}}<br />{{year}}' ")
          //- f7-block-title Welcome to my App
          //- f7-searchbar(cancel-link='Cancel', search-list='#search-list')
          //- // This block will become visible when there is nothing found
          //- f7-list.searchbar-not-found
          //-   f7-list-item(title='Nothing found')
          //- // Search through this list
          //- f7-list#search-list.searchbar-found(media-list='', virtual='', :virtual-items='movies.values[0].movies', :virtual-height='63', :virtual-search-all='searchAll')
          //-   // Templte 7 Virtual List Item Template
          //-   t7-template
          //-     f7-list-item(media-item='', link='#', :title="'{{title}}'", :subtitle="'{{director}}<br />{{year}}' ")
</template>

<script>
import json from './assets/json/movies.json'
import Movie from './assets/vue/Movie'
import localForage from 'localforage'

export default {
  components: {
    Movie
  },
  mounted () {
    localForage.getItem('dataset')
      .then(res => {
        if(!res){
          console.info('Getting from JSON')
          this.dataset = json
          this.movies = json.categories[0]

          return localForage.setItem('dataset', json)
        }
        else {
          console.info('Getting from localForage')
          this.dataset = res
          this.movies = res.categories[0]

          return Promise.resolve(true)
        }
      })
      .then(res => {
        console.log('Was saved? ', res)
      })
      .catch(err => {
        console.error('Oops! ', err)
      });
  },
  data () {
    return {
      dataset: {},
      movies: {},
    }
  },
  methods: {
    searchAll (query) {
      // var self = this;
      // var found = [];
      // for (var i = 0; i < self.items.length; i++) {
      //     if (self.items[i].name.indexOf(query) >= 0 ||
      //         self.items[i].email.indexOf(query) >= 0 ||
      //         query.trim() === '') found.push(i);
      // }
      return null;
    },
    changeView (index) {
      // console.log('Change View to ', index)
      this.movies = json.categories[index]
    }
  }
}
</script>

<style lang="stylus">
/*white = #fff*/
caramel = #ffd9a6
martini = #b3a2a5
cloud = #cbcbcb
estern_blue = #2e9cb1
grafite = #35373c


#search-list
  margin-top: 3px

.navbar
  background-color: estern_blue
  color: #fff
  font-weight: bold

.searchbar
  background-color: estern_blue

.list-group-title
  background-color: cloud
  color: martini

.panel .panel-left .panel-reveal .layout-dark .active
  .pages
    .page
      .page-content
        background-color: estern_blue

.list-block-group
  li
    background-color: grafite
    color: cloud

  li.list-group-title
    background-color: caramel

  .movie-info
    .movie-title
      font-weight: bold

    .movie-director
      color: cloud

#panel-content
  height: 100%
  display: flex
  flex-direction: column
  justify-content: space-between

  #credits
    text-align: center
    margin-bottom: 5px

    .author
      color: caramel
</style>
