<script setup>
import { ref, computed } from 'vue'

// Llista de tasques
const tasques = ref([
    {id: 1, titol: 'Tasca 1', completada: false},
    {id: 2, titol: 'Tasca 2', completada: true}
])

const novaTasca = ref('')
const mostrarPendents = ref(false)

// computed recalcula les tasques pendents quan canvia la llista
const tasquesPendents = computed(() => {
  return tasques.value.filter(tasca => !tasca.completada).length // 
})

// Si el filtre està activat, només mostra les tasques pendents
const tasquesVisibles = computed(() => {
  if (mostrarPendents.value) {
    return tasques.value.filter(tasca => !tasca.completada) // Treu les que estiguin completades
  }

  return tasques.value
})

// Afegeix una tasca si l'input no està buit
function afegirTasca() {
  const titol = novaTasca.value.trim()

  if (titol === '') {
    return // Si esta buit no crea res
  }

  tasques.value.push({
    id: Date.now(), // Genera un id a partir de la data actual en milisegons, aixi es unic
    titol: titol,
    completada: false
  })

  novaTasca.value = '' // Despres d'afegirla a la llista s'esborra
}

// Canvia l'estat de la tasca
function canviarEstat(tasca) {
  tasca.completada = !tasca.completada
}

// Elimina una tasca
function eliminarTasca(id) {
  tasques.value = tasques.value.filter(tasca => tasca.id !== id)
}
</script>

<template>
  <main>
    <h1>Gestor de tasques</h1>

    <section>
      <label for="novaTasca">Nova tasca:</label>
      <input v-model="novaTasca" type="text" placeholder="Escriu una nova tasca">
      <button type="button" @click="afegirTasca">Afegir</button>
    </section>
</template>