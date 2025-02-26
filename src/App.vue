<template>
  <div id="app">
    <div class="jumbotron">
      <h1 class="display-4">CALCULADORA DE CAMBIO</h1>
      <p class="lead">Convierte dólares a la moneda local fácilmente.</p>
    </div>
    
    
    <ConvertidorUSD /> 
    <hr>
    <p><b>Multiple choice:</b></p>
    <ul>
      <li>1: C</li>
      <li>2: B</li>
      <li>3: C</li>
      <li>4: A</li>
    </ul>
  </div>
</template>

<script>
  import ConvertidorUSD from './componentes/ConvertidorUSD.vue';

  export default {
    name: 'App',
    components: {
      ConvertidorUSD
    }
  }
</script>

<style>
  #app {
    font-family: Arial;
    margin: 20px;
  }
</style>