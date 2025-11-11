<script setup>
import { ref } from 'vue'

const emit = defineEmits(['afegir'])
const novaTasca = ref('')

const enviarTasca = () => {
  if (novaTasca.value.trim() === '') return
  emit('afegir', novaTasca.value)
  novaTasca.value = ''
}
</script>

<template>
  <div class="nova-tasca">
    <input v-model="novaTasca" placeholder="Escriu una nova tasca" />
    <button class="boto-afegir" @click="enviarTasca">Afegir</button>
  </div>
</template>

<style scoped>
.nova-tasca {
  display: flex;
  gap: 10px;
  justify-content: center;
  margin-bottom: 16px;
}

input {
  border-radius: 6px;
  padding: 8px;
  border: 1px solid #333;
  background-color: #111;
  color: #fff;
  transition: border-color 0.3s ease;
}

input:hover {
  border: 1px solid red;
}

input:focus {
  border: 4px solid red;
}

.boto-afegir {
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

.boto-afegir:hover {
  background-color: #e6b800;
}
</style>
