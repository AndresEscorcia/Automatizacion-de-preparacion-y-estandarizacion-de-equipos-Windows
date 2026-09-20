# 🖥️ Automatización de preparación y estandarización de equipos Windows

Script de automatización desarrollado en **PowerShell** para facilitar la preparación, configuración y estandarización inicial de equipos con Windows.

El proyecto nace de una necesidad común en entornos de soporte técnico e infraestructura: reducir el trabajo manual necesario para dejar un equipo listo para ser entregado y utilizado bajo unos parámetros previamente definidos.

La herramienta combina **PowerShell + Chocolatey + configuraciones nativas de Windows** para automatizar tareas de instalación de software, configuración del sistema, personalización del equipo y verificación del estado de las aplicaciones.

---

## 🎯 Objetivo

El objetivo principal es convertir un proceso que normalmente requiere múltiples pasos manuales en un flujo de trabajo más rápido, repetible y estandarizado.

Entre las tareas contempladas se encuentran:

* Instalación automatizada de software.
* Actualización de aplicaciones.
* Verificación del estado de los programas instalados.
* Gestión dinámica de la lista de aplicaciones.
* Configuración del nombre del equipo.
* Configuración de zona horaria.
* Sincronización de hora con `time.windows.com`.
* Configuración y aplicación de fondos corporativos.
* Restricción del cambio de fondo de pantalla.
* Desactivación del Mobile Hotspot.
* Desactivación de determinadas funciones relacionadas con Gaming/Game DVR.
* Verificación de conectividad a Internet antes de realizar instalaciones.
* Visualización del progreso durante la instalación de aplicaciones.

La idea es que un equipo pueda pasar de una instalación inicial a un estado previamente definido con la menor intervención manual posible.

---

## ⚙️ Tecnologías utilizadas

| Tecnología               | Uso                                              |
| ------------------------ | ------------------------------------------------ |
| **PowerShell**           | Automatización y configuración del sistema       |
| **Chocolatey**           | Gestión e instalación de paquetes                |
| **Windows Registry**     | Aplicación de políticas y configuraciones        |
| **Windows Services**     | Gestión de servicios del sistema                 |
| **Windows Time Service** | Sincronización horaria                           |
| **Git / GitHub**         | Control de versiones y distribución del proyecto |

Microsoft contempla PowerShell y otras herramientas de automatización como mecanismos habituales para estandarizar procesos de implementación y configuración de equipos Windows.

---

## 🧩 Funcionamiento general

El proceso puede dividirse conceptualmente en varias etapas:

```text
┌──────────────────────────────┐
│       Inicio del script      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Verificación / instalación   │
│       de Chocolatey          │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Selección de configuración   │
│   corporativa / wallpaper    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Configuración del sistema    │
│ • Nombre del equipo         │
│ • Zona horaria              │
│ • Hora del sistema          │
│ • Políticas de Windows      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Gestión de aplicaciones      │
│ • Instalar                  │
│ • Actualizar                │
│ • Verificar                 │
│ • Modificar lista           │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        Equipo preparado      │
└──────────────────────────────┘
```

---

## 📦 Software gestionado

Actualmente el script contempla una lista inicial de paquetes administrados mediante Chocolatey:

* Google Chrome
* Foxit Reader
* 7-Zip
* TSPrint Client
* Microsoft Edge WebView2 Runtime
* Lightshot
* Microsoft Teams
* POS for .NET
* .NET Framework 4.5.2
* .NET Framework 3.5
* Splashtop Streamer

La lista puede modificarse desde el propio menú del script, permitiendo agregar o eliminar paquetes según las necesidades del entorno.

---

## 🖥️ Configuración del equipo

El script permite establecer diferentes parámetros del equipo durante el proceso de preparación.

### Nombre del equipo

El usuario puede introducir el nombre que tendrá el dispositivo.

Esto permite incorporar el equipo posteriormente a una estrategia de identificación y administración basada en nombres estandarizados.

### Zona horaria

Se configura la zona horaria:

```text
SA Pacific Standard Time
```

correspondiente al horario utilizado en Colombia.

Además, se configura el servicio de hora de Windows para sincronizarse con:

```text
time.windows.com
```

### Fondo corporativo

El script permite seleccionar entre diferentes fondos de pantalla corporativos.

Actualmente contempla:

```text
1 - Agropaisa
2 - Agromilenio
3 - Ducol
```

Las URLs de los fondos se manejan mediante variables de entorno:

```powershell
$env:AGROPAISA_WALLPAPER
$env:AGROMILENIO_WALLPAPER
$env:DUCOL_WALLPAPER
```

Esto permite separar la configuración del código principal y facilita la adaptación del script a diferentes organizaciones.

---

## 📋 Menú interactivo

El script proporciona un menú para administrar las operaciones principales:

```text
1: Instalar programas
2: Actualizar programas
3: Verificar estado de instalación
4: Gestionar lista de programas
5: Buscar paquetes en la comunidad de Chocolatey
6: Salir
```

### 1. Instalar programas

Comprueba la conectividad a Internet y posteriormente procesa la lista de aplicaciones definida.

Los programas que ya se encuentran instalados son omitidos.

### 2. Actualizar programas

Permite recorrer la lista de aplicaciones y ejecutar su actualización mediante Chocolatey.

### 3. Verificar estado

Comprueba individualmente si los paquetes definidos se encuentran instalados.

### 4. Gestionar programas

Permite:

* Consultar la lista actual.
* Agregar nuevos paquetes.
* Eliminar paquetes.
* Regresar al menú principal.

---

## 🔐 Requisitos

Antes de ejecutar el proyecto se recomienda contar con:

* Windows 10 o Windows 11.
* PowerShell.
* Conexión a Internet.
* Permisos administrativos.
* Acceso a los repositorios de Chocolatey.
* Permisos suficientes para modificar configuraciones del sistema y el Registro.

El aprovisionamiento y configuración automatizada son mecanismos utilizados para reducir la intervención manual durante la preparación de dispositivos Windows.

---

## ▶️ Ejecución

Clonar el repositorio:

```powershell
git clone https://github.com/AndresEscorcia/Automatizacion-de-preparacion-y-estandarizacion-de-equipos-Windows.git
```

Entrar al directorio:

```powershell
cd Automatizacion-de-preparacion-y-estandarizacion-de-equipos-Windows
```

Ejecutar PowerShell como **Administrador** y posteriormente:

```powershell
.\T1Tics.ps1
```

Si la política de ejecución de PowerShell impide ejecutar el script, debe utilizarse una configuración apropiada para el entorno en lugar de deshabilitar las protecciones de forma permanente.

---

## ⚠️ Consideraciones

Este script realiza modificaciones sobre configuraciones del sistema operativo y debe ejecutarse únicamente en equipos sobre los cuales se tenga autorización administrativa.

Entre las modificaciones realizadas se encuentran:

* Registro de Windows.
* Políticas del sistema.
* Configuración de red.
* Configuración de zona horaria.
* Servicio de hora de Windows.
* Nombre del equipo.
* Instalación y actualización de software.

Se recomienda probar cualquier modificación en un entorno controlado antes de utilizar el script sobre equipos de producción.

---

## 🔧 Arquitectura del script

El proyecto utiliza funciones independientes para separar diferentes responsabilidades:

```text
T1Tics.ps1
│
├── Instalación de Chocolatey
│
├── Test-InternetConnection
│
├── Test-ChocolateyVersion
│
├── Show-ProgressBar
│
├── Get-ProgramInstalled
│
├── Install-Programs
│
├── Edit-ProgramList
│
├── Test-InstallationStatus
│
├── Show-Menu
│
└── Flujo principal
```

Esta estructura facilita la evolución del proyecto hacia una arquitectura más modular, con funciones independientes y reutilizables.

---

## 🚀 Próximas mejoras

El proyecto se encuentra en evolución. Algunas mejoras previstas son:

* [ ] Implementar correctamente la búsqueda de paquetes en Chocolatey.
* [ ] Agregar desinstalación de aplicaciones.
* [ ] Mejorar el manejo de errores.
* [ ] Incorporar logging de las operaciones realizadas.
* [ ] Generar un resumen final del proceso.
* [ ] Validar permisos administrativos antes de iniciar.
* [ ] Validar dependencias antes de ejecutar determinadas operaciones.
* [ ] Separar configuración y lógica del script.
* [ ] Incorporar archivos de configuración externos.
* [ ] Mejorar la detección de aplicaciones instaladas.
* [ ] Incorporar una interfaz gráfica mediante Windows Presentation Foundation (WPF).
* [ ] Evaluar soporte para ejecución desatendida.
* [ ] Incorporar parámetros para permitir diferentes perfiles de configuración.
* [ ] Crear perfiles de instalación según el tipo de equipo o usuario.

---

## 🛠️ Posibles perfiles de configuración

Una evolución natural del proyecto sería permitir definir diferentes perfiles:

```text
Perfiles
│
├── Administrativo
│   ├── Navegadores
│   ├── Suite ofimática
│   └── Herramientas corporativas
│
├── Soporte Técnico
│   ├── Herramientas de diagnóstico
│   ├── Remote Support
│   └── Utilidades IT
│
└── Operativo
    ├── Aplicaciones corporativas
    ├── Runtime / dependencias
    └── Herramientas específicas
```

Esto permitiría utilizar el mismo motor de automatización para diferentes escenarios de despliegue.

---

## 📈 Propósito del proyecto

Más allá de la instalación de aplicaciones, el proyecto representa un ejercicio práctico de:

* Automatización de procesos IT.
* Administración de sistemas Windows.
* Gestión de software.
* Estandarización de estaciones de trabajo.
* Administración mediante PowerShell.
* Gestión de configuraciones mediante Registry.
* Resolución de tareas repetitivas mediante scripting.
* Diseño de procesos reproducibles.

La estandarización de tareas operativas repetitivas permite reducir variabilidad y hacer que los procesos sean más predecibles y repetibles.

---

## 📌 Estado actual

**Estado:** En desarrollo

**Plataforma:** Windows

**Lenguaje:** PowerShell

**Gestor de paquetes:** Chocolatey

**Interfaz:** CLI interactiva

**Licencia:** GNU GPL v3.0

---

## 📄 Licencia

Este proyecto se distribuye bajo los términos de la **GNU General Public License v3.0**.

Consulta el archivo [`LICENSE`](./LICENSE) para conocer los términos completos de uso, modificación y distribución.

---

## 👤 Autor

**Andres Escorcia**

Proyecto desarrollado como parte de la exploración práctica de **automatización IT, administración de sistemas Windows, scripting y estandarización de infraestructura**.

---

## 🔗 Repositorio

[GitHub — Automatización de preparación y estandarización de equipos Windows](https://github.com/AndresEscorcia/Automatizacion-de-preparacion-y-estandarizacion-de-equipos-Windows)
