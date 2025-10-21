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
  background: linear-gradient(135deg, #ffffff 0%, #f8fdfb 100%);
  border-radius: 12px;
  padding: 20px;
  position: relative;
  transition: all 0.3s ease;
  border: 2px solid #e0f2ea;
  box-shadow: 0 2px 8px rgba(86, 197, 150, 0.1);
}

.acto-card:hover {
  box-shadow: 0 8px 24px rgba(86, 197, 150, 0.2);
  transform: translateY(-4px);
  border-color: #56c596;
}

.card-header {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  margin-bottom: 12px;
}

.expand-btn {
  background: linear-gradient(135deg, #a8e6cf 0%, #56c596 100%);
  border: none;
  border-radius: 8px;
  width: 28px;
  height: 28px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  font-size: 18px;
  line-height: 1;
  color: #fff;
  padding: 0;
  transition: all 0.3s ease;
  box-shadow: 0 2px 6px rgba(86, 197, 150, 0.2);
}

.expand-btn:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 12px rgba(86, 197, 150, 0.3);
}

.card-title {
  margin: 0;
  font-size: 18px;
  font-weight: 700;
  color: #1a4d2e;
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
  background: linear-gradient(135deg, #56c596 0%, #3aa676 100%);
  box-shadow: 0 2px 6px rgba(86, 197, 150, 0.2);
}

.tag-nivel.tag-inicial {
  background: linear-gradient(135deg, #f093a6 0%, #e75874 100%);
  box-shadow: 0 2px 6px rgba(231, 88, 116, 0.2);
}

.tag-nivel.tag-primaria {
  background: linear-gradient(135deg, #6ba5d6 0%, #4a89c7 100%);
  box-shadow: 0 2px 6px rgba(74, 137, 199, 0.2);
}

.tag-nivel.tag-otros {
  background: linear-gradient(135deg, #7c8b9a 0%, #5d6d7e 100%);
  box-shadow: 0 2px 6px rgba(93, 109, 126, 0.2);
}

.tag-tipo {
  background: linear-gradient(135deg, #a8e6cf 0%, #56c596 100%);
  box-shadow: 0 2px 6px rgba(86, 197, 150, 0.2);
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
  background: linear-gradient(135deg, #ffd89b 0%, #ffb74d 100%);
  color: #1a4d2e;
  padding: 6px 14px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 700;
  box-shadow: 0 2px 6px rgba(255, 183, 77, 0.3);
}

.icon {
  font-size: 16px;
}

.info-text {
  font-size: 14px;
  color: #1a4d2e;
}

.card-details {
  background: linear-gradient(135deg, #f0f9f4 0%, #e8f5ed 100%);
  border-radius: 10px;
  padding: 16px;
  margin-bottom: 16px;
  border: 1px solid #d4ebe0;
}

.detail-row {
  margin-bottom: 8px;
  font-size: 14px;
  color: #1a4d2e;
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
  color: #3aa676;
  text-decoration: none;
  font-weight: 600;
  font-size: 14px;
  transition: all 0.3s ease;
}

.link-detail:hover {
  color: #2d7a5b;
  text-decoration: underline;
}
</style>
