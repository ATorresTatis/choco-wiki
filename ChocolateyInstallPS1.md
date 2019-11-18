# Script PowerShell para instalar Chocolatey
Chocolatey usa PowerShell como proveedor de instalación de paquetes y buscará este archivo en el paquete. Si lo encuentra, ejecutará el contenido del archivo, adjuntando los módulos auxiliares. Consulte la [Referencia de ayudante](HelpersReference) para obtener más información sobre cada uno de los ayudantes que puede incluir.

Realmente es solo PowerShell, por lo que puede usar PowerShell regular aquí y debería funcionar bien. Nota: Mantenga la compatibilidad con Posh v2. No todos los sistemas operativos que admitimos están en Posh v2 (ni viene OOB con Posh v3 +). Es mejor trabajar con la compatibilidad más amplia de sistemas que existe.

## ¿Cuándo se activa el script?
Si está presente en un paquete, el script `ChocolateyInstall.ps1` se activará en los siguientes puntos:
* Cuando se instala un paquete por primera vez, después de extraer el contenido del paquete.
* En un escenario de [Actualización](CommandsUpgrade), la secuencia de comandos de instalación para el nuevo paquete se ejecutará después de cualquier `chocolateyBeforeModify.ps1` ps1secuencia de comandos asociada con la versión anterior del paquete.

### Ejemplo?
Esto es lo que se necesita para instalar [StExBar](https://chocolatey.org/packages/stexbar):

```powershell
$name   = 'StExBar'
$url = 'http://stexbar.googlecode.com/files/StExBar-1.8.3.msi'
$url64 = 'http://stexbar.googlecode.com/files/StExBar64-1.8.3.msi'
$silent = '/quiet'

Install-ChocolateyPackage $name 'msi' $silent $url $url64
```

El asistente Install-ChocolateyPackage usa los url, msi y args silenciosos para descargar e instalar y actualizar silenciosamente StExBar.
