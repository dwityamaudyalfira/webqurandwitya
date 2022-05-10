<template>
  <nav class="navbar navbar-expand-lg " >
    <div class="container-fluid">
      <img  src="../assets/logoquran.png" class="rounded float-end"  width = 70 height = 70/>

      <div class ="judul justify-content-center">QUR'AN WEB</div>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ml-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="/"></a>
          </li>
        </ul>

      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar"
};
</script>

<style scoped>
body {
  padding: 0;
  margin: 0;
  background: #f2f6e9;
}
.navbar {
  background: #4655b4;
}
.nav-link,
.navbar-brand {
  color: #fff;
  cursor: pointer;
}
.nav-link {
  margin-right: 1em !important;
}
.nav-link:hover {
  color: #000;
}
.navbar-collapse {
  justify-content: flex-end;
}
.judul {
  text-align: center;
  color: #f2f2f2;
  font-size: 20px;
  font-family: "Book Antiqua";
}
</style>