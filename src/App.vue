<script setup>
import TaskList from './component/TaskList.vue'
import TaskForm from './component/TaskForm.vue'
import { ref, computed } from 'vue'

// Llista de tasques
const tasques = ref([
    {id: 1, titol: 'Tasca 1', completada: false},
    {id: 2, titol: 'Tasca 2', completada: true}
])

const mostrarPendents = ref(false)

// computed recalcula les tasques pendents quan canvia la llista
const tasquesPendents = computed(() => {
  return tasques.value.filter(tasca => !tasca.completada).length
})

const tasquesCompletades = computed(() => {
  return tasques.value.filter(tasca => tasca.completada).length
})

// Si el filtre està activat, només mostra les tasques pendents
const tasquesVisibles = computed(() => {
  if (mostrarPendents.value) {
    return tasques.value.filter(tasca => !tasca.completada) // Treu les que estiguin completades
  }

  return tasques.value
})

// Rep el titol del fill
function afegirTasca(titol) {
  tasques.value.push({
    id: Date.now(), // Genera un id de la data actual en la que es crida a la funció
    titol: titol,
    completada: false
  })
}

// Canvia l'estat de la tasca amb el id que rep del fill
function canviarEstat(id) {
  const tasca = tasques.value.find(t => t.id === id)
  if (tasca) {
    tasca.completada = !tasca.completada
  }
}

// Elimina una tasca
function eliminarTasca(id) {
  tasques.value = tasques.value.filter(tasca => tasca.id !== id)
}
</script>

<template>
<main>
    <h1>Gestor de tasques</h1>

    <TaskForm @afegir-tasca="afegirTasca" />

    <section>
      <label>
        <input v-model="mostrarPendents" type="checkbox">Mostrar només tasques pendents
      </label>
    </section>

  <TaskList :tasques="tasquesVisibles" @canviar-estat="canviarEstat" @eliminar="eliminarTasca"/>

    <section>
      <p>Total: <b>{{ tasques.length }}</b> | Pendents: <b>{{ tasquesPendents }}</b> | Completades: <b>{{tasquesCompletades}}</b></p>
    </section>
  </main>
</template>
<style>
/* Per distingir les tasques completades */
.completada {
  text-decoration: line-through;
  color: gray;
}
main {
  max-width: 350px;
  margin: 40px auto;
  padding: 20px;
  text-align: center;
  background-color: #f2f2f2;
  border-radius: 10px;
}

ul {
  padding: 0;
  list-style: none;
}

li {
  margin: 10px;
}

button {
  background-color: #6c63ff;
  color: white;
  border: none;
  border-radius: 15px;
  padding: 8px 15px;
  cursor: pointer;
}
</style>