# Sistema de Gestion de Entidad Bancaria — Fundamentos de Bases de Datos

Este repositorio contiene el diseño, modelado relacional e implementacion SQL completa para un sistema de gestion bancario y asegurador, desarrollado para la asignatura Fundamentos de Bases de Datos.

El proyecto abarca desde el modelado Entidad-Relacion (conceptual y relacional) hasta la implementacion de un script ejecutable completo en Oracle SQL que incluye DDL (CREATE TABLE), DML (INSERT, UPDATE, DELETE) y una bateria de 25 consultas analiticas avanzadas.

---

## Estructura y Arquitectura de la Base de Datos

El dominio contempla la gestion integral de sucursales, empleados, clientes, cuentas bancarias, tarjetas, prestamos, transacciones, polizas de seguros y facturacion.

### 1. Diagramas Entidad-Relacion (E/R)

* Modelo Conceptual: Definicion de entidades, atributos y relaciones iniciales del dominio bancario.
* Modelo Relacional / Fisico: Resolucion de relaciones N:M mediante tablas asociativas (CLIENTE_CUENTA y TRANSACCION_FACTURA).

Las imagenes de los diagramas E/R estan disponibles en la raiz del repositorio (image_a861e1.png y image_a861bb.png).

### 2. Entidades del Sistema

* LOCALIDAD: Gestion de ubicaciones geograficas.
* SUCURSAL: Sedes del banco asociadas a una localidad.
* EMPLEADO: Registro de personal, salarios, puestos y sucursal asignada.
* CLIENTE: Titulares de servicios (NORMAL o PREMIUM).
* CUENTA: Cuentas bancarias de Ahorros o Corriente identificadas por IBAN (ES...).
* CLIENTE_CUENTA: Tabla asociativa (M:N) para la titularidad de cuentas.
* TARJETA: Tarjetas de debito y credito vinculadas a cuentas.
* PRESTAMO: Creditos asociados a cuentas con plazos e intereses (fijos o variables).
* TRANSACCION: Movimientos monetarios entre cuentas de origen y destino vinculados a tarjetas.
* SEGURO: Polizas contratadas por clientes (Hogar, Auto, Salud, Vida).
* FACTURA y TRANSACCION_FACTURA: Vinculacion contable N:M entre facturas y transacciones.

---

## Tecnologias y Caracteristicas Implementadas

* SGBD: Oracle Database (Sintaxis compatible con VARCHAR2/VARCHAR, NUMBER, DATE, DECIMAL, funciones de fecha como MONTHS_BETWEEN y SYSDATE).
* Integridad Referencial: Claves primarias y foraneas en cascada logica.
* Restricciones de Integridad (CONSTRAINTS):
  * Validacion de formato IBAN en cuentas (COD_CUENTA LIKE 'ES%').
  * Restriccion de valores en clientes (NORMAL, PREMIUM).
  * Verificacion de importes positivos en salarios y seguros (CHECK > 0).
  * Claves compuestas en tablas N:M (COD_TRANSACCION, COD_FACTURA) y (COD_CUENTA, COD_CLIENTE).

---

## Contenido del Script Trabajo.sql

El script principal se encuentra completamente estructurado en 4 bloques funcionales:

1. Creacion de Tablas y Restricciones (DDL): Definicion de las 11 tablas del sistema.
2. Insercion de Datos de Prueba (DML): Poblado con mas de 100 registros realistas repartidos entre todas las entidades.
3. Consultas de Explotacion de Datos (25 Consultas):
   * Subconsultas escalar, correlacionadas y de conjunto (IN, EXISTS, NOT IN, INTERSECT).
   * Operaciones de agregacion (SUM, AVG, COUNT, MAX, MIN) filtradas con HAVING.
   * Calculo de antiguedad/edad mediante funciones de fecha (MONTHS_BETWEEN, SYSDATE).
   * Analisis de saldos, prestamos, transacciones, coberturas de seguros y concurrencia geografica entre clientes y empleados.
4. Sentencias de Actualizacion y Borrado Avanzado:
   * Inserciones con subconsultas condicionales (ej. asignar prestamo a la cuenta mas antigua).
   * Updates dinamicos basados en maximos/minimos (ej. promocion a clientes PREMIUM por volumen de empleados en localidad).
   * Eliminaciones en cascada logica mediante filtros anidados en tablas intermedias.

---

## Estructura del Repositorio

```text
.
├── Trabajo.sql          # Script SQL unico (DDL, INSERT, 25 Consultas, UPDATES y DELETES)
├── image_a861e1.png     # Diagrama Entidad-Relacion Conceptual
├── image_a861bb.png     # Diagrama Entidad-Relacion Relacional
└── README.md            # Documentacion del proyecto
