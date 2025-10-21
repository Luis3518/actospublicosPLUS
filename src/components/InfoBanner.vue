<template>
  <div class="info-banner" v-if="isVisible">
    <div class="info-banner-content">
      <button class="close-btn" @click="closeBanner" title="Cerrar">×</button>
      <div class="info-icon">ℹ️</div>
      <div class="info-text">
        <p>
          Los cargos disponibles que se listan a continuación fueron obtenidos automáticamente el 
          <strong>{{ fecha }}</strong> a las <strong>{{ hora }}</strong> desde el sistema 
          <a href="https://actopublico.bue.edu.ar/" target="_blank" rel="noopener noreferrer" class="official-link">oficial</a> 
          de actos públicos.
        </p>
        <p>
          La información puede modificarse sin previo aviso y depende exclusivamente de las autoridades correspondientes.
        </p>
        <p>
          Esta plataforma tiene como objetivo facilitar la consulta y el análisis de los actos públicos, 
          pero no reemplaza al sistema 
          <a href="https://actopublico.bue.edu.ar/" target="_blank" rel="noopener noreferrer" class="official-link">oficial</a> 
          utilizado para la toma de cargos.
          Verifique siempre la información en la fuente 
          <a href="https://actopublico.bue.edu.ar/" target="_blank" rel="noopener noreferrer" class="official-link">oficial</a> 
          antes de tomar cualquier decisión.
        </p>
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
.info-banner {
  position: sticky;
  top: 0;
  z-index: 1000;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 1.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  animation: slideDown 0.5s ease-out;
}

@keyframes slideDown {
  from {
    transform: translateY(-100%);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.info-banner-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  gap: 1rem;
  align-items: flex-start;
  position: relative;
}

.close-btn {
  position: absolute;
  top: -0.5rem;
  right: -0.5rem;
  background: rgba(255, 255, 255, 0.2);
  border: none;
  color: white;
  font-size: 1.5rem;
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  line-height: 1;
}

.close-btn:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: scale(1.1);
}

.info-icon {
  font-size: 2rem;
  flex-shrink: 0;
}

.info-text {
  flex: 1;
}

.info-text p {
  margin: 0 0 0.75rem 0;
  line-height: 1.6;
  font-size: 0.95rem;
}

.info-text p:last-child {
  margin-bottom: 0;
}

.info-text strong {
  font-weight: 600;
  text-decoration: underline;
}

.official-link {
  color: white;
  font-weight: 600;
  text-decoration: underline;
  transition: all 0.3s ease;
}

.official-link:hover {
  color: #ffd700;
  text-decoration: none;
}

@media (max-width: 768px) {
  .info-banner {
    padding: 1rem;
  }

  .info-banner-content {
    flex-direction: column;
    gap: 0.5rem;
  }

  .info-icon {
    font-size: 1.5rem;
  }

  .info-text p {
    font-size: 0.9rem;
  }

  .close-btn {
    top: 0;
    right: 0;
  }
}
</style>
