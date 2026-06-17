<script setup>
import { ref } from 'vue'
// 1. Importamos correctamente todos los componentes que vas a usar abajo
//import CalculadoraEdad from './components/CalculadoraEdad.vue'
import GasolinaV from './components/GasolinaV.vue'
//import MiComponente from './components/MiComponente.vue'
//import BindComponente from './components/BindComponente.vue'
import LIstaComponent from './components/LIstaComponent.vue'
// 2. Declaramos las variables reactivas que usas en el template
const message = ref('')
const counter = ref(0)
</script>

<template>
  <div>
    <!-- Renderizado de variables -->
    <h1>{{ message }}</h1>
    <p>Contador: {{ counter }}</p>
    
    <!-- 3. Uso de tus componentes (Asegúrate de que los archivos existan) -->
  
    <GasolinaV/>
    <LIstaComponent/>
  </div>
</template>
