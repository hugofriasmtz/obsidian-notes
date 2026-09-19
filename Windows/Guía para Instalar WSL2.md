## ¿Qué es WSL2?

**WSL2 (Windows Subsystem for Linux 2)** es una característica de Windows que te permite ejecutar un entorno Linux dentro de Windows, usando una **máquina virtual ligera** (un kernel real de Linux).
### ¿Para qué sirve?

- Usar herramientas de Linux (bash, ssh, git, python, etc.) sin instalar Linux en dual-boot.
- Desarrollo web/backend y automatización con un entorno tipo Linux.
- Ejecutar y administrar una **distro** (distribución) de Linux dentro de Windows.

### Documentación oficial (enlaces)

- WSL (docs): [https://learn.microsoft.com/windows/wsl/](https://learn.microsoft.com/windows/wsl/)
- Instalar WSL: [https://learn.microsoft.com/windows/wsl/install](https://learn.microsoft.com/windows/wsl/install)
- Configuración básica de WSL: [https://learn.microsoft.com/windows/wsl/setup/environment](https://learn.microsoft.com/windows/wsl/setup/environment)
- Comandos de WSL: [https://learn.microsoft.com/windows/wsl/basic-commands](https://learn.microsoft.com/windows/wsl/basic-commands)
- Solución de problemas: [https://learn.microsoft.com/windows/wsl/troubleshooting](https://learn.microsoft.com/windows/wsl/troubleshooting)
- Kernel update (si se solicita): [https://aka.ms/wsl2kernel](https://aka.ms/wsl2kernel)

## Instalación por **línea de comando** (Windows 10 y Windows 11)

> Recomendado si quieres hacerlo rápido y controlado.

### Requisitos (Windows 10)

- Windows 10 **2004 (build 19041) o superior** (recomendado).
- Virtualización habilitada en BIOS/UEFI (Intel VT-x / AMD-V).

### 1) Habilitar características necesarias (Windows 10) — PowerShell como administrador

En Windows 11 basta con poner el comando `wsl --install` pues ya hace casi todo, pero en Windows 10 puede ser necesario habilitar estas características manualmente:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Reinicia Windows.

> (Opcional) Hyper-V (si tu edición lo soporta). No siempre es obligatorio para WSL2, pero puede ayudar en algunos escenarios:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Hyper-V /all /norestart
```

Reinicia Windows.

### 2) Instalar WSL (Windows 11 y algunos Windows 10 recientes)

```powershell
wsl --install
```

### 3) Asegurar que WSL2 sea la versión por defecto

```powershell
wsl --set-default-version 2
```

### 4) Instalar una **distro** desde línea de comando (opcional)

Primero, lista las distros disponibles:

```powershell
wsl --list --online
```

Luego instala la que quieras (ejemplo: Ubuntu):

```powershell
wsl --install -d Ubuntu
```

### 5) Abrir la distro y configurar usuario/contraseña

Cuando abras la distro por primera vez, te pedirá crear **usuario** y **contraseña**.

### 6) Verificar que quedó en WSL2

```powershell
wsl -l -v
```

Si una distro te aparece como versión 1 y quieres migrarla:

```powershell
wsl --set-version <NombreDeTuDistro> 2
```

## Instalación con **Microsoft Store** (más “guiada”)

> Ideal si prefieres instalar la distro como una app y gestionarla visualmente.

### 1) Activar WSL2 (Windows 10)

Si estás en Windows 10 y aún no habilitaste las características, ejecuta (PowerShell admin):

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Reinicia Windows.

### 2) Elegir e instalar tu **distro** desde la Store

1. Abrir **Microsoft Store**.
2. Buscar una distro (por ejemplo: Ubuntu, Debian, Kali, etc.).
3. Instalarla.

### 3) Abrir la distro y finalizar configuración

- Abre la distro desde el menú inicio.
- Configura **usuario** y **contraseña**.

### 4) Asegurar WSL2 como versión por defecto y verificar

```powershell
wsl --set-default-version 2
wsl -l -v
```

---

## Comandos útiles (para el día a día)

- Listar distros instaladas:
    
    ```powershell
    wsl -l -v
    ```
    
- Apagar WSL (por ejemplo, si se “queda colgado”):
    
    ```powershell
    wsl --shutdown
    ```
    
- Actualizar WSL:
    
    ```powershell
    wsl --update
    ```
    
- Ver tu versión de WSL:
    
    ```powershell
    wsl --version
    ```