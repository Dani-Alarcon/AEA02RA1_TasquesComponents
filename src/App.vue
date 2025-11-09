<script setup>
import { ref, computed } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'

const tasques = ref([
  { id: 1, nom: 'Tasca 1', completada: false },
  { id: 2, nom: 'Tasca 2', completada: false },
  { id: 3, nom: 'Tasca 3', completada: false },
  { id: 4, nom: 'Tasca 4', completada: false }
])

const mostrarPendents = ref(false)

const afegirTasca = (nom) => {
  if (!nom.trim()) return
  const nouId = tasques.value.length ? tasques.value[tasques.value.length - 1].id + 1 : 1
  tasques.value.push({ id: nouId, nom, completada: false })
}

const eliminarTasca = (id) => {
  tasques.value = tasques.value.filter(t => t.id !== id)
}

const marcarTasca = (id) => {
  const tasca = tasques.value.find(t => t.id === id)
  if (tasca) tasca.completada = !tasca.completada
}

const tasquesFiltrades = computed(() => {
  return mostrarPendents.value
    ? tasques.value.filter(t => !t.completada)
    : tasques.value
})

const totalTasques = computed(() => tasques.value.length)
const pendents = computed(() => tasques.value.filter(t => !t.completada).length)
</script>

<template>
  <div class="fons">
    <div class="contenidor">
      <h1>Gestor de Tasques</h1>

      <TaskForm @afegir="afegirTasca" />

      <div class="filtres">
        <input type="checkbox" v-model="mostrarPendents" id="pendents" />
        <label for="pendents">Mostra només pendents</label>
      </div>

      <TaskList
        :tasques="tasquesFiltrades"
        @eliminar="eliminarTasca"
        @marcar="marcarTasca"
      />

      <p class="infoTasques">
        Total: {{ totalTasques }} | Pendents: {{ pendents }}
      </p>
    </div>
  </div>
</template>

<style scoped>
/* Puedes mantener tu CSS original aquí */
.fons {
  background-color: #000;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.contenidor {
  text-align: center;
  width: 340px;
  background-color: #0a0a0a;
  color: #fff;
  border: 2px solid #ff0000;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 0 20px rgba(255, 0, 0, 0.4);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.contenidor:hover {
  transform: scale(1.1);
  box-shadow: 0 0 40px rgba(255, 0, 0, 0.7);
}

h1 {
  color: #ff4040;
  margin-bottom: 20px;
}

.filtres {
  margin-bottom: 16px;
  font-size: 14px;
  color: #ccc;
}

.infoTasques {
  margin-top: 16px;
  font-weight: bold;
  color: #ffcc00;
}
</style>
