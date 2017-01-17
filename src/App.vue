<template>
  <div id="app">
    <filters v-on:change-filters="onChangeFilters"></filters>
    <div class="column">
      <next-race :filter-obj="raceFilters"></next-race>
    </div>
  </div>
</template>

<script>
  import Filters from './components/filters'
  import NextRace from './components/next-race'

  export default {
    name: 'app',
    data () {
      return {
        raceFilters: {}
      }
    },
    methods: {
      onChangeFilters (filters) {
        this.raceFilters = filters
      }
    },
    components: {
      NextRace,
      Filters
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>

  html, body
    margin 0
    padding 0
    height 100%

  body
    background-color #FFF
    color #3c3c3c
    font-family 'Roboto', sans-serif
    font-weight 500
    *
      font-family 'Roboto', sans-serif
      font-weight 500

  input[type="search"]
    -moz-appearance textfield
    -webkit-appearance textfield
    appearance textfield
    -webkit-box-sizing border-box
    -moz-box-sizing border-box
    box-sizing border-box

  article, aside, details, figcaption, figure,
  footer, header, menu, nav, section, canvas
    display block

  .column
    width 240px

</style>
