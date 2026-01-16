# 🤖 Workshop: Construye un Agente de IA con Business Central MCP

> **Conecta Microsoft Copilot Studio con datos en vivo de Business Central usando Model Context Protocol**

[![Business Central](https://img.shields.io/badge/Business%20Central-v27+-blue)](https://learn.microsoft.com/dynamics365/business-central/)
[![Copilot Studio](https://img.shields.io/badge/Copilot%20Studio-MCP%20GA-green)](https://copilotstudio.microsoft.com)
[![MCP](https://img.shields.io/badge/MCP-Protocol-purple)](https://modelcontextprotocol.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 Descripción

Este workshop te guía paso a paso para construir un **agente de IA conversacional** que se conecta en tiempo real a datos de Business Central usando el protocolo MCP (Model Context Protocol).

**Inspirado en**: [Microsoft Copilot Studio Labs - Contoso Agent with Dataverse MCP](https://learn.microsoft.com/power-apps/maker/data-platform/data-platform-mcp-copilot-studio)

**Adaptado para**: Microsoft Dynamics 365 Business Central

---

## 🎯 ¿Qué Vas a Construir?

Un agente llamado **"Contoso BC Assistant"** que puede:

| Capacidad | Ejemplo de Interacción |
|-----------|------------------------|
| 📊 **Consultar clientes** | "¿Cuál es el saldo del cliente 10000?" |
| 📦 **Buscar artículos** | "Muéstrame los artículos con stock bajo" |
| 🧾 **Revisar pedidos** | "¿Cuántos pedidos pendientes hay hoy?" |
| 💰 **Analizar facturas** | "Lista las facturas vencidas de más de 30 días" |
| ✏️ **Crear registros** | "Crea un nuevo cliente llamado Fabrikam" |
| 🔄 **Modificar datos** | "Modifica el límite de crédito del cliente 20000" |

Todo esto usando **lenguaje natural** y con **datos en vivo** de Business Central.

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────────────────────┐
│                    Usuario Final                             │
│         (Teams, Web, M365 Copilot, Custom App)              │
└─────────────────────┬───────────────────────────────────────┘
                      │ Lenguaje Natural
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                 Microsoft Copilot Studio                     │
│    ┌─────────────────────────────────────────────────┐      │
│    │              Contoso BC Assistant                │      │
│    │  • Instrucciones del agente                      │      │
│    │  • Orquestación generativa                       │      │
│    │  • Flujos de conversación                        │      │
│    └─────────────────────┬───────────────────────────┘      │
└─────────────────────────┬───────────────────────────────────┘
                          │ MCP Protocol
                          ▼
┌─────────────────────────────────────────────────────────────┐
│           Business Central MCP Server                        │
│    ┌─────────────────────────────────────────────────┐      │
│    │              Herramientas (Tools)                │      │
│    │  • bc_customers_read                             │      │
│    │  • bc_items_read                                 │      │
│    │  • bc_salesOrders_read/create                    │      │
│    │  • bc_salesInvoices_read                         │      │
│    │  • bc_vendors_read                               │      │
│    │  • bc_actions_search (modo dinámico)             │      │
│    └─────────────────────┬───────────────────────────┘      │
└─────────────────────────┬───────────────────────────────────┘
                          │ OData / API
                          ▼
┌─────────────────────────────────────────────────────────────┐
│            Microsoft Dynamics 365 Business Central           │
│                                                              │
│    Clientes │ Artículos │ Pedidos │ Facturas │ Proveedores  │
└─────────────────────────────────────────────────────────────┘
```

---

## 📚 Módulos del Workshop

| Módulo | Descripción | Duración |
|--------|-------------|----------|
| **Módulo 0** | [Preparación del Entorno](./modulo-00-preparacion/README.md) | 15 min |
| **Módulo 1** | [Introducción a MCP](./modulo-01-introduccion-mcp/README.md) | 20 min |
| **Módulo 2** | [Configurar BC MCP Server](./modulo-02-configurar-bc-mcp/README.md) | 30 min |
| **Módulo 3** | [Crear el Agente en Copilot Studio](./modulo-03-crear-agente/README.md) | 45 min |
| **Módulo 4** | [Conectar Agente a BC MCP](./modulo-04-conectar-mcp/README.md) | 30 min |
| **Módulo 5** | [Casos de Uso Avanzados](./modulo-05-casos-avanzados/README.md) | 45 min |
| **Módulo 6** | [Publicar y Desplegar](./modulo-06-publicar/README.md) | 20 min |

**Duración total**: ~3.5 horas

---

## ✅ Prerequisitos

### Licencias y Acceso
- [ ] Licencia de Business Central (Essential o Premium)
- [ ] Licencia de Copilot Studio con capacidad disponible
- [ ] Acceso de administrador al entorno de BC (para configurar MCP Server)
- [ ] Cuenta Microsoft 365 en el mismo tenant que Business Central
- [ ] (Opcional) Licencia Microsoft 365 Copilot para usuarios finales si se despliega en ese canal

### Conocimientos Previos
- [ ] Familiaridad básica con Business Central
- [ ] Conceptos básicos de APIs REST
- [ ] No se requiere experiencia previa con IA/MCP

### Entorno Técnico
- [ ] Business Central versión 27 (2025 release wave 2) o superior
- [ ] Feature Management: "Feature: Enable MCP Server access" activado en BC
- [ ] Navegador moderno (Microsoft Edge o Chrome)
- [ ] Acceso a [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)

---

## 🚀 Inicio Rápido

### Opción A: Seguir los módulos en orden (recomendado)
```bash
# Empezar desde el principio
→ modulo-00-preparacion/README.md
```

### Opción B: Ya tengo BC MCP configurado
```bash
# Saltar a crear el agente
→ modulo-03-crear-agente/README.md
```

### Opción C: Solo quiero ver el resultado final
```bash
# Ver el agente completado
→ solucion-completa/README.md
```

---

## 🎯 Escenarios de Negocio

### Escenario 1: Asistente de Ventas
El agente ayuda al equipo de ventas a:
- Consultar información de clientes rápidamente
- Verificar disponibilidad de artículos
- Revisar pedidos pendientes
- Comprobar límites de crédito

### Escenario 2: Asistente de Compras
El agente ayuda al equipo de compras a:
- Buscar proveedores por artículo
- Revisar órdenes de compra pendientes
- Consultar precios de proveedores
- Verificar recepciones pendientes

### Escenario 3: Asistente Financiero
El agente ayuda al equipo financiero a:
- Analizar cuentas por cobrar vencidas
- Revisar saldos de clientes
- Consultar movimientos contables
- Generar resúmenes de facturación

---

## 📊 Comparativa: MCP vs Otros Métodos

| Aspecto | Conector BC | Power Automate | MCP Server |
|---------|-------------|----------------|------------|
| **Configuración** | Media | Alta | Baja |
| **Flexibilidad** | Limitada | Alta | Muy Alta |
| **Mantenimiento** | Por acción | Por flujo | Automático |
| **Lenguaje natural** | No | Parcial | Sí |
| **Acciones dinámicas** | No | No | Sí |
| **Contexto BC** | Básico | Medio | Completo |

### ¿Por qué MCP?

1. **Autodescubrimiento**: El agente descubre automáticamente qué puede hacer
2. **Actualizaciones automáticas**: Los cambios en BC se reflejan sin reconfigurar
3. **Lenguaje natural**: Los usuarios hablan normalmente, no aprenden comandos
4. **Seguridad integrada**: Respeta permisos de BC del usuario conectado
5. **Bajo mantenimiento**: No hay flujos que actualizar cuando cambia BC

---

## 🔗 Recursos Adicionales

### Documentación Oficial
- [Business Central MCP Server](https://learn.microsoft.com/dynamics365/business-central/dev-itpro/ai/configure-mcp-server)
- [Crear Agentes con Copilot Studio](https://learn.microsoft.com/dynamics365/business-central/dev-itpro/ai/create-agent-in-copilot-studio)
- [MCP en Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/agent-extend-action-mcp)

### Comunidad
- [GitHub - Microsoft MCS MCP Lab](https://github.com/microsoft/mcsmcp)
- [Copilot Developer Camp](https://microsoft.github.io/copilot-camp/)

---

## 🤝 Contribuir

¿Encontraste un error? ¿Tienes sugerencias?

1. Abre un Issue describiendo el problema/sugerencia
2. Si quieres contribuir, haz un Fork y Pull Request
3. Revisa las [guías de contribución](CONTRIBUTING.md)

---

## ⚠️ Notas Importantes

> **Preview Feature**: El Business Central MCP Server está en Public Preview (disponible desde octubre 2025). Las funcionalidades pueden cambiar antes de General Availability.

> **Licencias**: Asegúrate de tener las licencias adecuadas:
> - Business Central (Essential o Premium)
> - Copilot Studio con capacidad/créditos disponibles
> - Para usar el agente en Microsoft 365 Copilot, los usuarios necesitan licencia de Microsoft 365 Copilot

> **Seguridad**: El agente actúa con los permisos del usuario conectado. Configura roles adecuados en BC.

---

## 📄 Licencia

Este workshop está bajo licencia MIT. Puedes usarlo, modificarlo y distribuirlo libremente.

---

## 🙏 Créditos

- **Microsoft**: Por el framework MCP y Copilot Studio
- **Comunidad BC**: Por feedback y casos de uso


---

**¡Empezamos! 🚀**

👉 [Módulo 0: Preparación del Entorno](./modulo-00-preparacion/README.md)
