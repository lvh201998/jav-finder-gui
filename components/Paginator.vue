<template>
  <nav aria-label="Page navigation">
    <ul class="pagination justify-content-center">
      <li class="page-item" v-bind:class="{'disabled': this.page.current<=1}" @click="previousPage">
        <a class="page-link" href="#" tabindex="-1">trước</a>
      </li>
      <li>
        <div class="input-group">
          <input
            type="number"
            min="0"
            :max="this.page.count"
            class="form-control"
            placeholder="current page"
            aria-label="current page"
            style="width: 70px;"
            v-on:keyup.enter="changePage"
            v-model="page.current"
          />
          <div class="input-group-append">
            <span class="input-group-text">of {{this.page.count}}</span>
          </div>
        </div>
      </li>
      <li
        class="page-item"
        v-bind:class="{'disabled': this.page.current==this.page.count}"
        @click="nextPage"
      >
        <a class="page-link" href="#">sau</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Paginator',
  props: ['page'],
  data() {
    return {
      pages: []
    }
  },
  created() {},
  methods: {
    changePage() {
      this.$emit('changePage')
    },
    nextPage() {
      if (this.page.current < this.page.count) {
        this.page.current++
        this.$emit('changePage')
      }
    },
    previousPage() {
      if (this.page.current > 0) {
        this.page.current--
        this.$emit('changePage')
      }
    }
  }
}
</script>

<style>
</style>