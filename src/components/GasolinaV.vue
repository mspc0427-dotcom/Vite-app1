<script setup>
import { ref, computed } from 'vue';


const GAS_PRICE = 3.312;


const dollarsPaid = ref('');


const totalGallonsReceived = computed(() => {
  if (!dollarsPaid.value || dollarsPaid.value <= 0) return 0;
  

  return dollarsPaid.value / GAS_PRICE;
});

const errorMessage = computed(() => {
  if (dollarsPaid.value !== '' && dollarsPaid.value <= 0) {
    return 'Por favor, ingresa un monto mayor a $0.00';
  }
  return '';
});
</script>
<template>
  <div class="gas-calculator">
    <h2>Despacho de Gasolina</h2>
    
    <label for="dollarsInput">Cantidad de dólares a pagar ($):</label>
    <input 
      id="dollarsInput"
      v-model.number="dollarsPaid" 
      type="number" 
      placeholder="Ej. 10, 20, 50" 
      min="0" 
      step="0.01"
    >
    
    <div v-if="errorMessage" class="error-box">
      {{ errorMessage }}
    </div>
    
    <div v-else-if="dollarsPaid > 0" class="result-box">
      <p>Por un pago de <strong>${{ dollarsPaid.toFixed(2) }}</strong></p>
      <p>Al precio de <strong>${{ GAS_PRICE }}</strong> por galón</p>
      <hr>
      <h3>El cliente recibe: <span>{{ totalGallonsReceived.toFixed(3) }} Galones</span></h3>
    </div>
  </div>
</template>