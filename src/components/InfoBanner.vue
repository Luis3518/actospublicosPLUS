<template>
  <!-- Modal Overlay -->
  <div class="modal-overlay" v-if="isVisible">
    <div class="info-banner">
      <div class="info-banner-content">
        <div class="offline-icon">ℹ️</div>
        <h2 class="offline-title">Temporalmente Fuera de Línea</h2>
        <p class="offline-text">
          Este servicio se encuentra suspendido temporalmente y será reactivado en 2026.
        </p>
        <p class="offline-text demo-text">
          Podés navegar los cargos del acto público del <strong>{{ fecha }}</strong> a modo de prueba.
        </p>
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
  background: linear-gradient(135deg, #f0f4ff 0%, #e3ebf9 100%);
  color: #2c3e50;
  padding: 2.5rem;
  border-radius: 16px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  max-width: 650px;
  width: 90%;
  animation: slideUp 0.4s ease-out;
  border: 2px solid #cbd5e8;
}

.info-banner-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  align-items: center;
  text-align: center;
}

.offline-icon {
  font-size: 3.5rem;
  opacity: 0.8;
}

.offline-title {
  font-size: 1.75rem;
  font-weight: 700;
  margin: 0 0 1rem 0;
  color: #34495e;
}

.offline-text {
  font-size: 1.05rem;
  margin: 0 0 0.75rem 0;
  font-weight: 500;
  color: #5a6c7d;
  line-height: 1.6;
}

.demo-text {
  background: rgba(86, 197, 150, 0.1);
  padding: 0.75rem 1rem;
  border-radius: 8px;
  border-left: 3px solid #56c596;
  margin-top: 0.5rem;
  margin-bottom: 1rem;
}

.demo-text strong {
  color: #3aa676;
  font-weight: 700;
}

.accept-btn {
  background: linear-gradient(135deg, #56c596 0%, #3aa676 100%);
  color: white;
  border: none;
  padding: 0.875rem 3rem;
  font-size: 1.05rem;
  font-weight: 600;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 3px 12px rgba(58, 166, 118, 0.25);
}

.accept-btn:hover {
  background: linear-gradient(135deg, #3aa676 0%, #2d8c5d 100%);
  transform: translateY(-2px);
  box-shadow: 0 5px 18px rgba(58, 166, 118, 0.35);
}

.accept-btn:active {
  transform: translateY(0);
}

@media (max-width: 768px) {
  .info-banner {
    padding: 2rem 1.5rem;
    width: 95%;
  }

  .offline-icon {
    font-size: 2.5rem;
  }

  .offline-title {
    font-size: 1.4rem;
  }

  .offline-text {
    font-size: 0.95rem;
  }

  .demo-text {
    padding: 0.625rem 0.875rem;
    font-size: 0.9rem;
  }

  .accept-btn {
    padding: 0.75rem 2.5rem;
    font-size: 0.95rem;
  }
}
</style>
