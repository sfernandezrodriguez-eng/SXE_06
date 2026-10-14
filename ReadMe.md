<div align="center">

# 🧹 Limpiezas Lagares S.L. — Gestión Empresarial con Odoo ERP

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Odoo](https://img.shields.io/badge/Odoo-17.0-714B67?style=for-the-badge&logo=odoo&logoColor=white)](https://www.odoo.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![License: LGPL v3](https://img.shields.io/badge/License-LGPL_v3-blue.svg?style=for-the-badge)](https://www.gnu.org/licenses/lgpl-3.0.html)

*Solución integral para el control de jornada laboral deslocalizado, imputación de horas por cliente y facturación automatizada.*

</div>

---

## 📋 Índice
- [Descripción del Proyecto](#-descripción-del-proyecto)
- [Solución Implantada](#-solución-implantada)
- [Dictamen Técnico-Legal (Huella Dactilar)](#-dictamen-técnico-legal-huella-dactilar)
- [Requisitos de la Infraestructura](#-requisitos-de-la-infraestructura)
- [Guía de Despliegue Rápido](#-guía-de-despliegue-rápido)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Comprobaciones y Pruebas Operativas](#-comprobaciones-y-pruebas-operativas)
- [Gestión de Incidencias](#-gestión-de-incidencias)

---

## 🏬 Descripción del Proyecto

**Limpiezas Lagares S.L.** es una empresa de servicios de limpieza compuesta por **20 limpiadoras** operando directamente en casa o instalaciones de clientes y **2 personas de administración** en oficina central.

### 🔴 Problemática detectada:
1. **Deslocalización total:** El personal operativo no acude a la oficina para iniciar/finalizar la jornada.
2. **Partes en papel obsoletos:** Incongruencias entre las horas reportadas a fin de mes y las facturadas a los clientes.
3. **Riesgo legal:** Incapacidad de acreditar las horas trabajadas ante una eventual **Inspección de Trabajo** o reclamación de un cliente.

---

## 💡 Solución Implantada

A través de **Odoo 17 Community Edition**, se ha desplegado una pila completa en contenedores **Docker** que cubre:

* **Fichaje Móvil (Módulo `hr_attendance`):** Permite registrar entrada y salida desde navegadores móviles en 2 clics.
* **Partes de Horas (Módulo `hr_timesheet`):** Vincula las horas ejecutadas por trabajador a la ficha del cliente específico.
* **Facturación (Módulo `account`):** Genera informes y borradores de factura basados en horas reales auditadas.
* **Trazabilidad Garantizada:** Conservación de datos en base de datos PostgreSQL durante más de 4 años en servidor propio.

---

## ⚖️ Dictamen Técnico-Legal (Huella Dactilar)

> **Consulta de la empresa:** *¿Se puede usar el fichaje por huella dactilar ofreciendo un lector biométrico?*

❌ **RESPUESTA: NO RECOMENDADO / INCOMPATIBLE CON EL RGPD**

* **Criterio AEPD:** Siguiendo las directrices del Comité Europeo de Protección de Datos (CEPD 05/2020), el registro biométrico para control horario se considera **trata de datos de categoría especial de alto riesgo** (Art. 9 RGPD).
* **Juicio de Proporcionalidad:** Existen alternativas menos intrusivas e igualmente eficaces (fichaje web/App móvil con clave individual). El uso de huella dactilar en este contexto expondría a la empresa a **sanciones económicas graves**.

---

## 💻 Requisitos de la Infraestructura

* **Docker** `>= 20.10`
* **Docker Compose** `>= 2.0`
* **Puertos libres:** `8069` (HTTP Odoo)

---

## 🚀 Guía de Despliegue Rápido

Sigue estos pasos para levantar la pila en local o en un servidor VPS:

### 1️⃣ Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/limpiezas-lagares-odoo.git
cd limpiezas-lagares-odoo
```

### 2️⃣ Configurar las variables de entorno
Copia la plantilla de ejemplo y define contraseñas seguras:
```bash
cp .env.example .env
```

Edita `.env` para establecer tu propia clave de base de datos:
```env
POSTGRES_DB=odoo_lagares
POSTGRES_USER=odoo_user
POSTGRES_PASSWORD=tu_contraseña_segura_aqui
```

### 3️⃣ Levantar el contenedor
```bash
docker compose up -d
```

### 4️⃣ Acceso a la plataforma
Abre tu navegador e ingresa a:
👉 **`http://localhost:8069`** (o `http://IP_DEL_SERVIDOR:8069`)

---

## 📁 Estructura del Repositorio

```text
.
├── compose.yaml       # Definición de la pila Docker (Odoo + PostgreSQL)
├── .env.example       # Plantilla de variables de entorno (sin secretos)
├── .gitignore         # Exclusión de archivos sensibles (.env)
└── README.md          # Documentación general de la propuesta
```

---

## ✅ Comprobaciones y Pruebas Operativas

Se han ejecutado las siguientes pruebas en el entorno desplegado para certificar su correcto funcionamiento:

| Prueba | Descripción | Resultado |
| :--- | :--- | :---: |
| **Fichaje Móvil** | Entrada/Salida simulada de limpiadora desde smartphone | `OK` |
| **Imputación Cliente** | Asignación de 4 horas de trabajo al proyecto *Cliente X* | `OK` |
| **Resumen Semanal** | Consulta administrativa de total de horas por trabajadora | `OK` |
| **Exportación Legal** | Descarga de registro de jornada en formato `.xlsx` | `OK` |

---

## 🛠️ Gestión de Incidencias

During el despliegue de la infraestructura se detectaron y resolvieron las siguientes incidencias:

### ⚡ Incidencia 1: Fallo de conexión de Odoo al arrancar la BD
* **Síntoma:** El contenedor `lagares_odoo` se reiniciaba indicando `ConnectionRefusedError`.
* **Causa:** Odoo intentaba conectar antes de que PostgreSQL estuviese listo para recibir conexiones.
* **Solución:** Se incluyó un bloque `healthcheck` en el servicio `db` dentro de `compose.yaml` y la regla `condition: service_healthy` en la dependencia de Odoo.

### ⏰ Incidencia 2: Desfase horario en los registros de fichaje
* **Síntoma:** Las marcas de tiempo aparecían con 2 horas de retraso.
* **Causa:** La zona horaria predeterminada de la imagen base de Odoo es UTC.
* **Solución:** Ajuste de zona horaria del sistema a `Europe/Madrid` desde los ajustes generales de Odoo.

---

<div align="center">
  <sub>Proyecto desarrollado para el módulo de Sistemas de Gestión Empresarial (SGE) — CFGS DAM</sub>
</div>