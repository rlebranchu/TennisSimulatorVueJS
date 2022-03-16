<template>
  <img id="appLogo" alt="Logo ITF" :src="logo">
  <HomePage/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HomePage from './components/pages/HomePage.vue';

@Options({
  components: {
    HomePage,
  },
  data() {
    return {
      logo: require('./assets/logo.png')
    }
  }
})
export default class App extends Vue {}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

html, body {
  font-family: 'Montserrat', sans-serif;
}

#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}

#appLogo {
  width: 200px;
}
</style>
