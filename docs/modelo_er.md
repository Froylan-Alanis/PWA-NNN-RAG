# Modelo Entidad–Relación — Proyecto NNN (NANDA - NIC - NOC)

Este documento describe el Modelo Entidad–Relación (MER) de la base de datos utilizada en el proyecto NNN, el cual gestiona usuarios, búsquedas, roles, estatus y resultados generados por el sistema RAG.

---

#  1. Entidades principales

## 1.1. Usuarios
Representa al personal de salud que utiliza la plataforma.

| Campo | Tipo | Descripción |
|--------|------|-------------|
| id_usuario (PK) | INT | Identificador único |
| id_rol (FK) | INT | Rol asignado al usuario |
| id_estatus (FK) | INT | Activo/Inactivo |
| nombres | VARCHAR(100) | Nombre(s) |
| apellido_paterno | VARCHAR(100) | Apellido paterno |
| apellido_materno | VARCHAR(100) | Apellido materno |
| username | VARCHAR(50) | Nombre de usuario |
| password_hash | VARCHAR(255) | Contraseña encriptada |
| fecha_creado | DATETIME | Fecha de alta |

---

## 1.2. Roles
Define si un usuario es administrador o enfermera.

| Campo | Tipo |
|--------|------|
| id_rol (PK) | INT |
| nombre | VARCHAR(50) |
| descripcion | VARCHAR(200) |

---

## 1.3. Estatus de usuarios
Indica si el usuario puede iniciar sesión.

| Campo | Tipo |
|--------|------|
| id_estatus (PK) | INT |
| nombre | VARCHAR(50) |
| descripcion | VARCHAR(200) |

---

## 1.4. Búsquedas
Guarda las consultas realizadas por usuarios (síntomas ingresados).

| Campo | Tipo |
|--------|------|
| id_busqueda (PK) | INT |
| id_usuario (FK) | INT |
| sintomas_texto | TEXT |
| fecha_busqueda | DATETIME |
| cantidad_resultados | INT (null) |

---

## 1.5. Resultados (RAG)
Registra lo que el sistema devuelve tras analizar una búsqueda.

| Campo | Tipo |
|--------|------|
| id_resultado (PK) | INT |
| id_busqueda (FK) | INT |
| fuente | VARCHAR(20) (NANDA/NIC/NOC) |
| codigo | VARCHAR(20) |
| titulo | VARCHAR(300) |
| descripcion | TEXT |
| score_vectorial | DECIMAL |
| fecha_generado | DATETIME |

---

#  2. Relaciones

- **Usuarios — Roles**  
  - (N:1) Un usuario pertenece a un rol.  
  - Un rol puede tener varios usuarios.

- **Usuarios — Estatus**  
  - (N:1) Un usuario tiene un estatus.

- **Usuarios — Búsquedas**  
  - (1:N) Un usuario puede hacer muchas búsquedas.

- **Búsquedas — Resultados**  
  - (1:N) Una búsqueda puede tener múltiples resultados del RAG.

---

# 🟦 3. Diagrama MER (descripción textual)

[ROLES] (1)───────────────────< (N) [USUARIOS] >────────────────────(1) [ESTATUS]
│
│ (1:N)
▼
[BÚSQUEDAS] (1)──────────────< (N) [RESULTADOS]

---

#  Notas finales
- El MER está optimizado para registrar actividades clínicas.  
- La tabla RESULTADOS se llenará cuando el módulo RAG esté integrado.  
- Todas las contraseñas deben estar encriptadas con bcrypt. 
