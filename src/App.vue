<template>
  <div class="app">
    <!-- Error Banner -->
    <ErrorBanner v-if="hasError" :errorMessage="errorMessage" />

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
    <InfoBanner v-if="!hasError" :fecha="dataFecha" :hora="dataHora" />

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
          :niveles="uniqueNiveles"
          :cargos="uniqueCargos"
          :especialidades="uniqueEspecialidades"
          :escuelas="uniqueEscuelas"
          :turnos="uniqueTurnos"
          :distritos="uniqueDistritos"
          :causas="uniqueCausas"
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
import ErrorBanner from './components/ErrorBanner.vue'

// Import all JSON files automatically and get the most recent one
const jsonModules = import.meta.glob('../actos_publicos_*.json', { eager: true })

// Function to get the most recent JSON file
function getMostRecentJson() {
  const files = Object.keys(jsonModules)
  
  if (files.length === 0) {
    throw new Error('No se encontraron archivos JSON de actos públicos')
  }
  
  // Extract timestamps from filenames and sort
  const sortedFiles = files.sort((a, b) => {
    const timestampA = a.match(/(\d{8}_\d{6})/)?.[1] || ''
    const timestampB = b.match(/(\d{8}_\d{6})/)?.[1] || ''
    return timestampB.localeCompare(timestampA) // Most recent first
  })
  
  const mostRecentFile = sortedFiles[0]
  return {
    data: jsonModules[mostRecentFile].default,
    filename: mostRecentFile.split('/').pop()
  }
}

// Try to load the most recent JSON, handle errors gracefully
let actosData = null
let jsonFilename = ''
let loadError = null

try {
  const result = getMostRecentJson()
  actosData = result.data
  jsonFilename = result.filename
} catch (error) {
  loadError = error.message
}

export default {
  name: 'App',
  components: {
    ActoPublicoCard,
    FilterPanel,
    InfoBanner,
    ErrorBanner
  },
  setup() {
    // Check if there was an error loading the JSON
    const hasError = ref(!!loadError)
    const errorMessage = ref(loadError || '')

    // Extract date and time from JSON filename
    // Filename format: actos_publicos_todos_20251020_115648.json
    const dateTimeMatch = jsonFilename.match(/(\d{4})(\d{2})(\d{2})_(\d{2})(\d{2})(\d{2})/)
    
    let dataFecha = ''
    let dataHora = ''
    
    if (dateTimeMatch) {
      const [_, year, month, day, hour, minute, second] = dateTimeMatch
      dataFecha = `${day}/${month}/${year}`
      dataHora = `${hour}:${minute}:${second}`
    }
    
    const actosPublicos = ref(hasError.value ? [] : actosData.actos_publicos)
    const currentPage = ref(1)
    const itemsPerPage = 4
    
    const filters = ref({
      area: '',
      cargo: '',
      especialidad: '',
      escuela: '',
      turno: '',
      distrito: '',
      causa: ''
    })

    // Extract unique values from JSON for filters
    const uniqueNiveles = computed(() => {
      const niveles = [...new Set(actosPublicos.value.map(acto => acto.nivel).filter(Boolean))]
      return niveles.sort()
    })

    const uniqueCargos = computed(() => {
      const cargos = [...new Set(actosPublicos.value.map(acto => acto.titulo).filter(Boolean))]
      return cargos.sort()
    })

    const uniqueEspecialidades = computed(() => {
      const especialidades = [...new Set(actosPublicos.value.map(acto => acto.especialidad_tag).filter(Boolean))]
      return especialidades.sort()
    })

    const uniqueEscuelas = computed(() => {
      const escuelas = [...new Set(actosPublicos.value.map(acto => acto.establecimiento).filter(Boolean))]
      return escuelas.sort()
    })

    const uniqueTurnos = computed(() => {
      const turnos = [...new Set(actosPublicos.value.map(acto => acto.turno).filter(Boolean))]
      return turnos.sort()
    })

    const uniqueDistritos = computed(() => {
      const distritos = [...new Set(actosPublicos.value.map(acto => acto.distrito).filter(Boolean))]
      return distritos.sort()
    })

    const uniqueCausas = computed(() => {
      const causas = [...new Set(actosPublicos.value.map(acto => acto.causa).filter(Boolean))]
      return causas.sort()
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
      if (filters.value.especialidad && filters.value.especialidad !== 'Todos') {
        filtered = filtered.filter(acto => acto.especialidad_tag === filters.value.especialidad)
      }
      if (filters.value.escuela && filters.value.escuela !== 'Todos') {
        filtered = filtered.filter(acto => acto.establecimiento === filters.value.escuela)
      }
      if (filters.value.turno && filters.value.turno !== 'Todos') {
        filtered = filtered.filter(acto => acto.turno === filters.value.turno)
      }
      if (filters.value.distrito && filters.value.distrito !== 'Todos') {
        filtered = filtered.filter(acto => acto.distrito === filters.value.distrito)
      }
      if (filters.value.causa && filters.value.causa !== 'Todos') {
        filtered = filtered.filter(acto => acto.causa === filters.value.causa)
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
        especialidad: '',
        escuela: '',
        turno: '',
        distrito: '',
        causa: ''
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
      hasError,
      errorMessage,
      paginatedActos,
      filters,
      currentPage,
      totalPages,
      handleFilterChange,
      clearFilters,
      nextPage,
      previousPage,
      dataFecha,
      dataHora,
      uniqueNiveles,
      uniqueCargos,
      uniqueEspecialidades,
      uniqueEscuelas,
      uniqueTurnos,
      uniqueDistritos,
      uniqueCausas
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
