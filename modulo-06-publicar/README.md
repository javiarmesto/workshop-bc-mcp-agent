# 🚀 Módulo 6: Publicar y Desplegar el Agente

> **Tiempo estimado**: 20 minutos

---

## 🎯 Objetivo

Publicar el agente y hacerlo disponible para usuarios finales a través de diferentes canales.

---

## 📋 Canales de Despliegue Disponibles

| Canal | Descripción | Caso de Uso |
|-------|-------------|-------------|
| **Microsoft Teams** | Chat dentro de Teams | Uso interno corporativo |
| **Microsoft 365 Copilot** | Integrado en M365 Copilot | Usuarios con licencia Copilot |
| **Web** | Widget embebido | Portal de clientes |
| **Custom App** | API directa | Aplicaciones personalizadas |

---

## ✅ Paso 1: Verificar el Agente Antes de Publicar

### Checklist de Calidad

Antes de publicar, verifica:

- [ ] **Funcionalidad**: Todas las consultas funcionan
- [ ] **Respuestas**: Son claras y profesionales
- [ ] **Errores**: Se manejan correctamente
- [ ] **Permisos**: Están correctamente configurados
- [ ] **Instrucciones**: Son completas y claras

### Prueba Final

Ejecuta estas pruebas:

```
✅ Consulta de clientes
✅ Consulta de artículos  
✅ Consulta de pedidos
✅ Creación de pedido (con confirmación)
✅ Manejo de errores
✅ Respuestas en español correcto
```

---

## 📤 Paso 2: Publicar el Agente

### 2.1 Acceder a Publicación

1. En Copilot Studio, abre tu agente
2. En el menú de navegación, selecciona **"Publish"**

### 2.2 Confirmar Publicación

1. Revisa el resumen de cambios
2. Click en **"Publish"**
3. Espera a que se complete (1-2 minutos)

```
┌─────────────────────────────────────────────────────┐
│  Publish Contoso BC Assistant                       │
├─────────────────────────────────────────────────────┤
│                                                     │
│  This will publish your agent to all channels.     │
│                                                     │
│  Changes to publish:                                │
│  ├── Updated instructions                          │
│  ├── Added MCP Server connection                   │
│  └── New topics                                    │
│                                                     │
│  [Cancel]                    [Publish]             │
└─────────────────────────────────────────────────────┘
```

---

## 💬 Paso 3: Desplegar en Microsoft Teams

### 3.1 Configurar Canal de Teams y Microsoft 365 Copilot

1. Ve a **"Channels"** en el menú superior
2. Selecciona **"Teams and Microsoft 365 Copilot"**
3. Configura las opciones de disponibilidad
4. Click en **"Add channel"**

### 3.2 Opciones de Disponibilidad

| Opción | Descripción |
|--------|-------------|
| **Make agent available in Microsoft 365 Copilot** | Disponible en M365 Copilot además de Teams |
| **Share link** | Enlace directo para compartir con usuarios |
| **Show to the organization** | Enviar para aprobación del administrador |

### 3.3 Compartir con Usuarios

1. Copia el **link de instalación**
2. Comparte con los usuarios
3. Los usuarios pueden añadir el bot a Teams

```
Link de instalación:
(Se obtiene desde Copilot Studio > Channels > Teams and Microsoft 365 Copilot > "Copy link")
```

> 📝 **Nota**: Solo usuarios con acceso compartido al agente pueden usar el link de instalación

---

## 🌐 Paso 4: Configurar Disponibilidad en Microsoft 365 Copilot

> ⚠️ Requiere licencia de Microsoft 365 Copilot
> 📝 **Nota**: El canal de Teams and Microsoft 365 Copilot es unificado

### 4.1 Verificar Disponibilidad

Si marcaste **"Make agent available in Microsoft 365 Copilot"** al configurar el canal, el agente ya está disponible en M365 Copilot.

### 4.2 Uso en M365 Copilot

Una vez desplegado, los usuarios pueden:
1. Abrir Microsoft 365 Copilot Chat
2. Escribir **@** y seleccionar el agente
3. Interactuar directamente desde Copilot

> ⚠️ **Importante**: El agente requiere aprobación del administrador en Microsoft 365 admin center antes de estar disponible para toda la organización

---

## 🌍 Paso 5: Desplegar en Web (Widget)

### 5.1 Configurar Canal Web

1. Ve a **"Channels"** → **"Custom website"**
2. Obtén el código de embed

### 5.2 Código de Integración

El código completo incluye el token endpoint:

```html
<!-- Copilot Studio Web Widget -->
<!-- Debes obtener el token endpoint desde Copilot Studio -->
<!-- Ver: https://learn.microsoft.com/microsoft-copilot-studio/customize-default-canvas#retrieve-the-token-endpoint-for-your-agent -->
<iframe 
  src="https://web.powerva.microsoft.com/environments/[env]/bots/[bot]/webchat"
  style="width: 100%; height: 500px; border: none;">
</iframe>
```

> 📝 **Nota**: Para seguridad en producción, se recomienda configurar autenticación y usar el token endpoint

### 5.3 Personalización

Puedes personalizar:
- Colores del widget
- Mensaje de bienvenida
- Posición (flotante/embebido)
- Tamaño

---

## 🔐 Paso 6: Configurar Permisos de Acceso

### Quién Puede Usar el Agente

1. Ve a **"Settings"** → **"Security"**
2. Configura autenticación:

| Opción | Descripción |
|--------|-------------|
| **Authenticate with Microsoft** | Autenticación automática con Microsoft Entra ID (por defecto para Teams y M365) |
| **Authenticate manually** | Configuración manual de autenticación (para otros canales) |
| **No authentication** | Cualquiera puede usar (⚠️ NO recomendado para BC) |

### Recomendación para Business Central

```
✅ Usar "Authenticate with Microsoft"
✅ Autenticación automática con Microsoft Entra ID
✅ Mismo tenant que Business Central
✅ El usuario hereda permisos de BC vía OAuth 2.0
```

> ⚠️ **Importante**: Si seleccionas "No authentication", el agente no puede usar herramientas MCP que requieren credenciales de usuario

---

## 📊 Paso 7: Monitorear Uso

### Analytics en Copilot Studio

1. Ve a **"Analytics"** en el menú
2. Revisa métricas:

| Métrica | Descripción |
|---------|-------------|
| **Total Sessions** | Número total de sesiones de analytics |
| **Engagement Rate** | % de sesiones donde se activó un topic personalizado |
| **Resolution Rate** | % de sesiones engaged que se resolvieron |
| **Escalation Rate** | % de sesiones engaged que se escalaron |
| **Abandon Rate** | % de sesiones engaged que se abandonaron |
| **CSAT** | Puntuación promedio de satisfacción del cliente |

### Métricas Clave a Monitorear

```
📈 Conversaciones diarias
📊 Topics más usados
⚠️ Errores frecuentes
⭐ Satisfacción de usuarios
```

---

## 🔧 Paso 8: Mantenimiento Continuo

### Actualizar el Agente

1. Realiza cambios en Copilot Studio
2. Prueba en el panel de Test
3. Publica de nuevo

### Cambios que Requieren Republicar

- ✅ Cambios en instrucciones
- ✅ Nuevos topics
- ✅ Cambios en tools
- ❌ Cambios en datos de BC (automático vía MCP)

### Ciclo de Mejora

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│    Analizar  →  Mejorar  →  Probar  →  Publicar   │
│       ▲                                    │        │
│       └────────────────────────────────────┘        │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 🎉 ¡Workshop Completado!

### Lo Que Has Logrado

✅ Configurado el MCP Server en Business Central  
✅ Creado un agente en Copilot Studio  
✅ Conectado el agente a datos en vivo de BC  
✅ Implementado casos de uso avanzados  
✅ Publicado y desplegado el agente  

### Capacidades del Agente

| Área | Capacidades |
|------|-------------|
| **Clientes** | Consultar, crear, actualizar |
| **Artículos** | Consultar, verificar stock |
| **Pedidos** | Consultar, crear |
| **Facturas** | Consultar, analizar vencimientos |
| **Proveedores** | Consultar |

---

## 📚 Recursos para Seguir Aprendiendo

### Documentación Oficial
- [BC MCP Server Configuration](https://learn.microsoft.com/dynamics365/business-central/dev-itpro/ai/configure-mcp-server)
- [Create Agents with Copilot Studio](https://learn.microsoft.com/dynamics365/business-central/dev-itpro/ai/create-agent-in-copilot-studio)
- [MCP in Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/agent-extend-action-mcp)

### Comunidad
- [Business Central Community](https://community.dynamics.com/business)
- [Copilot Studio Community](https://powerusers.microsoft.com/t5/Microsoft-Copilot-Studio/ct-p/PVACommunity)

### Próximos Pasos Sugeridos
1. Añadir más APIs personalizadas al MCP Server
2. Integrar con Power Automate para workflows complejos
3. Crear agentes especializados por departamento
4. Implementar feedback de usuarios

---

## 💡 Ideas para Expandir

### Agentes Especializados

| Agente | Foco | APIs |
|--------|------|------|
| **Sales Assistant** | Ventas y clientes | Customers, Sales Orders, Items |
| **Purchase Assistant** | Compras | Vendors, Purchase Orders, Items |
| **Finance Assistant** | Finanzas | G/L Entries, Bank Accounts, Invoices |
| **Warehouse Assistant** | Almacén | Items, Warehouses, Transfers |

### Integraciones Adicionales

- 📧 Email automático para recordatorios
- 📅 Calendarios para seguimiento
- 📊 Power BI para dashboards
- 🔔 Alertas proactivas

---

## ✅ Checklist Final del Workshop

- [ ] MCP Server configurado en Business Central
- [ ] Agente creado en Copilot Studio
- [ ] Conexión MCP establecida y funcionando
- [ ] Pruebas de todos los casos de uso
- [ ] Agente publicado
- [ ] Canal de Teams configurado
- [ ] Permisos de acceso definidos
- [ ] Analytics revisados

---

## 🙏 ¡Gracias!

Gracias por completar este workshop. Tu agente **Contoso BC Assistant** está ahora listo para ayudar a usuarios a interactuar con Business Central usando lenguaje natural.

**¿Preguntas?** Abre un issue en el repositorio o contacta al instructor.

---

👉 [Volver al Inicio del Workshop](../README.md)
