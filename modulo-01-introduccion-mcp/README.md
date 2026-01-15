# 🧠 Módulo 1: Introducción a Model Context Protocol (MCP)

> **Tiempo estimado**: 20 minutos

---

## 🎯 Objetivo

Entender qué es MCP, por qué es importante, y cómo Business Central lo implementa.

---

## 📖 ¿Qué es Model Context Protocol?

### Definición Simple

**MCP** (Model Context Protocol) es un **estándar abierto** que permite a las aplicaciones de IA conectarse con fuentes de datos y herramientas externas de forma estandarizada.

> 💡 **Analogía**: MCP es como el **USB-C para aplicaciones de IA**. Así como USB-C proporciona una forma estándar de conectar dispositivos, MCP proporciona una forma estándar de conectar modelos de IA con datos y servicios.

### Antes de MCP

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Agente 1  │     │   Agente 2  │     │   Agente 3  │
└──────┬──────┘     └──────┬──────┘     └──────┬──────┘
       │                   │                   │
       │ Conector A        │ Conector B        │ Conector C
       │ Conector B        │ Conector D        │ Conector A
       │ Conector C        │ Conector E        │ Conector F
       ▼                   ▼                   ▼
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Sistema A  │     │  Sistema B  │     │  Sistema C  │
└─────────────┘     └─────────────┘     └─────────────┘

❌ Cada agente necesita múltiples conectores personalizados
❌ Mantenimiento complejo
❌ Duplicación de esfuerzo
```

### Con MCP

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Agente 1  │     │   Agente 2  │     │   Agente 3  │
└──────┬──────┘     └──────┬──────┘     └──────┬──────┘
       │                   │                   │
       └───────────────────┼───────────────────┘
                           │
                           │ MCP Protocol
                           ▼
              ┌─────────────────────────┐
              │       MCP Server        │
              │  (Business Central)     │
              └────────────┬────────────┘
                           │
                           ▼
              ┌─────────────────────────┐
              │   Business Central      │
              │   Datos y Lógica        │
              └─────────────────────────┘

✅ Un solo protocolo estándar
✅ Autodescubrimiento de capacidades
✅ Actualizaciones automáticas
✅ Seguridad centralizada
```

---

## 🔧 Componentes de MCP

### 1. MCP Server (Servidor)

El servidor **expone** datos y funcionalidades. En nuestro caso:
- **Business Central MCP Server** expone entidades como clientes, artículos, pedidos

**Capacidades del servidor:**
- **Tools (Herramientas)**: Funciones que el agente puede ejecutar
- **Resources (Recursos)**: Datos que el agente puede leer
- **Prompts**: Plantillas de prompts predefinidas

### 2. MCP Client (Cliente)

El cliente **consume** los servicios del servidor. Ejemplos:
- **Copilot Studio**: Nuestro cliente principal
- **GitHub Copilot** (VS Code)
- **Claude Desktop**
- **Agentes personalizados**

### 3. Transport (Transporte)

Cómo se comunican cliente y servidor:
- **Streamable** (recomendado): Comunicación en streaming
- **SSE** (deprecated): Server-Sent Events (obsoleto desde agosto 2025)

---

## 🏢 MCP Server de Business Central

### ¿Qué Expone?

El BC MCP Server expone las **APIs de Business Central** como herramientas MCP:

| API Page | Tool MCP | Operaciones |
|----------|----------|-------------|
| customers | bc_customers_read/create/update/delete | CRUD clientes |
| items | bc_items_read | Lectura artículos |
| salesOrders | bc_salesOrders_read/create | Pedidos venta |
| salesInvoices | bc_salesInvoices_read | Facturas |
| vendors | bc_vendors_read | Proveedores |
| ... | ... | ... |

### Modos de Operación

#### Modo Estático (por defecto)
- Cada API page se convierte en herramientas específicas
- El maker selecciona qué herramientas usar
- Más control, menos flexibilidad

```
bc_customers_read
bc_customers_create
bc_items_read
bc_salesOrders_read
...
```

#### Modo Dinámico
- El agente descubre herramientas en runtime
- Usa 3 tools genéricos:
  - `bc_actions_search`: Busca herramientas disponibles
  - `bc_actions_describe`: Describe una herramienta
  - `bc_actions_invoke`: Ejecuta una herramienta
- Más flexible, menos predecible

---

## 🔐 Seguridad en MCP

### Autenticación
- **OAuth 2.0**: El usuario se autentica contra Azure AD
- **Tokens**: El agente actúa en nombre del usuario
- **Refresh**: Tokens se renuevan automáticamente

### Autorización
- El agente **hereda los permisos** del usuario conectado
- Si el usuario no puede ver clientes en BC, el agente tampoco
- Los permission sets de BC se respetan completamente

### Ejemplo
```
Usuario: María (Vendedor)
├── Puede ver clientes: ✅
├── Puede crear pedidos: ✅
├── Puede ver costos: ❌
└── Puede modificar precios: ❌

El agente para María:
├── Puede consultar clientes: ✅
├── Puede crear pedidos: ✅
├── Puede ver costos: ❌ (heredado)
└── Puede modificar precios: ❌ (heredado)
```

---

## 📊 MCP vs Alternativas

### Conector de Business Central

| Aspecto | Conector BC | MCP Server |
|---------|-------------|------------|
| **Configuración** | Por cada acción | Una vez |
| **Descubrimiento** | Manual | Automático |
| **Actualizaciones** | Manuales | Automáticas |
| **Flexibilidad** | Limitada | Alta |
| **Complejidad** | Media | Baja |

### Power Automate

| Aspecto | Power Automate | MCP Server |
|---------|----------------|------------|
| **Tipo** | Flujos definidos | Dinámico |
| **Mantenimiento** | Alto | Bajo |
| **Lenguaje natural** | No | Sí |
| **Caso de uso** | Automatización | Conversación |

### Cuándo usar cada uno

- **Conector BC**: Acciones simples y predefinidas
- **Power Automate**: Procesos complejos multi-paso
- **MCP Server**: Interacción conversacional dinámica

---

## 🎓 Conceptos Clave para el Workshop

### 1. Tool (Herramienta)
Una función que el agente puede ejecutar.
```
Tool: bc_customers_read
├── Input: filtro (opcional)
└── Output: lista de clientes
```

### 2. Configuration (Configuración)
Define qué APIs exponer y qué operaciones permitir.
```
Configuration: "Contoso Sales Agent"
├── customers: read, create
├── items: read
├── salesOrders: read, create
└── salesInvoices: read
```

### 3. Connection (Conexión)
El enlace autenticado entre Copilot Studio y BC.
```
Connection
├── User: maria@contoso.com
├── Environment: Production
├── Company: CRONUS España S.A.
└── Status: Connected ✅
```

---

## 💡 Beneficios para Business Central

### Para Usuarios
- 🗣️ Interactúan con BC usando lenguaje natural
- ⚡ Obtienen información más rápido
- 📱 Acceden desde Teams, web, móvil

### Para IT/Desarrolladores
- 🔧 Menos código personalizado
- 🔄 Actualizaciones automáticas
- 🔐 Seguridad centralizada

### Para el Negocio
- 💰 Menor costo de desarrollo
- 📈 Mayor adopción de BC
- 🚀 Innovación más rápida

---

## ✅ Resumen del Módulo

| Concepto | Descripción |
|----------|-------------|
| **MCP** | Protocolo estándar para conectar IA con datos |
| **MCP Server** | Expone datos y funciones (Business Central) |
| **MCP Client** | Consume los servicios (Copilot Studio) |
| **Tools** | Funciones ejecutables por el agente |
| **Seguridad** | Basada en permisos del usuario de BC |

---

## ➡️ Siguiente Paso

Ahora que entiendes MCP, vamos a configurar el servidor en Business Central:

👉 [Módulo 2: Configurar BC MCP Server](../modulo-02-configurar-bc-mcp/README.md)
