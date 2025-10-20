Requerimientos para Sitio de Actos Públicos en Vue
1. Estructura General
1.1 Layout Principal

Header con logo "BA" y título "Acto Público"
Botón "Iniciar Sesión" en esquina superior derecha
Sidebar izquierdo con branding "mi BA" y mensaje "Vas a requerir de un usuario"
Área principal de contenido con título "Actos Públicos de la Ciudad"
Panel de filtros en lado derecho

1.2 Paleta de Colores

Amarillo: #FDB913 (principal, acentos)
Azul oscuro: #1F3A4F (sidebar, textos oscuros)
Azul claro: #00B4D8 (botones, tags)
Rojo: #F55555 (tags "INICIAL")
Gris claro: #F5F5F5 (fondos, tarjetas)

2. Componentes Principales
2.1 Tarjeta de Acto Público
Cada tarjeta debe mostrar:

Título principal (ej: "MAESTRO DE SECCION")
Tags: "INICIAL" (rojo) + "Interinatos y Suplencias" (azul)
Estado: badge amarillo con texto "Publicada"
Tipo de acto: ícono + texto (ej: "Interinatos y Suplencias")
Fecha de Acto Público: ícono + fecha y hora (ej: "lunes 20 de octubre de 2025 a las 10:30 hs.")
Link "Ver detalle": en color azul claro
Ícono expandible (+) en esquina superior izquierda

2.2 Grilla de Tarjetas

Mostrar exactamente 4 tarjetas por página
Layout responsivo en grid (2 columnas en desktop, 1 en mobile)
Espacio uniforme entre tarjetas
Fondo gris claro (#F5F5F5) para cada tarjeta

2.3 Panel de Filtros (Lado Derecho)
Estructura de filtros con:

Área: dropdown/selector con opción "Todos" (azul claro) y botón X para limpiar
Cargos: dropdown/selector con opción "Todos" y botón X
Asignatura: dropdown/selector con opción "Todos" y botón X
Especialidad: dropdown/selector con opción "Todos" y botón X
Escuela: dropdown/selector con opción "Todos" y botón X
Botón "Limpiar Filtros" arriba a la derecha (gris)
Ícono de búsqueda en cada filtro

3. Estructura de Datos (JSON)
3.1 Formato del JSON
