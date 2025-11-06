<script setup>
import { ref, computed } from 'vue'

const tasques = ref([
  { id: 1, nom: 'Tasca 1', completada: false },
  { id: 2, nom: 'Tasca 2', completada: false },
  { id: 3, nom: 'Tasca 3', completada: false },
  { id: 4, nom: 'Tasca 4', completada: false }
])

const novaTasca = ref('')
const mostrarPendents = ref(false)

const afegirTasca = () => {
  if (novaTasca.value.trim() === "") return
  let nouId = 1
  if (tasques.value.length > 0) {
    const ultimaTasca = tasques.value[tasques.value.length - 1]
    nouId = ultimaTasca.id + 1
  }
  tasques.value.push({
    id: nouId,
    nom: novaTasca.value,
    completada: false
  })
  novaTasca.value = ""
}

const eliminarTasca = (id) => {
  tasques.value = tasques.value.filter(tasca => tasca.id !== id)
}
const marcarTasca = (tasca) => {
  tasca.completada = !tasca.completada
}
const tasquesFiltrades = computed(() => {
  return mostrarPendents.value
    ? tasques.value.filter(tasca => !tasca.completada)
    : tasques.value
})
const totalTasques = computed(() => tasques.value.length)
const pendents = computed(() => tasques.value.filter(tasca => !tasca.completada).length)
</script>

<template>
  <div class="fons">
    <div class="contenidor">
      <h1>Gestor de Tasques</h1>

      <div class="nova-tasca">
        <input v-model="novaTasca" placeholder="Escriu una nova tasca" />
        <button class="boto-afegir" @click="afegirTasca">Afegir</button>
      </div>

      <div class="filtres">
        <input type="checkbox" v-model="mostrarPendents" id="pendents" />
        <label for="pendents">Mostra només pendents</label>
      </div>

      <ul>
        <li v-for="tasca in tasquesFiltrades" :key="tasca.id">
          <span :class="{ completada: tasca.completada }">
            {{ tasca.nom }}
          </span>
          <div class="botons">
            <button class="boto-completar" @click="marcarTasca(tasca)">
              {{ tasca.completada ? 'Desmarcar' : 'Completar' }}
            </button>
            <button class="boto-eliminar" @click="eliminarTasca(tasca.id)">
              🗑️
            </button>
          </div>
        </li>
      </ul>

      <p class="infoTasques">Total: {{ totalTasques }} | Pendents: {{ pendents }}</p>
    </div>
  </div>
</template>

<style scoped>
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

.nova-tasca {
  display: flex;
  gap: 10px;
  justify-content: center;
  margin-bottom: 16px;
}

button {
  border: none;
  font-weight: bold;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s ease;
}

.boto-afegir,
.boto-completar {
  background-color: #ffcc00;
  color: #000;
}

.boto-afegir:hover,
.boto-completar:hover {
  background-color: #e6b800;
}

.boto-eliminar {
  background-color: #ff4040;
  color: #fff;
}

.boto-eliminar:hover {
  background-color: #d93636;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

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

.infoTasques {
  margin-top: 16px;
  font-weight: bold;
  color: #ffcc00;
}
</style>
