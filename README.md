# Actos Públicos PLUS

Sistema de visualización de Actos Públicos de la Ciudad de Buenos Aires desarrollado con Vue 3 + Vite.

## 📋 Descripción

Esta aplicación web permite visualizar y filtrar los actos públicos disponibles en la Ciudad de Buenos Aires. Los usuarios pueden buscar por diferentes criterios como área, cargo, asignatura, especialidad y escuela.

## ✨ Características

- 📊 **Visualización de Actos Públicos**: Tarjetas con información detallada de cada acto
  - **Información visible**: estado, tipo de acto, fecha, escuela, distrito y turno
  - **Información expandible**: horario detallado, causa y ID POF
- 🔍 **Sistema de Filtros Dinámicos**: Los filtros se generan automáticamente desde los datos del JSON
  - Filtro por Área/Nivel (INICIAL, PRIMARIA, MEDIA, TECNICA, ARTISTICA, ESPECIAL, etc.)
  - Filtro por Cargo (todos los cargos disponibles en los datos)
  - Filtro por Especialidad (todas las especialidades disponibles)
  - Filtro por Escuela (lista desplegable con todas las escuelas/establecimientos disponibles)
  - Filtro por Turno (MAÑANA, TARDE, NOCHE, VESPERTINO, etc.)
  - Filtro por Distrito (todos los distritos escolares disponibles)
  - Filtro por Causa (todas las causas de vacante disponibles)
- 📄 **Paginación**: Muestra 4 actos por página para mejor navegación
- 📱 **Diseño Responsivo**: Adaptable a diferentes tamaños de pantalla
- 🎨 **Paleta de Colores Oficial**: Siguiendo los colores de la Ciudad de Buenos Aires
- ⚡ **Detalles Expandibles**: Cada tarjeta puede expandirse para ver más información adicional
- 🔔 **Banner Informativo Modal**: Aviso importante que se muestra al iniciar la aplicación con información sobre la fuente de datos y su actualización
- 🔄 **Carga Automática de Datos**: Detecta y usa automáticamente el archivo JSON más reciente disponible
- ⚠️ **Manejo de Errores**: Banner de error informativo si no se encuentran archivos de datos

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

3. **Importante**: Asegúrate de tener al menos un archivo JSON con datos de actos públicos en la raíz del proyecto. El archivo debe seguir el formato:
   - `actos_publicos_YYYYMMDD_HHMMSS.json`
   - Ejemplo: `actos_publicos_20251021_185353.json`

4. Inicia el servidor de desarrollo:
```bash
npm run dev
```

5. Abre tu navegador en `http://localhost:5173` (o el puerto que indique Vite)

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
│   │   ├── InfoBanner.vue         # Banner informativo modal
│   │   └── ErrorBanner.vue        # Banner de error
│   ├── App.vue                     # Componente principal
│   ├── main.js                     # Punto de entrada
│   └── style.css                   # Estilos globales
├── actos_publicos_*.json           # Archivos de datos (ignorados por git)
├── .gitignore                      # Archivos ignorados por git
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
- Tipo de acto
- Fecha del acto público
- **Escuela (establecimiento)** - visible sin expandir
- **Distrito** - visible sin expandir
- **Turno** - visible sin expandir
- Botón expandible para ver detalles adicionales (horario, causa, ID POF)
- Link al acto público original

### FilterPanel.vue
Panel de filtros dinámicos que incluye:
- **Filtro por Área/Nivel**: Se genera automáticamente con todos los niveles presentes en el JSON (INICIAL, PRIMARIA, MEDIA, TECNICA, ARTISTICA, ESPECIAL, etc.)
- **Filtro por Cargo**: Lista desplegable con todos los cargos únicos encontrados en los datos
- **Filtro por Especialidad**: Lista desplegable con todas las especialidades únicas del JSON
- **Filtro por Escuela**: Lista desplegable con todos los establecimientos/escuelas únicos del JSON
- **Filtro por Turno**: Lista desplegable con todos los turnos únicos del JSON (MAÑANA, TARDE, NOCHE, VESPERTINO, etc.)
- **Filtro por Distrito**: Lista desplegable con todos los distritos escolares únicos del JSON
- **Filtro por Causa**: Lista desplegable con todas las causas de vacante únicas del JSON
- Botón para limpiar todos los filtros
- Los filtros se adaptan automáticamente a los datos cargados, sin necesidad de configuración manual
- Todos los filtros muestran chips visuales cuando están activos

### InfoBanner.vue
Banner informativo modal que:
- Se muestra al iniciar la aplicación bloqueando el contenido
- Informa sobre la fecha y hora de extracción de los datos
- Incluye disclaimers legales sobre el uso de la información
- Proporciona enlace al sistema oficial de actos públicos
- Requiere que el usuario acepte antes de continuar
- Diseño modal con overlay y animaciones

### ErrorBanner.vue
Banner de error que:
- Se muestra cuando no se encuentran archivos JSON de datos
- Diseño en rojo con animación de advertencia
- Proporciona instrucciones sobre el formato de archivo esperado
- Bloquea la interfaz hasta que se solucione el problema
- Muestra mensaje de error técnico detallado

## 📊 Formato de Datos

### Carga Automática de Archivos JSON

La aplicación utiliza un sistema de carga automática que:
- Detecta todos los archivos JSON que coincidan con el patrón `actos_publicos_*.json` en la raíz del proyecto
- Ordena los archivos por timestamp (fecha y hora en el nombre del archivo)
- **Carga automáticamente el archivo más reciente** sin necesidad de modificar el código
- Muestra un banner de error si no encuentra ningún archivo

### Nomenclatura de Archivos

Los archivos JSON deben seguir este formato de nombre:
- **Patrón**: `actos_publicos_YYYYMMDD_HHMMSS.json`
- **Ejemplo**: `actos_publicos_20251021_185353.json`
  - `20251021` = 21 de octubre de 2025
  - `185353` = 18:53:53

### Estructura del JSON

Los datos deben tener la siguiente estructura:

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
      "titulo": "string",               // Nombre del cargo - usado para filtro de Cargos
      "nivel": "string",                // Nivel educativo - usado para filtro de Área
      "tipo": "string",
      "especialidad_tag": "string",     // Especialidad - usado para filtro de Especialidad
      "estado": "string",
      "fecha": "string",
      "link": "URL",
      "establecimiento": "string",      // Nombre de la escuela - mostrado como "Escuela" en el front, usado para filtro de Escuela
      "distrito": "string",             // Distrito escolar - visible en la tarjeta
      "turno": "string",                // Turno (MAÑANA, TARDE, etc.) - visible en la tarjeta
      "horario": "string",              // Horario detallado - solo visible al expandir
      "causa": "string",
      "id_pof": "string"
    }
  ]
}
```

**Nota importante sobre los filtros**: La aplicación extrae automáticamente todos los valores únicos de los campos `nivel`, `titulo`, `especialidad_tag`, `establecimiento`, `turno`, `distrito` y `causa` para generar las opciones de los filtros. Esto significa que:
- No necesitas configurar manualmente los valores de los filtros
- Los filtros siempre mostrarán exactamente las opciones disponibles en tus datos
- Si agregas nuevos niveles, cargos, especialidades, escuelas, turnos, distritos o causas en el JSON, aparecerán automáticamente en los filtros
- Todos los filtros son listas desplegables, lo que facilita la selección exacta de la opción deseada
- Los filtros se pueden combinar para búsquedas más específicas (ej: PRIMARIA + MAÑANA + Distrito 4)

## 🔧 Actualización de Datos

### Para agregar nuevos actos públicos:

1. Crea un nuevo archivo JSON en la raíz del proyecto siguiendo el formato de nombre: `actos_publicos_YYYYMMDD_HHMMSS.json`
2. Asegúrate de que el contenido siga la estructura especificada en la sección "Formato de Datos"
3. La aplicación detectará automáticamente el archivo más reciente y lo usará
4. No es necesario modificar ningún código fuente

### Gestión de Archivos

- Los archivos JSON están incluidos en `.gitignore` para evitar subir datos sensibles al repositorio
- Puedes mantener múltiples archivos JSON para histórico
- La aplicación siempre usará el más reciente basándose en el timestamp del nombre

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
5. No incluyas archivos JSON de datos en tus commits (están en `.gitignore`)

## ⚠️ Solución de Problemas

### "Error al Obtener la Información"
Si ves este banner de error al iniciar la aplicación:
- Verifica que existe al menos un archivo JSON en la raíz del proyecto
- Asegúrate de que el nombre del archivo siga el formato: `actos_publicos_YYYYMMDD_HHMMSS.json`
- Verifica que el archivo JSON tenga la estructura correcta y sea válido
- Revisa la consola del navegador para más detalles del error

## 📧 Contacto

Para más información sobre los Actos Públicos de la Ciudad de Buenos Aires, visita: https://actopublico.bue.edu.ar/

