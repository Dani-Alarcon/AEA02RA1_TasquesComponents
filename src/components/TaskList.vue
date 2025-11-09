<script setup>
import TaskItem from './TaskItem.vue'

const props = defineProps({
  tasques: Array
})

const emit = defineEmits(['eliminar', 'marcar'])
</script>

<template>
  <ul>
    <TaskItem
      v-for="tasca in tasques"
      :key="tasca.id"
      :tasca="tasca"
      @eliminar="emit('eliminar', tasca.id)"
      @marcar="emit('marcar', tasca.id)"
    />
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
