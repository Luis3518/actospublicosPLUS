# Actos Públicos PLUS

Sistema de visualización de Actos Públicos de la Ciudad de Buenos Aires desarrollado con Vue 3 + Vite.

## 📋 Descripción

Esta aplicación web permite visualizar y filtrar los actos públicos disponibles en la Ciudad de Buenos Aires. Los usuarios pueden buscar por diferentes criterios como área, cargo, asignatura, especialidad y escuela.

## ✨ Características

- 📊 **Visualización de Actos Públicos**: Tarjetas con información detallada de cada acto
- 🔍 **Sistema de Filtros**: Filtro por área, cargo, asignatura, especialidad y escuela
- 📄 **Paginación**: Muestra 4 actos por página para mejor navegación
- 📱 **Diseño Responsivo**: Adaptable a diferentes tamaños de pantalla
- 🎨 **Paleta de Colores Oficial**: Siguiendo los colores de la Ciudad de Buenos Aires
- ⚡ **Detalles Expandibles**: Cada tarjeta puede expandirse para ver más información
- 🔔 **Banner Informativo Modal**: Aviso importante que se muestra al iniciar la aplicación con información sobre la fuente de datos y su actualización

## 🎨 Paleta de Colores

- **Amarillo Principal**: #FDB913
- **Azul Oscuro**: #1F3A4F
- **Azul Claro**: #00B4D8
- **Rojo (Inicial)**: #F55555
- **Gris Claro**: #F5F5F5

## 🚀 Instalación

### Prerequisitos

- Node.js (versión 16 o superior)
- npm o yarn

### Pasos de Instalación

1. Clona o descarga este repositorio

2. Instala las dependencias:
```bash
npm install
```

3. Inicia el servidor de desarrollo:
```bash
npm run dev
```

4. Abre tu navegador en `http://localhost:3000`

## 📦 Scripts Disponibles

- `npm run dev` - Inicia el servidor de desarrollo
- `npm run build` - Genera la versión de producción
- `npm run preview` - Previsualiza la versión de producción

## 📁 Estructura del Proyecto

```
actospublicosPLUS/
├── src/
│   ├── components/
│   │   ├── ActoPublicoCard.vue    # Componente de tarjeta individual
│   │   ├── FilterPanel.vue        # Panel de filtros
│   │   └── InfoBanner.vue         # Banner informativo modal
│   ├── App.vue                     # Componente principal
│   ├── main.js                     # Punto de entrada
│   └── style.css                   # Estilos globales
├── actos_publicos_todos_20251020_115648.json  # Datos de ejemplo
├── index.html                      # HTML principal
├── package.json                    # Dependencias del proyecto
├── vite.config.js                  # Configuración de Vite
├── requerimientos.md               # Documentación de requerimientos
└── README.md                       # Este archivo
```

## 🧩 Componentes Principales

### App.vue
Componente principal que gestiona:
- Layout general (header, sidebar, contenido, filtros)
- Estado de filtros
- Paginación
- Lógica de filtrado

### ActoPublicoCard.vue
Tarjeta individual que muestra:
- Título del cargo
- Tags de nivel y tipo
- Badge de estado
- Fecha del acto público
- Botón expandible para ver detalles adicionales
- Link al acto público original

### FilterPanel.vue
Panel de filtros que incluye:
- Filtro por Área (INICIAL, PRIMARIA, PROGRAMAS SOCIOEDUCATIVOS)
- Filtro por Cargo
- Filtro por Asignatura
- Filtro por Especialidad
- Búsqueda por Escuela
- Botón para limpiar todos los filtros

### InfoBanner.vue
Banner informativo modal que:
- Se muestra al iniciar la aplicación bloqueando el contenido
- Informa sobre la fecha y hora de extracción de los datos
- Incluye disclaimers legales sobre el uso de la información
- Proporciona enlace al sistema oficial de actos públicos
- Requiere que el usuario acepte antes de continuar
- Diseño modal con overlay y animaciones

## 📊 Formato de Datos

Los datos se cargan desde el archivo JSON `actos_publicos_todos_20251020_115648.json` con la siguiente estructura:

```json
{
  "metadata": {
    "fecha_extraccion": "fecha",
    "nivel": "nivel",
    "total_registros": número,
    "total_paginas": número,
    "fuente": "URL"
  },
  "actos_publicos": [
    {
      "titulo": "string",
      "nivel": "string",
      "tipo": "string",
      "estado": "string",
      "fecha": "string",
      "link": "URL",
      "establecimiento": "string",
      "distrito": "string",
      "turno": "string",
      "horario": "string",
      "causa": "string",
      "id_pof": "string"
    }
  ]
}
```

## 🔧 Personalización

Para agregar nuevos actos públicos, simplemente actualiza el archivo JSON `actos_publicos_todos_20251020_115648.json` con el formato especificado.

## 🛠️ Tecnologías Utilizadas

- **Vue 3** - Framework JavaScript progresivo
- **Vite** - Herramienta de construcción rápida
- **Composition API** - API moderna de Vue 3
- **CSS3** - Estilos con diseño responsivo

## 📱 Responsive Design

La aplicación se adapta a diferentes tamaños de pantalla:

- **Desktop (>1200px)**: Vista completa con sidebar, contenido y panel de filtros
- **Tablet (900-1200px)**: Sin sidebar, contenido y filtros
- **Mobile (<900px)**: Vista de una sola columna con filtros abajo

## 📝 Licencia

Este proyecto fue desarrollado para la visualización de Actos Públicos de la Ciudad de Buenos Aires.

## 👥 Contribuciones

Para contribuir al proyecto:
1. Revisa los requerimientos en `requerimientos.md`
2. Asegúrate de seguir la paleta de colores oficial
3. Mantén la estructura de componentes organizada
4. Prueba en diferentes tamaños de pantalla

## 📧 Contacto

Para más información sobre los Actos Públicos de la Ciudad de Buenos Aires, visita: https://actopublico.bue.edu.ar/

