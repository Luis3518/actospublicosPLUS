<template>
  <!-- Modal Overlay -->
  <div class="modal-overlay">
    <div class="error-banner">
      <div class="error-banner-content">
        <div class="error-icon">⚠️</div>
        <div class="error-text">
          <h2 class="banner-title">Error al Obtener la Información</h2>
          <p>
            No se pudo encontrar información de actos públicos en el sistema.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ErrorBanner',
  props: {
    errorMessage: {
      type: String,
      default: 'No se encontraron archivos JSON de actos públicos'
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
  background: rgba(0, 0, 0, 0.85);
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

.error-banner {
  background: linear-gradient(135deg, #ff6b6b 0%, #ee5a6f 50%, #c92a2a 100%);
  color: #ffffff;
  padding: 2.5rem;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
  max-width: 600px;
  width: 90%;
  animation: slideUp 0.4s ease-out;
  border: 3px solid rgba(255, 255, 255, 0.3);
}

.error-banner-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  align-items: center;
  text-align: center;
}

.error-icon {
  font-size: 4rem;
  flex-shrink: 0;
  animation: shake 0.5s ease-in-out;
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
}

@keyframes shake {
  0%, 100% {
    transform: translateX(0);
  }
  10%, 30%, 50%, 70%, 90% {
    transform: translateX(-5px);
  }
  20%, 40%, 60%, 80% {
    transform: translateX(5px);
  }
}

.banner-title {
  font-size: 1.8rem;
  font-weight: 700;
  margin: 0 0 1rem 0;
  color: #ffffff;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.error-text {
  width: 100%;
}

.error-text p {
  margin: 0 0 1rem 0;
  line-height: 1.7;
  font-size: 1rem;
  text-align: left;
}

.error-text p:last-child {
  margin-bottom: 0;
}

.error-text strong {
  font-weight: 700;
  color: #fff;
  background: rgba(0, 0, 0, 0.2);
  padding: 2px 6px;
  border-radius: 4px;
}

.error-detail {
  margin-top: 1.5rem !important;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 8px;
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  color: #ffeb3b;
  text-align: center !important;
}

@media (max-width: 768px) {
  .error-banner {
    padding: 2rem 1.5rem;
    width: 95%;
  }

  .banner-title {
    font-size: 1.5rem;
  }

  .error-icon {
    font-size: 3rem;
  }

  .error-text p {
    font-size: 0.95rem;
  }

  .error-detail {
    font-size: 0.85rem;
  }
}
</style>
