<template>
  <div class="container">
    <div class="m-2">
      <h1 class="title mb-5">idol-finder</h1>
      <Finder v-on:find="find" />
      <component
        :is="currentComp"
        v-bind:data="data"
        v-bind:page="page"
        v-bind:itemPerPage="itemPerPage"
        v-on:changePage="changePage"
      ></component>
      <Footer />
    </div>
  </div>
</template>

<script>
import CardContainer from '~/components/CardContainer.vue'
import Finder from '~/components/Finder.vue'
import Footer from '~/layouts/Footer.vue'
import Loading from '~/components/Loading.vue'
import ErrorMessage from '~/components/ErrorMessage.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    CardContainer,
    Finder,
    Footer,
    Loading,
    ErrorMessage
  },
  data() {
    return {
      page: {
        current: 1, // 1 mean 1st page, page 0 is invalid
        count: 0
      },
      currentComp: 'CardContainer',
      data: {},
      itemPerPage: 100, //default
      offset: 0,
      actressName: ''
    }
  },
  head() {
    return {
      title: 'idol finder'
    }
  },
  methods: {
    fetch(name, itemPerPage, offset) {
      console.log({ name, itemPerPage, offset })
      this.currentComp = 'Loading'

      this.data = {}

      let url = `https://jav-rest-api-htpvmrzjet.now.sh/api/actress?name=${name}`
      if (itemPerPage != 100) url += `&hits=${itemPerPage}`
      if (offset > 0) url += `&offset=${offset}`

      console.log(url)

      this.$nuxt.$loading.start()
      axios
        .get(url)
        .then(res => {
          this.$nuxt.$loading.finish()
          console.log(res.data)
          this.data = res.data
          this.currentComp = 'CardContainer'

          this.page.count = Math.ceil((this.data.total || 0) / this.itemPerPage)
          if (this.page.current > this.page.count)
            this.page.current = this.page.count
        })
        .catch(err => {
          this.$nuxt.$loading.finish()
          console.error(err)
          this.data = {}
          this.currentComp = 'ErrorMessage'
        })
    },
    find(name) {
      console.log('finding ', name)
      this.page.current = 1
      this.page.count = 0
      this.actressName = name
      document.title = `${this.actressName} | idol finder`
      this.fetch(this.actressName, this.itemPerPage, 0)
    },
    changePage(page) {
      this.fetch(
        this.actressName,
        this.itemPerPage,
        (page.current - 1) * this.itemPerPage
      )
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 200;
  font-size: 60px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
