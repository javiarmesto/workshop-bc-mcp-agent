# 🔗 Módulo 4: Conectar el Agente al BC MCP Server

> **Tiempo estimado**: 30 minutos

---

## 🎯 Objetivo

Conectar nuestro agente de Copilot Studio con el MCP Server de Business Central para acceder a datos en vivo.

---

## 🔌 Lo Que Vamos a Conectar

```
┌─────────────────────┐         ┌─────────────────────┐
│  Copilot Studio     │         │  Business Central   │
│                     │   MCP   │                     │
│  Contoso BC         │ ◄─────► │  MCP Server         │
│  Assistant          │         │  CONTOSO-SALES      │
│                     │         │                     │
└─────────────────────┘         └─────────────────────┘
```

---

## 🚀 Paso 1: Abrir Configuración de Tools

1. En Copilot Studio, abre tu agente **"Contoso BC Assistant"**
2. Ve a la pestaña **"Tools"** en el menú lateral
3. Click en **"+ Add a tool"**

```
┌─────────────────────────────────────────────────────┐
│  Contoso BC Assistant                               │
├─────────────────────────────────────────────────────┤
│  Overview │ Topics │ Knowledge │ [Tools] │ Actions │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Tools                                              │
│                                                     │
│  No tools added yet                                 │
│                                                     │
│  [+ Add a tool]                                     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 🔍 Paso 2: Buscar el MCP Server de Business Central

1. En el diálogo "Add a tool", busca: **"Dynamics 365 Business Central MCP Server"**
2. Selecciona el servidor de la lista de resultados

```
┌─────────────────────────────────────────────────────┐
│  Add a tool                                         │
├─────────────────────────────────────────────────────┤
│  🔍 Search: [dynamics 365 business          ]       │
│                                                     │
│  Results:                                           │
│  ┌─────────────────────────────────────────────┐   │
│  │ 🔷 Dynamics 365 Business Central MCP Server │   │
│  │    (Preview)                                │   │
│  │    Connect to Business Central data         │   │
│  │    [Select]                                 │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
└─────────────────────────────────────────────────────┘
```

> 💡 Si no lo encuentras, verifica:
> - Que tu tenant tiene acceso al BC MCP Server
> - Que la feature está habilitada en BC (Feature Management)
> - Que tienes licencia de Copilot Studio con créditos disponibles

---

## 🔐 Paso 3: Crear Conexión

### 3.1 Estado de Conexión

Si el campo **"Connection"** muestra **"Not connected"**:

1. Click en el campo de conexión
2. Selecciona **"Create new connection"**

### 3.2 Autenticación

1. Se abrirá ventana de autenticación de Microsoft
2. Inicia sesión con tu cuenta de Business Central
3. Acepta los permisos solicitados

```
┌─────────────────────────────────────────────────────┐
│  Sign in to Business Central                        │
├─────────────────────────────────────────────────────┤
│                                                     │
│  [Microsoft logo]                                   │
│                                                     │
│  Sign in with your organizational account          │
│                                                     │
│  Email: [___________________________]              │
│                                                     │
│  [Next]                                            │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### 3.3 Verificar Conexión

Una vez conectado, verás:
- **Status**: Connected ✅
- **User**: tu.email@contoso.com

---

## ⚙️ Paso 4: Configurar Inputs del MCP Server

Después de conectar, debes configurar los **Inputs** en la sección de configuración:

### 4.1 Environment (Requerido)

| Campo | Descripción |
|-------|-------------|
| **Environment** | Selector desplegable. Haz clic en la flecha y selecciona tu entorno de BC (ej: `Production`, `Sandbox`) |

> 💡 El sistema carga automáticamente los entornos disponibles para tu cuenta

### 4.2 Company (Requerido)

| Campo | Descripción |
|-------|-------------|
| **Company** | Selector desplegable. Haz clic en la flecha y selecciona la compañía de BC (ej: `CRONUS España S.A.`) |

> 💡 Las compañías se cargan automáticamente del entorno seleccionado

### 4.3 MCP Server Configuration (Opcional)

| Campo | Descripción |
|-------|-------------|
| **MCP Server Configuration** | Nombre de la configuración creada en BC. Escribe: `CONTOSO-SALES` (o déjalo vacío para acceso read-only por defecto) |

> ⚠️ **Importante**: Si lo dejas vacío, el agente tendrá acceso de solo lectura a todas las API pages expuestas

```
┌─────────────────────────────────────────────────────┐
│  Dynamics 365 Business Central MCP Server          │
├─────────────────────────────────────────────────────┤
│  Connection: [Connected ✅                    ]    │
│                                                     │
│  Inputs:                                            │
│  ├── Environment*:              [Production ▼]     │
│  ├── Company*:                  [CRONUS España S.A. ▼] │
│  └── MCP Server Configuration:  [CONTOSO-SALES]    │
│                                                     │
│  [Add and configure]  [Add to agent]               │
└─────────────────────────────────────────────────────┘
```

---

## ✅ Paso 5: Añadir al Agente

1. Click en **"Add and configure"** para configurar las herramientas
   - O **"Add to agent"** para añadir con configuración por defecto

2. Si seleccionaste "Add and configure":
   - Verás la lista de herramientas disponibles (depende del modo de configuración)
   - Puedes habilitar/deshabilitar herramientas específicas
   - Puedes editar descripciones para mejorar la orquestación

### Herramientas Disponibles

Las herramientas que verás dependen del **modo** de tu configuración `CONTOSO-SALES`:

#### Si tu configuración NO usa Dynamic Tool Mode (modo estático):

Verás las herramientas específicas para cada API:

```
┌─────────────────────────────────────────────────────┐
│  Tools from Business Central MCP Server            │
├─────────────────────────────────────────────────────┤
│  [✓] bc_customers_read                             │
│      Read customer information                      │
│                                                     │
│  [✓] bc_customers_create                           │
│      Create a new customer                          │
│                                                     │
│  [✓] bc_customers_modify                           │
│      Modify customer information                    │
│                                                     │
│  [✓] bc_items_read                                 │
│      Read item/product information                  │
│                                                     │
│  [✓] bc_salesOrders_read                           │
│      Read sales orders                              │
│                                                     │
│  [✓] bc_salesOrders_create                         │
│      Create a new sales order                       │
│                                                     │
│  [✓] bc_salesInvoices_read                         │
│      Read sales invoices                            │
│                                                     │
│  [✓] bc_vendors_read                               │
│      Read vendor information                        │
└─────────────────────────────────────────────────────┘
```

#### Si tu configuración USA Dynamic Tool Mode:

Solo verás las herramientas de acciones dinámicas:

```
┌─────────────────────────────────────────────────────┐
│  Tools from Business Central MCP Server            │
├─────────────────────────────────────────────────────┤
│  [✓] bc_actions_search                             │
│      Search for available BC actions/tools          │
│                                                     │
│  [✓] bc_actions_describe                           │
│      Get detailed description of a BC action        │
│                                                     │
│  [✓] bc_actions_invoke                             │
│      Execute a BC action dynamically                │
└─────────────────────────────────────────────────────┘
```

> 💡 **Recomendación**: Para el workshop, usa modo estático (Dynamic Tool Mode = No) para ver claramente las herramientas específicas.

---

## 🧪 Paso 6: Probar la Conexión

### 6.1 Abrir Panel de Pruebas

1. En el panel derecho, abre **"Test your agent"**
2. Asegúrate de que la conexión está activa

### 6.2 Pruebas Básicas

Prueba estas consultas:

#### Consultar Clientes
```
Tú: ¿Cuántos clientes tenemos?

Bot: Según Business Central, tienen [X] clientes registrados.
     ¿Te gustaría ver el listado o buscar un cliente específico?
```

#### Buscar Cliente Específico
```
Tú: Muéstrame información del cliente 10000

Bot: Aquí está la información del cliente 10000:
     
     📋 **The Cannon Group PLC**
     - Número: 10000
     - Dirección: 192 Market Square, Birmingham
     - Saldo: 0.00 EUR
     - Límite de crédito: 12,600.00 EUR
     
     ¿Necesitas más detalles?
```

#### Consultar Artículos
```
Tú: ¿Tenemos el artículo 1896-S en stock?

Bot: El artículo 1896-S (ATHENS Desk):
     - Inventario: 15 unidades
     - Precio unitario: 1,005.00 EUR
     - Ubicación: MAIN
     
     ¿Quieres crear un pedido con este artículo?
```

#### Revisar Pedidos
```
Tú: ¿Cuántos pedidos de venta tenemos pendientes?

Bot: Actualmente hay [X] pedidos de venta pendientes:
     
     1. Pedido 1001 - Cliente: The Cannon Group - 2,500 EUR
     2. Pedido 1002 - Cliente: Selangorian Ltd. - 1,200 EUR
     ...
     
     ¿Quieres ver los detalles de alguno?
```

### 6.3 Verificar el Activity Map

1. Después de cada consulta, observa el **Activity Map**
2. Deberías ver las llamadas al MCP Server
3. Verifica que la herramienta correcta fue invocada

```
Activity Map:
┌─────────────────────────────────────────────────────┐
│ [User] ──► [Agent Orchestration] ──► [MCP Server]  │
│                      │                     │        │
│                      │                     ▼        │
│                      │            bc_customers_read │
│                      │                     │        │
│                      ◄─────────────────────┘        │
│                      │                              │
│                      ▼                              │
│               [Response to User]                    │
└─────────────────────────────────────────────────────┘
```

---

## 🔧 Paso 7: Ajustar Configuración (si es necesario)

### Mejorar Descripciones de Tools

Si el agente no selecciona la herramienta correcta:

1. Ve a **Tools** → **Business Central MCP Server** → **Edit**
2. Mejora las descripciones:

```
Original: "Read customers"
Mejorado: "Consultar información de clientes de Business Central 
          incluyendo nombre, dirección, saldo y límite de crédito"
```

### Ajustar Instrucciones del Agente

Añade contexto sobre cuándo usar cada herramienta:

```markdown
## Uso de Herramientas

- Para información de clientes → usa bc_customers_read
- Para crear clientes → usa bc_customers_create (confirma primero)
- Para inventario y productos → usa bc_items_read
- Para pedidos de venta → usa bc_salesOrders_read/create
- Para facturas → usa bc_salesInvoices_read
```

---

## 🐛 Troubleshooting

### "Connection failed"
- Verifica credenciales de BC
- Verifica que el usuario tiene acceso al entorno
- Verifica que el MCP Server está habilitado en BC

### "No tools available"
- Verifica que la configuración MCP está **Active** en BC
- Verifica el nombre exacto en el campo **MCP Server Configuration**
- Haz clic en el icono de refresh (🔄) en la lista de herramientas
- Espera unos minutos para que sincronice

### "Tool execution failed"
- Verifica permisos del usuario en BC
- Revisa si la API requiere datos específicos
- Comprueba los logs en Activity Map

### "Agent doesn't use MCP tools"
- Verifica que Generative Orchestration está habilitado
- Mejora las descripciones de los tools
- Añade instrucciones más específicas

### "Resultados incorrectos"
- Verifica el entorno y compañía configurados
- Comprueba que los datos existen en BC
- Revisa los filtros aplicados

---

## ✅ Checklist del Módulo

- [ ] Encontré el BC MCP Server en Copilot Studio
- [ ] Creé la conexión con mis credenciales de BC
- [ ] Seleccioné el Environment correcto desde el dropdown
- [ ] Seleccioné la Company correcta desde el dropdown
- [ ] Configuré MCP Server Configuration (CONTOSO-SALES)
- [ ] Añadí el MCP Server al agente
- [ ] Verifiqué las herramientas disponibles
- [ ] Probé consulta de clientes
- [ ] Probé consulta de artículos
- [ ] Probé consulta de pedidos
- [ ] El Activity Map muestra las llamadas MCP

---

## 🎉 ¡Felicidades!

Tu agente ahora está conectado a Business Central. Puede:
- ✅ Consultar datos en vivo
- ✅ Crear nuevos registros
- ✅ Actualizar información
- ✅ Responder con datos reales

---

## ➡️ Siguiente Paso

Ahora exploraremos casos de uso más avanzados:

👉 [Módulo 5: Casos de Uso Avanzados](../modulo-05-casos-avanzados/README.md)
