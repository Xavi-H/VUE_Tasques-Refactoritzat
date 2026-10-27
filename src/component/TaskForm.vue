<script setup>
import { ref } from 'vue'

const emit = defineEmits(['afegir-tasca'])

const titol = ref('') // Guarda el que l'usuari escriu

function enviar() {
  const text = titol.value.trim()

  if (text === '') {
    return // Si está buit, no envia res al pare
  }

  emit('afegir-tasca', text) // Envía el titol al pare
  titol.value = '' // Neteja el input del formulari
}
</script>

<template>
    <section>
      <label for="novaTasca">Nova tasca:</label>
      <input id="novaTasca" v-model="titol" type="text" placeholder="Escriu una nova tasca">
      <button type="button" @click="enviar">Afegir</button> <!--Crida a la funció que fa un emit del titol que escriu l'usuari pero comprovant que ha escrit alguna cosa-->
    </section>
</template>