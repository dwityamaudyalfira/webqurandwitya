<script>
import { RouterView } from 'vue-router'
import { ref } from "vue";
import axios from "axios";

export default {
  data()
  {
    return {
      error: false,
      loading: true,
      juzs: ref([]),
      surahs: ref([])
    }
  },

  components: {
    RouterView
  },

  mounted()
  {
    this.getJuz()
    this.getSurah()
  },

  methods: {
    getJuz()
    {
      axios.get('https://api.quran.com/api/v4/juzs')
        .then(response =>
        {
          this.juzs = response.data.juzs
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    },
    getSurah()
    {
      axios.get('https://api.quran.com/api/v4/chapters')
        .then(response =>
        {
          this.surahs = response.data.chapters
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    },
  }
}
</script>

<template>
  <section v-if="error">
    <div class="container">
      <h1 class="text-center">KODINGAN ERROR!</h1>
    </div>
  </section>

  <section v-else>
    <div v-if="loading" class="container">
      <h1 class="text-center">Loading...</h1>
    </div>

    <div v-else class="container">
      <nav
        class="navbar navbar-light"
        style="background-color: #E1BA9D"
      >
        <div class="container-fluid">
          <a class="navbar-brand" href="#">
            <img  src="../assets/logo1.ico" class="rounded float-start" alt="" width = 70 height = 70/>
            Quran.com by Dwitya Maudy Alfira
          </a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarText"
            aria-controls="navbarText"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarText">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <RouterLink class="nav-link active" aria-current="page" to="/"
                >Home</RouterLink
                >
              </li>
              <li class="nav-item">
                <router-link :to="{ name: 'search' }" class="nav-link">Search</router-link>
              </li>
              <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button"
                   aria-expanded="false">Surah</a>
                <ul class="dropdown-menu">
                  <li v-for="surah in surahs" :key="surah.id">
                    <router-link :to="{ name: 'surahs', params: { id: surah.id } }" class="dropdown-item">{{
                        surah.name_complex
                      }}</router-link>
                  </li>
                </ul>
              </li>
              <li class="nav-item">
                <router-link :to="{ name: 'random' }" class="nav-link">Ayat Pilihan</router-link>
              </li>
              <li class="nav-item">
                <RouterLink class="nav-link" to="/contact">Contact</RouterLink>
              </li>
            </ul>
          </div>
        </div>
      </nav>
      <RouterView />
    </div>
  </section>
</template>

<style>
.nav-link {
  font-size: 20px;
  color: black;
}
</style>