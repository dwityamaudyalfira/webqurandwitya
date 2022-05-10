<script setup>
import Navbar from "../components/navbar.vue";
import { onMounted } from "vue";

onMounted(() => {
  document.getElementsByTagName("body")[0].style.backgroundImage ="Url('src/assets/bg2.jpg')"
  document.getElementsByTagName("body")[0].style.backgroundSize ="cover";
});
</script>

<template>
  <main>
    <navbar/>
    <div class = "title">
      <h1> Selamat datang di Quran web, Silahkan pilih search atau juz  </h1>
    </div>

  </main>
</template>

<style>
.title{
  text-align: center;
}
</style>