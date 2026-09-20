# Sistema de Gestión de Entidad Bancaria — Fundamentos de Bases de Datos

Este repositorio contiene el diseño, modelado relacional e implementación SQL para un sistema de gestión de una entidad bancaria y aseguradora, desarrollado para la asignatura Fundamentos de Bases de Datos del curso 2024/2025 en la Universidad de Jaén.

El proyecto abarca desde el modelo Entidad-Relación conceptual y su transformación al modelo lógico relacional, hasta la creación del script DDL/DML ejecutable con restricciones de integridad y datos de prueba.

---

## Estructura y Arquitectura de la Base de Datos

La base de datos contempla la gestión integral de sucursales, empleados, clientes, cuentas bancarias, transacciones, préstamos, tarjetas, seguros y facturación.

### 1. Diagramas Entidad-Relación (E/R)

* Modelo Conceptual (Diagrama E/R inicial): Muestra las entidades principales, atributos clave y relaciones iniciales del dominio bancario.
* Modelo Relacional / Físico (Diagrama N-M resuelto): Incluye la resolución de relaciones N:M mediante tablas intermedias (como `CLIENTE_CUENTA` y `TRANSACCION_FACTURA`).

> *Las imágenes de los diagramas E/R se encuentran disponibles en la raíz del repositorio (`image_a861e1.png` y `image_a861bb.png`).*

### 2. Entidades Principales

* `LOCALIDAD`: Almacena las ubicaciones geográficas de clientes, empleados y sucursales.
* `SUCURSAL`: Representa las sedes del banco ligadas a una localidad.
* `EMPLEADO`: Gestión de personal, puestos, salarios y asignación a sucursales.
* `CLIENTE`: Registro de usuarios (`NORMAL` o `PREMIUM`).
* `CUENTA`: Cuentas bancarias identificadas por IBAN (`ES...`), de tipo *Ahorros* o *Corriente*.
* `CLIENTE_CUENTA`: Tabla asociativa que gestiona la relación M:N entre clientes y cuentas.
* `TARJETA`: Tarjetas de débito/crédito asociadas a una cuenta bancaria.
* `PRESTAMO`: Créditos asociados a cuentas con tasa de interés y plazo.
* `TRANSACCION`: Movimientos monetarios de origen/destino entre cuentas vinculados a tarjetas.
* `SEGURO`: Pólizas contratadas por los clientes (Hogar, Auto, Salud, Vida).
* `FACTURA` y `TRANSACCION_FACTURA`: Mapeo y registro contable de facturas asociadas a transacciones.

---

## Tecnologías y Características Implementadas

* SGBD: SQL / Oracle Database (Sintaxis compatible con tipos `NUMBER`, `VARCHAR2/VARCHAR`, `DATE`, `DECIMAL`).
* Claves Primarias y Foráneas: Garantizan la integridad referencial entre todas las tablas interconectadas.
* Restricciones de Integridad (`CONSTRAINTS`):
  * Validación del formato IBAN en cuentas (`CHECK (COD_CUENTA LIKE 'ES%')`).
  * Validación de tipos de cliente (`NORMAL`, `PREMIUM`).
  * Comprobaciones de valores positivos en salarios y precios (`CHECK > 0`).
  * Campos obligatorios `NOT NULL` en atributos clave (DNI, cuentas de origen/destino, importes, etc.).

---

## Estructura del Repositorio

```text
.
├── Trabajo.sql          # Script SQL con DDL (CREATE TABLE) y DML (INSERT)
├── image_a861e1.png     # Diagrama Entidad-Relación Conceptual
├── image_a861bb.png     # Diagrama Entidad-Relación Transformado / Relacional
└── README.md            # Documentación del proyecto
