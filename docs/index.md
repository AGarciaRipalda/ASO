# Proyecto Windows Server 2022 - Real Betis Balompié

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active%20Directory-Enabled-success?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

## 🏆 Bienvenido

Bienvenido a la documentación del **Proyecto Windows Server 2022** para el **Real Betis Balompié**. Este proyecto implementa una infraestructura completa de dominio Active Directory con políticas de grupo, perfiles de usuario, recursos compartidos y control horario de equipos.

**Dominio:** `betis.local`  
**Servidor:** Windows Server 2022 (LON-DC01)  
**Escenario:** Gestión centralizada de usuarios, equipos y recursos del club

---

## 🎯 Objetivos del Proyecto

- ✅ Crear y gestionar un dominio Active Directory completo
- ✅ Organizar usuarios en Unidades Organizativas (OUs) por departamento
- ✅ Aplicar directivas de grupo (GPOs) específicas por OU
- ✅ Configurar perfiles móviles y fijos para usuarios
- ✅ Compartir impresoras por departamento con control de acceso
- ✅ Controlar acceso a directorios según OU
- ✅ Implementar control horario automático en equipos

---

## 📚 Navegación

Utiliza el menú superior para navegar por las diferentes secciones de la documentación:

### [📖 Guía Completa](guia-completa.md)
Guía paso a paso completa con todos los procedimientos de configuración del proyecto.

### [🏗️ Estructura del Dominio](estructura-dominio.md)
Organización de las Unidades Organizativas (OUs) y distribución de usuarios.

### [🔐 Directivas de Grupo (GPOs)](gpos.md)
Configuración detallada de todas las políticas de grupo aplicadas.

### [📁 Recursos Compartidos](recursos-compartidos.md)
Configuración de carpetas compartidas, impresoras y unidades de red.

### [⏰ Control Horario](control-horario.md)
Implementación del sistema de apagado y encendido automático de equipos.

---

## 📊 Resumen del Proyecto

### Estructura del Dominio

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

## 🔧 Tecnologías Utilizadas

- **Windows Server 2022**
- **Active Directory Domain Services (AD DS)**
- **Group Policy Management (GPM)**
- **PowerShell**
- **Batch Scripting**
- **Wake-on-LAN**

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

**¡Viva el Betis manquepierda!** 💚🤍
