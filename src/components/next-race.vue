<template>
  <div class='race-block'>
    <div class="race-block__title title">
      <div class="title__info -heavy"></div>
      <div class="title__info -right"></div>
    </div>
    <div class="race-block__subtitle">
      <div class="subtitle__info"></div>
      <div class="subtitle__info"></div>
      <div class="subtitle__info"></div>
      <div class="subtitle__info--img"></div>
    </div>
    <div class="race-block__info">
      <div class="info__cell -img"></div>
      <div class="info__cell"></div>
      <div class="info__cell -btn"></div>
    </div>
  </div>
</template>

<script>
  import NextRaceData from './next_races_data'

  export default {
    name: 'NextRace',
    data () {
      return {
      }
    },
    props: {
      filter: {
        type: String
      }
    },
    methods: {
      some (some) {

      }
    },
    components: {
      NextRaceData
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  text_color = #464646


</style>
