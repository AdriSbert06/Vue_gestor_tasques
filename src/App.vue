<template>
  <h1>Gestor de Cartes</h1>
  
  <div class="resum">
    <p>Total de cartes: <strong>{{ totalCartes }}</strong> | Pendents: <strong>{{ totalPendents }}</strong></p>
  </div>
  
  <input 
    v-model="cartaNova" 
    type="text" 
    placeholder="Introdueix la carta" 
  />  

  <button @click="afegirCarta">Afegir</button>

  <label>
    <input type="checkbox" v-model="mostrarPendents" /> Mostrar només cartes pendents
  </label>

  <p v-if="cartesPendents.length === 0" style="color: gray;">
    No hi ha cap carta per mostrar.
  </p>

  <ul v-else>
    <li v-for="carta in cartesPendents" :key="carta.id">
      {{ carta.nom }} - {{ carta.estat }}
      
      <button @click="canviarEstat(carta)">
        {{ carta.estat === 'Obtinguda' ? 'Marcar pendent' : 'Marcar obtinguda' }}
      </button>

      <button @click="eliminarCarta(carta.id)">🗑️</button>
    </li>
  </ul>
</template>

<style scoped>
.resum {
  margin-bottom: 15px;
  font-size: 1.1em;
}
</style>


<script setup>
import { ref, computed } from 'vue'
import '../public/styles.css'

const mostrarPendents = ref(false)
const cartaNova = ref('')

const cartes = ref([
  { id: 1, nom: 'Pikachu', estat: 'Obtinguda' },
  { id: 2, nom: 'Charizard', estat: 'Pendent' },
  { id: 3, nom: 'Greninja', estat: 'Pendent' }
])

const cartesPendents = computed(() => {
  if (mostrarPendents.value) {
    return cartes.value.filter(carta => carta.estat === 'Pendent')
  }
  return cartes.value 
})

const totalCartes = computed(() => cartes.value.length)
const totalPendents = computed(() => cartes.value.filter(carta => carta.estat === 'Pendent').length)

function afegirCarta() {
  if (cartaNova.value.trim() === '') return
  
  const nova = {
    id: Date.now(),
    nom: cartaNova.value,
    estat: 'Pendent'
  }
  
  cartes.value.push(nova)
  cartaNova.value = ''
}

function canviarEstat(carta) {
  carta.estat = carta.estat === 'Obtinguda' ? 'Pendent' : 'Obtinguda'
}

function eliminarCarta(id) {
  cartes.value = cartes.value.filter(carta => carta.id !== id)
}
</script>