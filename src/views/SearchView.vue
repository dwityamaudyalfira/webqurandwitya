<script >
import { onMounted } from "vue";

onMounted(() => {
  document.getElementsByTagName("body")[0].style.backgroundColor = "#E1BA9D";
  document.getElementsByTagName("body")[0].style.backgroundSize ="cover";
});

import { ref } from "vue";
import axios from "axios";

export default {
  data() {
    return {
      cari: "",
      surah: ref([]),
      judul: ref([]),
      name: [],
      audio: "",
      translations: ref([]),
    };
  },

  watch: {
    cari()
    {
      this.getSurah();
      this.getJudul();
      this.getAudio();
      this.getTranslate();
    }
  },

  mounted()
  {
    this.getSurah();
    this.getJudul();
    this.getAudio();
    this.getTranslate();
  },

  methods: {
    getSurah()
    {
      axios.get("https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=" + this.cari)
        .then(response =>
        {
          this.surah = response.data.verses;
        })
        .catch(error =>
        {
          console.log(error);
        });
    },
    getJudul()
    {
      axios.get("https://api.quran.com/api/v4/chapters/" + this.cari + "?language=id")
        .then(response =>
        {
          this.judul = response.data.chapter;
          this.name = this.judul?.translated_name;
        })
        .catch(error =>
        {
          console.log(error);
        });
    },
    getAudio()
    {
      axios.get('https://api.quran.com/api/v4/chapter_recitations/4/' + this.cari)
        .then(response =>
        {
          this.audio = response.data.audio_file;
        })
        .catch(error =>
        {
          console.log(error);
        });
    },
    getTranslate()
    {
      axios.get('https://api.quran.com/api/v4/quran/translations/39?chapter_number=' + this.cari)
        .then(response =>
        {
          this.translations = response.data.translations;
        })
        .catch(error =>
        {
          console.log(error);
        });
    },
  }
};
</script>

<template>
  <header class="y">
  <div class="text-lg-center mt-5">
    <div class="h1">Silahkan masukkan nomor surat anda.</div>
    <input v-model="cari" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
    <div v-if="cari">
      <div class="mt-5">
        <h1>{{ judul?.name_complex }}</h1>
        <br>
        <h1>{{ judul?.name_arabic }}</h1>
        <br>
        <h3>{{ name.name }}</h3>
        <br>
        <h4>Diturunkan di {{ judul?.revelation_place }}</h4>
        <br>
        <h5>Terdiri dari {{judul?.verses_count}} ayat</h5>
        <p v-if="audio" class="text-lg-center mt-4">
          <audio v-bind:src="audio.audio_url" controls>
          </audio>
        </p>
    </div>
    </div>
    <div v-if="cari" v-for="(ayat,index) in surah" :key="index" class="card">
      <div class="card-body">
        <h5 class="card-title text-end  mt-3">{{ ayat?.text_uthmani}}{{ayat?.verse_key}}</h5>
        <p class="card-title text-start mt-3" v-html="translations[index]?.text"></p>
      </div>
    </div>
  </div>
  </header>
</template>

<style scoped>
header.y .h1 {
  font-size: 25px;
  font-style: italic;
  line-height: 2.25rem;

  text-align: center;
  font-family: "Segoe UI";
  color: white;
}
header.y {
    background-repeat: no-repeat;
    background-size: cover;
    background-color: #E1BA9D;
    display:flex;
    align-items:center;
  }
</style>
