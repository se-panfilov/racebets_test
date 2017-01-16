<template>
  <div class='race-block'>
    <div class="race-block__title title">
      <div class="title__info -heavy"></div>
      <div class="title__info -right"></div>
      <span>Upcoming:</span>
      <span v-text="upcomingRace.race_type"></span>
      <span v-text="upcomingRace.purse.amount"></span>
      <span v-text="upcomingRace.post_time"></span>
      <div>-----</div>
    </div>
    <div class="race-block__subtitle" v-for="race in selectedRaces">
      <div class="subtitle__info">
        <span v-text="race.race_type"></span>
        <span v-text="race.purse.amount"></span>
        <span v-text="race.post_time"></span>
      </div>
      <div class="subtitle__info"></div>
      <div class="subtitle__info"></div>
      <div class="subtitle__info--img"></div>
      <ul class="race-block__runners" v-for="runner in race.runners">
        <li class="runners__cell" v-show="runner.silk">
          <a v-bind:href="getSilkUrl(runner.id_race)">
            <img v-bind:src="getSilkImg(runner.silk)" v-bind:alt="runner.silk">
          </a>
        </li>
        <li class="runners__cell" v-text="runner.name"></li>
        <li class="runners__cell">
          <button type="button" v-text="runner.odds" @click="onOddsClick()"></button>
        </li>
      </ul>
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
      },
      onOddsClick () {

      },
      getSilkUrl (id) {
        return `http://www.racebets.com/bet/${id}` // https?
      },
      getSilkImg (img) {
        return `static/assets/silks/${img}`
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
      },
      upcomingRace () {
        const sortedRaces = this.selectedRaces.sort((a, b) => a.post_time - b.post_time)

        return sortedRaces.length > 0 ? sortedRaces[0] : { purse: {} }
//        return this.selectedRaces().sort((a, b) => a.post_time - b.post_time)
//        return this.races().sort((a, b) => a.post_time - b.post_time)
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
