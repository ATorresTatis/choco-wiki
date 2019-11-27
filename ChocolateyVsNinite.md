# Chocolatey vs Ninite

Mucha gente siempre quiere señalar que existe Ninite cuando alguien menciona Chocolatey. Eso está bien, Ninite funciona, pero solo tiene más de 90 cosas que puedes instalar. Están limitados por lo que Ninite se puede reagrupar y redistribuir. Ambas son soluciones sólidas por derecho propio, pero debe comprender las necesidades y lo que proporcionan las dos soluciones para elegir lo que mejor se adecue a sus necesidades

<!-- TOC -->

- [Enfoque de gestión de paquetes](#package-management-approach)
  - [Ninite](#ninite)
  - [Chocolatey](#chocolatey)
    - [Necesidades de empaquetado de aplicaciones (que inspiraron el desarrollo de Chocolatey)](#packaging-solution-needs-that-brought-about-chocolatey-in-the-first-place)
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

#### Necesidades de empaquetado de aplicaciones (que inspiraron el desarrollo de Chocolatey)
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

## Chocolatey y Ninite: comparación y contraste

### Interfaces:
* Ninite: elija las aplicaciones de un sitio web, descargue el instalador solo para esas aplicaciones. Pague la versión pro y use la línea de comando.
* Chocolatey: abre una línea de comando. Instale las aplicaciones con choco install appname <options>. Repita por cada instalación.

### Paquetes:
* Ninite: cerrado, solo están disponibles los elementos que el personal de Ninite elige poner a disposición.
* Chocolatey - paquetes comunitarios en un servidor central
* Chocolatey (uso interno): cree paquetes en su propio servidor de repositorio interno

### Fuentes del paquete:
* Ninite - uno en Ninite.com
* Chocolatey - repositorio central de paquetes de la comunidad en https://chocolatey.org/packages, cree y use fuentes públicas/privadas (carpeta, recurso compartido de red, feed OData como nuget.org, [chocolatey.org] y/o [myget.org]). Consulte  [Hospedar su propio servidor](How-To-Host-Feed) para ver más opciones.
* Chocolatey también se puede instalar desde [fuentes alternativas ](CommandsInstall#alternative-sources) - choco install bash --source cygwin | choco isntall gemcutter --source ruby | choco install sphynx --source python | choco install IISExpress --source webpi

### Creación de paquetes:
* Ninite - no
* Chocolatey - sí y bastante simple. Ejecute  `choco new test` y observe el resultado - tenga en cuenta que muchas veces se requieren tareas complejas para administrar la instalación de algún software hasta 1 llamada a la función PowerShell. Considere por ejemplo  windirstat: `Install-ChocolateyPackage 'windirstat' 'exe' '/S' 'https://windirstat.info/wds_current_setup.exe' -Checksum 123456 -ChecksumType 'sha256'`
* Chocolatey se basa en tecnologías que quizás ya conozca:
  * PowerShell: aproveche al máximo PowerShell.
  * Instalaciones desatendidas/Instalaciones silenciosas.
* Extienda Chocolatey fácilmente con módulos de PowerShell llamados [paquetes de extensión](How-To-Create-Extensions).
* Utilice [Package Builder](FeaturesCreatePackagesFromInstallers) para apuntar a Chocolatey a un instalador y hacer que detecte automáticamente y genere una implementación de software completa.
* Utilice [Package Internalizer](FeaturesAutomaticallyRecompilePackages) para internalizar rápidamente los paquetes comunitarios existentes.

### Disponibilidad de paquetes:
* Ninite: manejado por el personal de Ninite, por lo que hay menos posibilidades de que algo se rompa.
* Chocolatey (repositorio comunitario) - manejado por la comunidad, revisado por moderadores. Posibilidad de roturas a menos que se utilicen [ediciones con licencia de Chocolatey](https://chocolatey.org/compare) debido a [CDN Cache](FeaturesPrivateCdn).
* Chocolatey (repositorios internos): manejado por usted, integrando software o utilizando enlaces internos que usted controla. Cero posibilidades de roturas que no controlas.

### Actualizaciones de paquetes:
* Tanto el repositorio de la comunidad de Ninite como el de Chocolatey pueden sufrir por mantener los paquetes actualizados.
* Chocolatey (uso interno) - listo para usar

### Dependencias de paquetes:
* Ninite - no realmente
* Chocolatey - ¡Sí, las dependencias son fáciles! Instala las extensiones de Git, se asegura de que Git también esté instalado.

### Versiones/actualizaciones:
* Ninite - de alguna manera, sólo tienes que volver a ejecutar el instalador de vez en cuando.
* Chocolatey - Si. Utilice `choco upgrade <pkgname> <options>` para actualizar una pieza de software. Considere también `choco upgrade all`/`cup all` como una actualización de Windows para todo su software de terceros.

## Conclusion
Chocolatey internal use is the best solution for an organization that has a low tolerance for breakages. There are no issues, you have a secure solution with complete control. You are building on top of technologies you know with a small amount of learning for packaging. Because it is PowerShell, you are not limited to just installers, and you can add additional logic before and after installations, and you are not limited to just "installing" software with packaging.

Ninite is a solid solution if you don't mind not being able to script it and only install the applications that it has listed on the Ninite page. You are, however, possibly guaranteed that you have everything you need to install sheerly by having the Ninite Installer. In that way it may be better than using Chocolatey's community repository, which most packages require access to the internet to download installers that do not have distribution rights with them (Ninite may not incur this extra point of failure, but is quite limited in its offerings). Chocolatey community repository with [licensed editions of Chocolatey](https://chocolatey.org/compare) have almost no chance of breakages due to a [[CDN Cache|FeaturesPrivateCdn]] of those downloads.

Chocolatey community repository has over 4,000 more packages than Ninite and a community that is driving to continually make it better. If you need to get to older versions of packages, many of the packages on the community repository allow for this. What Chocolatey community repository may lack in the possible guarantee that Ninite provides, it makes up for in features and options. Chocolatey can provide packages for non-free products, have multiple sources and folks can script the installations. Chocolatey is more than just an installer and with that does not require administrative privileges to use.

Both Ninite and Chocolatey community repository solutions suffer from the issue of having the most up-to-date packages available, it's just that Chocolatey is more transparent about it.

When it comes to internal use and creating and hosting your own (or internalizing existing) packages, nothing else holds a candle to Chocolatey. When you step up to [Chocolatey for Business](https://chocolatey.org/compare), you get access to features that allow an organization to really excel quickly.

Whether you use Chocolatey or Ninite, consider that the two answer the same question differently and that is okay. They can live in harmony with each other and at some point Chocolatey may offer Ninite as package source.
