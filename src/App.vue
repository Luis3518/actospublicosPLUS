<template>
  <div class="app">
    <!-- Header -->
    <header class="header">
      <div class="header-content">
        <div class="header-left">
          <div class="logo">Actos Públicos PLUS</div>
        </div>
        <button class="btn-login">test@bue.edu.ar</button>
      </div>
    </header>

    <!-- Info Banner -->
    <InfoBanner :fecha="dataFecha" :hora="dataHora" />

    <div class="main-container">
      <!-- Sidebar -->
      <aside class="sidebar">
      </aside>

      <!-- Main Content -->
      <main class="content">
        <div class="content-header">
          <h2 class="content-title">Cargos disponibles</h2>
        </div>

        <!-- Cards Grid -->
        <div class="cards-grid">
          <ActoPublicoCard
            v-for="acto in paginatedActos"
            :key="acto.link"
            :acto="acto"
          />
        </div>

        <!-- Pagination -->
        <div class="pagination" v-if="totalPages > 1">
          <button 
            class="pagination-btn" 
            @click="previousPage" 
            :disabled="currentPage === 1"
          >
            Anterior
          </button>
          <span class="pagination-info">
            Página {{ currentPage }} de {{ totalPages }}
          </span>
          <button 
            class="pagination-btn" 
            @click="nextPage" 
            :disabled="currentPage === totalPages"
          >
            Siguiente
          </button>
        </div>
      </main>

      <!-- Filter Panel -->
      <aside class="filter-panel">
        <FilterPanel 
          :filters="filters"
          @filter-change="handleFilterChange"
          @clear-filters="clearFilters"
        />
      </aside>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import ActoPublicoCard from './components/ActoPublicoCard.vue'
import FilterPanel from './components/FilterPanel.vue'
import InfoBanner from './components/InfoBanner.vue'
import actosData from '../actos_publicos_todos_20251020_115648.json'

export default {
  name: 'App',
  components: {
    ActoPublicoCard,
    FilterPanel,
    InfoBanner
  },
  setup() {
    // Extract date and time from JSON filename
    // Filename format: actos_publicos_todos_20251020_115648.json
    const jsonFilename = 'actos_publicos_todos_20251020_115648.json'
    const dateTimeMatch = jsonFilename.match(/(\d{4})(\d{2})(\d{2})_(\d{2})(\d{2})(\d{2})/)
    
    let dataFecha = ''
    let dataHora = ''
    
    if (dateTimeMatch) {
      const [_, year, month, day, hour, minute, second] = dateTimeMatch
      dataFecha = `${day}/${month}/${year}`
      dataHora = `${hour}:${minute}:${second}`
    }
    const actosPublicos = ref(actosData.actos_publicos)
    const currentPage = ref(1)
    const itemsPerPage = 4
    
    const filters = ref({
      area: '',
      cargo: '',
      asignatura: '',
      especialidad: '',
      escuela: ''
    })

    // Computed filtered actos
    const filteredActos = computed(() => {
      let filtered = actosPublicos.value

      if (filters.value.area && filters.value.area !== 'Todos') {
        filtered = filtered.filter(acto => acto.nivel === filters.value.area)
      }
      if (filters.value.cargo && filters.value.cargo !== 'Todos') {
        filtered = filtered.filter(acto => acto.titulo === filters.value.cargo)
      }
      if (filters.value.escuela && filters.value.escuela !== 'Todos') {
        filtered = filtered.filter(acto => 
          acto.establecimiento.toLowerCase().includes(filters.value.escuela.toLowerCase())
        )
      }

      return filtered
    })

    // Computed pagination
    const totalPages = computed(() => {
      return Math.ceil(filteredActos.value.length / itemsPerPage)
    })

    const paginatedActos = computed(() => {
      const start = (currentPage.value - 1) * itemsPerPage
      const end = start + itemsPerPage
      return filteredActos.value.slice(start, end)
    })

    // Methods
    const handleFilterChange = (filterType, value) => {
      filters.value[filterType] = value
      currentPage.value = 1 // Reset to first page when filtering
    }

    const clearFilters = () => {
      filters.value = {
        area: '',
        cargo: '',
        asignatura: '',
        especialidad: '',
        escuela: ''
      }
      currentPage.value = 1
    }

    const nextPage = () => {
      if (currentPage.value < totalPages.value) {
        currentPage.value++
      }
    }

    const previousPage = () => {
      if (currentPage.value > 1) {
        currentPage.value--
      }
    }

    return {
      paginatedActos,
      filters,
      currentPage,
      totalPages,
      handleFilterChange,
      clearFilters,
      nextPage,
      previousPage,
      dataFecha,
      dataHora
    }
  }
}
</script>

<style scoped>
/* Estilos adicionales para mejorar el header */
.header {
  backdrop-filter: blur(10px);
}

.logo {
  letter-spacing: 0.5px;
  text-shadow: 0 2px 4px rgba(58, 166, 118, 0.2);
}

.btn-login {
  display: flex;
  align-items: center;
  gap: 8px;
  letter-spacing: 0.3px;
}

.btn-login::before {
  content: "👤";
  font-size: 16px;
}

/* Mejoras para botones de paginación */
.pagination {
  margin-top: 2rem;
}

.pagination-btn {
  min-width: 120px;
  letter-spacing: 0.5px;
  position: relative;
  overflow: hidden;
}

.pagination-btn::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.3);
  transform: translate(-50%, -50%);
  transition: width 0.6s, height 0.6s;
}

.pagination-btn:hover::before {
  width: 300px;
  height: 300px;
}

.pagination-info {
  padding: 12px 20px;
  background: linear-gradient(135deg, #ffffff 0%, #f8fdfb 100%);
  border-radius: 8px;
  border: 2px solid #e0f2ea;
  box-shadow: 0 2px 8px rgba(86, 197, 150, 0.1);
}

/* Animaciones suaves */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.content {
  animation: fadeInUp 0.6s ease-out;
}

.cards-grid {
  animation: fadeInUp 0.8s ease-out;
}

.filter-panel {
  animation: fadeInUp 1s ease-out;
}
</style>
