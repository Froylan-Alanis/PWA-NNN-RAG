# Proyecto NNN – PWA con RAG (NANDA, NIC, NOC)

Sistema clínico inteligente para el apoyo al diagnóstico e intervención de enfermería basado en los libros NANDA, NIC y NOC.  
Desarrollado como **PWA + Backend Node.js** y potenciado con un motor **RAG (Retrieval Augmented Generation)**.

---

# Índice
- [Descripción general](#descripción-general)
- [Objetivo del sistema](#objetivo-del-sistema)
- [Arquitectura](#arquitectura)
- [Tecnologías utilizadas](#tecnologías-utilizadas)
- [Requisitos previos](#requisitos-previos)
- [Instalación del proyecto](#instalación-del-proyecto)
- [Estructura de carpetas](#estructura-de-carpetas)
- [Uso del backend](#uso-del-backend)
- [Documentación de API](#documentación-de-api)
- [Pipeline completo del proyecto](#pipeline-completo-del-proyecto)
- [Base de datos](#base-de-datos)
- [Estado del desarrollo](#estado-del-desarrollo)
- [Créditos](#créditos)

---

# 🔍 Descripción general

El proyecto **NNN (NANDA - NIC - NOC)** es una herramienta digital orientada a personal de salud, especialmente enfermería, que permite:

- Registrar síntomas
- Buscar diagnósticos NANDA relacionados
- Sugerir intervenciones NIC
- Proponer resultados esperados NOC
- Consultar historial de búsquedas

Todo mediante un motor RAG que utiliza embeddings vectoriales y modelos de lenguaje avanzados.

---

# Objetivo del sistema

El propósito del sistema es mejorar la eficiencia clínica del personal de enfermería mediante:

- **Busqueda inteligente** basada en síntomas
- **Diagnóstico asistido**
- **Intervenciones sugeridas**
- **Resultados esperados**
- **Historial clínico del usuario**

---

# Arquitectura

Arquitectura dividida en 4 capas principales:
Frontend (PWA)
Backend (Node.js + Express)
Motor RAG (Embeddings + Vector Search + LLM)
Base de Datos (MySQL)



