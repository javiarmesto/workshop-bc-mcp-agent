# 📋 Módulo 0: Preparación del Entorno

> **Tiempo estimado**: 15 minutos

---

## 🎯 Objetivo

Verificar que tienes todo lo necesario antes de empezar el workshop.

---

## ✅ Checklist de Prerequisitos

### 1. Acceso a Business Central

- [ ] Tienes acceso a un entorno de Business Central
- [ ] El entorno es **v25 o superior** (2025 Wave 1+)
- [ ] Tienes permisos de **administrador** o el permission set `MCP - ADMIN`

**Verificar versión**:
1. Abre Business Central
2. Click en `?` → "Ayuda y soporte"
3. Verifica que la versión sea 25.x o superior

```
✅ Versión correcta: 25.0.xxxxx.xxxxx
❌ Versión incorrecta: 24.x o anterior
```

### 2. Acceso a Copilot Studio

- [ ] Puedes acceder a [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
- [ ] Tienes una licencia de Copilot Studio válida
- [ ] Tienes créditos de Copilot disponibles

**Verificar acceso**:
1. Ve a [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
2. Inicia sesión con tu cuenta Microsoft 365
3. Verifica que puedes ver el panel principal

### 3. Habilitar Feature en Business Central

El MCP Server debe estar habilitado en tu entorno.

**Pasos**:
1. En Business Central, busca **"Feature Management"**
2. Busca: **"Enable MCP Server access"**
3. Si no está habilitado, habilítalo
4. Puede requerir reinicio del entorno

```al
// El feature key es:
Feature: Enable MCP Server access
Status: Enabled ✅
```

### 4. Verificar Permission Set

Necesitas el permission set `MCP - ADMIN` para configurar el servidor.

**Verificar**:
1. Busca **"Users"** en Business Central
2. Selecciona tu usuario
3. Ve a **"Permission Sets"**
4. Verifica que tienes `MCP - ADMIN` o `SUPER`

---

## 🔧 Configuración Inicial de BC MCP Server

### Paso 1: Abrir Configuración MCP

1. En Business Central, busca **"Model Context Protocol (MCP) Server Configurations"**
2. Abre la página

### Paso 2: Verificar Estado

Si es la primera vez:
- La lista estará vacía
- Crearemos la configuración en el Módulo 2

Si ya existe configuración:
- Verifica que está activa
- Anota el nombre de la configuración

---

## 🌐 Verificar Conectividad

### Test de API de Business Central

El MCP Server usa las APIs de BC. Verifica que funcionan:

1. Abre un navegador
2. Ve a: `https://[tu-tenant].api.businesscentral.dynamics.com/v2.0/[environment]/api/v2.0/companies`
3. Deberías ver un JSON con las compañías

**Ejemplo de URL**:
```
https://api.businesscentral.dynamics.com/v2.0/production/api/v2.0/companies
```

**Respuesta esperada**:
```json
{
  "value": [
    {
      "id": "...",
      "name": "CRONUS España S.A.",
      ...
    }
  ]
}
```

---

## 📝 Datos del Entorno

Completa esta información para tenerla a mano durante el workshop:

| Dato | Tu Valor |
|------|----------|
| **Tenant ID** | _________________________ |
| **Environment Name** | _________________________ |
| **Company Name** | _________________________ |
| **BC Version** | _________________________ |
| **Tu Usuario BC** | _________________________ |

### Cómo obtener estos datos:

**Tenant ID y Environment**:
- En BC → `?` → "Ayuda y soporte" → "Solución de problemas"
- O desde la URL: `businesscentral.dynamics.com/[tenant]/[environment]/`

**Company Name**:
- En BC → Click en el nombre de empresa arriba a la derecha

---

## 🧪 Test Rápido: ¿Está Todo Listo?

### Checklist Final

| # | Verificación | ✅/❌ |
|---|--------------|-------|
| 1 | Puedo acceder a Business Central | |
| 2 | BC versión es 25+ | |
| 3 | Tengo permisos MCP - ADMIN | |
| 4 | Feature "Enable MCP Server access" está habilitado | |
| 5 | Puedo acceder a Copilot Studio | |
| 6 | La API de BC responde correctamente | |

**Si todos son ✅**: ¡Estás listo para continuar!

**Si alguno es ❌**: Revisa la sección correspondiente o pide ayuda al instructor.

---

## 🐛 Troubleshooting

### "No encuentro Feature Management"
- Busca exactamente "Feature Management" (sin traducir)
- Verifica que tienes permisos de administrador

### "No tengo MCP - ADMIN"
- Contacta a tu administrador de BC
- Alternativamente, usa SUPER para el workshop

### "API devuelve 401 Unauthorized"
- Verifica que estás logueado en el navegador
- Prueba en modo incógnito con login

### "No puedo acceder a Copilot Studio"
- Verifica tu licencia con el administrador de M365
- Puede requerir licencia específica de Copilot Studio

---

## ➡️ Siguiente Paso

Una vez verificado todo:

👉 [Módulo 1: Introducción a MCP](../modulo-01-introduccion-mcp/README.md)
