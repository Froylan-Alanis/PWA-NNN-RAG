# Arquitectura del Sistema — Proyecto NNN (NANDA - NIC - NOC)

Este documento describe la arquitectura técnica del proyecto NNN basado en una PWA con backend Node.js y sistema RAG para diagnóstico NANDA/NIC/NOC.

---

# 1. Vista general

El sistema se divide en 3 capas:

Frontend (PWA)
Backend API REST (Node.js)
Motor RAG (Embeddings + Vector Search + LLM)
Base de Datos MySQL

---

# 2. Componentes principales

## 2.1 Frontend (PWA)
- Construido con: **HTML / CSS / JS / Vite**  
- Funciones:
  - Login
  - Captura de síntomas
  - Visualización de diagnósticos
  - Historial de búsquedas
  - Interfaz responsiva para uso móvil

---

## 2.2 Backend (Node.js + Express)
- Provee todos los endpoints REST
- Maneja:
  - Usuarios (login, creación)
  - Búsquedas
  - Historial
  - Comunicación con el motor RAG
- Acceso a MySQL mediante **mysql2**

---

## 2.3 Motor RAG (Pipeline Inteligente)

Incluye:

1. **Limpieza de datos**  
   .txt generados desde PDF con PyPDF2

2. **Chunking**  
   Divisiones de 1200 caracteres con overlap de 200.

3. **Embeddings locales**  
   Modelo: **all-MiniLM-L6-v2** vía `@xenova/transformers`.

4. **Vector Search**  
   Opciones:
   - ChromaDB (servidor via Docker)
   - Alternativa local: similitud coseno + MySQL

5. **LLM**  
   - OpenAI GPT-4.1 / GPT-4o mini  
   - O modelo local según configuración

---

## 2.4 Base de Datos (MySQL)
- Contiene:
  - usuarios
  - roles
  - estatus_usuarios
  - busquedas
  - resultados (futuro)
- Optimizada con índices en:
  - username  
  - id_usuario  
  - id_busqueda  

---

#  3. Arquitectura lógica del flujo

PWA → Backend API → RAG Engine → Vector Search → LLM → Backend API → PWA

Paso a paso:

1. Usuario ingresa síntomas  
2. Backend guarda búsqueda  
3. Backend genera embeddings  
4. Motor vectorial encuentra chunks relevantes  
5. LLM genera diagnóstico NANDA + NIC + NOC  
6. Respuesta enviada al usuario  
7. Se guarda histórico

---

# 4. Arquitectura de despliegue

## Entorno local
- Backend → `localhost:3000`
- Frontend → `localhost:5173`
- MySQL → XAMPP (`localhost:3306`)
- Servidor vectorial (si se usa Chroma) → `localhost:8000`

## Producción (opcional)
- Backend → Render / Railway
- Frontend → Vercel
- MySQL → PlanetScale / Neon
- LLM → OpenAI
- Vector DB → Chroma Cloud

---

# Notas
- Arquitectura modular: cada capa puede evolucionar por separado.  
- El RAG es completamente sustituible sin afectar el frontend.
