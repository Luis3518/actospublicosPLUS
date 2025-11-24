<template>
  <!-- Modal Overlay -->
  <div class="modal-overlay" v-if="isVisible" @click.self="closeModal">
    <div class="info-modal">
      <button class="close-btn" @click="closeModal">✕</button>
      <div class="info-modal-content">
        <div class="info-icon">ℹ️</div>
        <div class="info-text">
          <h2 class="modal-title">Información del Sistema</h2>
          <div class="info-section">
            <h3 class="section-title">Datos actualizados</h3>
            <p>
              Los cargos disponibles que se listan fueron obtenidos automáticamente el 
              <strong>{{ fecha }}</strong> a las <strong>{{ hora }}</strong> desde el 
              <a href="https://actopublico.bue.edu.ar/" target="_blank" rel="noopener noreferrer" class="official-link">sistema oficial de actos públicos</a>.
            </p>
          </div>
          <div class="info-section">
            <h3 class="section-title">Aviso legal</h3>
            <p>
              Esta plataforma tiene como objetivo facilitar la consulta y el análisis de los actos públicos, 
              pero <strong>no reemplaza al sistema oficial</strong> utilizado para la toma de cargos.
            </p>
            <p>
              Verifique siempre la información en la fuente oficial antes de tomar cualquier decisión.
            </p>
          </div>
          <div class="info-section suggestion-section">
            <h3 class="section-title">💬 ¿Tienes sugerencias?</h3>
            <p>
              Tu opinión nos ayuda a mejorar esta plataforma. Si tienes ideas, comentarios o 
              encontraste algún problema, nos encantaría escucharte.
            </p>
            <a 
              href="https://forms.gle/iTJHHEhzy8LfoXWj9" 
              target="_blank" 
              rel="noopener noreferrer"
              class="suggestion-link"
            >
              📝 Enviar sugerencias
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'InfoModal',
  props: {
    fecha: {
      type: String,
      required: true
    },
    hora: {
      type: String,
      required: true
    },
    modelValue: {
      type: Boolean,
      default: false
    }
  },
  emits: ['update:modelValue'],
  setup(props, { emit }) {
    const isVisible = ref(props.modelValue)

    const closeModal = () => {
      isVisible.value = false
      emit('update:modelValue', false)
    }

    // Watch for prop changes
    const updateVisibility = (newValue) => {
      isVisible.value = newValue
    }

    return {
      isVisible,
      closeModal,
      updateVisibility
    }
  },
  watch: {
    modelValue(newValue) {
      this.updateVisibility(newValue)
    }
  }
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.75);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  backdrop-filter: blur(5px);
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(50px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.info-modal {
  background: linear-gradient(135deg, #a8e6cf 0%, #56c596 50%, #3aa676 100%);
  color: #1a4d2e;
  padding: 2.5rem;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  max-width: 700px;
  width: 90%;
  animation: slideUp 0.4s ease-out;
  position: relative;
  max-height: 85vh;
  overflow-y: auto;
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(255, 255, 255, 0.9);
  color: #3aa676;
  border: none;
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 50%;
  font-size: 1.5rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  line-height: 1;
}

.close-btn:hover {
  background: white;
  color: #2d7a5b;
  transform: rotate(90deg);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.info-modal-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  align-items: center;
  text-align: center;
}

.info-icon {
  font-size: 3.5rem;
  flex-shrink: 0;
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.modal-title {
  font-size: 2rem;
  font-weight: 700;
  margin: 0 0 1.5rem 0;
  color: #1a4d2e;
}

.info-text {
  width: 100%;
}

.info-section {
  background: rgba(255, 255, 255, 0.3);
  padding: 1.5rem;
  border-radius: 12px;
  margin-bottom: 1rem;
  text-align: left;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.5);
}

.info-section:last-child {
  margin-bottom: 0;
}

.section-title {
  font-size: 1.3rem;
  font-weight: 700;
  margin: 0 0 0.75rem 0;
  color: #0d3d29;
}

.info-section p {
  margin: 0 0 0.75rem 0;
  line-height: 1.7;
  font-size: 1rem;
  color: #1a4d2e;
}

.info-section p:last-child {
  margin-bottom: 0;
}

.info-section strong {
  font-weight: 700;
  color: #0d3d29;
}

.official-link {
  color: #0d3d29;
  font-weight: 600;
  text-decoration: underline;
  transition: all 0.3s ease;
}

.official-link:hover {
  color: #1a5f42;
  text-decoration: none;
}

.suggestion-section {
  background: rgba(255, 255, 255, 0.5);
  border: 2px solid rgba(255, 255, 255, 0.7);
}

.suggestion-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(26, 77, 46, 0.9);
  color: white;
  text-decoration: none;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 600;
  margin-top: 0.75rem;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.suggestion-link:hover {
  background: rgba(13, 61, 41, 1);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.suggestion-link:active {
  transform: translateY(0);
}

@media (max-width: 768px) {
  .info-modal {
    padding: 2rem 1.5rem;
    width: 95%;
    max-height: 90vh;
  }

  .close-btn {
    width: 2rem;
    height: 2rem;
    font-size: 1.2rem;
  }

  .modal-title {
    font-size: 1.5rem;
    margin-right: 2rem;
  }

  .info-icon {
    font-size: 2.5rem;
  }

  .section-title {
    font-size: 1.1rem;
  }

  .info-section {
    padding: 1.25rem;
  }

  .info-section p {
    font-size: 0.95rem;
  }
}
</style>
