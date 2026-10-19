<div align="center">

# 🧹 Limpiezas Lagares S.L. — Gestión Empresarial con Odoo ERP

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Odoo](https://img.shields.io/badge/Odoo-19.0-714B67?style=for-the-badge&logo=odoo&logoColor=white)](https://www.odoo.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![License: LGPL v3](https://img.shields.io/badge/License-LGPL_v3-blue.svg?style=for-the-badge)](https://www.gnu.org/licenses/lgpl-3.0.html)

*Solución integral para el control de jornada laboral deslocalizado, imputación de horas por cliente y consulta digital en tiempo real.*

---

**Autores:** Javier Casal González · Diego Currás Rodríguez · Sergio Fernández Rodríguez

</div>

---

## 📋 Índice
- [Descripción del Proyecto](#-descripción-del-proyecto)
- [Objetivos del Proyecto](#-objetivos-del-proyecto)
- [Análisis de Problemas y Requisitos](#-análisis-de-problemas-y-requisitos)
- [Estudio Comparativo de Software](#-estudio-comparativo-de-software)
- [Justificación de la Elección de Odoo 19](#-justificación-de-la-elección-de-odoo-19)
- [Proceso de Despliegue](#-proceso-de-despliegue)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Gestión de Incidencias](#-gestión-de-incidencias)
- [Conclusiones y Futuras Ampliaciones](#-conclusiones-y-futuras-ampliaciones)
- [Declaración de Uso de IA](#-declaración-de-uso-de-ia)

---

## 🏬 Descripción del Proyecto

**Limpiezas Lagares S.L.** es una empresa de servicios de limpieza cuya plantilla está compuesta por:
- **20 personas operativas:** Trabajan directamente en las casas e instalaciones de los clientes.
- **2 personas de administración:** Ubicadas en la oficina central.

El objetivo principal es implantar un sistema digitalizado de gestión de registros de jornada que aporte fiabilidad, disponibilidad inmediata ante inspecciones y facilite el trabajo del personal deslocalizado.

---

## 🎯 Objetivos del Proyecto

- **Registrar:** Capturar las entradas y salidas ($E/S$) de los 20 trabajadores directamente desde sus dispositivos móviles.
- **Facilitar:** Simplificar el proceso de fichaje diario al realizarlo desde el teléfono móvil.
- **Conservar:** Disponer de registros digitales fiables para demostrar las horas trabajadas ante posibles inspecciones laborales o reclamaciones.
- **Consultar:** Visualizar y analizar en tiempo real las horas trabajadas por cada empleado y cliente.

---

## 🔴 Análisis de Problemas y Requisitos

| Problema Detectado | Requisito / Solución Implantada |
| :--- | :--- |
| **Documentación en formato físico:** Dificultad de gestión y almacenamiento. | **Fichaje móvil ($E/S$):** Registro remoto desde la ubicación de cada cliente. |
| **Necesidad de no fichar en oficina:** El personal se desplaza directo al cliente. | **Fichaje deslocalizado:** Entrada/Salida directamente en la ubicación del cliente. |
| **Imposibilidad de consultar horas exactas:** Cómputo no exacto ni rápido por trabajador y cliente. | **Consulta digital:** Horas trabajadas exactas de forma digital en cualquier momento. |
| **Incapacidad de demostración legal:** Riesgo en inspecciones de trabajo o reclamaciones. | **Registros digitales:** Demostración de jornadas con exactitud. |

---

## ⚖️ Estudio Comparativo de Software

Se evaluaron tres alternativas de software para cubrir las necesidades de la empresa:

| Criterio | Odoo Community | Kimai | SuiteCRM |
| :--- | :--- | :--- | :--- |
| **Tipo** | ERP | Gestión de Tiempos | CRM |
| **Licencia** | Mixta, LGPLv3 | Libre, AGPLv3 | Libre, AGPLv3 |
| **Coste (22 personas)** | Licencia 0 € + Alojamiento variable | Licencia 0 € + Alojamiento variable | Licencia 0 € + Alojamiento variable |
| **Alojamiento** | Propio o Nube | Propio o Nube Gestionada | Propio o Nube Gestionada |
| **Requisitos Téc.** | BD PostgreSQL | BD compatible (MariaDB/MySQL) | Servidor Web, PHP, MariaDB/MySQL |
| **Cubre** | Todos los requisitos | $E/S$, tiempos y jornadas | Clientes y Contactos |
| **No Cubre** | Nada relevante | Gestión de empleados | Gestión de Jornadas |

---

## 💡 Justificación de la Elección de Odoo 19

Se seleccionó **Odoo Community Edition** por las siguientes razones principales:

1. **Registro de Jornada:** Permite centralizar las entradas y salidas ($E/S$) en una misma herramienta.
2. **Gestión Doble:** Administra simultáneamente tanto la información de los clientes como la de las trabajadoras.
3. **Alternativa al CRM:** Presenta funcionalidades más amplias que un CRM tradicional como SuiteCRM.
4. **Coste y Despliegue:** Odoo Community es gratuito y fácilmente desplegable. Se consideró la mejor opción gracias a la experiencia previa de los desarrolladores en este sistema, además de ofrecer una gestión empresarial muy amplia y en constante mantenimiento de forma gratuita.

---

## 🚀 Proceso de Despliegue

El procedimiento de despliegue comprende los siguientes pasos:

| Paso | Operación | Justificación |
| :---: | :--- | :--- |
| **1** | Base de Datos y Volumen | Garantizar la persistencia obligatoria de la BD. |
| **2** | Configurar Odoo y Variables de Entorno (`.env`) | Establecer parámetros y datos de conexión con la BD. |
| **3** | Añadir herramienta de administración de la BD | Permite comprobar las *cards* y los datos almacenados. |
| **4** | Inicialización de BD en la web y carga de datos de prueba | Creación e inicialización de la BD `odoo_lagares`. |

### Guía Rápida de Despliegue

1. **Clonar el repositorio:**
   ```bash
   git clone [https://github.com/tu-usuario/limpiezas-lagares-odoo.git](https://github.com/tu-usuario/limpiezas-lagares-odoo.git)
   cd limpiezas-lagares-odoo
   ```

2. **Configurar las variables de entorno:**
   ```bash
   cp .env.example .env
   ```

3. **Levantar la pila Docker:**
   ```bash
   docker compose up -d
   ```

4. **Acceso a la plataforma:**
   Abre tu navegador e ingresa a `http://localhost:8069`.

---

## 📁 Estructura del Repositorio

```text
.
├── compose.yaml       # Definición de la pila Docker (Odoo + PostgreSQL)
├── .env.example       # Plantilla de variables de entorno
├── .gitignore         # Exclusión de archivos sensibles
└── README.md          # Documentación general del proyecto
```

---

## 🛠️ Gestión de Incidencias

### ⚡ Incidencia 1: Versión obsoleta de Odoo (v17)
- **Síntoma / Problema:** Se detectó el uso de Odoo v17, siendo la versión mínima compatible requerida la **v19**.
- **Solución:** Reinstalación y despliegue de Odoo en la **versión 19.0** para asegurar la compatibilidad con los requerimientos del proyecto.

---

## 📌 Conclusiones y Futuras Ampliaciones

### Lo que se consiguió:
- ✅ Fichaje centralizado accesible en cualquier momento.
- ✅ Registro e imputación de horas trabajadas por cliente y por trabajadora.
- ✅ Consultoría y auditoría de datos exactos digitalmente.

### Ampliaciones Futuras (Huella Digital):
El fichaje por huella digital se considerará como una ampliación posterior. Para su implementación se deberá estudiar:
1. **Legislación de protección de datos:** Análisis de la normativa legal respecto a datos biométricos.
2. **Programación e integración:** Adaptación técnica de la huella digital dentro de la aplicación.

---

## 🤖 Declaración de Uso de IA

Se han utilizado herramientas de Inteligencia Artificial (**ChatGPT** y **Gemini**) como apoyo para redactar el contenido del proyecto y colaborar en la programación. Todo el apoyo fue revisado y adaptado por el equipo de desarrollo para obtener una mayor eficiencia en los resultados.

---

<div align="center">
  <sub>Proyecto desarrollado para el módulo de Sistemas de Gestión Empresarial (SGE) — CFGS DAM</sub>
  <br>
  <sub><b>Autores:</b> Javier Casal González · Diego Currás Rodríguez · Sergio Fernández Rodríguez</sub>
</div>
