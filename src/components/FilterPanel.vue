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
            <option value="INICIAL">INICIAL</option>
            <option value="PRIMARIA">PRIMARIA</option>
            <option value="PROGRAMAS SOCIOEDUCATIVOS">PROGRAMAS SOCIOEDUCATIVOS</option>
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
            <option value="MAESTRO DE SECCION">MAESTRO DE SECCION</option>
            <option value="DIRECTOR DE EDUCACIÓN PRIMARIA">DIRECTOR DE EDUCACIÓN PRIMARIA</option>
            <option value="SUPERVISOR ADJUNTO DE INICIAL">SUPERVISOR ADJUNTO DE INICIAL</option>
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

      <!-- Asignatura Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Asignatura
        </label>
        <div class="filter-input-wrapper">
          <select 
            class="filter-select"
            :value="filters.asignatura"
            @change="handleChange('asignatura', $event.target.value)"
          >
            <option value="">Todos</option>
          </select>
          <button 
            v-if="filters.asignatura" 
            class="btn-clear-filter"
            @click="clearFilter('asignatura')"
          >
            ×
          </button>
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
          </select>
          <button 
            v-if="filters.especialidad" 
            class="btn-clear-filter"
            @click="clearFilter('especialidad')"
          >
            ×
          </button>
        </div>
      </div>

      <!-- Escuela Filter -->
      <div class="filter-group">
        <label class="filter-label">
          <span class="icon-search">🔍</span>
          Escuela
        </label>
        <div class="filter-input-wrapper">
          <input 
            type="text"
            class="filter-input"
            placeholder="Buscar escuela..."
            :value="filters.escuela"
            @input="handleChange('escuela', $event.target.value)"
          >
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
  background: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.filter-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.filter-title {
  margin: 0;
  font-size: 18px;
  font-weight: 700;
  color: #1F3A4F;
}

.btn-clear-all {
  background: #e0e0e0;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  font-size: 12px;
  font-weight: 500;
  color: #666;
  cursor: pointer;
  transition: background 0.2s;
}

.btn-clear-all:hover {
  background: #d0d0d0;
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
  color: #1F3A4F;
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
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  color: #1F3A4F;
  background: #fff;
  cursor: pointer;
}

.filter-input {
  cursor: text;
}

.filter-select:focus,
.filter-input:focus {
  outline: none;
  border-color: #00B4D8;
}

.btn-clear-filter {
  position: absolute;
  right: 8px;
  background: none;
  border: none;
  font-size: 20px;
  color: #999;
  cursor: pointer;
  padding: 0;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 1;
}

.btn-clear-filter:hover {
  color: #666;
}

.filter-chip {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: #00B4D8;
  color: #fff;
  padding: 6px 12px;
  border-radius: 16px;
  font-size: 12px;
  font-weight: 500;
  max-width: fit-content;
}

.chip-close {
  background: none;
  border: none;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  padding: 0;
  width: 16px;
  height: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 1;
}

.chip-close:hover {
  opacity: 0.8;
}
</style>
