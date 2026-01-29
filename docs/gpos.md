# Directivas de Grupo (GPOs)

## 🔐 Políticas de Grupo del Dominio

Las **Group Policy Objects (GPOs)** permiten aplicar configuraciones de seguridad y restricciones específicas a usuarios y equipos del dominio.

---

## 🌐 GPO Global - Directiva de Contraseñas

**Nombre:** `Directiva de Contraseñas del Dominio`  
**Aplicada a:** Todo el dominio `betis.local`

### Directiva de Contraseñas

| Configuración | Valor |
|---------------|-------|
| **Longitud mínima de contraseña** | 8 caracteres |
| **Complejidad requerida** | ✅ Habilitada |
| **Vigencia máxima** | 90 días |
| **Vigencia mínima** | 1 día |
| **Historial de contraseñas** | 5 contraseñas recordadas |

### Directiva de Bloqueo de Cuenta

| Configuración | Valor |
|---------------|-------|
| **Duración del bloqueo** | 30 minutos |
| **Umbral de bloqueo** | 5 intentos no válidos |
| **Restablecer contador después de** | 30 minutos |

!!! info "Seguridad"
    Estas políticas garantizan que todas las contraseñas del dominio cumplan con estándares mínimos de seguridad y protegen contra ataques de fuerza bruta.

---

## 🥅 GPO_Porteros

**Aplicada a:** OU Porteros

### Configuraciones

#### ❌ Denegar acceso al Panel de Control

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Panel de control
- **Directiva:** Prohibir el acceso al Panel de control y a Configuración de PC
- **Estado:** Habilitada

#### 🖼️ Establecer fondo de pantalla

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Escritorio → Escritorio
- **Directiva:** Papel tapiz del escritorio
- **Estado:** Habilitada
- **Ruta del fondo:** `\\LON-DC01\Fondos\porteros.jpg`

#### 🔒 Restringir acceso a unidades USB

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Sistema → Acceso de almacenamiento extraíble
- **Directiva:** Todas las clases de almacenamiento extraíble: Denegar todos los accesos
- **Estado:** Habilitada

#### 🛡️ Deshabilitar cuentas de invitado

- **Ruta:** Configuración del equipo → Directivas → Configuración de Windows → Configuración de seguridad → Directivas locales → Opciones de seguridad
- **Directiva:** Cuentas: estado de la cuenta Invitado
- **Estado:** Deshabilitada

#### ✅ Evitar desactivación de Windows Defender

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Componentes de Windows → Antivirus de Microsoft Defender
- **Directiva:** Desactivar Antivirus de Microsoft Defender
- **Estado:** Deshabilitada (mantiene Defender activo)

---

## 🛡️ GPO_Defensas

**Aplicada a:** OU Defensas

### Configuraciones

#### ❌ Denegar acceso al símbolo del sistema

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Sistema
- **Directiva:** Impedir el acceso al símbolo del sistema
- **Estado:** Habilitada
- **Opción:** Deshabilitar también el procesamiento de scripts de símbolo del sistema

#### 🚫 Impedir instalación de software

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Componentes de Windows → Windows Installer
- **Directiva:** Desactivar Windows Installer
- **Estado:** Habilitada
- **Opción:** Siempre

#### 🔄 Deshabilitar reinicios forzados

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Componentes de Windows → Windows Update
- **Directiva:** No reiniciar automáticamente con usuarios que hayan iniciado sesión
- **Estado:** Habilitada

#### 🔐 Deshabilitar autenticación NTLM

- **Ruta:** Configuración del equipo → Directivas → Configuración de Windows → Configuración de seguridad → Directivas locales → Opciones de seguridad
- **Directiva:** Seguridad de red: Restringir NTLM: Autenticación NTLM en este dominio
- **Estado:** Denegar todo

#### ⚡ Deshabilitar PowerShell

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Sistema
- **Directiva:** Impedir el acceso a PowerShell
- **Estado:** Habilitada

---

## ⚽ GPO_Centrocampistas

**Aplicada a:** OU Centrocampistas

### Configuraciones

#### 🔧 Desactivar actualizaciones automáticas de controladores

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Sistema → Instalación de dispositivos
- **Directiva:** Impedir que Windows actualice controladores de dispositivos
- **Estado:** Habilitada

#### 🔒 Restringir acceso a unidades USB

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Sistema → Acceso de almacenamiento extraíble
- **Directiva:** Todas las clases de almacenamiento extraíble: Denegar todos los accesos
- **Estado:** Habilitada

#### 🔕 Ocultar notificaciones

- **Ruta:** Configuración de usuario → Directivas → Plantillas administrativas → Menú Inicio y barra de tareas
- **Directiva:** Quitar notificaciones y el centro de actividades
- **Estado:** Habilitada

#### ☁️ Eliminar OneDrive

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Componentes de Windows → OneDrive
- **Directiva:** Impedir el uso de OneDrive para el almacenamiento de archivos
- **Estado:** Habilitada

#### 🛡️ Apagar Windows Defender

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Componentes de Windows → Antivirus de Microsoft Defender
- **Directiva:** Desactivar Antivirus de Microsoft Defender
- **Estado:** Habilitada

!!! warning "Advertencia de Seguridad"
    Deshabilitar Windows Defender reduce la protección del sistema. Solo se recomienda si existe otra solución antivirus implementada.

---

## 🎯 GPO_Delanteros

**Aplicada a:** OU Delanteros

### Configuraciones

#### 📜 Ejecutar script en inicio de sesión

- **Ruta:** Configuración de usuario → Directivas → Configuración de Windows → Scripts (Inicio/Cierre de sesión)
- **Directiva:** Inicio de sesión
- **Script:** `\\LON-DC01\Scripts\inicio_delanteros.bat`

**Contenido del script:**
```batch
@echo off
REM Muestra un mensaje en la consola
echo Script de inicio de sesión completado.
REM Abre una aplicación, por ejemplo, el Bloc de notas
start notepad.exe
```

#### 🔒 Establecer protector de pantalla

- **Protector habilitado:** ✅
- **Tiempo de espera:** 600 segundos (10 minutos)
- **Protección con contraseña:** ✅ Habilitada

#### 📢 Mensaje de inicio de sesión

- **Título:** `Real Betis Balompié`
- **Mensaje:** `Este ordenador es propiedad del Real Betis`

#### 🌐 Gestión remota de PowerShell

- **Ruta:** Configuración del equipo → Directivas → Plantillas administrativas → Componentes de Windows → Administración remota de Windows (WinRM)
- **Directiva:** Permitir administración remota del servidor a través de WinRM
- **Estado:** Habilitada
- **Filtro IPv4:** `*`
- **Filtro IPv6:** `*`

---

## ⏰ GPO_ControlHorarioEquipos

**Aplicada a:** OU EquiposHorarios

### Configuraciones

#### 🕐 Apagado automático a las 22:00

**Tarea programada:**
- **Nombre:** Apagado Automático 22:00
- **Desencadenador:** Diariamente a las 22:00
- **Acción:** Ejecutar `\\LON-DC01\Scripts\apagado_automatico.bat`

**Script de apagado:**
```batch
@echo off
REM Script de apagado automático a las 22:00
shutdown /s /f /t 60 /c "El equipo se apagará en 1 minuto. Guarde su trabajo."
```

#### 🌅 Encendido automático a las 7:00 (Wake-on-LAN)

**Script PowerShell:**
```powershell
# Script Wake-on-LAN para encender equipos a las 7:00
$MacAddresses = @(
    "00-11-22-33-44-55",  # Equipo 1
    "AA-BB-CC-DD-EE-FF"   # Equipo 2
)

foreach ($Mac in $MacAddresses) {
    $MacByteArray = $Mac -split "[:-]" | ForEach-Object { [Byte] "0x$_"}
    $MagicPacket = (,0xFF * 6) + ($MacByteArray * 16)
    $UdpClient = New-Object System.Net.Sockets.UdpClient
    $UdpClient.Connect(([System.Net.IPAddress]::Broadcast),7)
    $UdpClient.Send($MagicPacket,$MagicPacket.Length)
    $UdpClient.Close()
}
```

!!! note "Requisito Hardware"
    El encendido automático requiere que los equipos tengan habilitado Wake-on-LAN en la BIOS y tarjeta de red compatible.

#### ⏱️ Restricciones de horario de inicio de sesión

- **Ruta:** Configuración del equipo → Directivas → Configuración de Windows → Configuración de seguridad → Directivas locales → Asignación de derechos de usuario
- **Directiva:** Permitir el inicio de sesión local
- **Horario permitido:** 7:00 - 22:00 (configurable por usuario)

---

## 🔄 Aplicar y Verificar GPOs

### Forzar actualización de directivas

En los equipos cliente, ejecutar:

```powershell
gpupdate /force
```

### Verificar directivas aplicadas

```powershell
gpresult /r
```

### Ver reporte detallado en HTML

```powershell
gpresult /h C:\GPReport.html
```

---

## 📊 Resumen de GPOs

| GPO | OU Aplicada | Restricciones Principales |
|-----|-------------|---------------------------|
| **Directiva de Contraseñas** | Todo el dominio | Contraseñas seguras, bloqueo de cuenta |
| **GPO_Porteros** | Porteros | Sin Panel Control, sin USB, Defender activo |
| **GPO_Defensas** | Defensas | Sin CMD, sin PowerShell, sin instalación software |
| **GPO_Centrocampistas** | Centrocampistas | Sin USB, sin OneDrive, Defender deshabilitado |
| **GPO_Delanteros** | Delanteros | Script inicio, protector pantalla, mensaje login |
| **GPO_ControlHorarioEquipos** | EquiposHorarios | Apagado/encendido automático |

---

!!! tip "Buena Práctica"
    Siempre prueba las GPOs en un entorno de prueba antes de aplicarlas en producción. Utiliza `gpresult` para verificar que las directivas se aplican correctamente.
