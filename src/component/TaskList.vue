<script setup>
import TaskItem from './TaskItem.vue'

// Rep l'array de tasques
const props = defineProps({
  tasques: {
    type: Array,
    required: true
  }
})
// Declara els avisos que pot enviar al pare  (igual que TaskItem)
const emit = defineEmits(['canviar-estat', 'eliminar'])
</script>

<template>
  <p v-if="tasques.length === 0">No hi ha tasques per mostrar.</p>

  <ul v-else>
    <!--Crea un TaskItem per cada tasca de la llista que rep amb el prop-->
    <TaskItem
      v-for="tasca in tasques"
      :key="tasca.id"
      :tasca="tasca"
      @canviar-estat="emit('canviar-estat', $event)"
      @eliminar="emit('eliminar', $event)"
    /> <!--$event es el valor que rep del emi del fill (taskItem)-->
  </ul>
</template>