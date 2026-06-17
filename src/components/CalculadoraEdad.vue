<script setup>
import { ref } from 'vue'

const edad = ref('')
const f_nacimiento = ref('')

const calcularEdad = () => {
    if (!f_nacimiento.value) {
        alert("Por favor, ingresa tu fecha de nacimiento")
        return
    }

    const fechaElegida = new Date(f_nacimiento.value)
    const anioNacimiento = fechaElegida.getFullYear()
    const mesNacimiento = fechaElegida.getMonth()
    const diaNacimiento = fechaElegida.getDate() + 1

    const hoy = new Date()
    const anioActual = hoy.getFullYear()
    const mesActual = hoy.getMonth()
    const diaActual = hoy.getDate()

    let edadCalculada = anioActual - anioNacimiento

    const haCumplidoAnios = mesActual > mesNacimiento || (mesActual === mesNacimiento && diaActual >= diaNacimiento)
    if (!haCumplidoAnios) {
        edadCalculada--
    }

    edad.value = edadCalculada
}
</script>

<template>
  <div class="edad-card">
    <div class="edad-card__glow"></div>
    <div class="edad-card__content">
      <div class="edad-card__icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="12" cy="8" r="4"/>
          <path d="M20 21a8 8 0 1 0-16 0"/>
        </svg>
      </div>
      <h1 class="edad-card__title">Calculadora de Edad</h1>
      <p class="edad-card__subtitle">Descubre cuántos años tienes</p>

      <div class="edad-card__input-group">
        <label class="edad-card__label" for="birthdate">Fecha de nacimiento</label>
        <input
          id="birthdate"
          type="date"
          v-model="f_nacimiento"
          class="edad-card__input"
        />
      </div>

      <button class="edad-card__button" @click="calcularEdad">
        <span>Calcular Edad</span>
        <svg class="edad-card__button-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="12" y1="2" x2="12" y2="6"/>
          <line x1="12" y1="18" x2="12" y2="22"/>
          <line x1="4.93" y1="4.93" x2="7.76" y2="7.76"/>
          <line x1="16.24" y1="16.24" x2="19.07" y2="19.07"/>
          <line x1="2" y1="12" x2="6" y2="12"/>
          <line x1="18" y1="12" x2="22" y2="12"/>
          <line x1="4.93" y1="19.07" x2="7.76" y2="16.24"/>
          <line x1="16.24" y1="7.76" x2="19.07" y2="4.93"/>
        </svg>
      </button>

      <transition name="fade">
        <div v-if="edad !== ''" class="edad-card__result">
          <span class="edad-card__result-label">Tu edad es</span>
          <span class="edad-card__result-value">{{ edad }}</span>
          <span class="edad-card__result-unit">años</span>
        </div>
      </transition>
    </div>
  </div>
</template>

<style scoped>
.edad-card {
  position: relative;
  max-width: 420px;
  margin: 2rem auto;
  padding: 2.5rem;
  background: var(--bg, #ffffff);
  border-radius: 24px;
  border: 1px solid var(--border, #e5e4e7);
  box-shadow: var(--shadow, 0 10px 15px -3px rgba(0,0,0,0.1));
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.edad-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04);
}

.edad-card__glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle at 30% 20%, var(--accent-bg, rgba(170,59,255,0.1)) 0%, transparent 50%);
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.edad-card:hover .edad-card__glow {
  opacity: 1;
}

.edad-card__content {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.edad-card__icon {
  width: 56px;
  height: 56px;
  color: var(--accent, #aa3bff);
  background: var(--accent-bg, rgba(170,59,255,0.1));
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 12px;
  box-sizing: border-box;
}

.edad-card__icon svg {
  width: 100%;
  height: 100%;
}

.edad-card__title {
  font-size: 1.75rem;
  font-weight: 700;
  margin: 0;
  color: var(--text-h, #08060d);
  letter-spacing: -0.5px;
}

.edad-card__subtitle {
  margin: -0.5rem 0 0.5rem;
  color: var(--text, #6b6375);
  font-size: 0.95rem;
}

.edad-card__input-group {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.edad-card__label {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--text-h, #08060d);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.edad-card__input {
  width: 100%;
  padding: 0.85rem 1rem;
  border: 2px solid var(--border, #e5e4e7);
  border-radius: 12px;
  font-size: 1rem;
  font-family: inherit;
  background: var(--bg, #fff);
  color: var(--text-h, #08060d);
  box-sizing: border-box;
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
  -webkit-appearance: none;
  appearance: none;
}

.edad-card__input:focus {
  outline: none;
  border-color: var(--accent, #aa3bff);
  box-shadow: 0 0 0 4px var(--accent-bg, rgba(170,59,255,0.1));
}

.edad-card__input::-webkit-calendar-picker-indicator {
  cursor: pointer;
  opacity: 0.6;
  transition: opacity 0.2s;
}

.edad-card__input::-webkit-calendar-picker-indicator:hover {
  opacity: 1;
}

.edad-card__button {
  width: 100%;
  padding: 0.9rem 1.5rem;
  border: none;
  border-radius: 12px;
  background: linear-gradient(135deg, var(--accent, #aa3bff), #7c3aed);
  color: #fff;
  font-size: 1rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  box-shadow: 0 4px 14px rgba(170, 59, 255, 0.3);
}

.edad-card__button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(170, 59, 255, 0.4);
}

.edad-card__button:active {
  transform: translateY(0);
}

.edad-card__button-icon {
  width: 18px;
  height: 18px;
}

.edad-card__result {
  width: 100%;
  padding: 1.25rem;
  border-radius: 16px;
  background: linear-gradient(135deg, var(--accent-bg, rgba(170,59,255,0.1)), rgba(124, 58, 237, 0.05));
  border: 1px solid var(--accent-border, rgba(170,59,255,0.3));
  display: flex;
  align-items: baseline;
  justify-content: center;
  gap: 0.5rem;
}

.edad-card__result-label {
  font-size: 1rem;
  color: var(--text, #6b6375);
}

.edad-card__result-value {
  font-size: 2.5rem;
  font-weight: 800;
  color: var(--accent, #aa3bff);
  line-height: 1;
}

.edad-card__result-unit {
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--text-h, #08060d);
}

.fade-enter-active {
  animation: fadeInUp 0.4s ease;
}

.fade-leave-active {
  animation: fadeInUp 0.3s ease reverse;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
