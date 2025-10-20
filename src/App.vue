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
import actosData from '../actos_publicos_todos_20251020_115648.json'

export default {
  name: 'App',
  components: {
    ActoPublicoCard,
    FilterPanel
  },
  setup() {
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
      previousPage
    }
  }
}
</script>
