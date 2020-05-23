<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="d-block mx-auto my-3" alt="Vue logo">
    <Search />
  </div>
</template>

<script>
import Search from './components/Search.vue';

export default {
  name: 'App',
  components: {
    Search
  }
}
</script>

<style>
@import '~bootstrap/dist/css/bootstrap.min.css';
@import '~@fortawesome/fontawesome-free/css/all.min.css';

body {
  background-color: #f5f5f5;
}
</style>