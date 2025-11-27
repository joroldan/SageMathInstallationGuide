# Instalar SageMath en Windows

## 1. Instalar Arch en WSL

Para ello accede a [https://apps.microsoft.com/store/detail/arch-wsl/9MZNMNKSM73X](https://apps.microsoft.com/store/detail/arch-wsl/9MZNMNKSM73X) y haz la instalación desde la web o la tienda de Windows. La instalación tardará unos minutos y te pedirá crear un usuario y contraseña para Arch. Recuérdalos para pasos posteriores.

## 2. Instalar dentro de Arch sage y jupyter

Para ello ejecutar dentro de la terminal de WSL Arch:

```sudo pacman -Syu --noconfirm sagemath jupyterlab```

Recuerda que al usar `sudo` te pedirá la contraseña y ¡ten paciencia!, el proceso es lento, pero luego ya estará casi. Con este paso SageMath ya está instalado. Se podría probar poniendo el comando `sage` y usar a través de la consola. Si hemos entrado para salir se hace con el comando `exit()`.

## 3. Hacer que se use el navegador externo

Para ello ejecutar dentro de la terminal de WSL Arch:

```
sudo bash -c "printf '[wslutilities]\nSigLevel=Never\nServer=https://raw.githubusercontent.com/joroldan/SageMathInstallationGuide/main/' >> /etc/pacman.conf"
sudo pacman -Syu --noconfirm wslu
export BROWSER=wslview && echo "export BROWSER=wslview" >> .bashrc
```

Con esto ya se abre el navegador de Windows al ejecutar dentro de Arch `jupyter lab` y podemos usar SageMath fácilmente.

## 4. Crear el acceso directo a SageMath en nuestro escritorio

Por último vamos a crear un acceso directo a SageMath en nuestro escritorio para facilitar el acceso. Para ello hacemos el acceso directo a mano poniendo como:
 - Destino (target): `%LocalAppData%\Microsoft\WindowsApps\arch.exe run 'export BROWSER=wslview && jupyter lab'`
 - Iniciar en (working directory): `%USERPROFILE%`

O ejecutamos las siguiente líneas en PowerShell (Windows):
```
$sh = New-Object -ComObject WScript.Shell
$s = $sh.CreateShortcut('$env:USERPROFILE\Desktop\SageMath.lnk')
$s.TargetPath = '$env:LocalAppData\Microsoft\WindowsApps\arch.exe' run "export BROWSER=wslview && jupyter lab"
$s.WorkingDirectory = '$env:USERPROFILE'
$s.Save()
```
De forma opcional puedes ponerle un icono bonito al acceso directo.

## 5. Poner el acceso directo a SageMath en el menú de inicio también

Copia el acceso de antes a `%AppData%\Microsoft\Windows\Start Menu\Programs`.
