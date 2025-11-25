# Pipeline del Proyecto NNN (NANDA - NIC - NOC)

Este pipeline describe todos los pasos del sistema, desde la ingestión de datos hasta la entrega de resultados procesados en el frontend PWA.

---

##  1. Ingesta de Datos (ETL)

### 1.1. Entrada
- Archivos PDF:  
  - NANDA 2021–2023  
  - NIC  
  - NOC  

### 1.2. Extracción
- Extracción de texto usando **PyPDF2**
- Generación de archivos `.txt` por libro:
  - `backend/data/nanda.txt`
  - `backend/data/nic.txt`
  - `backend/data/noc.txt`

### 1.3. Limpieza de texto
- Eliminación de:
  - Saltos de línea
  - Espacios dobles
  - Encabezados y pies repetidos
  - Números de página
  - Símbolos no válidos

---

##  2. Procesamiento (Pre-RAG)

### 2.1. Chunking
- División de cada libro en fragmentos:
  - Tamaño: 1200 caracteres  
  - Overlap: 200 caracteres  
- Fragmentos listos para embeddings.

---

## 🟦 3. Embeddings y almacenamiento

### 3.1. Embeddings
- Modelo local: **MiniLM-L6-v2** mediante `@xenova/transformers`
- Embeddings generados para cada chunk

### 3.2. Almacenamiento
- Los embeddings se guardarán en:
  - **ChromaDB** *(cuando reanudemos desarrollo)*
  - O alternativa sin Chroma: Base de datos MySQL + similitud coseno

---

##  4. Backend API (RAG)

### Flujo:

1. Usuario envía síntomas → `/api/busquedas`
2. Backend genera embedding de la consulta
3. Se realiza **búsqueda vectorial** (Chroma o MySQL)
4. Se recuperan los chunks relevantes
5. Se envían al modelo LLM
6. El modelo genera diagnóstico clínico (NANDA, NIC, NOC)
7. Se guardan resultados en la base de datos
8. Se devuelve la respuesta al frontend

---

##  5. Frontend PWA

### Funcionalidades:
- Login
- Búsqueda por síntomas
- Visualización de diagnósticos
- Historial de búsquedas

---

##  6. Despliegue

### En desarrollo:
- `localhost:3000` → backend  
- `localhost:5173` → frontend  
- Accesible desde celular por IP local

### En producción (opcional):
- Vercel / Netlify → PWA
- Railway / Render → Backend Node
- Neon / PlanetScale → MySQL
