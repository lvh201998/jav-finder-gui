<template>
  <div class="d-flex flex-column">
    <Paginator
      class="d-flex flex-column m-3"
      v-bind:page="page"
      v-bind:class="{'invisible': this.page.count < 1}"
      v-on:changePage="$emit('changePage', page)"
    />
    <div class="row">
      <div class="col-12 col-sm-6 col-lg-3 col-xl-2" v-bind:key="r.id" v-for="r in data.result">
        <Card v-bind:data="r" />
      </div>
    </div>
    <Paginator
      class="d-flex flex-column m-3"
      v-bind:page="page"
      v-bind:class="{'invisible': this.page.count < 1}"
      v-on:changePage="$emit('changePage', page)"
    />
  </div>
</template>

<script>
import Card from './Card.vue'
import Paginator from './Paginator'

export default {
  name: 'CardsContainer',
  components: {
    Card,
    Paginator
  },
  props: ['data', 'itemPerPage', 'page']
}
</script>

<style>
.invisible {
  display: none;
}
</style>