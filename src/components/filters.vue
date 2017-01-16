<template>
  <div class='filter-block'>
    <label> Trot
      <input type="checkbox"
             v-model="filters.trot"
             v-on:change="changeFilter"
      />
    </label>
    <label> Gallop
      <input type="checkbox"
             v-model="filters.gallop"
             v-on:change="changeFilter"
      />
    </label>
    <label> Dogs
      <input type="checkbox"
             v-model="filters.dogs"
             v-on:change="changeFilter"
      />
    </label>
    <label> Jumping
      <input type="checkbox"
             id="jumping"
             name="jumping"
             v-model="filters.jumping"
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
          trot: true,
          gallop: true,
          dogs: false,
          jumping: true
        }
      }
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
