<template>

<!-- Código HTML del Menú -->

  <nav class="navbar navbar-expand navbar-light bg-light" style="background-color: #0088CC;">
    <a class="navbar-brand" href="#">
      <img v-bind:src="require('./assets/cmv.png')" alt="" height="100" >
    </a>
    <div class="nav navbar-nav">

      <!-- Botones de Navegación -->
      <router-link to="/crear" class="nav-link">Crear</router-link>
      <router-link to="/listar" class="nav-link">Clientes</router-link>

    </div>
  </nav>

  <br><br>

  <router-view/>

</template>