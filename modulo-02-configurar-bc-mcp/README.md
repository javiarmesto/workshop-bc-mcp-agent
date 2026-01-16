# ⚙️ Módulo 2: Configurar Business Central MCP Server

> **Tiempo estimado**: 30 minutos

---

## 🎯 Objetivo

Configurar el MCP Server en Business Central para exponer las APIs necesarias para nuestro agente.

---

## 📋 Lo Que Vamos a Configurar

Crearemos una configuración MCP llamada **"Contoso Sales Agent"** con acceso a:

| Entidad | Operaciones | Propósito |
|---------|-------------|-----------|
| Customers | Read, Create, Update | Gestión de clientes |
| Items | Read | Consulta de artículos |
| Sales Orders | Read, Create | Gestión de pedidos |
| Sales Invoices | Read | Consulta de facturas |
| Vendors | Read | Consulta de proveedores |

---

## 🔧 Paso 1: Abrir Configuración MCP

1. En Business Central, abre la **búsqueda** (🔍 o Alt+Q)
2. Escribe: **"Model Context Protocol (MCP) Server Configurations"**
3. Selecciona la página

![MCP Server Configurations](./images/mcp-config-search.png)

---

## 🆕 Paso 2: Crear Nueva Configuración

1. Click en **"New"** (o Ctrl+N)
2. Se abre la página de configuración

### Campos Principales

| Campo | Valor | Descripción |
|-------|-------|-------------|
| **Code** | `CONTOSO-SALES` | Identificador único |
| **Description** | `Contoso Sales Agent Configuration` | Descripción legible |
| **Active** | `Yes` | Activa la configuración |
| **Dynamic Tool Mode** | `No` | Usaremos modo estático |

```
┌─────────────────────────────────────────────────────┐
│  MCP Server Configuration                           │
├─────────────────────────────────────────────────────┤
│  Code:           [CONTOSO-SALES              ]      │
│  Description:    [Contoso Sales Agent Config ]      │
│  Active:         [✓]                                │
│  Dynamic Mode:   [ ]                                │
└─────────────────────────────────────────────────────┘
```

---

## 📦 Paso 3: Añadir APIs como Tools

### Opción A: Añadir APIs Estándar Automáticamente

1. En la sección **"Tools"**, click en **"Add All Standard APIs as Tools"**
2. Se añaden todas las APIs de BC automáticamente
3. Elimina las que no necesites

### Opción B: Añadir APIs Manualmente (Recomendado para el workshop)

Click en **"New Line"** en la sección Tools y añade cada API.
> ⚠️ **Importante**: Asegúrate de usar los IDs de la **API v2.0** (rango 30000+), NO las páginas de UI (rango 20-50).

#### Tool 1: Customers
| Campo | Valor |
|-------|-------|
| API Page ID | 30009 |
| API Page Name | APIV2 - Customers |
| Read | ✅ |
| Create | ✅ |
| Modify | ✅ |
| Delete | ❌ |

#### Tool 2: Items
| Campo | Valor |
|-------|-------|
| API Page ID | 30008 |
| API Page Name | APIV2 - Items |
| Read | ✅ |
| Create | ❌ |
| Modify | ❌ |
| Delete | ❌ |

#### Tool 3: Sales Orders
| Campo | Valor |
|-------|-------|
| API Page ID | 30028 |
| API Page Name | APIV2 - Sales Orders |
| Read | ✅ |
| Create | ✅ |
| Modify | ❌ |
| Delete | ❌ |

#### Tool 4: Sales Invoices
| Campo | Valor |
|-------|-------|
| API Page ID | 30012 |
| API Page Name | APIV2 - Sales Invoices |
| Read | ✅ |
| Create | ❌ |
| Modify | ❌ |
| Delete | ❌ |

#### Tool 5: Vendors
| Campo | Valor |
|-------|-------|
| API Page ID | 30010 |
| API Page Name | APIV2 - Vendors |
| Read | ✅ |
| Create | ❌ |
| Modify | ❌ |
| Delete | ❌ |

---

## 📝 Paso 4: Verificar la Configuración

Tu configuración debería verse así:

```
┌─────────────────────────────────────────────────────────────────┐
│  MCP Server Configuration: CONTOSO-SALES                        │
├─────────────────────────────────────────────────────────────────┤
│  General                                                        │
│  ├── Code: CONTOSO-SALES                                        │
│  ├── Description: Contoso Sales Agent Configuration             │
│  ├── Active: Yes                                                │
│  └── Dynamic Tool Mode: No                                      │
├─────────────────────────────────────────────────────────────────┤
│  Tools                                                          │
│  ┌──────────────────────┬──────┬────────┬────────┬────────┐    │
│  │ API Page             │ Read │ Create │ Modify │ Delete │    │
│  ├──────────────────────┼──────┼────────┼────────┼────────┤    │
│  │ Customers (30009)    │  ✅  │   ✅   │   ✅   │   ❌   │    │
│  │ Items (30008)        │  ✅  │   ❌   │   ❌   │   ❌   │    │
│  │ Sales Orders (30049) │  ✅  │   ✅   │   ❌   │   ❌   │    │
│  │ Sales Invoices (30048│  ✅  │   ❌   │   ❌   │   ❌   │    │
│  │ Vendors (30010)      │  ✅  │   ❌   │   ❌   │   ❌   │    │
│  └──────────────────────┴──────┴────────┴────────┴────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✅ Paso 5: Guardar y Activar

1. Click en **"Close"** o guarda con Ctrl+S
2. Verifica que **"Active"** está marcado
3. La configuración está lista

---


## 📊 Herramientas Generadas

Con nuestra configuración, el MCP Server expondrá estas herramientas:

```
Herramientas Disponibles:
├── bc_customers_read       → Consultar clientes
├── bc_customers_create     → Crear cliente
├── bc_customers_update     → Actualizar cliente
├── bc_items_read           → Consultar artículos
├── bc_salesOrders_read     → Consultar pedidos
├── bc_salesOrders_create   → Crear pedido
├── bc_salesInvoices_read   → Consultar facturas
└── bc_vendors_read         → Consultar proveedores
```

---

## 🔐 Consideraciones de Seguridad

### Permisos del MCP Server

| Permission Set | Capacidad |
|----------------|-----------|
| MCP - ADMIN | Configurar el servidor |
| MCP - USER | Usar el servidor (implícito) |

### Permisos de Datos

El agente **solo puede acceder** a datos que el usuario conectado puede ver:

```
Usuario: Juan (Vendedor Región Norte)
├── Clientes Región Norte: ✅ Visible
├── Clientes Región Sur: ❌ No visible
└── El agente solo ve clientes del Norte
```

---

## 🐛 Troubleshooting

### "No puedo crear la configuración"
- Verifica que tienes `MCP - ADMIN` permission set
- Verifica que el feature está habilitado

### "API Page ID no existe"
- Usa los IDs estándar de BC
- Verifica que la API está publicada en tu entorno

### "La configuración no aparece en Copilot Studio"
- Verifica que "Enabled" está marcado
- Espera unos minutos (puede tardar en sincronizar)
- Verifica conectividad de red

### IDs de API Pages Comunes

| Entidad | API Page ID |
|---------|-------------|
| Customers | 30 |
| Items | 31 |
| Vendors | 32 |
| Sales Orders | 48 |
| Sales Invoices | 44 |
| Purchase Orders | 49 |
| G/L Entries | 36 |

---

## ✅ Checklist del Módulo
Active" está marcado
- Espera unos minutos (puede tardar en sincronizar)
- Verifica conectividad de red

### IDs de API Pages Comunes (v2.0)

| Entidad | API Page ID |
|---------|-------------|
| Customers | 30009 |
| Items | 30008 |
| Vendors | 30010 |
| Sales Orders | 30049 |
| Sales Invoices | 30048 |
| Purchase Orders | 30050 |
| G/L Entries | 30017onfigurado. Ahora vamos a crear el agente en Copilot Studio:

👉 [Módulo 3: Crear el Agente en Copilot Studio](../modulo-03-crear-agente/README.md)
Active