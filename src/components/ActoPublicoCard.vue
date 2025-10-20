<template>
  <div class="acto-card">
    <div class="card-header">
      <button class="expand-btn" @click="toggleExpanded">
        {{ isExpanded ? '−' : '+' }}
      </button>
      <h3 class="card-title">{{ acto.titulo }}</h3>
    </div>

    <div class="card-tags">
      <span class="tag tag-nivel" :class="getNivelClass(acto.nivel)">
        {{ acto.nivel }}
      </span>
      <span class="tag tag-tipo">{{ acto.tipo }}</span>
    </div>

    <div class="card-info">
      <div class="info-item">
        <span class="badge-estado">{{ acto.estado }}</span>
      </div>

      <div class="info-item">
        <span class="icon">📋</span>
        <span class="info-text">{{ acto.tipo_acto }}</span>
      </div>

      <div class="info-item">
        <span class="icon">📅</span>
        <span class="info-text">{{ acto.fecha }}</span>
      </div>
    </div>

    <div v-if="isExpanded" class="card-details">
      <div v-if="acto.establecimiento" class="detail-row">
        <strong>Establecimiento:</strong> {{ acto.establecimiento }}
      </div>
      <div v-if="acto.distrito" class="detail-row">
        <strong>Distrito:</strong> {{ acto.distrito }}
      </div>
      <div v-if="acto.turno" class="detail-row">
        <strong>Turno:</strong> {{ acto.turno }}
      </div>
      <div v-if="acto.horario" class="detail-row">
        <strong>Horario:</strong> {{ acto.horario }}
      </div>
      <div v-if="acto.causa" class="detail-row">
        <strong>Causa:</strong> {{ acto.causa }}
      </div>
      <div v-if="acto.id_pof" class="detail-row">
        <strong>ID POF:</strong> {{ acto.id_pof }}
      </div>
    </div>

    <div class="card-footer">
      <a :href="acto.link" target="_blank" class="link-detail">
        Ver detalle →
      </a>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'ActoPublicoCard',
  props: {
    acto: {
      type: Object,
      required: true
    }
  },
  setup() {
    const isExpanded = ref(false)

    const toggleExpanded = () => {
      isExpanded.value = !isExpanded.value
    }

    const getNivelClass = (nivel) => {
      return {
        'tag-inicial': nivel === 'INICIAL',
        'tag-primaria': nivel === 'PRIMARIA',
        'tag-otros': nivel !== 'INICIAL' && nivel !== 'PRIMARIA'
      }
    }

    return {
      isExpanded,
      toggleExpanded,
      getNivelClass
    }
  }
}
</script>

<style scoped>
.acto-card {
  background: #F5F5F5;
  border-radius: 8px;
  padding: 20px;
  position: relative;
  transition: box-shadow 0.3s ease;
}

.acto-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.card-header {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  margin-bottom: 12px;
}

.expand-btn {
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  font-size: 18px;
  line-height: 1;
  color: #1F3A4F;
  padding: 0;
}

.expand-btn:hover {
  background: #FDB913;
  border-color: #FDB913;
  color: #fff;
}

.card-title {
  margin: 0;
  font-size: 18px;
  font-weight: 700;
  color: #1F3A4F;
  flex: 1;
}

.card-tags {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.tag {
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 500;
  color: #fff;
}

.tag-nivel {
  background: #00B4D8;
}

.tag-nivel.tag-inicial {
  background: #F55555;
}

.tag-nivel.tag-primaria {
  background: #00B4D8;
}

.tag-nivel.tag-otros {
  background: #1F3A4F;
}

.tag-tipo {
  background: #00B4D8;
}

.card-info {
  margin-bottom: 16px;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 8px;
}

.badge-estado {
  background: #FDB913;
  color: #1F3A4F;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 600;
}

.icon {
  font-size: 16px;
}

.info-text {
  font-size: 14px;
  color: #1F3A4F;
}

.card-details {
  background: #fff;
  border-radius: 6px;
  padding: 16px;
  margin-bottom: 16px;
}

.detail-row {
  margin-bottom: 8px;
  font-size: 14px;
  color: #1F3A4F;
}

.detail-row:last-child {
  margin-bottom: 0;
}

.detail-row strong {
  font-weight: 600;
  margin-right: 8px;
}

.card-footer {
  display: flex;
  justify-content: flex-end;
}

.link-detail {
  color: #00B4D8;
  text-decoration: none;
  font-weight: 500;
  font-size: 14px;
}

.link-detail:hover {
  text-decoration: underline;
}
</style>
