# 🤖 Módulo 3: Crear el Agente en Microsoft Copilot Studio

> **Tiempo estimado**: 45 minutos

---

## 🎯 Objetivo

Crear un agente conversacional en Microsoft Copilot Studio que se conectará a Business Central.

---

## 📋 Lo Que Vamos a Crear

**Nombre del Agente**: Contoso BC Assistant

**Capacidades**:
- Responder preguntas sobre clientes
- Consultar inventario y artículos
- Ayudar con pedidos de venta
- Proporcionar información de facturas

---

## 🚀 Paso 1: Acceder a Copilot Studio

1. Abre tu navegador
2. Ve a [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
3. Inicia sesión con tu cuenta Microsoft 365
4. Selecciona el **entorno** correcto (mismo tenant que BC)

```
┌─────────────────────────────────────────────────────┐
│  Microsoft Copilot Studio                           │
│                                                     │
│  Environment: [Production        ▼]                 │
│                                                     │
│  [ + Create ]  [ Agents ]  [ Analytics ]            │
└─────────────────────────────────────────────────────┘
```

---

## 🆕 Paso 2: Crear Nuevo Agente

### 2.1 Iniciar Creación

1. Click en **"+ Create"** o **"Create an agent"**
2. Selecciona **"New agent"**

### 2.2 Configuración Básica

En el asistente de creación:

| Campo | Valor |
|-------|-------|
| **Name** | `Contoso BC Assistant` |
| **Description** | `Asistente de IA para consultas de Business Central. Ayuda con clientes, artículos, pedidos y facturas.` |
| **Language** | `Spanish (Spain)` o tu preferencia |

### 2.3 Instrucciones del Agente

En el campo **"Instructions"**, escribe:

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

## Tono
- Profesional pero amigable
- Directo y eficiente
- En español (España)

## Limitaciones
- No puedes eliminar registros
- No puedes modificar precios directamente
- Siempre respetas los permisos del usuario conectado
```

### 2.4 Crear el Agente

1. Click en **"Create"**
2. Espera a que se cree el agente (30-60 segundos)
3. Se abrirá el editor del agente

---

## ⚙️ Paso 3: Configurar el Agente

### 3.1 Verificar Configuración General

En la pestaña **"Overview"**:

| Configuración | Valor Recomendado |
|---------------|-------------------|
| **Orchestration** | Generative (Classic) |
| **Primary model** | GPT-4o o Claude Sonnet 4 |
| **Allow agent to use its own knowledge** | ✅ Enabled |

### 3.2 Habilitar Orquestación Generativa

> ⚠️ **Importante**: MCP requiere Generative Orchestration habilitado.

1. Ve a **Settings** → **Generative AI**
2. Verifica que **"Generative orchestration"** está habilitado
3. Si no está disponible, contacta a tu administrador

---

## 📝 Paso 4: Crear Topics de Conversación (Opcional)

Aunque MCP permite orquestación dinámica, podemos crear topics para casos específicos.

### Topic: Bienvenida

1. Ve a **Topics** → **+ New topic** → **From blank**
2. Nombre: `Greeting`
3. Trigger phrases:
   - "Hola"
   - "Buenos días"
   - "Ayuda"
   - "Qué puedes hacer"

4. Respuesta:
```
¡Hola! Soy Contoso BC Assistant. 

Puedo ayudarte con:
📊 **Clientes**: Consultar datos, saldos, crear nuevos
📦 **Artículos**: Buscar productos, verificar stock
🧾 **Pedidos**: Revisar pedidos, crear nuevos
💰 **Facturas**: Consultar facturas, estados de pago

¿En qué puedo ayudarte hoy?
```

### Topic: Despedida

1. Nombre: `Goodbye`
2. Trigger phrases:
   - "Adiós"
   - "Hasta luego"
   - "Gracias, eso es todo"

3. Respuesta:
```
¡Ha sido un placer ayudarte! Si necesitas algo más, aquí estaré.

¡Hasta pronto! 👋
```

---

## 🧪 Paso 5: Probar el Agente (Sin MCP aún)

### 5.1 Abrir Panel de Pruebas

1. En la esquina derecha, busca **"Test your agent"**
2. Click para abrir el panel de chat

### 5.2 Probar Conversación Básica

Prueba estas interacciones:

```
Tú: Hola
Bot: ¡Hola! Soy Contoso BC Assistant...

Tú: ¿Qué puedes hacer?
Bot: Puedo ayudarte con clientes, artículos, pedidos...

Tú: Adiós
Bot: ¡Ha sido un placer ayudarte!...
```

### 5.3 Verificar Respuestas

| Prueba | Resultado Esperado |
|--------|-------------------|
| Saludo | Respuesta de bienvenida |
| Pregunta general | Explicación de capacidades |
| Despedida | Mensaje de cierre |

---

## 📊 Paso 6: Revisar Estructura del Agente

Tu agente debería tener esta estructura:

```
Contoso BC Assistant
├── Overview
│   ├── Name: Contoso BC Assistant
│   ├── Description: Asistente de IA para BC
│   └── Instructions: [Configuradas]
├── Topics
│   ├── System Topics (automáticos)
│   ├── Greeting (creado)
│   └── Goodbye (creado)
├── Knowledge (vacío por ahora)
├── Tools (vacío - añadiremos MCP)
├── Actions (vacío)
└── Settings
    └── Generative AI: Enabled
```

---

## 💡 Mejores Prácticas para Instrucciones

### Sé Específico
```
❌ "Ayuda con Business Central"
✅ "Ayuda a consultar clientes, crear pedidos y revisar facturas en Business Central"
```

### Define Límites
```
✅ "No puedes eliminar registros"
✅ "Siempre confirma antes de crear datos"
```

### Establece Tono
```
✅ "Responde de forma profesional pero amigable"
✅ "Usa español de España"
```

### Incluye Ejemplos
```
✅ "Cuando muestres clientes, incluye: nombre, número, ciudad y saldo"
```

---

## 🐛 Troubleshooting

### "No puedo crear el agente"
- Verifica tu licencia de Copilot Studio
- Verifica que tienes créditos disponibles
- Intenta en otro entorno

### "Generative orchestration no disponible"
- Verifica la configuración del tenant
- Contacta al administrador de Power Platform
- Puede requerir licencia específica

### "El agente no responde como esperaba"
- Revisa las instrucciones
- Verifica que el idioma está configurado
- Prueba reformular las instrucciones

### "Error al guardar"
- Verifica conexión a internet
- Intenta guardar de nuevo
- Comprueba si hay errores de validación

---

## ✅ Checklist del Módulo

- [ ] Accedí a Copilot Studio
- [ ] Seleccioné el entorno correcto
- [ ] Creé el agente "Contoso BC Assistant"
- [ ] Configuré las instrucciones
- [ ] Verifiqué Generative Orchestration habilitado
- [ ] Creé topic de Greeting
- [ ] Creé topic de Goodbye
- [ ] Probé conversación básica
- [ ] El agente responde correctamente

---

## ➡️ Siguiente Paso

El agente está creado. Ahora lo conectaremos al MCP Server de Business Central:

👉 [Módulo 4: Conectar Agente a BC MCP](../modulo-04-conectar-mcp/README.md)
