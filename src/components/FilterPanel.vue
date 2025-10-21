<template>
  <div class="filter-panel-container">
    <div class="filter-header">
      <h3 class="filter-title">Filtros</h3>
      <button class="btn-clear-all" @click="clearAll">
        Limpiar Filtros
      </button>
    </div>

    <div class="filters-list">
      <!-- Área Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Área
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.area"
            @change="handleChange('area', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="nivel in niveles" :key="nivel" :value="nivel">
              {{ nivel }}
            </option>
          </select>
          <button 
            v-if="filters.area" 
            class="btn-clear-filter"
            @click="clearFilter('area')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.area" class="filter-chip">
          {{ filters.area }}
          <button class="chip-close" @click="clearFilter('area')">×</button>
        </div>
      </div>

      <!-- Cargos Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Cargos
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.cargo"
            @change="handleChange('cargo', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="cargo in cargos" :key="cargo" :value="cargo">
              {{ cargo }}
            </option>
          </select>
          <button 
            v-if="filters.cargo" 
            class="btn-clear-filter"
            @click="clearFilter('cargo')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.cargo" class="filter-chip">
          {{ filters.cargo }}
          <button class="chip-close" @click="clearFilter('cargo')">×</button>
        </div>
      </div>

      <!-- Especialidad Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Especialidad
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.especialidad"
            @change="handleChange('especialidad', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="especialidad in especialidades" :key="especialidad" :value="especialidad">
              {{ especialidad }}
            </option>
          </select>
          <button 
            v-if="filters.especialidad" 
            class="btn-clear-filter"
            @click="clearFilter('especialidad')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.especialidad" class="filter-chip">
          {{ filters.especialidad }}
          <button class="chip-close" @click="clearFilter('especialidad')">×</button>
        </div>
      </div>

      <!-- Escuela Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Escuela
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.escuela"
            @change="handleChange('escuela', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="escuela in escuelas" :key="escuela" :value="escuela">
              {{ escuela }}
            </option>
          </select>
          <button 
            v-if="filters.escuela" 
            class="btn-clear-filter"
            @click="clearFilter('escuela')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.escuela" class="filter-chip">
          {{ filters.escuela }}
          <button class="chip-close" @click="clearFilter('escuela')">×</button>
        </div>
      </div>

      <!-- Turno Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Turno
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.turno"
            @change="handleChange('turno', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="turno in turnos" :key="turno" :value="turno">
              {{ turno }}
            </option>
          </select>
          <button 
            v-if="filters.turno" 
            class="btn-clear-filter"
            @click="clearFilter('turno')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.turno" class="filter-chip">
          {{ filters.turno }}
          <button class="chip-close" @click="clearFilter('turno')">×</button>
        </div>
      </div>

      <!-- Distrito Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Distrito
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.distrito"
            @change="handleChange('distrito', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="distrito in distritos" :key="distrito" :value="distrito">
              {{ distrito }}
            </option>
          </select>
          <button 
            v-if="filters.distrito" 
            class="btn-clear-filter"
            @click="clearFilter('distrito')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.distrito" class="filter-chip">
          {{ filters.distrito }}
          <button class="chip-close" @click="clearFilter('distrito')">×</button>
        </div>
      </div>

      <!-- Causa Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Causa
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.causa"
            @change="handleChange('causa', $event.target.value)"
          >
            <option value="">Todos</option>
            <option v-for="causa in causas" :key="causa" :value="causa">
              {{ causa }}
            </option>
          </select>
          <button 
            v-if="filters.causa" 
            class="btn-clear-filter"
            @click="clearFilter('causa')"
          >
            ×
          </button>
        </div>
        <div v-if="filters.causa" class="filter-chip">
          {{ filters.causa }}
          <button class="chip-close" @click="clearFilter('causa')">×</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FilterPanel',
  props: {
    filters: {
      type: Object,
      required: true
    },
    niveles: {
      type: Array,
      default: () => []
    },
    cargos: {
      type: Array,
      default: () => []
    },
    especialidades: {
      type: Array,
      default: () => []
    },
    escuelas: {
      type: Array,
      default: () => []
    },
    turnos: {
      type: Array,
      default: () => []
    },
    distritos: {
      type: Array,
      default: () => []
    },
    causas: {
      type: Array,
      default: () => []
    }
  },
  emits: ['filter-change', 'clear-filters'],
  setup(props, { emit }) {
    const handleChange = (filterType, value) => {
      emit('filter-change', filterType, value)
    }

    const clearFilter = (filterType) => {
      emit('filter-change', filterType, '')
    }

    const clearAll = () => {
      emit('clear-filters')
    }

    return {
      handleChange,
      clearFilter,
      clearAll
    }
  }
}
</script>

<style scoped>
.filter-panel-container {
  background: linear-gradient(135deg, #ffffff 0%, #f8fdfb 100%);
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 4px 16px rgba(86, 197, 150, 0.15);
  border: 2px solid #e0f2ea;
}

.filter-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  padding-bottom: 12px;
  border-bottom: 2px solid #e0f2ea;
}

.filter-title {
  margin: 0;
  font-size: 18px;
  font-weight: 700;
  color: #1a4d2e;
  background: linear-gradient(135deg, #2d7a5b 0%, #1a4d2e 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.btn-clear-all {
  background: linear-gradient(135deg, #f0f9f4 0%, #e0f2ea 100%);
  border: 1px solid #56c596;
  border-radius: 8px;
  padding: 6px 12px;
  font-size: 12px;
  font-weight: 600;
  color: #2d7a5b;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-clear-all:hover {
  background: linear-gradient(135deg, #56c596 0%, #3aa676 100%);
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(86, 197, 150, 0.3);
}

.filters-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.filter-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.filter-label {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 14px;
  font-weight: 600;
  color: #1a4d2e;
}

.icon-search {
  font-size: 14px;
}

.filter-input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.filter-select,
.filter-input {
  width: 100%;
  padding: 10px 32px 10px 12px;
  border: 2px solid #d4ebe0;
  border-radius: 8px;
  font-size: 14px;
  color: #1a4d2e;
  background: #ffffff;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-input {
  cursor: text;
}

.filter-select:focus,
.filter-input:focus {
  outline: none;
  border-color: #56c596;
  box-shadow: 0 0 0 3px rgba(86, 197, 150, 0.1);
}

.btn-clear-filter {
  position: absolute;
  right: 8px;
  background: none;
  border: none;
  font-size: 20px;
  color: #56c596;
  cursor: pointer;
  padding: 0;
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 1;
  transition: all 0.3s ease;
  border-radius: 50%;
}

.btn-clear-filter:hover {
  color: #3aa676;
  background: rgba(86, 197, 150, 0.1);
}

.filter-chip {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: linear-gradient(135deg, #56c596 0%, #3aa676 100%);
  color: #fff;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 600;
  max-width: fit-content;
  box-shadow: 0 2px 6px rgba(86, 197, 150, 0.3);
}

.chip-close {
  background: rgba(255, 255, 255, 0.2);
  border: none;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  padding: 0;
  width: 18px;
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 1;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.chip-close:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: scale(1.1);
}
</style>
