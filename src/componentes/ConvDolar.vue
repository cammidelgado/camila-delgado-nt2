<template>

  <section class="src-componentes-conv-dolar">
    <div class="jumbotron">
      <h1>Conversor a dólares</h1>
      <hr>
      <p>Ingrese monto $ <input type="text" v-model="pesos" ></p>
      <p>Valor del dólar en $ <input type="text" v-model="cotizacion" :readonly="actualizacion">
        - Actualización <input type="checkbox" v-model="actualizacion" @click="getCotizacion()"><span v-if="actualizacion">{{ ultActualizacion }}</span></p> 
      <p>Valor convertido USD {{ convDolar }}</p>

    </div>
    
  </section>

</template>

<script>
import axios from 'axios';

  export default  {
    name: 'src-componentes-conv-dolar',
    props: [],
    mounted () {
    },
    data () {
      return {
        pesos: '',
        cotizacion: '',
        conversion: '',
        actualizacion: false,
        intervalo: null,
        ultActualizacion: ''
      }
    },
    watch: {
      actualizacion(int) {
        if(int) {
          this.iniciarIntervalo()
        }else {
          this.frenarIntervalo()
        }
      }
    },
    methods: {
      async getCotizacion() {
        const response = await axios.get('https://api.bluelytics.com.ar/v2/latest')
        this.cotizacion = response.data.blue.value_sell
        
        this.ultActualizacion = new Date().toLocaleString()
      },

      iniciarIntervalo(){
        this.getCotizacion()
        this.intervalo = setInterval(() => {
          this.getCotizacion()
          this.ultActualizacion = new Date().toLocaleString()
        },2000)
        
      },

      frenarIntervalo() {
        clearInterval(this.intervalo)
        this.intervalo = null
      }

    },
    computed: {
      convDolar() {
        let conversion = !isNaN(this.pesos) && this.pesos && this.cotizacion? (Number(this.pesos) / Number(this.cotizacion)).toFixed(2) : ''
        return conversion
      },

    }
}


</script>

<style scoped lang="css">
  
</style>
