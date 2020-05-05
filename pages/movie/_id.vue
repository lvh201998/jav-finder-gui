<template>
  <div class="container">
    <div class="m-2">
      <h1 class="title mb-5">{{name}}</h1>
      <div class="row">
        <div class="col-12 col-sm-6 col-lg-3" v-bind:key="index" v-for="(movie, index) in result">
          <div class="card mt-2 mb-2">
            <img class="card-img-top" :src="movie.imageUrl" alt="Card image cap" />
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
              <li class="list-group-item">review: {{movie.review.average || '? '}}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  head() {
    return {
      title: this.name
    }
  },
  created: function() {
    this.name = this.$route.query.name
    document.title = this.name
  },
  async asyncData({ params, error }) {
    if (
      !confirm(
        'Trang web có chứa nội dung không lành mạnh, bạn có trên 18 tuổi?'
      )
    ) {
      document.location.href = '/'
    } else {
      console.log(params)
      let response = {}
      try {
        response = await axios.get(
          `https://jav-rest-api-htpvmrzjet.now.sh/api/videos/${params.id}`
        )
        // console.log(response.data)
      } catch (e) {
        error({
          message: `Lỗi API ${e.response.status}`,
          statusCode: e.response.status
        })
      }
      response.data.result.forEach(element => {
        element.imageUrl = element.imageUrl.replace('httpss', 'https')
        let code = element.siteUrl.substring(
          element.siteUrl.lastIndexOf('cid=') + 4
        )
        code = code.substring(0, code.lastIndexOf('/')).toUpperCase()
        if (!element.review) element.review = { count: 0, average: '?' }
      })
      return response.data
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