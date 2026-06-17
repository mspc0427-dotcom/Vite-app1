<script setup>
import { ref } from 'vue'

const nuevaTarea = ref('')
const tareas = ref([
  { id: 1, nombre: 'Comprar leche' },
  { id: 2, nombre: 'Lavar el auto' },
  { id: 3, nombre: 'Estudiar para el examen' },
  { id: 4, nombre: 'Hacer ejercicio' }
])

const agregarTarea = () => {
  if (nuevaTarea.value.trim() !== '') {
    tareas.value.push({ id: Date.now(), nombre: nuevaTarea.value })
    nuevaTarea.value = ''
  } else {
    alert("Por favor, ingresa una tarea válida")
  }
}

const removerTarea = (id) => {
  tareas.value = tareas.value.filter(tarea => tarea.id !== id)
}
</script>

<template>
  <div>
    <h1>Lista de Tareas</h1>
    <input v-model="nuevaTarea" placeholder="Nueva tarea" @keyup.enter="agregarTarea" />
    <button @click="agregarTarea">Agregar</button>
    
    <ul>
      <li v-for="tarea in tareas" :key="tarea.id">
        {{ tarea.nombre }}
        <button @click="removerTarea(tarea.id)" style="margin-left: 10px;">Eliminar</button>
      </li>
    </ul>
  </div>
</template>
