<template>
  <div class="container">
    <div class="m-2">
      <h1 class="title mb-5">jav-finder</h1>

      <Finder v-on:find="find" />
      <component :is="currentComp" v-bind:data="data"></component>
      <Footer />
    </div>
  </div>
</template>

<script>
import CardContainer from '~/components/CardContainer.vue'
import Finder from '~/components/Finder.vue'
import Footer from '~/components/Footer.vue'
import Loading from '~/components/Loading.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    CardContainer,
    Finder,
    Footer,
    Loading
  },
  data() {
    return {
      currentComp: 'CardContainer',
      data: {}
    }
  },
  methods: {
    find(name) {
      this.currentComp = 'Loading'
      axios
        .get(`https://jav-rest-api-htpvmrzjet.now.sh/api/actress?name=${name}`)
        .then(res => {
          this.data = res.data
          this.currentComp = 'CardContainer'
        })
        .catch(err => console.error(err))
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
  font-weight: 300;
  font-size: 100px;
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
