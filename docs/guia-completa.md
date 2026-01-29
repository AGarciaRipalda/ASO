# Guía Paso a Paso - Proyecto Windows Server 2022
## Real Betis Balompié - Gestión de Dominio Active Directory

---

## 📋 Información General

**Dominio:** `betis.local`  
**Servidor:** Windows Server 2022 (LON-DC01)  
**Escenario:** Administración de sistemas para el club de fútbol Real Betis Balompié

---

## 🎯 Objetivos del Proyecto

- Crear y gestionar un dominio Active Directory
- Organizar usuarios en Unidades Organizativas (OUs)
- Aplicar directivas de grupo (GPOs)
- Configurar perfiles móviles y fijos
- Compartir impresoras por departamento
- Controlar acceso a directorios según OU
- Implementar control horario en equipos

---

## 📝 PREPARACIÓN INICIAL

### Paso 1: Verificar Objetos Existentes

1. Encender la máquina virtual **LON-DC01**
2. Abrir **Usuarios y equipos de Active Directory**
3. Verificar la existencia de las siguientes UOs y usuarios de la práctica anterior:

| Tipo | Nombre | Ubicación |
|------|--------|-----------|
| OU | Development | Raíz del dominio |
| OU | Managers | Raíz del dominio |
| OU | Marketing | Raíz del dominio |
| OU | Research | Raíz del dominio |
| OU | Sales | Raíz del dominio |
| OU | IT | Raíz del dominio |
| Usuario | Antonio de Triana | IT |
| Usuario | Isco | Development |
| Usuario | Marc Bartra | Managers |
| Usuario | [Tu Nombre] | Marketing |
| Usuario | [Tu Nombre] | Research |
| Usuario | Pablo Fornals | Sales |
| Usuario | Cucho Hernández | Sales |

> [!IMPORTANT]
> **ENTREGABLE 1:** Captura de pantalla mostrando las unidades organizativas existentes

---

## 🏗️ ACTIVIDAD 01: Configuración del Dominio Real Betis

### Paso 2: Instalación de Active Directory

1. Abrir **Administrador del servidor**
2. Clic en **Agregar roles y características**
3. Seleccionar **Servicios de dominio de Active Directory**
4. Completar la instalación
5. Clic en la notificación **Promover este servidor a controlador de dominio**
6. Seleccionar **Agregar un nuevo bosque**
7. Nombre de dominio raíz: `betis.local`
8. Establecer contraseña de DSRM (Modo de restauración)
9. Completar el asistente y reiniciar el servidor
10. Verificar que el servicio esté activo

### Paso 3: Crear Unidades Organizativas (OUs)

1. Abrir **Usuarios y equipos de Active Directory**
2. Clic derecho en `betis.local` → **Nuevo** → **Unidad organizativa**
3. Crear las siguientes OUs:

| OU | Descripción |
|-----|-------------|
| **Porteros** | Jugadores que ocupan la posición de portero |
| **Defensas** | Jugadores de la línea defensiva |
| **Centrocampistas** | Jugadores del centro del campo |
| **Delanteros** | Jugadores de ataque |
| **Administración** | Personal administrativo y técnico |

**Para cada OU:**
- Clic derecho en la OU → **Propiedades** → Pestaña **Descripción**
- Añadir la descripción correspondiente

### Paso 4: Crear Usuarios (Jugadores del Betis)

#### 4.1 OU Porteros

1. Clic derecho en **Porteros** → **Nuevo** → **Usuario**
2. Crear los siguientes usuarios:

| Nombre | Nombre de inicio de sesión |
|--------|---------------------------|
| Álvaro Valles | avalles |
| Pau López | plopez |
| Adrián | adrian |
| Fran Vieites | fvieites |
| Germán García | ggarcia |
| Guilherme Fernandes | gfernandes |
| Manu González | mgonzalez |

**Configuración para cada usuario:**
- Contraseña inicial: `Betis2024!`
- ✅ El usuario debe cambiar la contraseña en el siguiente inicio de sesión
- ✅ La contraseña nunca expira (desmarcar si se requiere)

#### 4.2 OU Defensas

Crear los siguientes usuarios en la OU **Defensas**:

| Nombre | Nombre de inicio de sesión |
|--------|---------------------------|
| Héctor Bellerín | hbellerin |
| Diego Llorente | dllorente |
| Natan | natan |
| Marc Bartra | mbartra |
| Ricardo Rodríguez | rrodriguez |
| Romain Perraud | rperraud |
| Víctor Gómez | vgomez |
| Júnior Firpo | jfirpo |
| Youssouf Sabaly | ysabaly |
| Nobel Mendy | nmendy |
| Félix Garreta | fgarreta |
| Ángel Ortiz | aortiz |
| Pablo Busto | pbusto |
| Lucas Alcázar | lalcazar |
| Rodrigo Kohon | rkohon |
| Sergio Arribas | sarribas |

#### 4.3 OU Centrocampistas

Crear los siguientes usuarios en la OU **Centrocampistas**:

| Nombre | Nombre de inicio de sesión |
|--------|---------------------------|
| Sofyan Amrabat | samrabat |
| João Cardoso | jcardoso |
| Sergi Altimira | saltimira |
| Antony | antony |
| Pablo Fornals | pfornals |
| Chimy Ávila | cavila |
| Anass Ezzalzouli | aezzalzouli |
| William Carvalho | wcarvalho |
| Iker Losada | ilosada |
| Rodrigo Riquelme | rriquelme |
| Nelson Deossa | ndeossa |
| Giovani Lo Celso | glocelso |
| Marc Roca | mroca |
| Iván Corralejo | icorralejo |
| Isco | isco |
| Aitor Ruibal | aruibal |
| Mawuli Mensah | mmensah |
| Carlos Guirao | cguirao |
| Jesús Rodríguez | jrodriguez |
| Dani Pérez | dperez |
| Mateo Flores | mflores |
| Carlos Reina | creina |

#### 4.4 OU Delanteros

Crear los siguientes usuarios en la OU **Delanteros**:

| Nombre | Nombre de inicio de sesión |
|--------|---------------------------|
| Cédric Bakambu | cbakambu |
| José Morante | jmorante |
| Cristian Hernández | chernandez |
| Marcos Fernández | mfernandez |
| Pablo García | pgarcia |

#### 4.5 OU Administración

Crear los siguientes usuarios en la OU **Administración**:

| Nombre | Nombre de inicio de sesión |
|--------|---------------------------|
| Manuel Pellegrini | mpellegrini |
| Juan Sevillano | jsevillano |

### Paso 5: Configurar Directivas de Grupo (GPOs)

#### 5.1 Directivas Globales (Aplicar a todas las OUs)

**Crear GPO de Directiva de Contraseñas:**

1. Abrir **Administración de directivas de grupo**
2. Expandir **Bosque: betis.local** → **Dominios** → **betis.local**
3. Clic derecho en **betis.local** → **Crear una GPO en este dominio y vincularla aquí**
4. Nombre: `Directiva de Contraseñas del Dominio`
5. Clic derecho en la GPO → **Editar**
6. Navegar a: **Configuración del equipo** → **Directivas** → **Configuración de Windows** → **Configuración de seguridad** → **Directivas de cuenta** → **Directiva de contraseñas**

Configurar:
- **Longitud mínima de contraseña:** 8 caracteres
- **La contraseña debe cumplir los requisitos de complejidad:** Habilitada
- **Vigencia máxima de la contraseña:** 90 días
- **Vigencia mínima de la contraseña:** 1 día
- **Forzar el historial de contraseñas:** 5 contraseñas recordadas

7. Navegar a: **Directivas de cuenta** → **Directiva de bloqueo de cuenta**

Configurar:
- **Duración del bloqueo de cuenta:** 30 minutos
- **Umbral de bloqueo de cuenta:** 5 intentos no válidos
- **Restablecer el contador de bloqueos de cuenta después de:** 30 minutos

#### 5.2 GPO para OU Porteros

1. Clic derecho en **Porteros** → **Crear una GPO en este dominio y vincularla aquí**
2. Nombre: `GPO_Porteros`
3. Clic derecho → **Editar**

**Configuraciones:**

**a) Denegar acceso al Panel de Control:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Panel de control**
- Directiva: **Prohibir el acceso al Panel de control y a Configuración de PC**
- Estado: **Habilitada**

**b) Establecer fondo de pantalla:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Escritorio** → **Escritorio**
- Directiva: **Papel tapiz del escritorio**
- Estado: **Habilitada**
- Nombre del papel tapiz: `\\LON-DC01\Fondos\porteros.jpg` (crear carpeta compartida previamente)

**c) Restringir acceso a unidades USB:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Sistema** → **Acceso de almacenamiento extraíble**
- Directiva: **Todas las clases de almacenamiento extraíble: Denegar todos los accesos**
- Estado: **Habilitada**

**d) Deshabilitar cuentas de invitado:**
- Ruta: **Configuración del equipo** → **Directivas** → **Configuración de Windows** → **Configuración de seguridad** → **Directivas locales** → **Opciones de seguridad**
- Directiva: **Cuentas: estado de la cuenta Invitado**
- Estado: **Deshabilitada**

**e) Evitar desactivación de Windows Defender:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Componentes de Windows** → **Antivirus de Microsoft Defender**
- Directiva: **Desactivar Antivirus de Microsoft Defender**
- Estado: **Deshabilitada**

#### 5.3 GPO para OU Defensas

1. Crear GPO: `GPO_Defensas` vinculada a **Defensas**

**Configuraciones:**

**a) Denegar acceso al símbolo del sistema:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Sistema**
- Directiva: **Impedir el acceso al símbolo del sistema**
- Estado: **Habilitada**
- Opción: **Deshabilitar también el procesamiento de scripts de símbolo del sistema**

**b) Impedir instalación de software:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Componentes de Windows** → **Windows Installer**
- Directiva: **Desactivar Windows Installer**
- Estado: **Habilitada**
- Opción: **Siempre**

**c) Deshabilitar reinicios forzados:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Componentes de Windows** → **Windows Update**
- Directiva: **No reiniciar automáticamente con usuarios que hayan iniciado sesión para instalaciones de actualizaciones automáticas programadas**
- Estado: **Habilitada**

**d) Deshabilitar autenticación NTLM:**
- Ruta: **Configuración del equipo** → **Directivas** → **Configuración de Windows** → **Configuración de seguridad** → **Directivas locales** → **Opciones de seguridad**
- Directiva: **Seguridad de red: Restringir NTLM: Autenticación NTLM en este dominio**
- Estado: **Denegar todo**

**e) Deshabilitar PowerShell:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Sistema**
- Directiva: **Impedir el acceso a PowerShell**
- Estado: **Habilitada**

#### 5.4 GPO para OU Centrocampistas

1. Crear GPO: `GPO_Centrocampistas` vinculada a **Centrocampistas**

**Configuraciones:**

**a) Desactivar actualizaciones automáticas de controladores:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Sistema** → **Instalación de dispositivos**
- Directiva: **Impedir que Windows actualice controladores de dispositivos**
- Estado: **Habilitada**

**b) Restringir acceso a unidades USB:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Sistema** → **Acceso de almacenamiento extraíble**
- Directiva: **Todas las clases de almacenamiento extraíble: Denegar todos los accesos**
- Estado: **Habilitada**

**c) Ocultar notificaciones:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Menú Inicio y barra de tareas**
- Directiva: **Quitar notificaciones y el centro de actividades**
- Estado: **Habilitada**

**d) Eliminar OneDrive:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Componentes de Windows** → **OneDrive**
- Directiva: **Impedir el uso de OneDrive para el almacenamiento de archivos**
- Estado: **Habilitada**

**e) Apagar Windows Defender:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Componentes de Windows** → **Antivirus de Microsoft Defender**
- Directiva: **Desactivar Antivirus de Microsoft Defender**
- Estado: **Habilitada**

#### 5.5 GPO para OU Delanteros

1. Crear GPO: `GPO_Delanteros` vinculada a **Delanteros**

**Configuraciones:**

**a) Ejecutar script en inicio de sesión:**

Primero, crear el script:
1. Abrir Bloc de notas
2. Escribir:
```batch
@echo off
REM Muestra un mensaje en la consola
echo Script de inicio de sesión completado.
REM Abre una aplicación, por ejemplo, el Bloc de notas
start notepad.exe
```
3. Guardar como `C:\Scripts\inicio_delanteros.bat`
4. Compartir la carpeta Scripts

Configurar GPO:
- Ruta: **Configuración de usuario** → **Directivas** → **Configuración de Windows** → **Scripts (Inicio/Cierre de sesión)**
- Directiva: **Inicio de sesión**
- Clic en **Agregar** → Examinar → `\\LON-DC01\Scripts\inicio_delanteros.bat`

**b) Establecer protector de pantalla:**
- Ruta: **Configuración de usuario** → **Directivas** → **Plantillas administrativas** → **Panel de control** → **Personalización**
- Directiva: **Habilitar protector de pantalla**
- Estado: **Habilitada**
- Directiva: **Tiempo de espera del protector de pantalla**
- Estado: **Habilitada** → 600 segundos (10 minutos)
- Directiva: **Protección con contraseña del protector de pantalla**
- Estado: **Habilitada**

**c) Mensaje de inicio de sesión:**
- Ruta: **Configuración del equipo** → **Directivas** → **Configuración de Windows** → **Configuración de seguridad** → **Directivas locales** → **Opciones de seguridad**
- Directiva: **Inicio de sesión interactivo: texto del mensaje para los usuarios que intentan iniciar sesión**
- Texto: `Este ordenador es propiedad del Real Betis`
- Directiva: **Inicio de sesión interactivo: título del mensaje para los usuarios que intentan iniciar sesión**
- Texto: `Real Betis Balompié`

**d) Gestión remota de PowerShell:**
- Ruta: **Configuración del equipo** → **Directivas** → **Plantillas administrativas** → **Componentes de Windows** → **Administración remota de Windows (WinRM)** → **Servicio WinRM**
- Directiva: **Permitir administración remota del servidor a través de WinRM**
- Estado: **Habilitada**
- Filtro IPv4: `*`
- Filtro IPv6: `*`

### Paso 6: Configurar Perfiles de Usuario

#### 6.1 Crear Carpetas para Perfiles

1. En el servidor, crear las carpetas:
   - `C:\Perfiles\Moviles`
   - `C:\Perfiles\Fijos`

2. Compartir las carpetas:
   - Clic derecho en cada carpeta → **Propiedades** → **Compartir** → **Uso compartido avanzado**
   - ✅ Compartir esta carpeta
   - Nombre del recurso compartido: `PerfMovil` y `PerfFijo`
   - **Permisos** → Agregar **Usuarios del dominio** → Control total

3. Configurar permisos NTFS:
   - Pestaña **Seguridad** → **Editar**
   - Agregar **Usuarios del dominio** → Control total

#### 6.2 Asignar Perfiles Móviles

Ejemplo: Asignar perfil móvil a usuarios de **Porteros**

1. Abrir **Usuarios y equipos de Active Directory**
2. Seleccionar un usuario (ej: Álvaro Valles)
3. Clic derecho → **Propiedades** → Pestaña **Perfil**
4. **Ruta de acceso al perfil:** `\\LON-DC01\PerfMovil\%username%`
5. Aplicar y Aceptar

Repetir para varios usuarios de Porteros.

#### 6.3 Asignar Perfiles Fijos

Ejemplo: Asignar perfil fijo a usuarios de **Defensas**

1. Seleccionar un usuario (ej: Héctor Bellerín)
2. Clic derecho → **Propiedades** → Pestaña **Perfil**
3. **Ruta de acceso al perfil:** `\\LON-DC01\PerfFijo\hbellerin`
4. Crear manualmente la carpeta en el servidor
5. Aplicar y Aceptar

#### 6.4 Verificar Funcionamiento

1. Iniciar sesión desde un equipo cliente con un usuario de perfil móvil
2. Realizar cambios (crear archivos en el escritorio, cambiar configuración)
3. Cerrar sesión
4. Iniciar sesión desde otro equipo cliente
5. Verificar que los cambios se mantienen

### Paso 7: Compartir Impresoras por Departamento

#### 7.1 Instalar Impresora en el Servidor

1. Abrir **Panel de control** → **Dispositivos e impresoras**
2. Clic en **Agregar una impresora**
3. Seleccionar **Agregar una impresora local**
4. Puerto: **FILE: (Imprimir a archivo)** o crear puerto TCP/IP
5. Fabricante: **Generic** → Modelo: **Generic / Text Only**
6. Nombre: `Impresora_Administracion`
7. Completar instalación

#### 7.2 Compartir Impresora

1. Clic derecho en la impresora → **Propiedades de impresora**
2. Pestaña **Compartir**
3. ✅ Compartir esta impresora
4. Nombre del recurso compartido: `ImpAdministracion`

#### 7.3 Configurar Permisos

1. Pestaña **Seguridad**
2. **Quitar** el grupo **Todos**
3. **Agregar** → Buscar **Administración** (la OU)
4. Permisos: **Imprimir** y **Administrar esta impresora**
5. Aplicar y Aceptar

#### 7.4 Repetir para Otras OUs

Crear y compartir impresoras adicionales:
- `Impresora_Porteros` → Solo OU Porteros
- `Impresora_Defensas` → Solo OU Defensas
- `Impresora_Centrocampistas` → Solo OU Centrocampistas
- `Impresora_Delanteros` → Solo OU Delanteros

### Paso 8: Crear Directorios Compartidos por OU

#### 8.1 Crear Carpetas Compartidas

1. En el servidor, crear carpetas:
   - `C:\Compartidas\Porteros`
   - `C:\Compartidas\Defensas`
   - `C:\Compartidas\Centrocampistas`
   - `C:\Compartidas\Delanteros`
   - `C:\Compartidas\Administracion`

#### 8.2 Compartir y Configurar Permisos

Para cada carpeta (ejemplo: **Porteros**):

1. Clic derecho → **Propiedades** → **Compartir** → **Uso compartido avanzado**
2. ✅ Compartir esta carpeta
3. Nombre: `Porteros`
4. **Permisos** → Quitar **Todos**
5. **Agregar** → Buscar la OU **Porteros**
6. Permisos de compartición: **Control total**

7. Pestaña **Seguridad** → **Editar**
8. Quitar **Usuarios**
9. **Agregar** → OU **Porteros**
10. Permisos NTFS: **Modificar, Leer y ejecutar, Mostrar el contenido de la carpeta, Leer, Escribir**

Repetir para todas las OUs.

#### 8.3 Mapear Unidades de Red mediante GPO

Para cada OU (ejemplo: **Porteros**):

1. Editar la GPO correspondiente (`GPO_Porteros`)
2. Navegar a: **Configuración de usuario** → **Preferencias** → **Configuración de Windows** → **Asignaciones de unidad**
3. Clic derecho → **Nuevo** → **Unidad asignada**
4. Configurar:
   - **Acción:** Crear
   - **Ubicación:** `\\LON-DC01\Porteros`
   - **Reconectar:** ✅
   - **Etiqueta como:** Carpeta Porteros
   - **Letra de unidad:** P:
   - **Mostrar esta unidad:** ✅
5. Aplicar y Aceptar

Repetir para cada OU con letras diferentes:
- Defensas → D:
- Centrocampistas → C:
- Delanteros → E:
- Administración → A:

#### 8.4 Verificar Acceso

1. Iniciar sesión con un usuario de Porteros
2. Abrir **Explorador de archivos**
3. Verificar que aparece la unidad **P:** (Carpeta Porteros)
4. Intentar acceder a otras carpetas compartidas (debe denegar acceso)

---

## 🕐 ACTIVIDAD 02: Control Horario de Equipos

### Paso 9: Crear OU para Equipos con Control Horario

1. Abrir **Usuarios y equipos de Active Directory**
2. Clic derecho en `betis.local` → **Nuevo** → **Unidad organizativa**
3. Nombre: `EquiposHorarios`
4. Aceptar

### Paso 10: Mover Equipos a la OU

1. Localizar los objetos de equipo en **Computers**
2. Seleccionar los equipos que necesitan control horario
3. Clic derecho → **Mover**
4. Seleccionar **EquiposHorarios**

### Paso 11: Crear GPO de Control Horario

1. Abrir **Administración de directivas de grupo**
2. Clic derecho en **EquiposHorarios** → **Crear una GPO en este dominio y vincularla aquí**
3. Nombre: `ControlHorarioEquipos`
4. Clic derecho → **Editar**

### Paso 12: Configurar Restricciones de Horario

#### 12.1 Configurar Horarios de Inicio de Sesión

1. Navegar a: **Configuración del equipo** → **Directivas** → **Configuración de Windows** → **Configuración de seguridad** → **Directivas locales** → **Asignación de derechos de usuario**
2. Directiva: **Permitir el inicio de sesión local**
3. Configurar usuarios/grupos permitidos

#### 12.2 Crear Script de Apagado Automático

1. Crear archivo `C:\Scripts\apagado_automatico.bat`:

```batch
@echo off
REM Script de apagado automático a las 22:00
shutdown /s /f /t 60 /c "El equipo se apagará en 1 minuto. Guarde su trabajo."
```

2. Compartir carpeta Scripts

#### 12.3 Configurar Tarea Programada mediante GPO

1. En la GPO `ControlHorarioEquipos`:
2. Navegar a: **Configuración del equipo** → **Preferencias** → **Configuración del Panel de control** → **Tareas programadas**
3. Clic derecho → **Nuevo** → **Tarea programada (Windows Vista y posterior)**
4. Configurar:
   - **Acción:** Crear
   - **Nombre:** Apagado Automático 22:00
   - Pestaña **Desencadenadores** → **Nuevo**
     - **Iniciar la tarea:** Según una programación
     - **Configuración:** Diariamente
     - **Hora:** 22:00
   - Pestaña **Acciones** → **Nueva**
     - **Acción:** Iniciar un programa
     - **Programa:** `\\LON-DC01\Scripts\apagado_automatico.bat`
   - Pestaña **Condiciones** → Ajustar según necesidad
   - Pestaña **Configuración** → ✅ Permitir que la tarea se ejecute a petición

#### 12.4 Script de Encendido (Wake-on-LAN)

> [!NOTE]
> El encendido automático requiere hardware compatible con Wake-on-LAN y configuración en BIOS

1. Crear script PowerShell `C:\Scripts\wake_on_lan.ps1`:

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

2. Programar ejecución diaria a las 7:00 desde el servidor

### Paso 13: Aplicar y Probar la GPO

1. En los equipos cliente, abrir PowerShell como administrador
2. Ejecutar:
```powershell
gpupdate /force
```

3. Verificar que las directivas se aplican:
```powershell
gpresult /r
```

4. Intentar iniciar sesión fuera del horario permitido
5. Verificar que el equipo se apaga automáticamente a las 22:00

> [!IMPORTANT]
> **ENTREGABLE 2:** Captura de pantalla mostrando la OU EquiposHorarios y la GPO aplicada

---

## ✅ Verificación Final del Proyecto

### Checklist de Comprobación

- [ ] Dominio `betis.local` creado y funcional
- [ ] 5 OUs creadas (Porteros, Defensas, Centrocampistas, Delanteros, Administración)
- [ ] Todos los usuarios creados en sus respectivas OUs
- [ ] GPO de contraseñas aplicada globalmente
- [ ] GPO específica para cada OU con todas las restricciones
- [ ] Perfiles móviles configurados y probados
- [ ] Perfiles fijos configurados y probados
- [ ] Impresoras compartidas por departamento con permisos correctos
- [ ] Carpetas compartidas creadas con permisos NTFS adecuados
- [ ] Unidades de red mapeadas automáticamente por GPO
- [ ] OU EquiposHorarios creada
- [ ] GPO de control horario configurada
- [ ] Scripts de apagado/encendido funcionando
- [ ] Todas las configuraciones probadas desde equipos cliente

### Pruebas Recomendadas

1. **Prueba de Usuarios:**
   - Iniciar sesión con usuarios de diferentes OUs
   - Verificar que las restricciones de GPO se aplican correctamente

2. **Prueba de Perfiles:**
   - Iniciar sesión desde diferentes equipos
   - Verificar sincronización de perfiles móviles

3. **Prueba de Recursos Compartidos:**
   - Intentar acceder a carpetas de otras OUs (debe denegar)
   - Verificar acceso a impresoras asignadas

4. **Prueba de Control Horario:**
   - Verificar apagado automático
   - Intentar acceso fuera de horario

---

## 📸 Entregables Requeridos

> [!WARNING]
> Asegúrate de capturar todas las pantallas requeridas durante la realización del proyecto

### Lista de Capturas Necesarias

1. **Entregable 1 (Preparación):** Unidades organizativas existentes de la práctica anterior
2. **Entregable 1 (Actividad 01):** Nuevas unidades organizativas del proyecto Real Betis
3. **Entregable 2 (Actividad 02):** OU EquiposHorarios y GPO de control horario

### Capturas Adicionales Recomendadas

- Usuarios creados en cada OU
- Configuración de cada GPO
- Perfiles móviles y fijos funcionando
- Carpetas compartidas con permisos
- Impresoras compartidas
- Unidades de red mapeadas
- Scripts de control horario
- Resultados de `gpresult /r`

---

## 📚 Documentación del Proyecto

### Estructura del Informe

1. **Portada**
   - Título del proyecto
   - Nombre del alumno
   - Fecha de entrega

2. **Índice**

3. **Introducción**
   - Descripción del escenario
   - Objetivos del proyecto

4. **Desarrollo**
   - Cada paso realizado con su captura correspondiente
   - Explicación breve del efecto de cada configuración

5. **Pruebas y Verificación**
   - Resultados de las pruebas realizadas
   - Problemas encontrados y soluciones

6. **Conclusiones**
   - Aprendizajes obtenidos
   - Dificultades superadas

7. **Anexos**
   - Scripts utilizados
   - Configuraciones adicionales

---

## 🔧 Solución de Problemas Comunes

### Problema: GPO no se aplica

**Solución:**
```powershell
gpupdate /force
gpresult /r
```

### Problema: No se puede acceder a carpetas compartidas

**Solución:**
- Verificar permisos NTFS y de compartición
- Comprobar que el usuario pertenece a la OU correcta
- Verificar conectividad de red

### Problema: Perfil móvil no se sincroniza

**Solución:**
- Verificar permisos en la carpeta de perfiles
- Comprobar ruta UNC correcta
- Revisar logs de eventos en el servidor

### Problema: Impresora no aparece

**Solución:**
- Verificar que el usuario pertenece al grupo con permisos
- Reiniciar el servicio de cola de impresión
- Ejecutar `gpupdate /force`

---

## 📅 Fecha de Entrega

> [!CAUTION]
> **Fecha límite:** Indicada en el campus  
> **La fecha NO es prorrogable**  
> **Entrega fuera de plazo = Calificación 0**

---

## 🎓 Conclusión

Este proyecto te ha permitido:
- ✅ Crear y gestionar un dominio Active Directory completo
- ✅ Organizar usuarios en estructuras jerárquicas
- ✅ Aplicar políticas de seguridad y restricciones
- ✅ Configurar perfiles de usuario
- ✅ Gestionar recursos compartidos
- ✅ Implementar control horario en equipos

**¡Éxito en tu proyecto!** 🚀

---

*Guía creada para el proyecto Windows Server 2022 - Real Betis Balompié*
