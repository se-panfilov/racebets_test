<template>
  <div class='race-block'>
    <div class="race-block__title title">
      <div class="title__info -heavy"></div>
      <div class="title__info -right"></div>
    </div>
    <div class="race-block__subtitle" v-for="r in selectedRaces">
      <div class="subtitle__info">
        <span v-text="r.race_type"></span>
        <span v-text="r.purse.amount"></span>
      </div>
      <div class="subtitle__info"></div>
      <div class="subtitle__info"></div>
      <div class="subtitle__info--img"></div>
    </div>
    <div class="race-block__info">
      <div class="info__cell -img"></div>
      <div class="info__cell"></div>
      <div class="info__cell -btn"></div>
    </div>
    <button @click="debug">Debug</button>
    <span v-text="selectedRaces.length"></span>
  </div>
</template>

<script>
  import NextRaceData from './next_races_data'

  export default {
    name: 'NextRace',
    data () {
      return {
        races: NextRaceData.data.races
      }
    },
    props: {
      filterObj: {
        type: Object,
        required: true
      }
    },
    methods: {
      debug () {
//        console.info(this.races)
//        console.log(this.selectedRaces)
      }
    },
    computed: {
      selectedRaces () {
        const arr = this.races
        const filters = Object.keys(this.filterObj).filter(v => {
          return this.filterObj[v] === true
        })
        return arr.filter(v => {
          return filters.includes(v.race_type)
        })
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
