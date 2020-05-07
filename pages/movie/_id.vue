<template>
  <div class="container-fluid m-lg-5 p-lg-5">
    <div class="m-2">
      <div class="d-flex flex-column">
        <NuxtLink to="/">
          <h2 class="title mb-4">{{name}} ({{data.total}})</h2>
        </NuxtLink>

        <ErrorMessage v-if="error" />
        <Loading v-if="loading" />

        <Paginator
          class="d-flex flex-column m-3"
          v-bind:page="page"
          v-if="this.page.count >= 1"
          v-on:changePage="changePage(page)"
        />

        <div class="row">
          <div
            class="col-12 col-sm-6 col-lg-3 col-xl-2"
            v-bind:key="index"
            v-for="(movie, index) in data.result"
          >
            <div class="card mt-2 mb-2">
              <img
                class="card-img-top"
                :src="movie.imageUrl"
                alt="Card image cap"
              />
              <div class="card-body pb-1">
                <h5 class="card-title">{{movie.name}}</h5>
              </div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item">
                  code:
                  <a
                    class="font-weight-bold"
                    :href="`https://www.google.com/search?q=${movie.code}`"
                    target="_blank"
                  >{{movie.code || '? '}}</a>
                </li>
                <li class="list-group-item">review: {{movie.review.average || '? '}} ({{movie.review.count || '? '}})</li>
                <li class="list-group-item">date: {{movie.date || '? '}}</li>
                <li class="list-group-item">maker: 
                  <div v-for="(maker, index) in movie.maker" v-bind:key="index">{{maker.name}}<div v-if="index>0">, </div></div>
                </li>
                <!-- <li class="list-group-item">actress: 
                  <div v-for="(actress, index) in movie.actress" v-bind:key="index">{{actress.name}}<div v-if="index>0">, </div></div>
                </li> -->
              </ul>
            </div>
          </div>
        </div>
        <Paginator
          class="d-flex flex-column m-3"
          v-bind:page="page"
          v-if="this.page.count >= 1"
          v-on:changePage="changePage(page)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Paginator from '~/components/Paginator'
import Loading from '~/components/Loading'
import ErrorMessage from '~/components/ErrorMessage'
import axios from 'axios'

export default {
  loading: false,
  components: {
    Paginator,
    Loading,
    ErrorMessage
  },
  head() {
    return {
      title: this.name
    }
  },
  created: function() {
    document.title = this.name
    // if (
    //   !confirm(
    //     'Trang web có chứa nội dung không lành mạnh, bạn có trên 18 tuổi?'
    //   )
    // ) {
    //   document.location.href = '/'
    // } else {
    // }
    this.fetch(this.id, this.itemPerPage, 0)
  },
  data({ params }) {
    return {
      page: {
        count: 0,
        current: 1
      },
      itemPerPage: 100,
      offset: 0,
      data: { count: 0, total: 0, result: [] },
      id: this.$route.params.id,
      name: this.$route.query.name,
      loading: true,
      error: false
    }
  },
  methods: {
    showLoading() {
      this.$nuxt.$loading.start()
      this.loading = true
    },
    hideLoading() {
      this.$nuxt.$loading.finish()
      this.loading = false
    },
    changePage(page) {
      console.log(page)
      this.fetch(
        this.id,
        this.itemPerPage,
        (page.current - 1) * this.itemPerPage
      )
    },
    fetch(actressId, itemPerPage, offset) {
      setTimeout(() => {
        this.showLoading()
      }, 500)
      this.error = false
      let response = {}
      let url = `https://jav-rest-api-htpvmrzjet.now.sh/api/videos/${actressId}?`
      if (itemPerPage != 100) url += `hits=${itemPerPage}`
      if (offset > 0) url += ` &offset=${offset}`
      console.log(url)
      axios
        .get(url)
        .then(res => {
          this.hideLoading()
          response = res

          this.page.count = Math.ceil(
            (response.data.total || 0) / this.itemPerPage
          )
          if (this.page.current > this.page.count)
            this.page.current = this.page.count

          response.data.result.forEach(element => {
            element.imageUrl = element.imageUrl.replace('httpss', 'https')
            let code = element.siteUrl.substring(
              element.siteUrl.lastIndexOf('cid=') + 4
            )
            element.code = code
              .substring(0, code.lastIndexOf('/'))
              .toUpperCase()
            if (!element.review) element.review = { count: 0, average: '?' }
          })
          this.data = response.data
        })
        .catch(e => {
          console.error(e)
          this.error = true
          this.hideLoading()
        })
    }
  }
}
</script>

<style>
</style>