# Disparadores-y-Procedimientos-PL-SQL

Proyecto académico desarrollado para la materia de **Bases de Datos (2024-10)**.  
El trabajo consiste en reforzar la lógica operativa de una base de datos existente mediante la creación de **procedimientos almacenados, funciones y disparadores (triggers)** en Oracle PL/SQL, orientados a mejorar la integridad, automatización y control de procesos sobre pedidos, productos, empleados y auditoría.

---

## 📌 Objetivo General

Implementar una capa de lógica de negocio en Oracle Database que complemente el modelo relacional entregado, mediante la programación de **PL/SQL** para asegurar:

- Integridad de datos  
- Auditoría de operaciones  
- Automatización de procesos  
- Aplicación de reglas de negocio  
- Control de inventario y pedidos

---

# 🧠 Estructura del proyecto

```plaintext
Disparadores-y-Procedimientos-PL-SQL/
├── ProyectoFinal.sql             # Script completo con todos los procedimientos, funciones y disparadores
├── .gitignore
├── LICENSE
└── README.md                      # Este archivo
```
---

# 📊 Estado del proyecto

Este proyecto se revisó y reorganizó para su publicación en GitHub con fines académicos y de portafolio personal.
Los scripts fueron probados en OracleXE - Oracle Live y funcionan de forma independiente

---

# 🟦 1. Funcionalidades iniciales Implementadas

## 🔧 Procedimientos almacenados

- **Actualizar el valor de un producto**  
  - Recibe ID de producto y nuevo valor.

- **Actualizar inventario de un producto**  
  - Recibe código de producto y cantidad.

- **Insertar detalle de un pedido**  
  - Inserta una fila en `detallepedido` validando existencia previa.


## 🧮 Funciones

- **Valor del producto más vendido**
- **Gama de productos más vendida**
- **Registro de medios de pago**  
  Función o procedimiento que:
  - Verifica existencia del `codigocliente`
  - Permite registrar un nuevo medio de pago



# 🟩 2. Disparadores (Triggers)

- **Descontar existencias al crear un pedido**  
  `AFTER INSERT ON detallepedido`

- **Evitar que un empleado sea su propio jefe**  
  Se activa en:
  - `INSERT` de empleado  
  - `UPDATE` de `codigojefe`


# 🟦 3. Ampliación de la base de datos (Primera fase)

### 📌 Nuevos elementos:

- Atributo `valortotal` en tabla `pedidos`
- Tablas de auditoría:
  - `logsClientes`
  - `logsPedidos`


## 🧮 Nuevos procedimientos

- **Actualizar el valor total de un pedido**  
  El código de pedido entra como parámetro.

- **Actualizar todos los pedidos**  
  Llama al procedimiento anterior para cada pedido.


## 🔥 Nuevos disparadores

- **Auditoría automática**  
  Sobre:
  - clientes (INSERT, UPDATE, DELETE)
  - pedidos (INSERT, UPDATE, DELETE)

- **Actualizar automáticamente el valor total del pedido**
  - Por operaciones sobre `detallepedido`
  - Se activa en: INSERT, UPDATE, DELETE


# 🟦 4. Ampliación de la base de datos (Segunda fase)

### 📌 Nuevos campos en `gamaproductos`:

- `descuento`  
  - Se aplica a cualquier compra de la gama.


## 🧨 Nuevos disparadores solicitados

- **Aplicar el descuento automáticamente**
  - `AFTER INSERT OR UPDATE ON detallepedido`
  - Aplica el descuento al facturar

- **Impedir que un pedido exceda el inventario**
  - Verifica existencia suficiente antes de descontar

- **Actualizar automáticamente el inventario**
  - Cuando se registra un nuevo pedido


# 🚨 5. Control adicional y notificaciones

Para esta fase, se incorpora una nueva tabla encargada de almacenar avisos generados automáticamente por el sistema:

```sql
notificaciones(id, fecha, destinatario, mensaje)
```

## 📩 Disparador solicitado:

-**Registrar una notificación cuando:**
 - Un cliente hace un pago
 - Y supera su límite de crédito
 - Se registra automáticamente:
 - fecha del sistema
 - mensaje
 - destinatario = código del empleado asignado
---

 - ## 🚀 Cómo ejecutar los scripts

⭐Opción 1 **Oracle Live SQL**:
```bash
1. Ingresa a https://livesql.oracle.com

2. Abre SQL Worksheet.

3. Ejecutar secciones desde ProyectoFinal.sql en el orden del archivo.

   ```
⭐Opción 2 **Oracle SQL Developer o XE**:
   ```bash
1. Crear conexión con SYSTEM o usuario propio.

2. Abrir ProyectoFinal.sql.

3. Ejecutar como script (F5).

Validar triggers y procedimientos usando consultas de prueba.
```

---
   
>  Nota: Por razones de derechos académicos, el enunciado original del proyecto **no será publicado en este repositorio**.
