<template>
  <div class='filter-block'>
    <label> Trot
      <input type="checkbox"
             v-model="filters.T"
             v-on:change="changeFilter"
      />
    </label>
    <label> Gallop
      <input type="checkbox"
             v-model="filters.G"
             v-on:change="changeFilter"
      />
    </label>
    <label> Dogs
      <input type="checkbox"
             v-model="filters.D"
             v-on:change="changeFilter"
      />
    </label>
    <label> Jumping
      <input type="checkbox"
             id="jumping"
             name="jumping"
             v-model="filters.J"
             v-on:change="changeFilter"
      />
    </label>
  </div>
</template>

<script>
  export default {
    name: 'Filters',
    data () {
      return {
        filters: {
          T: true,
          G: true,
          D: false,
          J: true
        }
      }
    },
    mounted () {
      this.$emit('change-filters', this.filters)
    },
    methods: {
      changeFilter () {
        this.$emit('change-filters', this.filters)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>

</style>
