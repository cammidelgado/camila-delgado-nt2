<template>
  <div id="app">
    <h1>Final Camila Delgado</h1>
    <h3>YA-21E NT2</h3>
    <br>
    <ConvDolar />
    <hr>
    <p><b>Respuestas:</b> 1:b, d - 2:b - 3:c - 4:e - 5:c</p>
  </div>
</template>

<script>
import ConvDolar from './componentes/ConvDolar.vue';

export default {
  name: 'App',
  components: {
    ConvDolar
  }
}
</script>

<style>
#app {
  
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 30px;
  margin-right: 30px;
}
</style>
