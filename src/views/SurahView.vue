<script>
import { onMounted } from "vue";

onMounted(() => {
  document.getElementsByTagName("body")[0].style.backgroundColor = "#E1BA9D";
  document.getElementsByTagName("body")[0].style.backgroundSize ="cover";
});

import { ref } from "vue";
import axios from "axios";

export default {
  data()
  {
    return {
      error: false,
      loading: true,
      info: '',
      surah: ref([]),
      infosurah: ref([]),
      translation : ref([])
    }
  },
  watch:{
    $route(){
      this.getSurah();
      this.getInfoSurah();
    }
  },

  mounted()
  {
    this.getSurah()
    this.getInfoSurah()
  },

  methods: {
    getSurah()
    {
      axios.get('https://api.quran.com/api/v4/chapters/' + this.$route.params.id)
        .then(response =>
        {
          this.surah = response.data.chapter
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    },
    getInfoSurah()
    {
      axios.get('https://api.quran.com/api/v4/chapters/' + this.$route.params.id + '/info?language=id')
        .then(response =>
        {
          this.infosurah = response.data.chapter_info
          this.info = this.infosurah.text
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    },
    getTranslate()
    {
      axios.get('https://api.quran.com/api/v4/quran/translations/134?chapter_number=' + this.$route.params.id )
        .then(response =>
        {
          this.translation = response.data.translations
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    }
  }
}
</script>

<template>
  <div class="text-center">
    <h1>Surah {{ surah.name_complex }}</h1>
    <div v-html="info"></div>
  </div>
</template>

<style scoped>
.text-center {
font-size: 25px;
font-weight: bold;
line-height: 2.25rem;

  margin-top: 50px;

text-align: center;
font-family: "monospace";
color: #453F79;
}
</style>