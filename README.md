# 🏆 Proyecto Windows Server 2022 - Real Betis Balompié

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active%20Directory-Enabled-success?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

## 📋 Descripción del Proyecto

Proyecto de administración de sistemas para la gestión de un dominio **Active Directory** del club de fútbol **Real Betis Balompié**. Este proyecto implementa una infraestructura completa de dominio con políticas de grupo, perfiles de usuario, recursos compartidos y control horario de equipos.

**Dominio:** `betis.local`
**Servidor:** Windows Server 2022 (LON-DC01)
**Escenario:** Gestión centralizada de usuarios, equipos y recursos del club

---

## 🎯 Objetivos

- ✅ Crear y gestionar un dominio Active Directory completo
- ✅ Organizar usuarios en Unidades Organizativas (OUs) por departamento
- ✅ Aplicar directivas de grupo (GPOs) específicas por OU
- ✅ Configurar perfiles móviles y fijos para usuarios
- ✅ Compartir impresoras por departamento con control de acceso
- ✅ Controlar acceso a directorios según OU
- ✅ Implementar control horario automático en equipos

---

## 🏗️ Estructura del Dominio

### Unidades Organizativas (OUs)

El dominio está organizado en las siguientes unidades organizativas:

```
betis.local/
├── Porteros/           (7 usuarios)
├── Defensas/           (16 usuarios)
├── Centrocampistas/    (22 usuarios)
├── Delanteros/         (5 usuarios)
├── Administración/     (2 usuarios)
└── EquiposHorarios/    (Equipos con control horario)
```

### Usuarios Totales: 52

- **Porteros:** 7 jugadores
- **Defensas:** 16 jugadores
- **Centrocampistas:** 22 jugadores
- **Delanteros:** 5 jugadores
- **Administración:** 2 miembros del cuerpo técnico

---

## 🔐 Directivas de Grupo (GPOs)

### GPO Global - Directiva de Contraseñas

Aplicada a todo el dominio:

- Longitud mínima: 8 caracteres
- Complejidad requerida
- Vigencia máxima: 90 días
- Historial: 5 contraseñas
- Bloqueo tras 5 intentos fallidos

### GPOs Específicas por OU

#### 🥅 GPO_Porteros

- ❌ Denegar acceso al Panel de Control
- 🖼️ Fondo de pantalla personalizado
- 🔒 Restringir acceso a USB
- 🛡️ Deshabilitar cuenta de invitado
- ✅ Windows Defender siempre activo

#### 🛡️ GPO_Defensas

- ❌ Denegar acceso al símbolo del sistema
- 🚫 Impedir instalación de software
- 🔄 Deshabilitar reinicios forzados
- 🔐 Deshabilitar autenticación NTLM
- ⚡ Deshabilitar PowerShell

#### ⚽ GPO_Centrocampistas

- 🔧 Desactivar actualizaciones automáticas de controladores
- 🔒 Restringir acceso a USB
- 🔕 Ocultar notificaciones del sistema
- ☁️ Eliminar OneDrive
- 🛡️ Apagar Windows Defender

#### 🎯 GPO_Delanteros

- 📜 Script de inicio de sesión automático
- 🔒 Protector de pantalla con contraseña (10 min)
- 📢 Mensaje de inicio de sesión personalizado
- 🌐 Gestión remota de PowerShell habilitada

#### ⏰ GPO_ControlHorarioEquipos

- 🕐 Apagado automático a las 22:00
- 🌅 Encendido automático a las 7:00 (Wake-on-LAN)
- ⏱️ Restricciones de horario de inicio de sesión

---

## 👤 Perfiles de Usuario

### Perfiles Móviles

- **Ubicación:** `\\LON-DC01\PerfMovil\%username%`
- **Aplicado a:** Usuarios de Porteros
- **Ventaja:** Sincronización automática entre equipos

### Perfiles Fijos

- **Ubicación:** `\\LON-DC01\PerfFijo\[username]`
- **Aplicado a:** Usuarios de Defensas
- **Ventaja:** Configuración consistente y controlada

---

## 📁 Recursos Compartidos

### Carpetas Compartidas por OU

| OU              | Ruta de Red                    | Letra de Unidad | Permisos                |
| --------------- | ------------------------------ | --------------- | ----------------------- |
| Porteros        | `\\LON-DC01\Porteros`        | P:              | Solo OU Porteros        |
| Defensas        | `\\LON-DC01\Defensas`        | D:              | Solo OU Defensas        |
| Centrocampistas | `\\LON-DC01\Centrocampistas` | C:              | Solo OU Centrocampistas |
| Delanteros      | `\\LON-DC01\Delanteros`      | E:              | Solo OU Delanteros      |
| Administración | `\\LON-DC01\Administracion`  | A:              | Solo OU Administración |

### 🖨️ Impresoras Compartidas

Cada departamento tiene su propia impresora con acceso restringido:

- `Impresora_Porteros` → Solo OU Porteros
- `Impresora_Defensas` → Solo OU Defensas
- `Impresora_Centrocampistas` → Solo OU Centrocampistas
- `Impresora_Delanteros` → Solo OU Delanteros
- `Impresora_Administracion` → Solo OU Administración

---

## ⏰ Control Horario de Equipos

### Características

- **Apagado automático:** 22:00 horas diariamente
- **Encendido automático:** 7:00 horas (requiere Wake-on-LAN)
- **Notificación:** 60 segundos antes del apagado
- **Aplicado a:** Equipos en la OU `EquiposHorarios`

### Scripts Utilizados

#### Apagado Automático

```batch
shutdown /s /f /t 60 /c "El equipo se apagará en 1 minuto. Guarde su trabajo."
```

#### Wake-on-LAN (PowerShell)

Script para encendido remoto de equipos mediante paquetes mágicos.

---

## 📚 Documentación

Este repositorio contiene:

- **[GUIA_PROYECTO_WINDOWS_SERVER.md](GUIA_PROYECTO_WINDOWS_SERVER.md)** - Guía paso a paso completa del proyecto
- **[UD 04 - Proyecto Windows Server.pdf](UD%2004%20-%20Proyecto%20Windows%20Server.pdf)** - Especificaciones originales del proyecto

---

## 🔧 Tecnologías Utilizadas

- **Windows Server 2022**
- **Active Directory Domain Services (AD DS)**
- **Group Policy Management (GPM)**
- **PowerShell**
- **Batch Scripting**
- **Wake-on-LAN**

---

## ✅ Checklist de Implementación

- [X] Dominio `betis.local` creado y funcional
- [X] 5 OUs principales creadas
- [X] 52 usuarios creados y organizados
- [X] GPO de contraseñas aplicada globalmente
- [X] 5 GPOs específicas configuradas
- [X] Perfiles móviles implementados
- [X] Perfiles fijos implementados
- [X] 5 impresoras compartidas con permisos
- [X] 5 carpetas compartidas con control de acceso
- [X] Unidades de red mapeadas automáticamente
- [X] OU EquiposHorarios creada
- [X] Control horario automático configurado
- [X] Scripts de apagado/encendido funcionando

---

## 🧪 Pruebas Realizadas

### ✓ Pruebas de Usuarios

- Inicio de sesión con usuarios de diferentes OUs
- Verificación de restricciones de GPO

### ✓ Pruebas de Perfiles

- Sincronización de perfiles móviles entre equipos
- Persistencia de configuración en perfiles fijos

### ✓ Pruebas de Recursos Compartidos

- Acceso correcto a carpetas asignadas
- Denegación de acceso a carpetas de otras OUs
- Funcionamiento de impresoras por departamento

### ✓ Pruebas de Control Horario

- Apagado automático a las 22:00
- Restricciones de inicio de sesión fuera de horario

---

## 👨‍💻 Autor

**Alejandro García Ripalda**
Proyecto de Administración de Sistemas Operativos
ASIR - 2º Curso

---

## 📅 Información del Proyecto

- **Asignatura:** Administración de Sistemas Operativos (ASO)
- **Unidad Didáctica:** UD04
- **Curso:** 2º ASIR
- **Fecha:** 2026

---

## 📄 Licencia

Este proyecto es material educativo desarrollado como parte del ciclo formativo de ASIR.

---

**¡Viva el Betis manquepierda!** 💚🤍
