<template>
  <section class="src-componentes-pantalla-dolar">
    <h2>Conversor a USD</h2>
    
    <label>
      Monto en ARS: <input type="number" v-model="pesos">
    </label>

    <label>
      Cotización USD: <input type="number" v-model="cotizacion" :readonly="autoActualizarCotizacion">
    </label>

    <label>
      <input type="checkbox" v-model="autoActualizarCotizacion" @change="autoActualizar">
      actualizar
    </label>

    <p v-if="ultimaActualizacion">
      Última actualización: <strong>{{ ultimaActualizacion }}</strong>
    </p>

    <p>
      Total en USD: <strong>{{ convertidorPesosADolar }}</strong>
    </p>
  </section>
</template>

<script>
import axios from 'axios';

export default {
  name: 'src-componentes-pantalla-dolar',
  data() {
    return {
      pesos: '',
      cotizacion: '',
      autoActualizarCotizacion: false,
      temporizador: null,
      ultimaActualizacion: ''
    };
  },
  watch: {
    autoActualizarCotizacion(valorBool) {
      if (valorBool) {
        this.comenzarActualizacion();
      } else {
        this.detenerActualizacion();
      }
    }
  },
  methods: {
    async obtenerCotizacion() {
      const respuesta = await axios.get('https://api.bluelytics.com.ar/v2/latest');
      this.cotizacion = respuesta.data.blue.value_sell;
      this.ultimaActualizacion = new Date().toLocaleString();
    },

    comenzarActualizacion() {
      this.obtenerCotizacion();
      this.temporizador = setInterval(() => {
        this.obtenerCotizacion();
      }, 2000);
    },

    detenerActualizacion() {
      clearInterval(this.temporizador);
      this.temporizador = null;
    },

    autoActualizar() {
      if (this.autoActualizarCotizacion) {
        this.comenzarActualizacion();
      } else {
        this.detenerActualizacion();
      }
    }
  },
  computed: {
    convertidorPesosADolar() {
      if (this.pesos && this.cotizacion) {
        return (this.pesos / this.cotizacion).toFixed(2);
      }
      return '';
    }
  }
};
</script>

<style scoped lang="css">

</style>
