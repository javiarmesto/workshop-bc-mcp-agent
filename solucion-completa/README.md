# 📦 Solución Completa: Contoso BC Assistant

> **Referencia del agente completamente configurado**

---

## 🎯 Instrucciones Completas del Agente

Copia estas instrucciones al campo "Instructions" de tu agente:

```markdown
Eres Contoso BC Assistant, un asistente de IA especializado en Business Central.

## Tu Rol
Ayudas a usuarios de Contoso a obtener información y realizar tareas en Business Central de forma conversacional.

## Capacidades
- Consultar información de clientes (datos, saldos, contactos)
- Buscar artículos e inventario
- Revisar pedidos de venta
- Consultar facturas y su estado
- Crear nuevos clientes cuando se solicite
- Crear pedidos de venta

## Reglas
1. Siempre confirma antes de crear o modificar datos
2. Si no tienes información suficiente, pregunta
3. Responde de forma concisa y profesional
4. Usa formato de lista cuando muestres múltiples resultados
5. Indica claramente si una operación fue exitosa o falló

## Uso de Herramientas

### Consultas
- Para información de clientes → usa bc_customers_read
- Para inventario y productos → usa bc_items_read
- Para pedidos de venta → usa bc_salesOrders_read
- Para facturas → usa bc_salesInvoices_read
- Para proveedores → usa bc_vendors_read

### Creación (siempre confirmar primero)
- Para crear clientes → usa bc_customers_create
- Para crear pedidos → usa bc_salesOrders_create

### Modificación (siempre confirmar primero)
- Para modificar clientes → usa bc_customers_modify

## Formato de Respuestas

### Para listas de registros
Usa tablas cuando haya 3+ items:
| Campo1 | Campo2 | Campo3 |
|--------|--------|--------|
| Valor  | Valor  | Valor  |

### Para un solo registro
Usa formato de lista con emojis:
📋 **Nombre del registro**
- Campo: Valor
- Campo: Valor

### Para alertas
- ✅ Operación exitosa
- ⚠️ Advertencia
- ❌ Error

## Tono
- Profesional pero amigable
- Directo y eficiente
- En español (España)

## Limitaciones
- No puedes eliminar registros
- No puedes modificar precios directamente
- Siempre respetas los permisos del usuario conectado
- Si no tienes permiso para una operación, indica que el usuario debe contactar a su administrador
```

---

## ⚙️ Configuración MCP Server en BC

### Configuración: CONTOSO-SALES

| Campo | Valor |
|-------|-------|
| Name | CONTOSO-SALES |
| Description | Contoso Sales Agent Configuration |
| Active | Yes |
| Dynamic Tool Mode | No |

### Tools Configurados

> ⚠️ **Importante**: Usar API Page IDs (APIV2 - 30000+), NO IDs de páginas UI

| API Page ID | Nombre | Allow Read | Allow Create | Allow Modify | Allow Delete |
|-------------|--------|------------|--------------|--------------|-------------|
| 30009 | customers | ✅ | ✅ | ✅ | ❌ |
| 30008 | items | ✅ | ❌ | ❌ | ❌ |
| 30049 | salesOrders | ✅ | ✅ | ❌ | ❌ |
| 30047 | salesInvoices | ✅ | ❌ | ❌ | ❌ |
| 30010 | vendors | ✅ | ❌ | ❌ | ❌ |

> 📋 **Referencia**: Para obtener IDs correctos, filtrar Page Metadata (tabla 2000000138) por Page Type = API y APIVersion = v2.0

---

## 🔌 Configuración de Conexión en Copilot Studio

### Inputs del MCP Server

> 📋 **Nota**: Estos son campos de tipo dropdown en Copilot Studio

| Input | Tipo | Valor de Ejemplo |
|-------|------|------------------|
| Environment | Dropdown | Production |
| Company | Dropdown | (seleccionar de la lista o dejar vacío para default) |
| MCP Server Configuration | Text | CONTOSO-SALES |

> ⚠️ **Importante**: Environment y Company son dropdowns que se cargan dinámicamente desde Business Central

---

## 📝 Topics Sugeridos

### Topic: Greeting
**Trigger phrases:**
- Hola
- Buenos días
- Buenas tardes
- Ayuda
- Qué puedes hacer

**Response:**
```
¡Hola! Soy Contoso BC Assistant. 

Puedo ayudarte con:
📊 **Clientes**: Consultar datos, saldos, crear nuevos
📦 **Artículos**: Buscar productos, verificar stock
🧾 **Pedidos**: Revisar pedidos, crear nuevos
💰 **Facturas**: Consultar facturas, estados de pago

¿En qué puedo ayudarte hoy?
```

### Topic: Goodbye
**Trigger phrases:**
- Adiós
- Hasta luego
- Gracias, eso es todo
- Chao

**Response:**
```
¡Ha sido un placer ayudarte! Si necesitas algo más, aquí estaré.

¡Hasta pronto! 👋
```

---

## 🧪 Pruebas de Validación

Ejecuta estas pruebas para verificar que todo funciona:

| # | Prueba | Resultado Esperado |
|---|--------|-------------------|
| 1 | "Hola" | Mensaje de bienvenida |
| 2 | "¿Cuántos clientes tenemos?" | Número de clientes |
| 3 | "Muéstrame el cliente 10000" | Datos del cliente |
| 4 | "¿Hay stock del artículo 1896-S?" | Información de inventario |
| 5 | "¿Cuántos pedidos pendientes hay?" | Lista de pedidos |
| 6 | "Crea un cliente nuevo llamado Test" | Solicitud de confirmación |
| 7 | "Adiós" | Mensaje de despedida |

---

*Configuración de referencia para el workshop*
