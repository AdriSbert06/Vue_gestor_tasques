<script setup></script>

<template>
  <h1>Gestio de Tasques</h1>
  <p>
    Escriu una carta
  </p>   
  <button @click="mostrar = !mostrar">Afegir</button>


  <button @click="mostrar = !mostrar">Mostrar cartes faltants</button>
  <p v-show="mostrar">Aquest text es mostra o amaga sense eliminar-lo del DOM</p>
</template>


<script setup>
import { ref } from 'vue'

const mostrar = ref(true)
</script>
<style scoped></style>

