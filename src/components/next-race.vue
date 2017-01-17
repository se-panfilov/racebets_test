<template>
  <div class='race-block'>
    <div class="race-block__title">
      <span class="title__info">
        <img v-bind:src="getFlagImg(nextRace.event.country)" width="14" height="11">
      </span>
      <span class="title__info -heavy -top" v-text="nextRace.event.title"></span>
      <span class="title__info -right" v-text="getDue(nextRace.post_time)"></span>
    </div>
    <div class="race-block__subtitle">
      <div class="subtitle__info">
        <span v-text="runnersCount"></span> Runners |
        <span v-text="nextRace.distance"></span>m |
        <span v-text="nextRace.purse.amount"></span>
        <span v-text="nextRace.purse.currency"></span>
        <!--<img v-bind:src="getRaceTypeImg(nextRace.race_type)"/>-->
        <span class="subtitle__race-type -right" v-bind:class="raceTypeClassObj"></span>
      </div>
    </div>
    <ul class="race-block__runners">
      <li class="runners__item" v-for="runner in nextRace.runners">
        <a v-bind:href="getSilkUrl(runner.id_race)"
           class="runners-item__cell -order1"
           v-show="runner.silk"
        >
          <img v-bind:src="getSilkImg(runner.silk)" v-bind:alt="runner.silk" width="20" height="20"/>
        </a>
        <span class="runners-item__cell -order2" v-text="runner.name"></span>
        <span class="runners-item__cell -order3">
          <button type="button" class="item-cell__btn" v-text="runner.odds" @click="onOddsClick()"></button>
        </span>
      </li>
    </ul>
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
      getDue (dt) {
        const now = (new Date()).getTime()

        if (dt <= now) return 'Due'
        return parseInt((dt - now) / 1000 / 60)
      },
      getSilkUrl (id) {
        if (!id) return ''
        return `http://www.racebets.com/bet/${id}` // https?
      },
      getSilkImg (img) {
        if (!img) return ''
        return `static/assets/silks/${img}`
      },
//      getRaceTypeImg (type) {
//        if (!type) return ''
//        return `static/assets/race-types/race-type-${type}.svg`
//      },
      getFlagImg (country) {
        if (!country) return ''
        return `static/assets/flags/${country.toLowerCase()}.png`
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
      nextRace () {
        const emptyRace = { purse: {}, event: {}, runners: {}, race_type: 'T', post_time: 0 }

        if (!this.selectedRaces) return emptyRace
        const sortedRaces = this.selectedRaces.sort((a, b) => a.purse.amount - b.purse.amount)
        return sortedRaces.length > 0 ? sortedRaces[0] : emptyRace
      },
      runnersCount () {
        if (!this.nextRace || !this.nextRace.runners) return 0
        return this.nextRace.runners.length
      },
      raceTypeClassObj () {
        return {
          '-trot': this.nextRace.race_type === 'T',
          '-gallop': this.nextRace.race_type === 'G',
          '-jumping': this.nextRace.race_type === 'J',
          '-dogs': this.nextRace.race_type === 'D'
        }
      }
    },
    components: {
      NextRaceData
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  primary_color = #333
  bg_color = #FFF
  text_color = #444
  alt_text_color = #FFF
  alt_border_color = #d9d9d9

  .race-block
    font-weight normal
    font-size 0.8em
    border 1px solid primary_color
    border-radius 3px
    background-color bg_color
    font-family Tahoma, Geneva, Kalimati, sans-serif
    box-sizing border-box
    &__title
      background-color primary_color
      color alt_text_color
      padding 7px 8px 4px 8px
      font-size 11px

    .title
      &__info
        &.-heavy
          font-weight bold
        &.-top
          vertical-align top
        &.-right
          float right

    &__subtitle
      padding 4px 8px 8px 8px
      background-color primary_color
      color alt_text_color

    .subtitle
      &__info
        font-size 11px
        border-top 1px solid #666
        padding-top 8px
      &__race-type
        background white
        height 16px
        width 27px
        display inline-block
        &.-trot
          mask url('../../static/assets/race-types/race-type-T.svg') center / contain no-repeat
        &.-dogs
          mask url('../../static/assets/race-types/race-type-D.svg') center / contain no-repeat
        &.-gallop
          mask url('../../static/assets/race-types/race-type-G.svg') center / contain no-repeat
        &.-jumping
          mask url('../../static/assets/race-types/race-type-J.svg') center / contain no-repeat
        &.-right
          float right

    &__runners
      background-color bg_color
      border 3px solid primary_color
      color text_color
      overflow-y auto
      margin 0
      padding 0

      .runners
        &__item
          display flex
          list-style none
          margin 0
          padding 8px 4px
          font-size 11px
          border-top 1px solid alt_border_color
          &:first-of-type
            border-color #FFF

          .runners-item
            &__cell
              display inline-block
              flex 1 0 33%
              box-sizing border-box
              line-height 11px
              padding 3px
              &.-order1
                order 1
                flex 1 0 20%
              &.-order2
                order 2
                flex 1 0 60%
                padding 8px
              &.-order3
                order 3
                flex 1 0 20%
              .item-cell__btn
                color text_color
                background-color #f8ae17
                background-image: linear-gradient(#ffdd86, #f8ae17)
                border 1px solid #f8ae17
                border-radius 3px
                outline none
                font-weight 400
                min-width 36px
                box-sizing border-box
                cursor pointer
                padding 2px 0
                  line-height 11px
</style>
