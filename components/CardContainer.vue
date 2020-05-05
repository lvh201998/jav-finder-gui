<template>
  <div class="d-flex flex-column">
    <div class="row">
      <div class="col-12 col-sm-6 col-lg-3" v-bind:key="r.id" v-for="r in data.result">
        <Card v-bind:data="r" />
      </div>
    </div>
    <Paginator
      class="d-flex flex-column"
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
  props: ['data', 'itemPerPage'],
  data() {
    return {
      page: {
        current: 2,
        count: 0
      }
    }
  },
  watch: {
    data: {
      immediate: true,
      handler(newVal, _) {
        console.log(newVal)
        this.page.count = Math.ceil((newVal.total || 0) / this.itemPerPage);
        this.page.current = 1
      }
    }
  }
}
</script>

<style>
.invisible {
  display: none;
}
</style>