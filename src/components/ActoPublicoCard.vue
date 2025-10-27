<template>
  <div class="acto-card">
    <div class="card-header">
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
        <span class="icon">📋</span>
        <span class="info-text">{{ acto.tipo_acto }}</span>
      </div>

      <div class="info-item">
        <span class="icon">📅</span>
        <span class="info-text">{{ acto.fecha }}</span>
      </div>

      <div v-if="acto.establecimiento" class="info-item">
        <span class="icon">🏫</span>
        <span class="info-text"><strong>Escuela:</strong> {{ acto.establecimiento }}</span>
      </div>

      <div v-if="acto.distrito" class="info-item">
        <span class="icon">📍</span>
        <span class="info-text"><strong>Distrito:</strong> {{ acto.distrito }}</span>
      </div>

      <div v-if="acto.turno" class="info-item">
        <span class="icon">🕐</span>
        <span class="info-text"><strong>Turno:</strong> {{ acto.turno }}</span>
      </div>

      <div v-if="acto.horario" class="info-item">
        <span class="icon">⏰</span>
        <span class="info-text"><strong>Horario:</strong> {{ acto.horario }}</span>
      </div>

      <div v-if="acto.causa" class="info-item">
        <span class="icon">📝</span>
        <span class="info-text"><strong>Causa:</strong> {{ acto.causa }}</span>
      </div>

      <div v-if="acto.id_pof" class="info-item">
        <span class="icon">🆔</span>
        <span class="info-text"><strong>ID POF:</strong> {{ acto.id_pof }}</span>
      </div>
    </div>

    <div class="card-footer">
      <a :href="acto.link" target="_blank" class="link-detail">
        Postular →
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ActoPublicoCard',
  props: {
    acto: {
      type: Object,
      required: true
    }
  },
  setup() {
    const getNivelClass = (nivel) => {
      return {
        'tag-inicial': nivel === 'INICIAL',
        'tag-primaria': nivel === 'PRIMARIA',
        'tag-otros': nivel !== 'INICIAL' && nivel !== 'PRIMARIA'
      }
    }

    return {
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
  margin-bottom: 12px;
}

.card-title {
  margin: 0;
  font-size: 18px;
  font-weight: 700;
  color: #1a4d2e;
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

.icon {
  font-size: 16px;
}

.info-text {
  font-size: 14px;
  color: #1a4d2e;
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
