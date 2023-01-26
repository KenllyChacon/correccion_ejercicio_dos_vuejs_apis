<template>
  <div id="container">
    <h1>CODIGO DE ESTADOS</h1>

    <div id="lista">
      <ul>
        <li v-for="state in arreglo">
          <span>{{ state }}</span>
        </li>
      </ul>
    </div>

    <input id="entrada" v-model="this.texto" type="text" placeholder="Ingrese el codigo estado"
           v-on:keypress.enter="buscar(this.texto)">

    <div id="resultado" v-if="resultadoBusqueda">

      <div class="salida">
        <label id="id_casos_positivos" for="id_casos_positivos_input">Casos positivos:</label>
        <input v-model="this.casosPositivos" id="id_casos_positivos_input" type="text">
      </div>

      <div class="salida">
        <label id="id_total_resultados_pruebas" for="id_total_resultados_pruebas_input">Total de resultados de
          pruebas:</label>
        <input v-model="this.totalResultadosPruebas" id="id_total_resultados_pruebas_input" type="text">
      </div>

      <div class="salida">
        <label id="id_actualmente_hospitalizados" for="id_actualmente_hospitalizados_input">Actualmente
          hospitalizados:</label>
        <input v-model="this.actualmenteHospitalizados" id="id_actualmente_hospitalizados_input" type="text">
      </div>

      <div class="salida">
        <label id="id_muertos" for="id_muertos_input">Muertos:</label>
        <input v-model="this.muertos" id="id_muertos_input" type="text">
      </div>

      <div class="salida">
        <label id="id_casos_positivos_virales" for="id_casos_positivos_virales_input">Casos positivos virales:</label>
        <input v-model="this.casosPositivosVirales" id="id_casos_positivos_virales_input" type="text">
      </div>

      <div class="salida">
        <label id="id_número_aumento_muertes" for="id_número_aumento_muertes_input">Número de aumento en
          muertes:</label>
        <input v-model="this.numeroAumentoMuertes" id="id_número_aumento_muertes_input" type="text">
      </div>
    </div>
  </div>

</template>

<script>
  export default {
    name: "CovidTracking",
    data() {
      return {
        arreglo: null,

        texto: null,

        casosPositivos: null,
        totalResultadosPruebas: null,
        actualmenteHospitalizados: null,
        muertos: null,
        casosPositivosVirales: null,
        numeroAumentoMuertes: null,

        resultadoBusqueda: false
      }
    },
    methods: {
      async consumirAPILista() {
        return await fetch("https://api.covidtracking.com/v1/states/current.json").then(r => r.json())
      },
      async crearVector() {
        const lista = await this.consumirAPILista()
        const resLista = []
        for (const valor in lista) {
          const item = lista[valor]
          const {state} = item
          resLista.unshift(state)
        }
        this.arreglo = resLista
      },
      async consumirAPIEspecifico(codigoEstado) {
        return await fetch("https://api.covidtracking.com/v1/states/" + codigoEstado + "/current.json").then(r => r.json())
      },
      async buscar(codigoEstado) {
        const data = await this.consumirAPIEspecifico(codigoEstado.toLowerCase())
        const {positive, totalTestResults, hospitalizedCurrently, death, totalTestsViral, deathIncrease} = data
        this.casosPositivos = positive
        this.totalResultadosPruebas = totalTestResults
        this.actualmenteHospitalizados = hospitalizedCurrently
        this.muertos = death
        this.casosPositivosVirales = totalTestsViral
        this.numeroAumentoMuertes = deathIncrease
        this.resultadoBusqueda = true
      }
    },
    mounted() {
      this.crearVector()
    }
  }
</script>

<style scoped>

#entrada{
  margin: 50px auto;
  width: 500px;
}

  ul li {
    margin: 25px;
  }

  ul {
    column-count: 5;
    margin: 50px auto;
    font-size: 15px;
    background-color: #1F2E3C;
    border: black solid;
    padding: 25px;
    text-align: center;
    list-style-type: none;
  }

  #resultado {
    width: 350px;
    margin: 15px auto;
  }

  input {
    left: 15px;
    font-size: 20px;
    text-align: center;
    display: block;
    width: 300px;
  }

  label {
    text-align: left;
  }

  .salida {
    margin: 25px;
    font-size: 20px;
  }

  h1 {
    text-align: center;
    margin: 50px 0;
  }

</style>