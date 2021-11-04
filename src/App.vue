<template>
<div class='row'>

  <div v-show="loaded">
    <div class='col-lg-10 view3d'>
      <Viewer3D/>
    </div>
    <div class='col-lg-2 configurator'>
      <Configurator/>
    </div>
    <div class='col-lg-12 footer'>
      <Footer/>
    </div>
  </div>

</div>
</template>

<script>
import Viewer3D from './components/Viewer3D_2.vue'
import Configurator from './components/Configurator.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Viewer3D,
    Configurator,
    Footer
  },
  data() {
    return {
      loaded: false,
    }
  },
  created() {
    this.loaded = true
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  background: #121212;
  margin-top: 0px;
  overflow: hidden;
  height: 100vh;
}

.view3d {
  height: 85vh;
}

.configurator {
  height: 85vh;
  background: #0a0a0a;
}

.footer {
  background: #1f1f1f;
  height: 15vh;
}

h1 {
    user-select: none;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    text-transform: uppercase;
    color: whitesmoke;
    opacity: 0.55;
}
</style>
