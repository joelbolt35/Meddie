<template>
  <b-nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="#">
      <img src="../static/pill.png" width="30" height="30" class="d-inline-block align-top" alt="">
      Bootstrap
    </a>

    <b-nav class="nav nav-pills mb-3" id="pills-tab">
      <b-nav-item to="/" :active="(activePage==='/') ? true : false">Home</b-nav-item>
      <b-nav-item to="/about" :active="(activePage==='/about') ? true : false">About</b-nav-item>
      <b-nav-item to="/contact" :active="(activePage==='/contact') ? true : false">Contact</b-nav-item>
    </b-nav>


  </b-nav>
</template>
<script>
export default {
  name: 'AppHeader',
  computed: {
    activePage() {
      return this.$route.path;
    }
  }
}
</script>

<style>
.active {
  background-color: gray !important;
}
#pills-tab {
  padding-top: 17px;
  margin: auto;
}

.navbar {
  padding-top: 0 !important;
  padding-bottom: 0 !important;
}
.navbar-light .navbar-brand {
  margin: auto;
}

</style>
