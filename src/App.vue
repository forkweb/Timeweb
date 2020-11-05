<template>
  <div id="app">
    <div class="site">
      <div class="header">
        <div class="header__logo">
          <img src="~@/assets/img/logo.png" alt="">
        </div>
      </div>
      <div class="container">
        <ListPerson/>
      </div>
    </div>
  </div>
</template>

<script>
import ListPerson from './components/ListPerson.vue'

export default {
  name: 'App',
  components: {
    ListPerson
  }
}
</script>

<style lang="scss" type="text/scss">
  @import "~@/style/main.scss";
  // @import "~@/style/adaptive.css";
</style>