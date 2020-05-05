<template>
  <div class="container">
    <div class="m-2">
      <h1 class="title mb-5">idol-finder</h1>

      <Finder v-on:find="find" />
      <component
        :is="currentComp"
        v-bind:data="data"
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
      currentComp: 'CardContainer',
      data: {
        count: 10,
        total: '872',
        result: [
          {
            id: '1030629',
            name: 'Kahara Erina',
            japanName: '華原恵里奈',
            bust: '85',
            waist: '59',
            hip: '83',
            height: '148',
            birthday: '1997-03-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/kahara_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1030629%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1032668',
            name: 'Hasimoto Arina',
            japanName: '橋本ありな',
            bust: '84',
            waist: '56',
            hip: '83',
            height: '166',
            birthday: '1996-12-15',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hasimoto_arina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1032668%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1041476',
            name: 'Kurokawa Sarina',
            japanName: '黒川さりな',
            bust: '88',
            waist: '56',
            hip: '85',
            height: '160',
            birthday: '1996-12-12',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/kurokawa_sarina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1041476%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1035509',
            name: 'Okazawa Rina',
            japanName: '岡沢リナ',
            bust: '98',
            waist: '59',
            hip: '92',
            height: '156',
            birthday: '1996-07-07',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/okazawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1035509%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1025436',
            name: 'Nisida Karina',
            japanName: '西田カリナ',
            bust: '78',
            waist: '56',
            hip: '82',
            height: '159',
            birthday: '1995-07-07',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/nisida_karina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1025436%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1032628',
            name: 'Aizawa Yurina',
            japanName: '相澤ゆりな',
            bust: '87',
            waist: '58',
            hip: '83',
            height: '148',
            birthday: '1995-06-11',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/aizawa_yurina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1032628%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1021334',
            name: 'Lina',
            japanName: 'LINA',
            bust: '85',
            waist: '57',
            hip: '86',
            height: '160',
            birthday: '1994-09-09',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/lina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1021334%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1032166',
            name: 'Misuzu Rina',
            japanName: '美涼りな',
            bust: '88',
            waist: '59',
            hip: '90',
            height: '157',
            birthday: '1994-07-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/misuzu_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1032166%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1022611',
            name: 'Nagasawa Erina',
            japanName: '長澤えりな',
            bust: '82',
            waist: '59',
            hip: '88',
            height: '158',
            birthday: '1994-07-04',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/nagasawa_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1022611%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1026486',
            name: 'Nanase Rina',
            japanName: '七瀬リナ',
            bust: '78',
            waist: '55',
            hip: '80',
            height: '160',
            birthday: '1994-04-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/nanase_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1026486%2F&af_id=10278-996&ch=api'
          }
        ]
      },
      itemPerPage: 15,
      offset: 0,
      actressName: ''
    }
  },
  created() {
    document.title = 'idol finder'
  },
  methods: {
    fetch(name, itemPerPage, offset) {
      this.currentComp = 'Loading'
      const url = `https://jav-rest-api-htpvmrzjet.now.sh/api/actress?name=${name}&hits=${itemPerPage}&offset=${offset}`
      console.log('fetch: ', url)
      axios
        .get(url)
        .then(res => {
          this.data = res.data
          this.currentComp = 'CardContainer'
        })
        .catch(err => {
          console.error(err)
          this.data = {}
          this.currentComp = 'ErrorMessage'
        })
    },
    find(name) {
      this.actressName = name
      document.title = `${this.actressName} | idol finder`
      this.fetch(this.actressName, this.itemPerPage, 0)
    },
    changePage(page) {
      console.log('changePage: ' + page)
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
