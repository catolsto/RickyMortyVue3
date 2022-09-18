
<script setup>
  import axios from "axios";
  import { ref } from "vue";
  import { RouterLink } from "vue-router";
  import ControlPaginacion from "../components/ControlPaginacion.vue";
  import Cargando from "../components/Cargando.vue";

  const personajes = ref(null)
  const fin = ref(42)
  const actual = ref(1)
  const carga = ref(true)

  const siguiente = () => {
    actual.value = actual.value + 1
    getData();
  }
  const previo = () => {
    actual.value = actual.value - 1
    getData();
  }

  const getData = async () => {
    carga.value = true
    try {
        const { data } = await axios.get(`https://rickandmortyapi.com/api/character?page=${actual.value}`);
        personajes.value = data.results;
    } catch (error) {
        console.log(error);
    }  finally {
        setTimeout(() => { 
          carga.value = false  
         }, 10);
    }
};

getData();

</script>

<template>

  <div class="container">
    <h1>Personajes de Rick and Morty:</h1>

      <ControlPaginacion  
      :actual = "actual"
      :fin = "fin"
      @siguiente="siguiente"
      @previo="previo" 
    />
    <p>Página: {{actual}} de {{fin}}</p>

    <div v-if="carga">
      <Cargando  />
    </div>
    <div v-else>
      <div class="row">
          <div class="col" v-for="personaje in personajes" :key="personaje.id">
              <div class="card" style="width: 18rem;">
                <router-link  :to="`/personaje/${personaje.id}`">
                  <img :src="personaje.image" class="card-img-top" :alt="personaje.name" >
                </router-link>
                <div class="card-body">
                  <h5 class="card-title">
                  <router-link  :to="`/personaje/${personaje.id}`">
                    {{ personaje.name }}
                  </router-link>
                  </h5>
                  <p class="card-text">Estado: {{ personaje.status }} - Origen: {{ personaje.origin.name }}</p>
                  <router-link class="btn btn-primary" :to="`/personaje/${personaje.id}`">
                    Ver Detalles...
                  </router-link>
                </div>
              </div>
          </div>
      </div>
    </div>

  </div>

</template>
