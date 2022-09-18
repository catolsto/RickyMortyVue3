
<script setup>
    import axios from "axios";
    import { ref } from "vue";
    import { useRoute, useRouter } from "vue-router";
    import Cargando from "../components/Cargando.vue";

    const route = useRoute();
    const router = useRouter();
    const personaje = ref({})
    const carga = ref(true)

    const getData = async () => {
        try {
            const { data } = await axios.get(
                `https://rickandmortyapi.com/api/character/${route.params.id}`
                );
            personaje.value = data;
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
    <div v-if="carga">
        <Cargando />
    </div>
    <div v-else class="container">
        <div class="alert alert-primary" role="alert">
            <h1>Personaje id: {{ $route.params.id }}</h1>
        </div>
        <br>
        <div class="row">
            <div class="col text-center">
                <h2 class="mb-3">Nombre: {{ personaje.name }}</h2>
                <img :src="personaje.image" alt="">
            </div>
            <div class="col mt-5">
                <hr>
                <h3>Estado: {{ personaje.status }}</h3>
                <h3>Especie: {{ personaje.species }}</h3>
                <h3>Genero: {{ personaje.gender }}</h3>
                <h3>Lugar: {{ personaje.location?.name }}</h3>
                <h3>Fecha: {{ personaje.created}}</h3>
                <hr>
            </div>
        </div>
        <router-link class="btn btn-danger btn-lg col-12 mt-5" to="/">
            VOLVER ATRAS...
        </router-link>
    </div>
</template>

<style lang="scss" scoped>

</style>