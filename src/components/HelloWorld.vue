<template>
  <div class="hello">
    <input type="text" v-model="hora">
    <p>Serie generada: {{ serie }}</p>
    <button v-on:click="generarSerie" variant="success">Generar Fibonnaci</button>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      horas:0,
      minutos:0,
      segudos:0,
      serie: 0,
      hora: 0,
      time: null
    }
  },
  methods:{

    generarSerie: function(){
      var today = new Date();
      var minutos = today.getMinutes().toString();
      var segundos = today.getSeconds();

      var semilla1 = parseInt(minutos.charAt(0));
      var semilla2 = parseInt(minutos.charAt(1));
      var repeticiones = segundos;

      var valorObtenido = this.obtener(semilla1, semilla2, repeticiones);

      this.serie= valorObtenido;

      return valorObtenido;

    },

    obtener: function(semilla_1 , semilla_2, repeticiones){
      var fib = [semilla_1, semilla_2];

      for(let i = 2; i < repeticiones + 2; i++){
        fib[i]=fib[i-1]+fib[i-2];
      }

      fib.reverse();

      return fib;

    },

    actualizarTiempo: function(){
      var date= new Date(Date.now());

      this.horas = date.getHours();
      this.minutos = date.getMinutes();
      this.segundos = date.getSeconds();

      this.minutos = this.minutp > 9? this.minutos: + (this.minutos.toString());
      this.segudos = this.segundos >9? this.segundos: '0' + (this.segundos.toString());

      this.hora = this.horas + ':' + this.minutos + ':' + this.segudos;
    },

    crearGrafica: function(){
      var speedCanvas = document.getElementById("speedChart");

    Chart.defaults.global.defaultFontFamily = "Lato";
    Chart.defaults.global.defaultFontSize = 18;

    var speedData = {
      labels: ["0s", "10s", "20s", "30s", "40s", "50s", "60s"],
      datasets: [{
        label: "Car Speed (mph)",
        data: [0, 59, 75, 20, 20, 55, 40],
      }]
    };

    var chartOptions = {
      legend: {
        display: true,
        position: 'top',
        labels: {
          boxWidth: 80,
          fontColor: 'black'
        }
      }
    };

    var lineChart = new Chart(speedCanvas, {
      type: 'line',
      data: speedData,
      options: chartOptions
    });
  }
  
  },
  mounted(){
    this.time = setInterval(()=>{this.actualizarTiempo()},1000);
  },
  beforeDestroy() {
            clearInterval(this.time)
        },
}
/* eslint-disable */
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
