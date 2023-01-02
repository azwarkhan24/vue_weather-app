<template>
  <div id="app">
    <weatherApp class="bg-light comp"></weatherApp>
  </div>
</template>

<script>
import weatherApp from './components/weatherApp.vue';

export default {
  name: 'App',
  components: {
    weatherApp
  }
}
</script>

<style>
::-webkit-scrollbar{
  width: 0;
}

.comp{
  height: 100vh;
}


</style>
