#  Documentación de Endpoints — Proyecto NNN (NANDA, NIC, NOC)
API REST desarrollada en **Node.js + Express**, conectada a **MySQL** y con módulos de **RAG** (pendientes de activación).

Versión del documento: **v1.0**  
Estado de desarrollo: **Backend básico completado – RAG en progreso**

---

# 📁 **Índice**
- [1. Autenticación](#1-autenticación)
- [2. Usuarios](#2-usuarios)
- [3. Búsquedas (Historial)](#3-búsquedas-historial)
- [4. Resultados](#4-resultados)
- [5. RAG (Pendiente de activación)](#5-rag-proceso-completo)
- [6. Errores comunes](#6-errores-comunes)

---

---

# 🟦 **1. Autenticación**

## ▶ POST `/api/login`
Inicia sesión verificando `username` y `password`.

### 📨 Body (JSON)
```json
{
  "username": "froylan",
  "password": "123456"
}
