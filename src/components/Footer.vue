<template>
  <div class="row footerContainer">

    <div class="col-lg-6 titleContainer">
        <br>
        <h3>Three.js+Vue.Js Configurator Interactive demo</h3>
        <br>
    </div>

    <div class="col-lg-6 textContainer">
        <h5>Interactive demo incorporating the Vue.js Framework alongside Three.js</h5>
        <p>Model materials as well as scene lighting can be controlled by selecting the options on the right. Model will update in real-time.
        Requires stable internet connection. For some settings will require a device with greater performance.
        </p>
        Developed by S. Marlokov, 2021.
    </div>

  </div>
</template>

<script>
export default {
  name: 'Footer',
  props: {
  },
  data() {
    return {
        loaded: false,
    }
  },
  methods: {

  },
  mounted() {
      this.loaded = true
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3{
    text-align: center;
}
.footerContainer{
  padding: 1.5% 0;
  text-align: center;
}

.titleContainer{
    border-right: 1px solid rgb(163, 163, 163);
}
.textContainer{
    color:honeydew;
    text-align:left;
}
</style>
