# Chocolatey vs Ninite

Mucha gente siempre quiere señalar que existe Ninite cuando alguien menciona Chocolatey. Eso está bien, Ninite funciona, pero solo tiene más de 90 cosas que puedes instalar. Están limitados por lo que Ninite se puede reagrupar y redistribuir. Ambas son soluciones sólidas por derecho propio, pero debe comprender las necesidades y lo que proporcionan las dos soluciones para elegir lo que mejor se adecue a sus necesidades

<!-- TOC -->

- [Enfoque de gestión de paquetes](#package-management-approach)
  - [Ninite](#ninite)
  - [Chocolatey](#chocolatey)
    - [Packaging solution needs (that brought about Chocolatey in the first place)](#packaging-solution-needs-that-brought-about-chocolatey-in-the-first-place)
- [Chocolatey and  Ninite : Compare and Contrast](#chocolatey-and--ninite--compare-and-contrast)
  - [Interfaces:](#interfaces)
  - [Packages:](#packages)
  - [Package sources:](#package-sources)
  - [Creating packages:](#creating-packages)
  - [Available packages:](#available-packages)
  - [Package updates:](#package-updates)
  - [Package dependencies:](#package-dependencies)
  - [Versioning/upgrades:](#versioningupgrades)
- [Conclusion](#conclusion)

<!-- /TOC -->


## Enfoque de gestión de paquetes

### Ninite
* Propósito principal: Ninite es un instalador que evita el crapware.
* Mantiene todo centralizado.
* Tiene una estrecha integración con los productos, ya que el personal de Ninite es el único que actualiza los paquetes.
* Garantiza el éxito con las instalaciones, ya que controlan todos los aspectos de los paquetes.
* No toma contribuciones.
* Todo está basado en GUI a menos que pague por la versión Pro..
* Actualiza las aplicaciones simplemente ejecutando el instalador nuevamente.
* El único caso de uso es para personas que tienen acceso para instalar aplicaciones en sus máquinas.
* Solo funciona con instaladores de software
* De fuente cerrada, pero gratuito.
* Opciones de pago para CLI.

### Chocolatey
* Propósito principal: Chocolatey es un motor de ejecución de PowerShell global capaz de procesar un formato de empaquetado
* Descentralizado, pero con un repositorio de paquetes de la comunidad.
* Múltiples fuentes, incluidas fuentes privadas.
* Los paquetes en https://chocolatey.org/packages (Repositorio de Paquetes Comunitarios de Chocolatey) son creados por la comunidad y revisados por moderadores.
* Los paquetes pueden incrustar software, usar rutas UNC o descargar software desde otra ubicación (como las ubicaciones de distribución oficiales).
* Permite contribuciones de la comunidad.
* Permite que las aplicaciones de pago se incluyan como paquetes.
* CLI enfocado, aunque hay una GUI (ChocolateyGUI)
* Fácilmente programable ya que permite agregar secuencias de comandos de configuración a cosas como el control de fuente.
* Actualiza aplicaciones simplemente ejecutando`cup packagename` o `choco upgrade all`.
* Integración con otros gestores de paquetes (Ruby Gems, Python PIP, WebPI, Windows Features, CygWin, etc.).
* Capaz de usarse sin necesidad de permisos administrativos (los paquetes portátiles no rqeuieren permisos administrativos)
* Los paquetes pueden funcionar con instaladores nativos, establecer y/o registrar configuraciones, además de realizar otras tareas o cualquier combinación
* De código abierto y gratuito.
* Opciones de pago [disponibles](https://chocolatey.org/compare).

#### Necesidades de empaquetado de aplicaciones (que inspiraron le desarrollo de Chocolatey)
* Una buena CLI simple de utilizar
* Un repositorio central que toma contribuciones de paquetes de la comunidad (además de ser mantienido por la comunidad)
* Capacidad para usar fuentes adicionales/múltiples
* Metapaquetes que pueden encadenar dependencias
* Paquetes virtuales
* Los paquetes deben ser fáciles de crear/mantener
* Los paquetes deben ser concisos y deben poder crearse sin preocuparse por los derechos de distribución
* Instalaciones desatendidas
* Instalación de múltiples paquetes con un comando
* Configuración de entornos a través de scripts
* Una herramienta que impone más seguridad automáticamente

## Chocolatey and  Ninite : Compare and Contrast

### Interfaces:
* Ninite - choose apps from a website, download installer just for those apps. Pay for the pro version and use the command line.
* Chocolatey - open a command line. Install app with `choco install appname <options>`. Lather rinse repeat.

### Packages:
* Ninite - closed, only items available are what Ninite staff choose to make available.
* Chocolatey - community packages on a central server
* Chocolatey (internal use) - create packages on your own internal repository server

### Package sources:
* Ninite - one at Ninite.com
* Chocolatey - central community package repository at https://chocolatey.org/packages, create and use public/private sources (folder, network share, OData feed like nuget.org, [chocolatey.org] and/or myget.org). See [[Host Your Own Server|How-To-Host-Feed]] for options.
* Chocolatey can also install from [[alternative sources|CommandsInstall#alternative-sources]] - choco install bash --source cygwin | choco isntall gemcutter --source ruby | choco install sphynx --source python | choco install IISExpress --source webpi

### Creating packages:
* Ninite - no
* Chocolatey - yes and quite simple. Run `choco new test` and look at the output - keep in mind that many times it takes complex tasks for managing software installation down to 1 PowerShell function call. Consider windirstat is: `Install-ChocolateyPackage 'windirstat' 'exe' '/S' 'https://windirstat.info/wds_current_setup.exe' -Checksum 123456 -ChecksumType 'sha256'`
* Chocolatey is building on technologies you may already know:
  * PowerShell - take full advantage of PowerShell.
  * Unattended installations / Silent installation
* Extend Chocolatey easily with PowerShell modules called [[extension packages|How-To-Create-Extensions]].
* Use [[Package Builder|FeaturesCreatePackagesFromInstallers]] to point Chocolatey to an installer and have it auto-detect and generate a full software deployment.
* Use [[Package Internalizer|FeaturesAutomaticallyRecompilePackages]] to internalize existing community packages quickly.

### Available packages:
* Ninite - Handled by Ninite staff, so there's less chance of anything being broken.
* Chocolatey (community repository) - Handled by the community, reviewed by moderators. Possibility of breakages unless using [licensed editions of Chocolatey](https://chocolatey.org/compare) due to [[CDN Cache|FeaturesPrivateCdn]].
* Chocolatey (internal repositories) - Handled by you, embedding software or using internal links you control. Zero chance of breakages that you don't control.

### Package updates:
* Ninite and Chocolatey community repository both can suffer from keeping packages up to date.
* Chocolatey (internal use) - good to go

### Package dependencies:
* Ninite - not really
* Chocolatey - Yes, dependencies are easy! Install Git Extensions, it makes sure Git is also installed.

### Versioning/upgrades:
* Ninite - sort of, you just rerun the installer every once in awhile
* Chocolatey - Yes. Consider `choco upgrade <pkgname> <options>` to upgrade a piece of software. Also consider `choco upgrade all`/`cup all` as a Windows Update for all of your 3rd party software.

## Conclusion
Chocolatey internal use is the best solution for an organization that has a low tolerance for breakages. There are no issues, you have a secure solution with complete control. You are building on top of technologies you know with a small amount of learning for packaging. Because it is PowerShell, you are not limited to just installers, and you can add additional logic before and after installations, and you are not limited to just "installing" software with packaging.

Ninite is a solid solution if you don't mind not being able to script it and only install the applications that it has listed on the Ninite page. You are, however, possibly guaranteed that you have everything you need to install sheerly by having the Ninite Installer. In that way it may be better than using Chocolatey's community repository, which most packages require access to the internet to download installers that do not have distribution rights with them (Ninite may not incur this extra point of failure, but is quite limited in its offerings). Chocolatey community repository with [licensed editions of Chocolatey](https://chocolatey.org/compare) have almost no chance of breakages due to a [[CDN Cache|FeaturesPrivateCdn]] of those downloads.

Chocolatey community repository has over 4,000 more packages than Ninite and a community that is driving to continually make it better. If you need to get to older versions of packages, many of the packages on the community repository allow for this. What Chocolatey community repository may lack in the possible guarantee that Ninite provides, it makes up for in features and options. Chocolatey can provide packages for non-free products, have multiple sources and folks can script the installations. Chocolatey is more than just an installer and with that does not require administrative privileges to use.

Both Ninite and Chocolatey community repository solutions suffer from the issue of having the most up-to-date packages available, it's just that Chocolatey is more transparent about it.

When it comes to internal use and creating and hosting your own (or internalizing existing) packages, nothing else holds a candle to Chocolatey. When you step up to [Chocolatey for Business](https://chocolatey.org/compare), you get access to features that allow an organization to really excel quickly.

Whether you use Chocolatey or Ninite, consider that the two answer the same question differently and that is okay. They can live in harmony with each other and at some point Chocolatey may offer Ninite as package source.
