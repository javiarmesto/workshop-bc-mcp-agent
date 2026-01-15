# 🚀 Módulo 5: Casos de Uso Avanzados

> **Tiempo estimado**: 45 minutos

---

## 🎯 Objetivo

Explorar escenarios avanzados que demuestran el poder de conectar agentes de IA con Business Central a través de MCP.

---

## 📊 Caso 1: Análisis de Cuentas por Cobrar

### Escenario
El departamento financiero necesita identificar rápidamente clientes con facturas vencidas.

### Conversación de Ejemplo

```
Tú: ¿Qué clientes tienen facturas vencidas?

Bot: Consultando facturas vencidas en Business Central...

     📊 **Resumen de Cuentas por Cobrar Vencidas**
     
     Total vencido: 45,230.00 EUR
     
     🔴 **Vencimiento > 90 días (Crítico)**
     - The Cannon Group (10000): 12,500 EUR
     
     🟠 **Vencimiento 60-90 días**
     - Selangorian Ltd. (20000): 8,730 EUR
     - Progressive Home Furnishings (30000): 5,000 EUR
     
     🟡 **Vencimiento 30-60 días**
     - New Concepts Furniture (40000): 19,000 EUR
     
     ¿Quieres ver el detalle de algún cliente específico?

Tú: Dame más detalles del cliente 10000

Bot: 📋 **The Cannon Group PLC (10000)**
     
     **Datos de Contacto:**
     - Dirección: 192 Market Square, Birmingham
     - Teléfono: +44 121 456 7890
     - Email: accounts@cannongroup.co.uk
     
     **Situación Financiera:**
     - Saldo actual: 12,500 EUR
     - Límite de crédito: 12,600 EUR
     - % utilizado: 99.2% ⚠️
     
     **Facturas Pendientes:**
     | Factura | Fecha | Vencimiento | Importe |
     |---------|-------|-------------|---------|
     | 103001  | 15/09 | 15/10       | 5,000   |
     | 103015  | 01/10 | 01/11       | 7,500   |
     
     ⚠️ Cliente cerca del límite de crédito.
     
     ¿Quieres que prepare un recordatorio de pago?
```

### Instrucciones para el Agente

Añade a las instrucciones:

```markdown
## Análisis de Cuentas por Cobrar

Cuando el usuario pregunte por facturas vencidas:
1. Consulta las facturas con fecha de vencimiento < hoy
2. Agrupa por antigüedad: >90 días (crítico), 60-90 días, 30-60 días
3. Muestra totales y detalle por cliente
4. Destaca clientes cerca del límite de crédito
5. Ofrece acciones de seguimiento
```

---

## 📦 Caso 2: Verificación de Stock para Pedido

### Escenario
Un vendedor necesita verificar disponibilidad antes de crear un pedido.

### Conversación de Ejemplo

```
Tú: ¿Tenemos stock para vender 20 unidades del artículo 1896-S 
    y 10 del artículo 1900-S al cliente The Cannon Group?

Bot: Verificando disponibilidad en Business Central...

     📦 **Verificación de Stock**
     
     | Artículo | Descripción | Solicitado | Disponible | Estado |
     |----------|-------------|------------|------------|--------|
     | 1896-S   | ATHENS Desk | 20         | 15         | ⚠️     |
     | 1900-S   | PARIS Chair | 10         | 45         | ✅     |
     
     ⚠️ **Alerta**: No hay suficiente stock de ATHENS Desk
     
     **Opciones:**
     1. Crear pedido parcial (15 unidades de 1896-S)
     2. Verificar transferencias de otros almacenes
     3. Crear pedido completo con aviso de backorder
     
     ¿Cómo quieres proceder?

Tú: Crea el pedido parcial con lo que hay disponible

Bot: Antes de crear el pedido, confirmo los datos:
     
     📝 **Nuevo Pedido de Venta**
     - Cliente: The Cannon Group (10000)
     - Fecha: 14/01/2026
     
     | Línea | Artículo | Descripción   | Cant. | Precio U. | Total     |
     |-------|----------|---------------|-------|-----------|-----------|
     | 1     | 1896-S   | ATHENS Desk   | 15    | 1,005.00  | 15,075.00 |
     | 2     | 1900-S   | PARIS Chair   | 10    | 315.00    | 3,150.00  |
     |       |          |               |       | **Total** | 18,225.00 |
     
     ¿Confirmo la creación del pedido?

Tú: Sí, créalo

Bot: ✅ **Pedido creado exitosamente**
     
     - Número de pedido: SO-001045
     - Cliente: The Cannon Group (10000)
     - Total: 18,225.00 EUR
     - Estado: Abierto
     
     📌 Nota: Quedan 4 unidades de ATHENS Desk pendientes.
     ¿Quieres que cree un aviso para cuando haya stock?
```

### Instrucciones para el Agente

```markdown
## Creación de Pedidos

Cuando el usuario quiera crear un pedido:
1. Primero verifica el stock disponible de todos los artículos
2. Si hay insuficiencia, presenta opciones claras
3. SIEMPRE pide confirmación antes de crear
4. Muestra resumen con totales antes de confirmar
5. Tras crear, proporciona número de pedido y detalles
```

---

## 👤 Caso 3: Crear Nuevo Cliente

### Escenario
Un vendedor necesita dar de alta un nuevo cliente rápidamente.

### Conversación de Ejemplo

```
Tú: Necesito crear un nuevo cliente

Bot: Perfecto, te ayudo a crear el nuevo cliente.
     Necesito algunos datos:
     
     ¿Cuál es el nombre de la empresa?

Tú: Fabrikam España S.L.

Bot: Entendido: **Fabrikam España S.L.**
     
     ¿Cuál es la dirección completa?

Tú: Calle Gran Vía 45, 28013 Madrid

Bot: Dirección registrada.
     
     ¿Tienes el email de contacto?

Tú: ventas@fabrikam.es

Bot: Casi listo. Una última pregunta:
     
     ¿Qué límite de crédito asignamos?
     (El límite estándar es 10,000 EUR)

Tú: Ponle 15000

Bot: Perfecto. Confirmo los datos del nuevo cliente:
     
     📋 **Nuevo Cliente**
     - Nombre: Fabrikam España S.L.
     - Dirección: Calle Gran Vía 45, 28013 Madrid
     - Email: ventas@fabrikam.es
     - Límite de crédito: 15,000.00 EUR
     - Moneda: EUR
     - Términos de pago: (estándar)
     
     ¿Creo el cliente con estos datos?

Tú: Sí

Bot: ✅ **Cliente creado exitosamente**
     
     - Número asignado: **C00125**
     - Nombre: Fabrikam España S.L.
     - Estado: Activo
     
     El cliente ya está disponible para crear pedidos.
     ¿Quieres crear un pedido para este cliente?
```

### Instrucciones para el Agente

```markdown
## Creación de Clientes

Cuando el usuario quiera crear un cliente:
1. Solicita los datos paso a paso, no todos a la vez
2. Datos mínimos: Nombre, Dirección
3. Datos recomendados: Email, Teléfono, Límite de crédito
4. Sugiere valores por defecto cuando aplique
5. SIEMPRE muestra resumen y pide confirmación
6. Tras crear, muestra el número asignado
7. Ofrece siguiente acción lógica (crear pedido)
```

---

## 🔄 Caso 4: Consultas Combinadas

### Escenario
Análisis que requiere combinar información de múltiples entidades.

### Conversación de Ejemplo

```
Tú: Dame un resumen de la situación del cliente 10000 
    incluyendo pedidos pendientes y facturas

Bot: 📊 **Resumen Completo: The Cannon Group (10000)**
     
     **═══ Datos Generales ═══**
     - Nombre: The Cannon Group PLC
     - Desde: Cliente desde 2018
     - Vendedor asignado: John Smith
     - Categoría: Premium
     
     **═══ Situación Financiera ═══**
     - Saldo actual: 12,500 EUR
     - Límite de crédito: 12,600 EUR
     - Crédito disponible: 100 EUR ⚠️
     - Ventas YTD: 145,000 EUR
     
     **═══ Pedidos Pendientes (2) ═══**
     | Pedido    | Fecha      | Importe   | Estado     |
     |-----------|------------|-----------|------------|
     | SO-001032 | 10/01/2026 | 5,200 EUR | Pendiente  |
     | SO-001038 | 12/01/2026 | 3,100 EUR | En proceso |
     | **Total** |            | 8,300 EUR |            |
     
     **═══ Facturas Abiertas (3) ═══**
     | Factura | Fecha      | Vence      | Importe   | Estado    |
     |---------|------------|------------|-----------|-----------|
     | 103001  | 15/09/2025 | 15/10/2025 | 5,000 EUR | Vencida   |
     | 103015  | 01/10/2025 | 01/11/2025 | 5,000 EUR | Vencida   |
     | 103022  | 15/12/2025 | 15/01/2026 | 2,500 EUR | Por vencer|
     
     **⚠️ Alertas:**
     - Cliente casi al límite de crédito (99.2%)
     - Facturas vencidas por 10,000 EUR
     - Nuevos pedidos por 8,300 EUR no caben en crédito
     
     **Recomendaciones:**
     1. Gestionar cobro de facturas vencidas
     2. Revisar límite de crédito si procede
     3. Los pedidos pendientes superan el crédito disponible
     
     ¿Quieres que tome alguna acción?
```

---

## 🎭 Caso 5: Múltiples Herramientas en Secuencia

### Escenario
El agente usa varias herramientas MCP automáticamente.

### Activity Map

```
Usuario: "Crea un pedido de 5 escritorios ATHENS para el cliente Fabrikam"

Orquestación:
│
├─► [bc_items_read] → Buscar "ATHENS" → Encontrado: 1896-S
│
├─► [bc_customers_read] → Buscar "Fabrikam" → Encontrado: C00125
│
├─► [bc_items_read] → Verificar stock 1896-S → Disponible: 15
│
├─► [bc_salesOrders_create] → Crear pedido
│   ├── Customer: C00125
│   └── Lines: 1896-S x 5
│
└─► Respuesta al usuario con confirmación
```

---

## 💡 Mejores Prácticas para Casos Avanzados

### 1. Confirmación en Operaciones de Escritura

```markdown
SIEMPRE:
- Crear registro → Mostrar resumen → Pedir confirmación → Crear
- Actualizar registro → Mostrar cambios → Pedir confirmación → Actualizar
```

### 2. Manejo de Errores Gracioso

```markdown
Si una operación falla:
- No mostrar errores técnicos
- Explicar qué salió mal en lenguaje simple
- Ofrecer alternativas o siguiente paso
```

### 3. Contexto entre Turnos

```markdown
Si el usuario pregunta "¿y sus pedidos?":
- Recordar el cliente del turno anterior
- No pedir de nuevo el número de cliente
```

### 4. Formato de Respuestas

```markdown
Para listas cortas (<5 items): Mostrar todos
Para listas largas: Mostrar top 5 + total + ofrecer filtrar
Para datos numéricos: Usar tablas alineadas
Para alertas: Usar emojis de estado (✅ ⚠️ ❌)
```

---

## ✅ Ejercicio Práctico

Prueba estos escenarios en tu agente:

1. **Escenario Financiero**
   ```
   "¿Cuáles son nuestros 5 clientes con mayor saldo pendiente?"
   ```

2. **Escenario de Ventas**
   ```
   "Necesito crear un pedido de prueba para el cliente 10000 
    con 2 unidades del artículo más vendido"
   ```

3. **Escenario Combinado**
   ```
   "Prepara un resumen de ventas de hoy incluyendo 
    nuevos pedidos y facturas emitidas"
   ```

---

## ✅ Checklist del Módulo

- [ ] Probé consulta de cuentas por cobrar vencidas
- [ ] Probé verificación de stock antes de pedido
- [ ] Probé creación de cliente paso a paso
- [ ] Probé consulta combinada de múltiples entidades
- [ ] El agente maneja errores correctamente
- [ ] El agente pide confirmación antes de crear/modificar

---

## ➡️ Siguiente Paso

El agente está funcionando. Ahora lo publicaremos para que otros lo usen:

👉 [Módulo 6: Publicar y Desplegar](../modulo-06-publicar/README.md)
