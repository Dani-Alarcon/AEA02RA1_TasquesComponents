<script setup>
const props = defineProps({
  tasca: Object
})

const emit = defineEmits(['eliminar', 'marcar'])
</script>

<template>
  <li>
    <span :class="{ completada: tasca.completada }">
      {{ tasca.nom }}
    </span>
    <div class="botons">
      <button class="boto-completar" @click="emit('marcar')">
        {{ tasca.completada ? 'Desmarcar' : 'Completar' }}
      </button>
      <button class="boto-eliminar" @click="emit('eliminar')">🗑️</button>
    </div>
  </li>
</template>

<style scoped>
li {
  background-color: #111;
  margin: 8px 0;
  padding: 10px;
  border-radius: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #5f0000;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

li:hover {
  background-color: #181818;
}

span.completada {
  text-decoration: line-through;
  color: #ff4040;
}

.botons {
  display: flex;
  gap: 6px;
}

.boto-completar {
  background-color: #ffcc00;
  color: #000;
  border: none;
  font-weight: bold;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.2s ease;
}

.boto-completar:hover {
  background-color: #e6b800;
}

.boto-eliminar {
  background-color: #ff4040;
  color: #fff;
  border: none;
  font-weight: bold;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.2s ease;
}

.boto-eliminar:hover {
  background-color: #d93636;
}
</style>
