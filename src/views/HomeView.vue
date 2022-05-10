<script setup>
import { onMounted } from "vue";

onMounted(() => {
  document.getElementsByTagName("body")[0].style.backgroundColor = "#E1BA9D";
  document.getElementsByTagName("body")[0].style.backgroundSize ="cover";
});
</script>

<template>
  <header class="y">
    <div class="container">
      <div class="h1">Assalamu'alaikum! </div>
      <div class="h2">HARI INI SUDAH BACA AL-QUR'AN BELUM?</div>
      <center><a class="btn btn-primary btn-xl" href="surah">MULAI MEMBACA</a></center>
    </div>
  </header>
</template>

<style scoped>
@media (min-width: 1280px) {
  header.y {
    background-repeat: no-repeat;
    background-size: cover;
  }
  header.y .h1 {
    padding-top: 50px;
    font-size: 25px;
    font-style: italic;
    line-height: 2.25rem;

    text-align: center;
    font-family: "Segoe UI";
    color: white;
  }
  header.y .h2 {
    font-size: 40px;
    font-weight: 700;
    line-height: 4.5rem;

    text-align: center;
    font-family: "Segoe UI";
    color: white;
  }
  .btn-primary {
    text-align: center;
    color: #fff;
    background-color: #453F79;
    border-color: #453F79;
    font-weight: 700;

    margin-bottom: 449px;
  }
}
</style>
