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
</script>

<template>
  <li>
    <span :class="{ completada: tasca.completada }">{{ tasca.titol }}</span>

    <button type="button" @click="emit('canviar-estat', tasca.id)">
      {{ tasca.completada ? 'Desmarcar' : 'Completar' }}
    </button>

    <button type="button" @click="emit('eliminar', tasca.id)">Eliminar</button> <!--Avisa al pare que vol eliminar la tasca-->
  </li>
</template>