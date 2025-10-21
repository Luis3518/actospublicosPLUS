<template>
  <!-- Modal Overlay -->
  <div class="modal-overlay" v-if="isVisible">
    <div class="info-banner">
      <div class="info-banner-content">
        <div class="info-icon">ℹ️</div>
        <div class="info-text">
          <h2 class="banner-title">Aviso Importante</h2>
          <p>
            Los cargos disponibles que se listan a continuación fueron obtenidos automáticamente el 
            <strong>{{ fecha }}</strong> a las <strong>{{ hora }}</strong> desde el 
            <a href="https://actopublico.bue.edu.ar/" target="_blank" rel="noopener noreferrer" class="official-link">sistema oficial de actos públicos</a>.
          </p>
          <p>
            La información puede modificarse sin previo aviso y depende exclusivamente de las autoridades correspondientes.
          </p>
          <p>
            Esta plataforma tiene como objetivo facilitar la consulta y el análisis de los actos públicos, 
            pero no reemplaza al sistema oficial utilizado para la toma de cargos.
            Verifique siempre la información en la fuente oficial antes de tomar cualquier decisión.
          </p>
        </div>
        <button class="accept-btn" @click="closeBanner">Entendido</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'InfoBanner',
  props: {
    fecha: {
      type: String,
      required: true
    },
    hora: {
      type: String,
      required: true
    }
  },
  setup() {
    const isVisible = ref(true)

    const closeBanner = () => {
      isVisible.value = false
    }

    return {
      isVisible,
      closeBanner
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

.info-banner {
  background: linear-gradient(135deg, #a8e6cf 0%, #56c596 50%, #3aa676 100%);
  color: #1a4d2e;
  padding: 2.5rem;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  max-width: 700px;
  width: 90%;
  animation: slideUp 0.4s ease-out;
}

.info-banner-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  align-items: center;
  text-align: center;
}

.info-icon {
  font-size: 3.5rem;
  flex-shrink: 0;
  animation: bounce 1s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.banner-title {
  font-size: 1.8rem;
  font-weight: 700;
  margin: 0 0 1rem 0;
  color: #1a4d2e;
}

.info-text {
  width: 100%;
}

.info-text p {
  margin: 0 0 1rem 0;
  line-height: 1.7;
  font-size: 1rem;
  text-align: left;
}

.info-text p:last-child {
  margin-bottom: 0;
}

.info-text strong {
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

.accept-btn {
  background: white;
  color: #2d7a5b;
  border: none;
  padding: 0.875rem 3rem;
  font-size: 1.1rem;
  font-weight: 700;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  margin-top: 1rem;
}

.accept-btn:hover {
  background: #1a4d2e;
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.accept-btn:active {
  transform: translateY(0);
}

@media (max-width: 768px) {
  .info-banner {
    padding: 2rem 1.5rem;
    width: 95%;
  }

  .banner-title {
    font-size: 1.5rem;
  }

  .info-icon {
    font-size: 2.5rem;
  }

  .info-text p {
    font-size: 0.95rem;
  }

  .accept-btn {
    padding: 0.75rem 2.5rem;
    font-size: 1rem;
  }
}
</style>
