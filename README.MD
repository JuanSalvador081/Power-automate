# Automatización de Procesos de Facturación con Power Automate

Recreación personal (con datos ficticios) de un sistema de automatización de
gestión documental desarrollado originalmente durante mi experiencia como
Data Analyst / Data Engineer en Niyval. Los flujos aquí documentados replican
la lógica real aplicada en un entorno de cliente, usando datos y una cuenta
propia para poder mostrar el trabajo libremente, sin comprometer información
confidencial del cliente original.

## Contexto

El sistema gestiona un flujo de facturación end-to-end: desde la ingesta
dinámica de datos hasta el seguimiento operativo y la generación de reportes,
usando **Power Automate**, **SharePoint** y **Excel**.

## Flujos incluidos

### 1. Ingesta dinámica de datos + permisos por elemento
Extrae filas desde una tabla de Excel, valida duplicados antes de crear cada
elemento en una lista de SharePoint, y asigna permisos de forma dinámica al
responsable de cada factura (rompiendo la herencia de permisos y otorgando
acceso individual mediante llamadas HTTP a la API REST de SharePoint).

[`capturas/01-ingesta`](capturas/01-ingesta)

### 2. Notificación automática por cambio de estado
Detecta cuando una factura cambia de estado de "Pendiente" a "Válido" y
envía una notificación automática.

[`capturas/02-notificacion-estado`](capturas/02-notificacion-estado)

### 3. Alerta semanal de facturas pendientes
Flujo programado que revisa semanalmente las facturas sin resolver y envía
un resumen consolidado.

[`capturas/03-alerta-semanal`](capturas/03-alerta-semanal)

### 4. Versionado mensual con exportación a Excel
Consolida mensualmente los registros del período y genera un archivo Excel
con el historial de datos para trazabilidad.

[`capturas/04-versionado-mensual`](capturas/04-versionado-mensual)

---

## Vista general

### Flujo 1 — Ingesta y permisos
![Flujo completo](/01-ingesta/flujo-completo.png)
![Lógica de permisos](01-ingesta/asegurar-usuario.png)![Lógica de permisos](01-ingesta/romper-herencia.png)![Lógica de permisos](01-ingesta/id-edicion.png)![Lógica de permisos](01-ingesta/permiso-gestor.png)
![Vista de permiso administrador](01-ingesta/visualizacion-lista-admin.png)
![Vista de permiso individual](01-ingesta/visualizacion-lista-individual-1.png)![Vista de permiso individual](01-ingesta/visualizacion-lista-individual-2.jpeg)

### Flujo 2 — Notificación por cambio de estado
![Flujo completo](02-notificacion-estado/flujo-completo.png)
![Condicion del desencadenante](02-notificacion-estado/condicional-desencadenante.png)
![Condicional para el envio del correo](02-notificacion-estado/condicional-envio.png)
![Ejecucion exitosa](02-notificacion-estado/ejecucion-exitosa.png)
![Correo enviado](02-notificacion-estado/correo-enviado.png)
### Flujo 3 — Alerta semanal
![Flujo completo](03-alerta-semanal/flujo-completo.png)
![Condicion que filtra facturas pendientes](03-alerta-semanal/condicion-pendiente.png)
![Condicion que filtra correos unicos](03-alerta-semanal/condicion-correo-unico-1.png)![Condicion que filtra correos unicos](03-alerta-semanal/condicion-correo-unico-2.png)
![Filtrado de la matriz](03-alerta-semanal/filtro-matriz.png)
![Filtrado de duplicados](03-alerta-semanal/condicion-facturas-gestor-1.png)![Filtrado de duplicados](03-alerta-semanal/condicion-facturas-gestor-2.png)
![Creacion de la tabla html](03-alerta-semanal/crear-tabla.png)
![Ejecucion exitosa](03-alerta-semanal/ejecucion-exitosa.png)
![Correo recibido](03-alerta-semanal/correo-enviado.png)
### Flujo 4 — Versionado mensual
![Flujo completo](04-versionado-mensual/flujo-completo.png)
![Filtro fecha](04-versionado-mensual/filtro-fecha.png)
![Ejecucion exitosa](04-versionado-mensual/ejecucion-exitosa.png)
![Excel que se genero](04-versionado-mensual/excel-generado.png)
---

## Stack

Power Automate · SharePoint (API REST) · Excel Online · Power Platform

## Nota

Los datos de facturas, proveedores y responsables mostrados son **ficticios**,
creados exclusivamente para esta demostración. La lógica y arquitectura de
los flujos reflejan fielmente el trabajo realizado en un contexto profesional real.