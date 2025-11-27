# Instalar SageMath en Windows
## 1. Instalar Arch en WSL

Para ello accede a [https://apps.microsoft.com/store/detail/arch-wsl/9MZNMNKSM73X](https://apps.microsoft.com/store/detail/arch-wsl/9MZNMNKSM73X)

## 2. Instalar dentro de Arch sage y jupyter

Para ello ejecutar dentro de WSL Arch:

```sudo pacman -Syu --no-confirm sagemath jupyterlab```

Con esto SageMath ya está instalado. Se podría probar poniendo el comando `sage`.

## 3. Hacer que se use el navegador externo

Para ello ejecutar dentro de WSL Arch:

```
sudo bash -c "printf '[wslutilities]\nSigLevel=Never\nServer=https://raw.githubusercontent.com/joroldan/SageMathInstallationGuide/main/' >> /etc/pacman.conf"
sudo pacman -Syu --no-confirm wslu
echo "export BROWSER=wslview" >> .bashrc
```

Con esto ya se abre el navegador de Windows al ejecutar dentro de Arch `sage -n jupyterlab`.

## 4. Crear el acceso directo

Por último vamos a crear un acceso directo a SageMath en nuestro escritorio para facilitar el uso. Para ello hacemos el acceso directo a mano poniendo como:
 - Destino (target): `%LocalAppData%\Microsoft\WindowsApps\arch.exe run 'export BROWSER=wslview && jupyter lab'`
 - Iniciar en (working directory): `%USERPROFILE%`

O ejecutamos las siguiente líneas en PowerShell (Windows):
```
$sh = New-Object -ComObject WScript.Shell
$s = $sh.CreateShortcut("$env:USERPROFILE\Desktop\SageMath.lnk")
$s.TargetPath = "$env:LocalAppData\Microsoft\WindowsApps\arch.exe run 'export BROWSER=wslview && jupyter lab'"
$s.WorkingDirectory = "$env:USERPROFILE"
$s.Save()
```
