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
//    computed: {
//      filteredGames () {
//        return this.games
//          .filter(v => {
//            if (!this.category) return true
//            return v.gameType === this.category
//          })
//          .filter(v => {
//            if (!this.vendor) return true
//            return v.vendor === this.vendor
//          })
//          .filter(v => {
//            if (!this.text && this.text.length === 0) return true
//            return v.name.toLowerCase().indexOf(this.text.toLowerCase()) !== -1
//          })
//      }
//    },
    components: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  text_color = #464646


</style>
