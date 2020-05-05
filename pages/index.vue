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
        current: 0,
        count: 0
      },
      currentComp: 'CardContainer',
      data: {
        count: 100,
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
          },
          {
            id: '1018835',
            name: 'Sakita Arina',
            japanName: '咲田ありな',
            bust: '85',
            waist: '58',
            hip: '84',
            height: '160',
            birthday: '1994-03-27',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sakita_arina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1018835%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1016259',
            name: 'Oosima Rina',
            japanName: '双葉かな（大島里奈）',
            bust: '80',
            waist: '58',
            hip: '84',
            height: null,
            birthday: '1994-02-07',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/oosima_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1016259%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1043775',
            name: 'Itihasi Erina',
            japanName: '市橋えりな',
            bust: '84',
            waist: '58',
            hip: '86',
            height: '154',
            birthday: '1993-10-17',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/itihasi_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1043775%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1016264',
            name: 'Itou Rina',
            japanName: '伊藤りな',
            bust: '88',
            waist: '60',
            hip: '90',
            height: '158',
            birthday: '1993-09-26',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/itou_rina2.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1016264%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1017088',
            name: 'Oosawa Rina',
            japanName: '大沢里菜',
            bust: '80',
            waist: '58',
            hip: '82',
            height: '150',
            birthday: '1993-03-09',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/oosawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1017088%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1015428',
            name: 'Ayasiro Yurina',
            japanName: '彩城ゆりな',
            bust: '80',
            waist: '58',
            hip: '82',
            height: '153',
            birthday: '1993-02-24',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/ayasiro_yurina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1015428%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1020949',
            name: 'Siina Marina',
            japanName: '椎名まりな',
            bust: '98',
            waist: '59',
            hip: '87',
            height: '163',
            birthday: '1992-11-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/siina_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1020949%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1003532',
            name: 'Rukawa Rina',
            japanName: '瑠川リナ',
            bust: '81',
            waist: '59',
            hip: '85',
            height: '155',
            birthday: '1991-02-23',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/rukawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1003532%2F&af_id=10278-996&ch=api'
          },
          {
            id: '30585',
            name: 'Umemiya Rina',
            japanName: '梅宮リナ',
            bust: '86',
            waist: '59',
            hip: '88',
            height: '160',
            birthday: '1990-08-28',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/umemiya_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D30585%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1010339',
            name: 'Hatume Rina',
            japanName: '初芽里奈',
            bust: '78',
            waist: '56',
            hip: '81',
            height: '147',
            birthday: '1990-06-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hatume_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1010339%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1008111',
            name: 'Katou Rina',
            japanName: '加藤リナ',
            bust: '85',
            waist: '58',
            hip: '85',
            height: '157',
            birthday: '1990-06-04',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/katou_rina3.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1008111%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1005358',
            name: 'Aizawa Rina',
            japanName: '相澤リナ',
            bust: '88',
            waist: '56',
            hip: '82',
            height: '152',
            birthday: '1990-03-24',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/aizawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1005358%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1005198',
            name: 'Sawamura Sarina',
            japanName: '沢村サリナ（ひかりれお）',
            bust: '83',
            waist: '57',
            hip: '85',
            height: null,
            birthday: '1990-02-14',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sawamura_sarina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1005198%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1001596',
            name: 'Sasaki Karina',
            japanName: '佐々木香里奈',
            bust: '84',
            waist: '60',
            hip: '86',
            height: '170',
            birthday: '1989-12-25',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sasaki_karina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1001596%2F&af_id=10278-996&ch=api'
          },
          {
            id: '26813',
            name: 'Hukada Rina',
            japanName: '深田梨菜（深田梨奈）',
            bust: '92',
            waist: '62',
            hip: '90',
            height: '163',
            birthday: '1989-12-21',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hukada_rina2.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D26813%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1002651',
            name: 'Morito Marina',
            japanName: 'もりとまりな',
            bust: '95',
            waist: '61',
            hip: '88',
            height: '163',
            birthday: '1989-08-08',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/morito_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1002651%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1013277',
            name: 'Erina Moa',
            japanName: '絵里奈モア',
            bust: '92',
            waist: '58',
            hip: '88',
            height: '160',
            birthday: '1989-04-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/erina_moa.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1013277%2F&af_id=10278-996&ch=api'
          },
          {
            id: '23141',
            name: 'Koizumi Rina',
            japanName: '小泉梨菜',
            bust: '82',
            waist: '56',
            hip: '82',
            height: '153',
            birthday: '1989-03-03',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/koizumi_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D23141%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1034956',
            name: 'Ayana Rina',
            japanName: '彩奈リナ（七原あかり）',
            bust: '100',
            waist: '60',
            hip: '96',
            height: '163',
            birthday: '1989-02-26',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/ayana_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1034956%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1003192',
            name: 'Sirase Erina',
            japanName: '白瀬エリナ',
            bust: '85',
            waist: '59',
            hip: '88',
            height: '161',
            birthday: '1989-02-06',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sirase_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1003192%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1000880',
            name: 'Ono Sarina',
            japanName: '小野紗里奈',
            bust: '90',
            waist: '58',
            hip: '84',
            height: '157',
            birthday: '1988-11-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/ono_sarina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1000880%2F&af_id=10278-996&ch=api'
          },
          {
            id: '24032',
            name: 'Marina',
            japanName: 'MARINA',
            bust: '88',
            waist: '56',
            hip: '88',
            height: '161',
            birthday: '1988-07-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D24032%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1019322',
            name: 'Huzisaki Erina',
            japanName: '藤崎エリナ',
            bust: '89',
            waist: '58',
            hip: '84',
            height: '163',
            birthday: '1988-05-16',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/huzisaki_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1019322%2F&af_id=10278-996&ch=api'
          },
          {
            id: '25413',
            name: 'Isihara Rina',
            japanName: '石原莉奈',
            bust: '85',
            waist: '56',
            hip: '84',
            height: '155',
            birthday: '1987-08-29',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/isihara_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D25413%2F&af_id=10278-996&ch=api'
          },
          {
            id: '28479',
            name: 'Oda Marina',
            japanName: '織田マリナ',
            bust: '88',
            waist: '58',
            hip: '85',
            height: '162',
            birthday: '1987-08-25',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/oda_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D28479%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1002406',
            name: 'Ozawa Marina',
            japanName: '小沢真理奈',
            bust: '90',
            waist: '59',
            hip: '89',
            height: '162',
            birthday: '1987-06-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/ozawa_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1002406%2F&af_id=10278-996&ch=api'
          },
          {
            id: '15901',
            name: 'Morino Marina',
            japanName: '森野まりな',
            bust: '83',
            waist: '60',
            hip: '86',
            height: '163',
            birthday: '1987-03-09',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/morino_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D15901%2F&af_id=10278-996&ch=api'
          },
          {
            id: '18156',
            name: 'Himekawa Rina',
            japanName: '姫川りな',
            bust: '85',
            waist: '56',
            hip: '83',
            height: '159',
            birthday: '1987-02-13',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/himekawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D18156%2F&af_id=10278-996&ch=api'
          },
          {
            id: '21305',
            name: 'Ganaha Rina',
            japanName: '我那覇りな',
            bust: '85',
            waist: '56',
            hip: '85',
            height: null,
            birthday: '1987-01-29',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/ganaha_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D21305%2F&af_id=10278-996&ch=api'
          },
          {
            id: '14163',
            name: 'Huzimoto Marina',
            japanName: '藤本まりな',
            bust: '84',
            waist: '56',
            hip: '88',
            height: '160',
            birthday: '1986-12-24',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/huzimoto_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D14163%2F&af_id=10278-996&ch=api'
          },
          {
            id: '15299',
            name: 'Sarina',
            japanName: 'SARINA',
            bust: '85',
            waist: '60',
            hip: '84',
            height: '160',
            birthday: '1986-11-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sarina2.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D15299%2F&af_id=10278-996&ch=api'
          },
          {
            id: '23694',
            name: 'Aina Rina',
            japanName: '愛菜りな',
            bust: '88',
            waist: '58',
            hip: '86',
            height: '153',
            birthday: '1986-08-29',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/aina_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D23694%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1020504',
            name: 'Siraisi Marina',
            japanName: '白石茉莉奈',
            bust: '90',
            waist: '60',
            hip: '90',
            height: '154',
            birthday: '1986-08-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/siraisi_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1020504%2F&af_id=10278-996&ch=api'
          },
          {
            id: '21066',
            name: 'Sawaziri Marina',
            japanName: '沙希（沢尻マリナ）',
            bust: '80',
            waist: '58',
            hip: '87',
            height: '160',
            birthday: '1986-05-05',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sawaziri_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D21066%2F&af_id=10278-996&ch=api'
          },
          {
            id: '16618',
            name: 'Hayakawa Serina',
            japanName: '早川瀬里奈',
            bust: '86',
            waist: '57',
            hip: '83',
            height: '160',
            birthday: '1986-02-04',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hayakawa_serina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D16618%2F&af_id=10278-996&ch=api'
          },
          {
            id: '15349',
            name: 'Yuuki Rina',
            japanName: '結城リナ',
            bust: '84',
            waist: '59',
            hip: '85',
            height: '163',
            birthday: '1985-12-27',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/yuuki_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D15349%2F&af_id=10278-996&ch=api'
          },
          {
            id: '11106',
            name: 'Katase Marina',
            japanName: '片瀬茉莉奈',
            bust: '86',
            waist: '56',
            hip: '85',
            height: '157',
            birthday: '1985-12-14',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/katase_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D11106%2F&af_id=10278-996&ch=api'
          },
          {
            id: '24261',
            name: 'Mori Nanako',
            japanName: '森ななこ',
            bust: '92',
            waist: '58',
            hip: '87',
            height: '164',
            birthday: '1985-08-01',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/mori_nanako.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D24261%2F&af_id=10278-996&ch=api'
          },
          {
            id: '10353',
            name: 'Kurosawa Erina',
            japanName: '黒沢英里奈（喜田嶋りお）',
            bust: '84',
            waist: '54',
            hip: '84',
            height: '155',
            birthday: '1985-07-18',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/kurosawa_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D10353%2F&af_id=10278-996&ch=api'
          },
          {
            id: '11028',
            name: 'Aikawa Rina',
            japanName: '相川リナ',
            bust: '85',
            waist: '59',
            hip: '88',
            height: null,
            birthday: '1985-06-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/aikawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D11028%2F&af_id=10278-996&ch=api'
          },
          {
            id: '17411',
            name: 'Wakamiya Rina',
            japanName: '若宮莉那',
            bust: '92',
            waist: '60',
            hip: '86',
            height: '160',
            birthday: '1985-06-01',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/wakamiya_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D17411%2F&af_id=10278-996&ch=api'
          },
          {
            id: '7187',
            name: 'Morinaga Noa',
            japanName: '森永のあ',
            bust: '84',
            waist: '58',
            hip: '83',
            height: '157',
            birthday: '1984-10-13',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/morinaga_noa.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D7187%2F&af_id=10278-996&ch=api'
          },
          {
            id: '4929',
            name: 'Katou Marina',
            japanName: '加藤まりな',
            bust: '80',
            waist: '58',
            hip: '85',
            height: null,
            birthday: '1984-02-02',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/katou_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D4929%2F&af_id=10278-996&ch=api'
          },
          {
            id: '7182',
            name: 'Rina',
            japanName: 'Rina',
            bust: '86',
            waist: '58',
            hip: '86',
            height: '158',
            birthday: '1983-11-26',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D7182%2F&af_id=10278-996&ch=api'
          },
          {
            id: '6627',
            name: 'Nakayama Rina',
            japanName: '中山里菜',
            bust: '87',
            waist: '60',
            hip: '87',
            height: null,
            birthday: '1983-11-07',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/nakayama_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D6627%2F&af_id=10278-996&ch=api'
          },
          {
            id: '27986',
            name: 'Maezima Erina',
            japanName: '前島エリナ',
            bust: '84',
            waist: '57',
            hip: '82',
            height: '155',
            birthday: '1983-07-01',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/maezima_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D27986%2F&af_id=10278-996&ch=api'
          },
          {
            id: '7319',
            name: 'Huzisawa Rina',
            japanName: '藤沢理名',
            bust: '83',
            waist: '58',
            hip: '83',
            height: '160',
            birthday: '1983-06-18',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/huzisawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D7319%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1000567',
            name: 'Erina',
            japanName: '英里奈',
            bust: '84',
            waist: '57',
            hip: '82',
            height: '162',
            birthday: '1983-05-29',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/erina2.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1000567%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1021399',
            name: 'Takeuti Sarina',
            japanName: '竹内紗里奈',
            bust: '88',
            waist: '60',
            hip: '87',
            height: '167',
            birthday: '1983-05-24',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/takeuti_sarina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1021399%2F&af_id=10278-996&ch=api'
          },
          {
            id: '8597',
            name: 'Hirasawa Rinako',
            japanName: '平沢里菜子',
            bust: '80',
            waist: '58',
            hip: '82',
            height: '156',
            birthday: '1983-05-18',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hirasawa_rinako.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D8597%2F&af_id=10278-996&ch=api'
          },
          {
            id: '4699',
            name: 'Siratori Nami',
            japanName: '白鳥奈未',
            bust: '83',
            waist: '59',
            hip: '87',
            height: null,
            birthday: '1983-03-12',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/siratori_nami.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D4699%2F&af_id=10278-996&ch=api'
          },
          {
            id: '700',
            name: 'Kyouno Marina',
            japanName: '京野真里奈',
            bust: '84',
            waist: '58',
            hip: '88',
            height: '158',
            birthday: '1983-02-13',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/kyouno_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D700%2F&af_id=10278-996&ch=api'
          },
          {
            id: '2091',
            name: 'Mayuzumi Marina',
            japanName: '黛まりな',
            bust: '80',
            waist: '56',
            hip: '82',
            height: '162',
            birthday: '1983-02-11',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/mayuzumi_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D2091%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1601',
            name: 'Hukada Rina',
            japanName: '深田里菜',
            bust: '90',
            waist: '60',
            hip: '89',
            height: null,
            birthday: '1983-01-27',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hukada_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1601%2F&af_id=10278-996&ch=api'
          },
          {
            id: '993',
            name: 'Sarina Yui',
            japanName: '沙里奈ユイ',
            bust: '88',
            waist: '57',
            hip: '83',
            height: '154',
            birthday: '1982-12-13',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sarina_yui.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D993%2F&af_id=10278-996&ch=api'
          },
          {
            id: '11379',
            name: 'Morinaga Mika',
            japanName: '森永みか',
            bust: '90',
            waist: '57',
            hip: '84',
            height: '150',
            birthday: '1982-09-21',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/morinaga_mika.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D11379%2F&af_id=10278-996&ch=api'
          },
          {
            id: '4958',
            name: 'Takase Rina',
            japanName: '高瀬りな',
            bust: '86',
            waist: '58',
            hip: '86',
            height: '158',
            birthday: '1982-08-14',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/takase_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D4958%2F&af_id=10278-996&ch=api'
          },
          {
            id: '3574',
            name: 'Utuki Rina',
            japanName: '卯月梨奈',
            bust: '83',
            waist: '60',
            hip: '85',
            height: null,
            birthday: '1982-07-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/utuki_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D3574%2F&af_id=10278-996&ch=api'
          },
          {
            id: '2165',
            name: 'Sawada Marina',
            japanName: '沢田麻梨菜',
            bust: null,
            waist: null,
            hip: null,
            height: null,
            birthday: '1982-07-08',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sawada_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D2165%2F&af_id=10278-996&ch=api'
          },
          {
            id: '436',
            name: 'Okada Rina',
            japanName: '岡田りな',
            bust: '84',
            waist: '58',
            hip: '84',
            height: '152',
            birthday: '1982-05-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/okada_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D436%2F&af_id=10278-996&ch=api'
          },
          {
            id: '9180',
            name: 'Sibuya Rina',
            japanName: '渋谷りな',
            bust: '82',
            waist: '56',
            hip: '84',
            height: '150',
            birthday: '1982-03-04',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sibuya_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D9180%2F&af_id=10278-996&ch=api'
          },
          {
            id: '7848',
            name: 'Miduki Marina',
            japanName: '観月まりな',
            bust: '88',
            waist: '58',
            hip: '84',
            height: null,
            birthday: '1982-02-20',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/miduki_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D7848%2F&af_id=10278-996&ch=api'
          },
          {
            id: '3160',
            name: 'Sawaki Rina',
            japanName: '沢木理名',
            bust: '92',
            waist: '62',
            hip: '89',
            height: null,
            birthday: '1981-10-15',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sawaki_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D3160%2F&af_id=10278-996&ch=api'
          },
          {
            id: '3215',
            name: 'Usui Rina',
            japanName: '臼井利奈',
            bust: '83',
            waist: '60',
            hip: '87',
            height: '165',
            birthday: '1981-04-08',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/usui_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D3215%2F&af_id=10278-996&ch=api'
          },
          {
            id: '3329',
            name: 'Okabe Rina',
            japanName: '岡部リナ',
            bust: '85',
            waist: '58',
            hip: '83',
            height: null,
            birthday: '1981-03-10',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/okabe_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D3329%2F&af_id=10278-996&ch=api'
          },
          {
            id: '5218',
            name: 'Sibuya Marina',
            japanName: '渋谷まりな',
            bust: '84',
            waist: '58',
            hip: '86',
            height: '156',
            birthday: '1981-03-02',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sibuya_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D5218%2F&af_id=10278-996&ch=api'
          },
          {
            id: '13859',
            name: 'Satou Serina',
            japanName: '佐藤芹菜',
            bust: '86',
            waist: '59',
            hip: '83',
            height: '159',
            birthday: '1981-02-02',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/satou_serina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D13859%2F&af_id=10278-996&ch=api'
          },
          {
            id: '1468',
            name: 'Matusima Marina',
            japanName: '松嶋まりな',
            bust: '105',
            waist: '59',
            hip: '88',
            height: '156',
            birthday: '1980-12-24',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/matusima_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D1468%2F&af_id=10278-996&ch=api'
          },
          {
            id: '3282',
            name: 'Matusima Erina',
            japanName: '松嶋永里奈',
            bust: '84',
            waist: '58',
            hip: '86',
            height: null,
            birthday: '1980-05-23',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/matusima_erina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D3282%2F&af_id=10278-996&ch=api'
          },
          {
            id: '4695',
            name: 'Katayama Rina',
            japanName: '片山りな',
            bust: '86',
            waist: '56',
            hip: '83',
            height: null,
            birthday: '1980-05-14',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/katayama_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D4695%2F&af_id=10278-996&ch=api'
          },
          {
            id: '782',
            name: 'Kurumizawa Marina',
            japanName: '胡桃沢まり奈',
            bust: '84',
            waist: '59',
            hip: '86',
            height: '158',
            birthday: '1980-02-14',
            imageUrl:
              'https://pics.dmm.co.jp/mono/actjpgs/kurumizawa_marina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D782%2F&af_id=10278-996&ch=api'
          },
          {
            id: '422',
            name: 'Yokokura Rina',
            japanName: '横倉里奈',
            bust: '83',
            waist: '57',
            hip: '83',
            height: null,
            birthday: '1980-02-14',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/yokokura_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D422%2F&af_id=10278-996&ch=api'
          },
          {
            id: '10963',
            name: 'Gotou Rina',
            japanName: '後藤リナ',
            bust: '86',
            waist: '60',
            hip: '86',
            height: '158',
            birthday: '1979-12-05',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/gotou_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D10963%2F&af_id=10278-996&ch=api'
          },
          {
            id: '836',
            name: 'Hirosawa Rina',
            japanName: '広沢利那',
            bust: '83',
            waist: '58',
            hip: '88',
            height: null,
            birthday: '1979-03-03',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/hirosawa_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D836%2F&af_id=10278-996&ch=api'
          },
          {
            id: '2473',
            name: 'Huziwara Rina',
            japanName: '藤原りな',
            bust: '87',
            waist: '58',
            hip: '85',
            height: null,
            birthday: '1978-09-16',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/huziwara_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D2473%2F&af_id=10278-996&ch=api'
          },
          {
            id: '4481',
            name: 'Sakamoto Rina',
            japanName: '坂本リナ',
            bust: '85',
            waist: '58',
            hip: '85',
            height: '157',
            birthday: '1978-01-03',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sakamoto_rina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D4481%2F&af_id=10278-996&ch=api'
          },
          {
            id: '4577',
            name: 'Sakaki Arina',
            japanName: '榊ありな',
            bust: '82',
            waist: '58',
            hip: '86',
            height: null,
            birthday: '1977-12-22',
            imageUrl: 'https://pics.dmm.co.jp/mono/actjpgs/sakaki_arina.jpg',
            siteUrl:
              'https://al.dmm.co.jp/?lurl=https%3A%2F%2Fwww.dmm.co.jp%2Fdigital%2Fvideoa%2F-%2Flist%2F%3D%2Farticle%3Dactress%2Fid%3D4577%2F&af_id=10278-996&ch=api'
          }
        ]
      },
      itemPerPage: 100,
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
      let params = {
        name: name
        // hits: itemPerPage,
        // offset: offset
      }
      // sometime server fail with offset & hit param included
      if (offset > 0) params['offset'] = offset
      axios
        .get('https://jav-rest-api-htpvmrzjet.now.sh/api/actress', params)
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
      this.page.current = 0
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
