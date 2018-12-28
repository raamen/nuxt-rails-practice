<template lang="pug">
  v-layout
    v-flex
      v-list
        v-list-tile(v-for='example in examples', :key='example.id', :class='example.colour')
          v-list-tile-content {{example.name}}

</template>

<script>
import AppLogo from '~/components/AppLogo.vue'

export default {
  middleware: ['auth'],
  data () {
    return {
      examples: []
    }
  },
  methods: {
    async updateExamples() {
      this.examples = await this.$axios.$get('/examples')
      console.log(this.examples)
    }
  },
  mounted () {
    this.updateExamples()
  }
}
</script>

<style lang="stylus">
.container
  min-height: 100vh
  display: flex
  justify-content: center
  align-items: center
  text-align: center
</style>

