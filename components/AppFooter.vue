<template>
  <footer class="stikybottom row">
    <span class="text-muted copyright">&copy; Joel Mora 2019</span>
    <nuxt-link to="/print" class="nav-link align-right">Print</nuxt-link>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter'
}
</script>

<style scoped>
.stikybottom {
    position: fixed;
    bottom: 0;
    left: 0;
    right:0;
    background: lightgray;
    padding-top: 10px;
    padding-bottom: 10px;
}
.copyright {
    padding-top: 8px;
    padding-bottom: 8px;
    padding-left: 20px;

}
.align-right {
  display: inline;
  margin: 0 0 0 auto;
  padding-right: 36px;
}
</style>
