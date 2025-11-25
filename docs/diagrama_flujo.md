# Diagrama de Flujo — Proyecto NNN

Este documento describe el flujo completo del sistema desde la interacción del usuario hasta la generación de diagnósticos mediante RAG.

---

# 1. Diagrama de flujo (descripción textual)

[Inicio]
│
▼
[Login de usuario]
│ ¿Credenciales válidas?
├── No → [Error: Usuario o contraseña incorrectos] → [Fin]
▼ Sí
[Menú principal PWA]
│
▼
[Captura de síntomas]
│
▼
[Registrar búsqueda en BD]
│
▼
[Generar embedding de la consulta]
│
▼
[Búsqueda vectorial en Chroma/MySQL]
│
▼
[Recuperar chunks relevantes]
│
▼
[Enviar a LLM para análisis]
│
▼
[Obtener Diagnóstico NANDA]
│
▼
[Obtener Intervenciones NIC]
│
▼
[Obtener Resultados NOC]
│
▼
[Guardar resultados en BD]
│
▼
[Mostrar resultados en PWA]
│
▼
[¿Nueva búsqueda?]
├── Sí → Regresar a captura
└── No → [Fin]


---

# 2. Explicación paso a paso

### 1) Inicio
El usuario abre la PWA.

### 2) Login
Se valida usuario + contraseña desde la BD.

### 3) Captura de síntomas
El usuario escribe síntomas clínicos.

### 4) Registro de búsqueda
Se almacena para historial del usuario.

### 5) Embedding
Transformación de texto a vector numérico.

### 6) Vector Search
Se buscan fragmentos similares de NANDA/NIC/NOC.

### 7) LLM
Se genera el diagnóstico final.

### 8) Respuesta al usuario
Se muestra en la PWA.

---

#  Notas
- Este diagrama representa la versión completa del sistema cuando el módulo RAG esté terminado.
- El flujo actual llega hasta el registro de búsquedas; el análisis será agregado en la fase final del desarrollo.
