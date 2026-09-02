# 📊 ALUNA - Dashboard e Inventario de Contenidos

Este proyecto es una aplicación web de una sola página (SPA) diseñada para gestionar, registrar y visualizar las métricas de rendimiento de los contenidos (Artículos y Cuentos) de la plataforma ALUNA. 

Funciona de manera *Serverless* utilizando **Google Sheets como Base de Datos** a través de una API de Google Apps Script.

## 🌍 Entorno y Despliegue

Toda la infraestructura de este proyecto está administrada bajo la cuenta oficial de soporte: **`soporte@aluna.news`**.

* **Despliegue:** La aplicación web se encuentra alojada y desplegada a través de **Vercel**, garantizando actualizaciones continuas y alta disponibilidad.
* **Base de Datos:** El almacenamiento de datos funciona sobre Google Drive en la cuenta mencionada.
  * **Carpeta:** `informes aluna`
  * **Archivo:** `Base de Datos ALUNA` (Google Sheets)

## 🚀 Características Principales

* **Métricas Consolidadas:** Cálculo automático del total de artículos, cuentos, y alertas de bajo rendimiento (< 500 lecturas para artículos, < 100 para cuentos).
* **Gráficas Interactivas (Chart.js):**
  * Gráfica de anillo con la proporción de contenido.
  * Gráfica de barras con el histórico de lecturas anuales.
  * Ventana móvil de los **últimos 13 meses**, anclada al registro más reciente, con etiquetas de datos numéricos en pantalla.
* **Top Contenidos Automático:** Filtra y ordena de forma automática desde el inventario maestro los Artículos y Cuentos que superan las 1.000 lecturas.
* **Filtro Inteligente:** Normalización automática de textos al leer la base de datos (ignora mayúsculas, minúsculas, tildes y espacios accidentales).
* **Diseño Responsivo:** Interfaz construida con Tailwind CSS, optimizada para ordenadores y dispositivos móviles.

## 🛠️ Tecnologías Utilizadas

* **Frontend:** HTML5, Vanilla JavaScript.
* **Estilos:** Tailwind CSS (vía CDN).
* **Gráficos:** Chart.js (vía CDN).
* **Backend / Base de Datos:** Google Sheets + Google Apps Script (Fetch API).
* **Hosting:** Vercel.

---

## 🗄️ Estructura de la Base de Datos (Google Sheets)

Para que el programa sincronice correctamente, el archivo **`Base de Datos ALUNA`** conectado debe contener **exactamente** las siguientes 4 pestañas y encabezados (en la fila 1, en minúsculas y sin tildes):

### 1. Pestaña: `Inventario`
(Base de datos maestra de publicaciones)
* **A1:** `id`
* **B1:** `titulo`
* **C1:** `tipo` *(Se recomienda escribir "Articulo" o "Cuento")*
* **D1:** `visitas`

### 2. Pestaña: `Lecturas_Anuales`
(Histórico total por año)
* **A1:** `año`
* **B1:** `lecturas`

### 3. Pestaña: `Lecturas_Mensuales`
(Registro detallado para la ventana móvil de 13 meses)
* **A1:** `id`
* **B1:** `año`
* **C1:** `mes` *(0 = Enero, 11 = Diciembre)*
* **D1:** `articulos`
* **E1:** `cuentos`

### 4. Pestaña: `Metricas_Globales`
(Almacena el acumulado histórico de vistas generales del sitio)
* **A1:** `vistas_totales`

---

## ⚙️ Uso y Mantenimiento Local

1. **Clonar o descargar:** Guarda el archivo `index.html` en tu computadora.
2. **Configurar URL de la API:** Abre el archivo HTML y busca la constante `URL_GOOGLE_SHEETS` (alrededor de la línea 400). Asegúrate de que tenga el enlace web (`/exec`) generado por el despliegue de Google Apps Script asociado al archivo de Sheets.
   ```javascript
   const URL_GOOGLE_SHEETS = "[https://script.google.com/macros/s/TU_ID_AQUI/exec](https://script.google.com/macros/s/TU_ID_AQUI/exec)";
