<template>
  <div class="container">
    <div class="row">
      <div class="col-12 col-sm-6 col-lg-3" v-bind:key="r.id" v-for="r in data.result">
        <Cards
          v-bind:data="r"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Cards from './Cards.vue'

export default {
  name: 'CardsContainer',
  components: {
    Cards
  },
  props: ['data']
}
</script>

<style>
</style>