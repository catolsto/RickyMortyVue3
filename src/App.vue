<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>

<div class="container">
    <header class="d-flex flex-wrap justify-content-center py-3 mb-4 border-bottom">
      <a href="/" class="d-flex align-items-center mb-3 mb-md-0 me-md-auto text-dark text-decoration-none">
        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="65" height="65" />
        <span class="fs-4">RickyMorty App</span>
      </a>

      <ul class="nav nav-pills">
        <li class="nav-item">
          <RouterLink class="nav-link my-1" active-class="active" to="/">Inicio</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link my-1" active-class="active" to="/about">Acerca de</RouterLink>
        </li>

      </ul>
    </header>
  </div>

  <RouterView />

</template>

<style scoped>

</style>
