<script setup>
// Rep una tasca
const props = defineProps({
  tasca: {
    type: Object,
    required: true
  }
})
// Declara els avisos que pot enviar al pare 
const emit = defineEmits(['canviar-estat', 'eliminar'])

// Demana confirmació abans d'avisar al pare que vol eliminar la tasca
function confirmarEliminar() {
  const segur = confirm(`Estàs segur que vols eliminar la tasca "${props.tasca.titol}"?`)

  if (segur) {
    emit('eliminar', props.tasca.id) // Només s'envia l'emit si l'usuari accepta
  }
}
</script>

<template>
  <li>
    <span :class="{ completada: tasca.completada }">{{ tasca.titol }}</span>

    <button type="button" @click="emit('canviar-estat', tasca.id)">
      {{ tasca.completada ? 'Desmarcar' : 'Completar' }}
    </button>

    <button type="button" @click="confirmarEliminar">Eliminar</button> <!--Crida a la funció que demana confirmació abans de fer l'emit-->
  </li>
</template>