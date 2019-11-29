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

## Conclusión
El uso interno de Chocolatey es la mejor solución para una organización que tiene una baja tolerancia a las fallas. No hay problemas, usted tiene una solución segura con control total. Está construyendo sobre tecnologías que conoce con una pequeña cantidad de aprendizaje para el empaquetado. Debido a que se trata de PowerShell, no se limita a los instaladores, y puede añadir lógica adicional antes y después de las instalaciones. Tampoco se limita a "instalar" software empaquetado.

Ninite es una solución sólida si no te importa no poder personalizar e instalar sólo las aplicaciones que aparecen listadas en la página de Ninite.  Pero, a su vez, obtiene la garantía de que todo lo que se necesita para instalar pura y simplemente está incluido en el Instalador de Ninite.  De cierta manera puede ser mejor que usar el repositorio de la comunidad de Chocolatey, que en la mayoría de los paquetes requiere acceso a Internet para descargar los instaladores que no tienen derechos de distribución (Ninite puede no incurrir en este punto extra de fallo, pero está bastante limitado en sus ofertas).  El repositorio de la comunidad de Chocolatey con ediciones licenciadas de Chocolatey no tiene casi ninguna posibilidad de roturas debido al uso de un [CDN Cache](FeaturesPrivateCdn) de descargas.

El repositorio de la comunidad de Chocolatey tiene más de 4.000 paquetes más que Ninite y una comunidad que se esfuerza por mejorarlo continuamente.  Si necesita acceder a versiones anteriores de paquetes, muchos de los paquetes en el repositorio de la comunidad lo permiten.  Lo que el repositorio de la comunidad de Chocolatey puede carecer, es la posible garantía que Ninite proporciona, lo que podría compensar características y algunas opciones.  Chocolatey puede proporcionar paquetes para productos que no son libres, tener múltiples fuentes y la gente puede escribir scripts de instalación.  Chocolatey es más que un simple instalador y con ello no requiere privilegios administrativos para su uso. 

Tanto las soluciones de repositorio de la comunidad de Ninite como las de Chocolatey sufren el problema de tener los paquetes más actualizados disponibles, pero Chocolatey es más transparente al respecto.

Cuando se trata del uso interno y de crear y alojar sus propios paquetes (o internalizar los ya existentes), nada puede compararse con Chocolatey.  Cuando usted se acerca a [Chocolatey for Business](https://chocolatey.org/compare), obtiene acceso a funciones que permiten a una organización sobresalir rápidamente.

Ya sea que usted use Chocolatey o Ninite, considere que las dos responden a la misma pregunta de manera diferente, lo que está bien.  Pueden vivir en armonía y en algún momento Chocolatey podría ofrecer a Ninite como repositorio de paquetes. 
