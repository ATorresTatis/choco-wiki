# Preguntas frecuentes
<!-- TOC insertAnchor:true -->

- [General](#general)
  - [¿No encuentra su respuesta aquí?](#cant-find-your-answer-here)
  - [¿Qué es chocolatey?](#what-is-chocolatey)
  - [Necesito una herramienta que administre software: usar scripts para trabajar con esas instalaciones desatendidas. ¿Eso es chocolate?](#i-need-a-tool-that-manages-software---using-scripts-to-work-with-those-unattended-installs-is-that-chocolatey)
  - [¿Cuál es el propósito de Chocolatey?](#what-is-the-purpose-of-chocolatey)
  - [¿Cómo funciona Chocolatey?](#how-does-chocolatey-work)
  - [¿Por qué Chocolatey?](#why-chocolatey)
  - [¿Puedo usar Chocolatey en mi organización?](#can-i-use-chocolatey-at-my-organization)
  - [¿Están redistribuyendo software?](#are-you-redistributing-software)
  - [¿Dónde se instala Chocolatey por defecto?](#where-does-chocolatey-install-by-default)
  - [¿Qué tipo de paquetes soporta Chocolatey?](#what-kind-of-package-types-does-chocolatey-support)
  - [¿Tienen una hoja de ruta que puedo ver?](#do-you-have-a-roadmap-i-can-see)
- [Seguridad](#security)
  - [¿Chocolatey es seguro?](#is-chocolatey-secure)
  - [¿Por qué tengo que confirmar los paquetes ahora? ¿Hay alguna forma de eliminar esto?](#why-do-i-have-to-confirm-packages-now-is-there-a-way-to-remove-this)
  - [¿Por qué no se implementa el estándar de seguridad X? ](#what-doesnt-the-website-implement-x-security-standard)
  - [Tengo otras preguntas de seguridad](#i-have-other-security-questions)
- [Using Chocolatey](#using-chocolatey)
  - [Can I use Chocolatey in a cmd.exe shell?](#can-i-use-chocolatey-in-a-cmdexe-shell)
  - [Tab-completion?](#tab-completion)
  - [What is the difference between Open Source Chocolatey, Chocolatey Pro, and Chocolatey for Business?](#what-is-the-difference-between-open-source-chocolatey-chocolatey-pro-and-chocolatey-for-business)
  - [I'm interested in C4B (Chocolatey for Business) but I have questions.](#im-interested-in-c4b-chocolatey-for-business-but-i-have-questions)
  - [Does Chocolatey require administrative permissions to run?](#does-chocolatey-require-administrative-permissions-to-run)
  - [I would like to be able to offer my non-admin desktop users an option for self-service type of installations.](#i-would-like-to-be-able-to-offer-my-non-admin-desktop-users-an-option-for-self-service-type-of-installations)
  - [Can I use Chocolatey with existing installs?](#can-i-use-chocolatey-with-existing-installs)
  - [What is the default package source repository URL (community feed url)?](#what-is-the-default-package-source-repository-url-community-feed-url)
  - [What can I install?](#what-can-i-install)
  - [What if I install X and I already have X installed?](#what-if-i-install-x-and-i-already-have-x-installed)
  - [Can I override the installation directory?](#can-i-override-the-installation-directory)
  - [What distinction does Chocolatey make between an installable and a portable application?](#what-distinction-does-chocolatey-make-between-an-installable-and-a-portable-application)
    - [Installable application](#installable-application)
    - [Portable application – something that doesn't require a system install to use](#portable-application--something-that-doesnt-require-a-system-install-to-use)
  - [Why doesn't a package install software to Program Files?](#why-doesnt-a-package-install-software-to-program-files)
  - [What is the difference between packages no suffix as compared to *.install *.portable?](#what-is-the-difference-between-packages-no-suffix-as-compared-to-install-portable)
  - [When I install a portable app like autohotkey.portable, how is it on my path? Without littering my path?](#when-i-install-a-portable-app-like-autohotkeyportable-how-is-it-on-my-path-without-littering-my-path)
  - [Is there a PowerShell Module for Chocolatey?](#is-there-a-powershell-module-for-chocolatey)
  - [Does Chocolatey run on macOS/Linux?](#does-chocolatey-run-on-macoslinux)
- [Troubleshooting](#troubleshooting)
  - [I'm running into some issue with Chocolatey, packaging, or something else.](#im-running-into-some-issue-with-chocolatey-packaging-or-something-else)
- [Organizational Use](#organizational-use)
  - [I would like to use Chocolatey in my organization, is the licensing friendly?](#i-would-like-to-use-chocolatey-in-my-organization-is-the-licensing-friendly)
  - [Should my organization depend on (use) the community feed (https://chocolatey.org/packages)?](#should-my-organization-depend-on-use-the-community-feed-httpschocolateyorgpackages)
  - [Chocolatey is great! I need it to do something additional for my organization.](#chocolatey-is-great-i-need-it-to-do-something-additional-for-my-organization)
- [Licensed Editions](#licensed-editions)
  - [What is the difference between FOSS and the licensed editions?](#what-is-the-difference-between-foss-and-the-licensed-editions)
  - [Are the licensed editions costs annual?](#are-the-licensed-editions-costs-annual)
  - [Can you do monthly?](#can-you-do-monthly)
  - [What is C4B?](#what-is-c4b)
  - [I have not received my license.](#i-have-not-received-my-license)
  - [I just purchased and I need my license sooner!](#i-just-purchased-and-i-need-my-license-sooner)
  - [I have a different question about the licensed edition.](#i-have-a-different-question-about-the-licensed-edition)
- [Packaging](#packaging)
  - [What can a Chocolatey Package consist of?](#what-can-a-chocolatey-package-consist-of)
  - [Tell me about packaging](#tell-me-about-packaging)
  - [How do I create packages?](#how-do-i-create-packages)
  - [I'm creating packages with the software contained in the package.](#im-creating-packages-with-the-software-contained-in-the-package)
  - [I'm creating internal or offline packages, what do I need?](#im-creating-internal-or-offline-packages-what-do-i-need)
- [Videos / Reference](#videos--reference)
  - [Where can I learn more?](#where-can-i-learn-more)
  - [Do you have any references or videos I can see?](#do-you-have-any-references-or-videos-i-can-see)
  - [Is there a video I can watch to show me Chocolatey in action?](#is-there-a-video-i-can-watch-to-show-me-chocolatey-in-action)
- [Community Package Repository](#community-package-repository)
  - [I just took over as the primary maintainer of a package. What do I need to do?](#i-just-took-over-as-the-primary-maintainer-of-a-package-what-do-i-need-to-do)
  - [What is moderation?](#what-is-moderation)
  - [How does the moderation review process work?](#how-does-the-moderation-review-process-work)
  - [What is a trusted package?](#what-is-a-trusted-package)
  - [How do I install a package version under moderation?](#how-do-i-install-a-package-version-under-moderation)
  - [How do I install an unlisted package / package version?](#how-do-i-install-an-unlisted-package--package-version)
  - [How do I install a rejected package?](#how-do-i-install-a-rejected-package)
  - [How do I self-reject a package?](#how-do-i-self-reject-a-package)
  - [What is the validator?](#what-is-the-validator)
  - [What is the verifier?](#what-is-the-verifier)
  - [What is the package scanner?](#what-is-the-package-scanner)
  - [What is the package cacher?](#what-is-the-package-cacher)
- [Comparison](#comparison)
  - [How is Chocolatey different than OneGet/PowerShell Package Management?](#how-is-chocolatey-different-than-onegetpowershell-package-management)
  - [How is Chocolatey different than Ninite?](#how-is-chocolatey-different-than-ninite)
  - [How is Chocolatey different than NuGet and/or OpenWrap?](#how-is-chocolatey-different-than-nuget-andor-openwrap)
  - [How is/will Chocolatey be different than apt?](#how-iswill-chocolatey-be-different-than-apt)

<!-- /TOC -->

<a id="markdown-general" name="general"></a>
## General

<a id="markdown-cant-find-your-answer-here" name="cant-find-your-answer-here"></a>
### ¿No encuentra su respuesta aquí?
No dude en comunicarse con nosotros en [Gitter](https://gitter.im/chocolatey/choco) o por la [lista de distribución de correo electrónico/foro](https://groups.google.com/group/chocolatey)

<a id="markdown-what-is-chocolatey" name="what-is-chocolatey"></a>
### ¿Qué es chocolatey?
Chocolatey es algo así como apt-get, pero para Windows (con Windows vienen algunas limitaciones). Es un administrador de paquetes a nivel de máquina que se construye sobre la línea de comandos nuget y la infraestructura de nuget.
[[Más detrás del nombre |Historia]]

"OK, un administrador de paquetes de la máquina, eso es bueno, pero ¿qué significa?" Significa que simplemente puede instalar el software con algunas pulsaciones de teclas e ir a tomar un café mientras sus compañeros de trabajo están descargando y ejecutando una instalación manualmente (y quiero decir algo así como un MSI).

¿Qué hay de las actualizaciones? ¿No sería bueno actualizar casi todo en su máquina con unas pocas y sencillas pulsaciones? Nosotros también lo creemos. Chocolatey hace eso `choco upgrade all -y`

<a id="markdown-i-need-a-tool-that-manages-software---using-scripts-to-work-with-those-unattended-installs-is-that-chocolatey" name="i-need-a-tool-that-manages-software---using-scripts-to-work-with-those-unattended-installs-is-that-chocolatey"></a>
### Necesito una herramienta que administre software: usar scripts para trabajar con esas instalaciones desatendidas. ¿Eso es chocolate?
Sí, en pocas palabras, eso es lo que hace Chocolatey. Casi exactamente lo que ya está haciendo, excepto que está envuelto en un archivo de paquete que le permite modularizar y administrar fácilmente el pedido con dependencias de otros paquetes.

<a id="markdown-what-is-the-purpose-of-chocolatey" name="what-is-the-purpose-of-chocolatey"></a>
### ¿Cuál es el propósito de Chocolatey?

Gran pregunta ! Vea[El propósito de Chocolatey](Why#what-is-the-purpose-of-chocolatey)

<a id="markdown-how-does-chocolatey-work" name="how-does-chocolatey-work"></a>
### ¿Cómo funciona Chocolatey?

Vea [¿Qué es Chocolatey?[(Why#what-is-chocolatey)

<a id="markdown-why-chocolatey" name="why-chocolatey"></a>
### ¿Por qué Chocolatey?
Primero una [Historia](ChocolateyStory). y luego [¿Por qué Chocolatey?](Why)

<a id="markdown-can-i-use-chocolatey-at-my-organization" name="can-i-use-chocolatey-at-my-organization"></a>
### ¿Puedo usar Chocolatey en mi organización?
¡Absolutamente! La licencia es muy amigable para los negocios (además, tenemos [opciones de pago](https://chocolatey.org/compare) para ayudar mejor a las organizaciones: *sugerido*, *sugerido*). Por lo general, recomendamos que las organizaciones que dependen de Chocolatey manejen su propio empaquetado en lugar de usar el [Community Package Repository](https://chocolatey.org/packages) – ya que los paquetes puede que no sean 100% confiables debido a los derechos de distribución relacionados con paquetes disponibles públicamente (lo que haría un punto de falla importante). Vea la siguiente pregunta para más detalles.

<a id="markdown-are-you-redistributing-software" name="are-you-redistributing-software"></a>
### ¿Están redistribuyendo software?
No. Los paquetes en el [repositorio comunitario de Chocolatey](https://chocolatey.org/packages) están disponibles públicamente y, como tales, están sujetos a los derechos de distribución de software. Con esos paquetes se aplica lo siguiente

> Chocolatey hace lo mismo que usted haría en base a las instrucciones del paquete. Por lo general, esto significa ir a Internet y descargar un instalador desde el punto de distribución oficial para luego instalarlo silenciosamente en su máquina. Con la mayoría de los paquetes, esto significa que Chocolatey no está redistribuyendo el software porque va al mismo punto de distribución al que usted mismo iría a obtener el software si estuviera realizando este proceso manualmente

Para decirlo de otra manera, Microsoft estaría bastante molesto si los paquetes de Office 365 en el repositorio de la comunidad contuvieran los binarios de Office 365. Esto no es algo a lo que las organizaciones estarían sujetas cuando alojan su propio paquete interno.

Cuando aloja sus propios paquetes internos, esos paquetes pueden incrustar software y/o apuntar a recursos compartidos internos. De esta forma no está sujeto a derechos de distribución de software, por lo que puede crear paquetes que sean más confiables, sin conexión y seguros. Consulte [[Qué son los paquetes de Chocolatey]|(GettingStarted#what-are-chocolatey-packages) para más detalles.

Para obtener más información sobre las advertencias organizativas sobre el repositorio de paquetes de la comunidad, consulte [exención de responsabilidad del repositorio de la comunidad]|(CommunityPackagesDisclaimer).

<a id="markdown-where-does-chocolatey-install-by-default" name="where-does-chocolatey-install-by-default"></a>
### ¿Dónde se instala Chocolatey por defecto?
A partir de la versión 0.9.8.24, los binarios, bibliotecas y componentes de Chocolatey se instalan en ```C:\ProgramData\chocolatey``` (variable de entorno% ProgramData%) de forma predeterminada. Esto reduce la superficie de ataque en una instalación local de Chocolatey y limita quién puede realizar cambios en el directorio.


**NOTA:** Históricamente, Chocolatey se instalaba en ```C:\Chocolatey``` pero actualmente, realizando una actualización de Chocolatey se cambia la ubicación de la instalación, excepto cuando la ruta de instalación es ```C:\chocolatey```. Se actualizará esa ruta y todas las variables de forma automática. Para obtener más información sobre por qué se usó Chocolatey C:\Chocolatey como la ubicación predeterminada, consulte aquí [Razonamiento de instalación](DefaultChocolateyInstallReasoning)

<a id="markdown-what-kind-of-package-types-does-chocolatey-support" name="what-kind-of-package-types-does-chocolatey-support"></a>
### ¿Qué tipo de paquetes soporta Chocolatey?
* Paquetes binarios: aplicaciones instalables/portátiles: esto es el 98% de los paquetes Chocolatey. La mayoría son indicadores de los instaladores nativos y/ o del software comprimido.
* Paquetes de comandos de PowerShell: los paquetes que tienen el sufijo **.powershell** instalarán los scripts de PowerShell como comandos para que pueda llamarlos desde cualquier lugar.
* Paquetes de desarrollo - Paquetes que tienen el sufijo **.dev**. Por ejemplo [dropkick.dev](http://nuget.org/list/packages/dropkick.dev).
* Hojas de ruta - Paquetes virtuales - Paquetes que son como una categoría y solo desea un paquete de esa categoría. [Lea más aquí](https://github.com/chocolatey/chocolatey/issues/7)

<a id="markdown-do-you-have-a-roadmap-i-can-see" name="do-you-have-a-roadmap-i-can-see"></a>
### ¿Tienen una hoja de ruta que puedo ver?
Sí, echa un vistazo a [roadmap](Roadmap)


<a id="markdown-security" name="security"></a>
## Seguridad

<a id="markdown-is-chocolatey-secure" name="is-chocolatey-secure"></a>
¿Chocolatey es seguro?
Sí lo es. Puede leer más en [seguridad](Secutity) para comprender los detalles importantes.

<a id="markdown-why-do-i-have-to-confirm-packages-now-is-there-a-way-to-remove-this" name="why-do-i-have-to-confirm-packages-now-is-there-a-way-to-remove-this"></a>
### ¿Por qué tengo que confirmar los paquetes ahora? ¿Hay alguna forma de eliminar esto?
Respuesta corta sí, es completamente posible. Solo necesita establecer `allowGlobalConfirmation` o utilizar `-y`.

Consulte también la ayuda de  - `choco -h`, `choco install -h`

Respuesta larga, nos hemos acercado un poco más a otros administradores de paquetes por razones de seguridad, donde, por defecto, nos detenemos y confirmamos si está de acuerdo con el cambio de estado. Siempre comunicamos los cambios en las [notas de liberación](ReleaseNotes)/[Changelog](https://github.com/chocolatey/choco/blob/master/CHANGELOG.md), que también terminan en el archivo [nuspec](https://chocolatey.org/packages/chocolatey#releasenotes), por lo que recomendamos encarecidamente que la gente escanee al menos uno de ellos para ver cualquier cosa etiquetada como cambios importantes. Siempre escanee desde su versión actual hasta la que está actualizando para que pueda ver todos los cambios.

El cambio más importante en este momento es el `x.y.z` lanzamiento (en este caso, 0.9.9), una vez que lleguemos a v1 seremos totalmente compatibles con SemVer y los cambios de última hora constituirán un obstáculo importante en la versión (todavía estamos en SemVer menos v1), para que pueda escanear cambios importantes y nuevas características importantes en una `x` versión, nuevas características compatibles en una `.y` versión y las versiones `.z` soo contendrán correcciones compatibles para la versión actual.

0.9.9 introdujo un nuevo cliente compilado que fue/es una reescritura total. 0.9.10 y tendrá una paridad de características completa con el cliente anterior; consulte [FeatureParity](https://github.com/chocolatey/choco/labels/FeatureParity). ¿Por qué la reescritura? Para un cliente más rápido y más fácil de mantener que puede ejecutarse en mono, por lo que no está completamente vinculado a Windows. Hemos comenzado a agregar soporte para otros proveedores de instalación como [Scriptcs](https://github.com/chocolatey/choco/issues/247).

[Fragmentos relevantes de las notas de la versión](ReleaseNotes#099-march-3-2015) de las preguntas frecuentes

 - [Seguridad] Solicitud de confirmación: por razones de seguridad, ahora nos detenemos para la confirmación antes de cambiar el estado del sistema en la mayoría de los comandos. Puede pasar -y para confirmar cualquier solicitud o establecer un valor en la configuración que lo establecerá globalmente y se comportará como en las versiones anteriores de Chocolatey (`allowGlobalConfirmation` vea `choco feature -h` para saber cómo habilitarlo).

Algunas personas pueden encontrar el cambio bastante molesto. La perspectiva de algunas personas no es la perspectiva de todos y tenemos algunas personas muy conscientes de la seguridad que quieren una verificación de que lo que solicitaron, es con lo que terminan. Entonces este aviso es extremadamente importante para ellos. Nos estamos moviendo a un enfoque más seguro por defecto, por lo que este cambio fue importante para llegar allí. Los cambios relacionados con la seguridad son algunas de las únicas cosas que verá que afectan a Chocolatey de esa manera.

Pasamos muchos meses estresados por este cambio debido en parte a la ruptura y decidimos que no sería más fácil cambiarlo más adelante. Hemos agregado la capacidad para que vuelva a poner a Chocolatey en la forma en que estaba antes de `allowGlobalConfirmation` y si las indicaciones lo molestan, probablemente debería considerar hacer este cambio.

<a id="markdown-what-doesnt-the-website-implement-x-security-standard" name="what-doesnt-the-website-implement-x-security-standard"></a>
### ¿Por qué no se implementa el estándar de seguridad X? 
Si bien nos mantenemos al día con la mayoría de los aspectos de seguridad, a veces nos podemos perder algunas cosas. Siéntase libre de comunicarse con nosotros si siente que hay algo que debemos implementar para mejorarlo.

<a id="markdown-i-have-other-security-questions" name="i-have-other-security-questions"></a>
### Tengo otras preguntas de seguridad
Consulte [seguridad](Security) o comuníquese con nosotros si no puede encontrar respuestas a lo que está buscando.


<a id="markdown-using-chocolatey" name="using-chocolatey"></a>
## Uso de Chocolatey

<a id="markdown-can-i-use-chocolatey-in-a-cmdexe-shell" name="can-i-use-chocolatey-in-a-cmdexe-shell"></a>
### ¿Puedo usar Chocolatey en un shell cmd.exe?
Sí, Chocolatey tiene varios clientes oficiales, uno de los cuales es `choco.exe` que es una herramienta de línea de comandos, por lo que funciona igual de bien en Powershell.exe y cmd.exe. Sin embargo, si tiene instalado el perfil de PowerShell, también admite la característica de Tab-completion en Powershell.exe.

<a id="markdown-tab-completion" name="tab-completion"></a>
### Tab-completion?
Consulte la página [[troubleshooting|Troubleshooting]] si `choco <tab>` no funciona cuando utiliza PowerShell.

<a id="markdown-what-is-the-difference-between-open-source-chocolatey-chocolatey-pro-and-chocolatey-for-business" name="what-is-the-difference-between-open-source-chocolatey-chocolatey-pro-and-chocolatey-for-business"></a>
### ¿Cuál es la diferencia entre Open Source Chocolatey, Chocolatey Pro y Chocolatey for Business?
Buena pregunta, tenemos una tabla de comparación en [comparación](https://chocolatey.org/compare). También hay una sección de preguntas frecuentes relacionada específicamente con las licencias.

<a id="markdown-im-interested-in-c4b-chocolatey-for-business-but-i-have-questions" name="im-interested-in-c4b-chocolatey-for-business-but-i-have-questions"></a>
### Estoy interesado en C4B (Chocolatey for Business) pero algunas tengo preguntas.
Consulte la sección [de ediciones con licencia](#licensed-editions).

<a id="markdown-does-chocolatey-require-administrative-permissions-to-run" name="does-chocolatey-require-administrative-permissions-to-run"></a>
### ¿Chocolatey requiere permisos administrativos para ejecutarse?
Lo hace de manera predeterminada, según dónde esté instalado. Sin embargo, hay una instalación no administrativa para Chocolatey en [instalación|Installation]. Tenga en cuenta que hay una transferencia a lo que están haciendo los paquetes que determina si el paquete necesita permisos administrativos, y Chocolatey funciona dentro del contexto de los permisos de Windows, por lo que finalmente no podrá evitarlo (consulte la pregunta a continuación).

<a id="markdown-i-would-like-to-be-able-to-offer-my-non-admin-desktop-users-an-option-for-self-service-type-of-installations" name="i-would-like-to-be-able-to-offer-my-non-admin-desktop-users-an-option-for-self-service-type-of-installations"></a>
### Me gustaría poder ofrecer a mis usuarios de escritorio que no son administradores una opción para instalaciones de tipo autoservicio.
Sí, apoyamos ese escenario en Chocolatey for Business. Consulte [Ediciones con licencia](#licensed-editions) para más información.

<a id="markdown-can-i-use-chocolatey-with-existing-installs" name="can-i-use-chocolatey-with-existing-installs"></a>
### ¿Puedo usar Chocolatey con instalaciones existentes??
Fantástica pregunta, vea [¿Puedo usar Chocolatey con software existente?]|(Why#can-i-use-chocolatey-with-existing-software)

<a id="markdown-what-is-the-default-package-source-repository-url-community-feed-url" name="what-is-the-default-package-source-repository-url-community-feed-url"></a>
### ¿Cuál es la URL predeterminada del repositorio de origen del paquete (URL de feed de comunidad)?
Eso sería https://chocolatey.org/api/v2/ también conocido como Community Package Repository.

<a id="markdown-what-can-i-install" name="what-can-i-install"></a>
### ¿Qué puedo instalar?
Puede empaquetar e instalar cualquier cosa en Windows usando Chocolatey. Si puede automatizarse, Chocolatey y PowerShell pueden instalarlo, actualizarlo y desinstalarlo

Sin embargo, si tiene curiosidad sobre lo que está disponible en la comunidad, consulte el repositorio de paquetes de la comunidad en http://chocolatey.org/packages. Tenga en cuenta que tiene una gran limitación, los derechos de distribución, lo que hace que el repositorio de paquetes de la comunidad no sea totalmente confiable, diferente a un repositorio interno que no está sujeto a derechos de distribución.

También puede instalar paquetes de otras fuentes (nuget.org, rubygems.org, herramientas web, etc).

<a id="markdown-what-if-i-install-x-and-i-already-have-x-installed" name="what-if-i-install-x-and-i-already-have-x-installed"></a>
### ¿Qué sucede si instalo X y ya tengo X instalado?
Con la mayoría de los paquetes cuando ya tiene algo instalado, el proceso de Chocolatey solo realizará la instalación nuevamente de forma silenciosa. La mayoría de las veces esto significa que no hace nada y al final tiene lo que ya tenía.

<a id="markdown-can-i-override-the-installation-directory" name="can-i-override-the-installation-directory"></a>
### ¿Puedo anular el directorio de instalación??
Sí se puede. Vea [Anulando el directorio de instalación](GettingStarted#overriding-default-install-directory-or-other-advanced-install-concepts) y [Opción de directorio de instalación ubicua](FeaturesInstallDirectoryOverride).

<a name="AppVsTool"></a>
<a id="markdown-what-distinction-does-chocolatey-make-between-an-installable-and-a-portable-application" name="what-distinction-does-chocolatey-make-between-an-installable-and-a-portable-application"></a>
### ¿Qué distinción hace Chocolatey entre una aplicación instalable y una portátil?
<a id="markdown-installable-application" name="installable-application"></a>
#### Aplicación instalable
Una aplicación instalable es algo que viene con un instalador nativo y termina con una entrada en el panel de control bajo las opciones de programas de agregar/quitar. Las aplicaciones instalables terminan donde el instalador nativo quiere que terminen (es decir, archivos de programa). Si desea anular eso, siéntase libre de usar los comandos adecuados usando InstallArgs (-ia) desde la línea de comando. Sí, esto significa que necesitará tener un conocimiento profundo del instalador. Es probable que Chocolatey cree el directorio de anulación en algún momento, pero ese tema está completamente fuera del radar (finalmente a Rob se le paga por trabajar de alguna manera en Chocolatey a tiempo completo;) ).

<a id="markdown-portable-application--something-that-doesnt-require-a-system-install-to-use" name="portable-application--something-that-doesnt-require-a-system-install-to-use"></a>
#### Aplicación portátil: algo que no requiere la instalación de un sistema para ser utilizado
Una aplicación portátil es algo que no requiere un instalador nativo para su uso. En otras palabras, no está "instalado" en su sistema (donde puede ir a desinstalar en el panel de control). Tampoco requiere acceso administrativo para la instalación del paquete.

Las aplicaciones portátiles terminan en la carpeta %ChocolateyInstall%/lib (C:\ProgramData\Chocolatey\lib), pero se les genera un "shim" para colocarlas en en PATH de la máquina. Este comportamiento es muy similar a cómo funciona Chocolatey y no es configurable (el directorio). Donde terminan las aplicaciones portátiles seguirá siendo %ChocolateyInstall%/lib sin importar dónde mueva el directorio, a menos que un paquete en sí mismo desempaquete la aplicación portátil en otro lugar (como en el caso de [git-tfs](http://chocolatey.org/packages/gittfs)).

<a id="markdown-why-doesnt-a-package-install-software-to-program-files" name="why-doesnt-a-package-install-software-to-program-files"></a>
### ¿Por qué un paquete no instala software en los archivos de programa?
La mayoría de los paquetes que usan instaladores nativos (MSI, InnoSetup, etc.) se instalarán en Archivos de programa, pero hay paquetes que no lo hacen. Hay dos razones realmente importantes para que eso ocurra:

* Archivos de programa es sinónimo de software que tiene claves de desinstalación en el registro, o dicho de otro modo, aplicaciones que tienen instaladores nativos que puede encontrar para desinstalar en el Panel de control bajo Programas y características.
* Escribir en Archivos de programa requiere permisos administrativos y el paquete que está instalando es probablemente un paquete portátil (incluso si no se menciona explícitamente, puede tener un zip que se extrae). También hay una forma para que los no administradores utilicen Chocolatey y este tipo de paquetes también deben funcionar para ellos.

Realmente depende del software subyacente que el paquete "instala". Si el software subyacente es un instalador nativo, entonces tiene una instalación de máquina (lo que significa que obtiene una clave de registro para la desinstalación y aparece en Programas y características) y los Archivos de programa son el lugar apropiado para ello.

Chocolatey tiene una vía diferente para los paquetes portátiles que les permite a los administradores y no administradores poder usar estos paquetes, después de todo, solo están descargando y descomprimiendo un archivo. Estos paquetes van a una ubicación raíz de herramientas o simplemente obtienen shims (los archivos ejecutables se colocan en la ruta) y continúan permaneciendo en el directorio lib de Chocolatey. Si restringiéramos esto a un no administrador no funcionaría para ellos manualmente, ni haría que Choco sea útil para ellos. Como admitimos el uso de Chocolatey para usuarios no administradores, los paquetes que pueden admitir el modelo portátil deberían admitirlo.

También considere que si el paquete está usando `$env:ChocolateyBinRoot` (que luego se denominará `$env:ChocolateyToolsRoot`) puede configurar la raíz en Archivos de programa y  obtendrá lo mejor de ambos mundos.

<a id="markdown-what-is-the-difference-between-packages-no-suffix-as-compared-to-install-portable" name="what-is-the-difference-between-packages-no-suffix-as-compared-to-install-portable"></a>
### ¿Cuál es la diferencia entre paquetes sin sufijo en comparación con *.install y *.portable?

¿Cuál es la diferencia entre los paquetes llamados *.install (como [autohotkey.install](https://chocolatey.org/packages/autohotkey.install)), *.portable (como [autohotkey.portable](https://chocolatey.org/packages/autohotkey.portable)) y * (como [autohotkey](https://chocolatey.org/packages/autohotkey))?

Casi el 100% del tiempo, un paquete sin sufijo (autohotkey en este ejemplo) garantizará la instalación. El paquete sin el sufijo se utiliza para brindar la capacidad de detección como para que otros paquetes dependan de él.

¡Buena pregunta! ¡Estás prestando atención! Chocolatey tiene el concepto de paquetes virtuales (próximos) y metapaquetes. Los paquetes virtuales son paquetes que representan otros paquetes cuando se usan como dependencia. Los metapaquetes son paquetes que solo existen para proporcionar una agrupación de dependencias.

Un paquete sin sufijo rodeado de paquetes con sufijos es como proporcionar un paquete virtual. Entonces, en el caso de git, git.install y git.commandline (en desuso por .portable), git es ese paquete virtual (actualmente es un metapaquete hasta que se complete la función de paquetes virtuales). Eso significa que otros paquetes podrían depender de él y podría tener instalado git.install o git.portable y conocería la dependencia para tener instalado git. Eso evita que Chocolatey intente instalar algo que ya cumple con el requisito de dependencia para un paquete.

Hablando específicamente sobre el sufijo de paquete * .install: esos son para los paquetes que tienen un instalador nativo que han incluido o que se descargan y ejecutan.

**NOTA:** el sufijo * .app se ha utilizado anteriormente para significar lo mismo que * .install. Pero el sufijo * .app ahora está en desuso y no debe usarse para nuevos paquetes.

Los paquetes * .portable son los paquetes que generalmente darán como resultado un archivo ejecutable en su ruta en algún lugar, pero no se instalarán en el sistema (Agregar o quitar programas). Anteriormente, los sufijos * .tool y * .commandline se usaban para referirse al mismo tipo de paquetes.

**NOTA:** ahora * .tool y * .commandline están en desuso y no deben usarse para nuevos paquetes.

¿Quieres más información? Vea http://ferventcoder.com/archive/2012/02/25/chocolatey---guidance-on-packaging-apps-with-both-an-install.aspx

<a id="markdown-when-i-install-a-portable-app-like-autohotkeyportable-how-is-it-on-my-path-without-littering-my-path" name="when-i-install-a-portable-app-like-autohotkeyportable-how-is-it-on-my-path-without-littering-my-path"></a>
### Cuando instalo un paquete portátil como autohotkey.portable, ¿cómo se agrega al PATH? ¿Sin dañar mi PATH?
Cuando instala aplicaciones portátiles que tienen ejecutables en el paquete, Chocolatey crea automáticamente un archivo "shim" y lo coloca en una carpeta que se encuentra en la ruta. Eso le permite ejecutar una aplicación portátil solicitándola en la línea de comando.

Cuando toma una aplicación con un instalador nativo, digamos como WinDirStat, solo está en su ruta si el instalador nativo la ha colocado allí o las instrucciones en el paquete de Chocolatey han solicitado que esté en la ruta. 

<a id="markdown-is-there-a-powershell-module-for-chocolatey" name="is-there-a-powershell-module-for-chocolatey"></a>
### ¿Existe un módulo PowerShell para Chocolatey?
No hay ninguno oficial de Chocolatey Software. Cuanfo exista, se liberará probablemente como una DLL binaria.

El cliente principal de Chocolatey (choco.exe) es un cliente ejecutable que ejecuta un host PowerShell en proc y tiene un módulo PowerShell que w3ccarga para esos scripts de automatización de PowerShell. Intentar poner todas estas ideas en un módulo PowerShell superior podría ser un poco difícil.

Aunque originalmente se escribió en PowerShell, **Chocolatey NUNCA fue un módulo de PowerShell, solo usó PowerShell como lenguaje de programación y estaba destinado a ser una aplicación CLI.** Esto aparece en negrita esto para que pueda leerse dos veces ;)

Un poco de historia: Chocolatey hasta 0.9.9 se proporcionó completamente escrito en PowerShell, con el enfoque anterior. No conocemos ninguna otra aplicación / herramienta que haya intentado este enfoque cuando lo hicimos, lo que hizo que el cliente original de Chocolatey fuera una rareza. Allanó el camino para cosas como Pester [Pester](https://github.com/pester/Pester) ([Matt Wrock](https://github.com/mwrock) [added mocking](https://github.com/pester/Pester/compare/b103a3db951f123c485289f02eaa1d6ef686c21b...4178c343a6574a8a9521be8a77006572fc49e311) after [Rob Reynolds](https://github.com/ferventcoder) [determined](https://github.com/chocolatey/chocolatey/commit/5b2887240dfbda86629d6a1a296129f3a561e86a#diff-b61a6d542f9036550ba9c401c80f00ef) [the](https://github.com/chocolatey/chocolatey/commit/cc4aca0dc48840c7113167bd08aeddcaf83f65c0#diff-b61a6d542f9036550ba9c401c80f00ef) [general way](https://github.com/chocolatey/chocolatey/commit/ee883242c962dc886cd1282e4dbe4121d4fcc6cd#diff-b61a6d542f9036550ba9c401c80f00ef) [it works](https://github.com/chocolatey/chocolatey/commit/654703b9d4388eb385776986ce6d0ee53485a146#diff-b61a6d542f9036550ba9c401c80f00ef) in PowerShell back in 2012).

<a id="markdown-does-chocolatey-run-on-macoslinux" name="does-chocolatey-run-on-macoslinux"></a>
### Does Chocolatey run on macOS/Linux?
Speaking of POSIX environments, ever since we released 0.9.9 back in 2015, we've had it running in Mono which allows you to do package maintenance and simple things outside of managing software installations on Linux and macOS environments.

In fact we first showed it off at PuppetConf 2014 (prior to the official March 2015 release!) - https://www.youtube.com/watch?v=cZl_wKSciVk

Do we have plans to support fully running on POSIX environments? We've discussed it, but have no official stance on it yet. Keep your eyes on the [[roadmap|Roadmap]]


<a id="markdown-troubleshooting" name="troubleshooting"></a>
## Troubleshooting

<a id="markdown-im-running-into-some-issue-with-chocolatey-packaging-or-something-else" name="im-running-into-some-issue-with-chocolatey-packaging-or-something-else"></a>
### I'm running into some issue with Chocolatey, packaging, or something else.
See [[Troubleshooting|Troubleshooting]]



<a id="markdown-organizational-use" name="organizational-use"></a>
## Organizational Use

<a id="markdown-i-would-like-to-use-chocolatey-in-my-organization-is-the-licensing-friendly" name="i-would-like-to-use-chocolatey-in-my-organization-is-the-licensing-friendly"></a>
### I would like to use Chocolatey in my organization, is the licensing friendly?

Yes, it is. Chocolatey carries a FOSS Apache 2.0 license, which is extremely business friendly. You can use Chocolatey and most of its infrastructure completely free. Chocolatey also has a business edition with features organizations need for better software management . See [Compare](https://chocolatey.org/pricing) for details.

<a id="markdown-should-my-organization-depend-on-use-the-community-feed-httpschocolateyorgpackages" name="should-my-organization-depend-on-use-the-community-feed-httpschocolateyorgpackages"></a>
### Should my organization depend on (use) the community feed (https://chocolatey.org/packages)?

For production-level scenarios, I couldn't justify giving up that level of control and trust to the internet in an organization. It's recommended that you copy and modify existing packages and/or create your own internal packages and host them internally. That way you can completely guarantee that an install/upgrade/uninstall will always work every time. See [[Security|Security#chocolateyorg-the-community-feed]] for more details.

If you are just setting up or updating developer workstations and can tolerate things breaking every once in awhile because internet/uncertainty, it's fine to use the community feed.

<a id="markdown-chocolatey-is-great-i-need-it-to-do-something-additional-for-my-organization" name="chocolatey-is-great-i-need-it-to-do-something-additional-for-my-organization"></a>
### Chocolatey is great! I need it to do something additional for my organization.
Please see https://chocolatey.org/compare - we may already support it doing that for the business edition. If not, feel free to reach out to our team.

Also see the [Licensed Editions](#licensed-editions) section below.



<a id="markdown-licensed-editions" name="licensed-editions"></a>
## Licensed Editions

<a id="markdown-what-is-the-difference-between-foss-and-the-licensed-editions" name="what-is-the-difference-between-foss-and-the-licensed-editions"></a>
### What is the difference between FOSS and the licensed editions?
A lot of that is covered in the FAQ on the [pricing](https://chocolatey.org/pricing#faq), but also be sure to check out the [comparison table](https://chocolatey.org/pricing#compare).

<a id="markdown-are-the-licensed-editions-costs-annual" name="are-the-licensed-editions-costs-annual"></a>
### Are the licensed editions costs annual?
They are, but we can also do multi-year if you need to support something closer to that model. We also have a perpetual for Chocolatey for Business. For more detail, please see the [pricing FAQ](https://chocolatey.org/pricing#faq).

<a id="markdown-can-you-do-monthly" name="can-you-do-monthly"></a>
### Can you do monthly?
Not at this current time. Please see the [pricing FAQ](https://chocolatey.org/pricing#faq) for more details.

<a id="markdown-what-is-c4b" name="what-is-c4b"></a>
### What is C4B?
That is the short name for Chocolatey for Business.

<a id="markdown-i-have-not-received-my-license" name="i-have-not-received-my-license"></a>
### I have not received my license.
The license email is sent from a support email at chocolatey dot io with an xml file (the license) attachment within 1-3 business days. If it has been 3 business days and you have not received your business license, please reach through the [sales contact](https://chocolatey.org/contact) (choose "Other") (or any method you may already have for contacting sales) to get this resolved.

Any number of things could have happened:

* The message could be block by your servers
* The message could be misidentified as spam

To reduce these kind of occurrences, please make sure you have whitelisted the following email domains:

* `chocolatey.io`
* `chocolatey.org`

Once you receive a few emails from there, it will give you an idea of how to lock that down further to fewer email addresses.

<a id="markdown-i-just-purchased-and-i-need-my-license-sooner" name="i-just-purchased-and-i-need-my-license-sooner"></a>
### I just purchased and I need my license sooner!
Just reply to the order email you receive and let us know so we can bump the priority of your order.

<a id="markdown-i-have-a-different-question-about-the-licensed-edition" name="i-have-a-different-question-about-the-licensed-edition"></a>
### I have a different question about the licensed edition.
Check out the FAQ on the [pricing](https://chocolatey.org/pricing#faq). If it doesn't answer your questions, please feel free to reach out to the sales team from there!



<a id="markdown-packaging" name="packaging"></a>
## Packaging

<a id="markdown-what-can-a-chocolatey-package-consist-of" name="what-can-a-chocolatey-package-consist-of"></a>
### What can a Chocolatey Package consist of?
See [[What are Chocolatey Packages?|GettingStarted#what-are-chocolatey-packages]]

<a id="markdown-tell-me-about-packaging" name="tell-me-about-packaging"></a>
### Tell me about packaging
Chocolatey packages are what we like to think of as just fancy zip files. Zip files that have package metadata about the package and the underlying software a package may represent, dependencies, and optional binaries, files, and/or optional PowerShell automation scripts.

<a id="markdown-how-do-i-create-packages" name="how-do-i-create-packages"></a>
### How do I create packages?
Try running `choco new test` from a command shell and inspect the output. You will find quite a bit of helpful information and just in time documentation in there.

<a id="markdown-im-creating-packages-with-the-software-contained-in-the-package" name="im-creating-packages-with-the-software-contained-in-the-package"></a>
### I'm creating packages with the software contained in the package.
Great! This is the most reliable use of Chocolatey, to embed the binaries directly in the package. See the next question for more details.

<a id="markdown-im-creating-internal-or-offline-packages-what-do-i-need" name="im-creating-internal-or-offline-packages-what-do-i-need"></a>
### I'm creating internal or offline packages, what do I need?
Well, if you are not creating packages for the community package repository, you have different rules that apply. Embed as much as possible into the package (as long as it is under 500MB you should see no issues). We typically recommend 500MB as the threshhold for organizations for the following reasons:

* a nupkg file size takes up some space
* files in the package directory (can be cleaned up as part of the script)
* the actual install location if using an installer
* MSI cache for MSIs - Windows caches the complete MSI binaries (and now you know where all that space went)

If you are on a licensed edition of Chocolatey, you can turn on Package Reducer and the first two items above no longer take up any significant space. This can reduce space usage in the order of GBs for some installations of Chocolatey. See [[Package Reducer|FeaturesPackageReducer]] for more details.



<a id="markdown-videos--reference" name="videos--reference"></a>
## Videos / Reference

<a id="markdown-where-can-i-learn-more" name="where-can-i-learn-more"></a>
### Where can I learn more?
We have a documentation section of the site at https://chocolatey.org/docs

<a id="markdown-do-you-have-any-references-or-videos-i-can-see" name="do-you-have-any-references-or-videos-i-can-see"></a>
### Do you have any references or videos I can see?
Yes we do, take a look at [[videos|Videos]] and [[known posts, presentations, etc|Resources]].

<a id="markdown-is-there-a-video-i-can-watch-to-show-me-chocolatey-in-action" name="is-there-a-video-i-can-watch-to-show-me-chocolatey-in-action"></a>
### Is there a video I can watch to show me Chocolatey in action?
There is! This is a long video due to slow internet connections, but watch the first 1:30ish minutes and the last 1:30ish minutes and that will give you a general idea. [http://www.youtube.com/watch?v=N-hWOUL8roU](http://www.youtube.com/watch?v=N-hWOUL8roU)

**NOTE:** This video shows dependency chaining, so you are seeing it install 11 applications/tools. It's also 6+ years old and there have been many, many improvements since then.



<a id="markdown-community-package-repository" name="community-package-repository"></a>
## Community Package Repository

<a id="markdown-i-just-took-over-as-the-primary-maintainer-of-a-package-what-do-i-need-to-do" name="i-just-took-over-as-the-primary-maintainer-of-a-package-what-do-i-need-to-do"></a>
### I just took over as the primary maintainer of a package. What do I need to do?
See [[Package Maintainer Handover|PackageMaintainerHandover]]

<a id="markdown-what-is-moderation" name="what-is-moderation"></a>
### What is moderation?
Related to the community package repository only (aka the default feed aka https://chocolatey.org/packages), we have a concept called moderation, where submitted packages are held until they are considered safe and of minimal quality for regular consumption.

Moderation involves checking a package version for quality (validation) and correctness, whether it installs and uninstalls correctly (verification). We have two automated services that validate and verify packages. The validator checks the quality of a package. If no requirements are flagged as failing review, it will be passed on to the verifier, which checks that the package actually works as intended (it may help to think of the validator as unit testing and the verifier as integration testing). If both of these automated reviews pass the package version is submitted to a moderator for final review and approval.

Things to note:
* We have trusted packages, and those packages skip human review/moderation.
* A maintainer can not moderate his/her own pkgs.
* You can see if a package has been verified by the green circle next to its name on the package page. If it is green or red, it will also be a clickable link. To see all packages verified, see https://gist.github.com/choco-bot
* Besides trusted packages, a package version is never approved without a moderator clicking approve.

<a id="markdown-how-does-the-moderation-review-process-work" name="how-does-the-moderation-review-process-work"></a>
### How does the moderation review process work?
See [[Review Process|Moderation#package-review-process]].

<a id="markdown-what-is-a-trusted-package" name="what-is-a-trusted-package"></a>
### What is a trusted package?
Related to the community package repository only (aka the default feed aka https://chocolatey.org/packages).

A package that is considered trusted comes from the original software creator or is maintained by someone in the community who has a track record for high quality and safe packages.

Two ways your packages can become trusted:
* You write the underlying software that the package installs. For instance the ReSharper package that comes directly from JetBrains.
* You put in a lot of good packages and your packages will eventually become trusted.

For a package to switch to trusted, a moderator must manually make the change. It is not an automated process.

**Note:** Once everything is ready, all packages will go under automated verification and validation and be held for fixes if they don't pass, even trusted packages.

**Note:** Another note, we've been setting trust per package. That is planned to change at some point for the most part as the trust level has always been about the maintainer and not always the package itself.

<a id="markdown-how-do-i-install-a-package-version-under-moderation" name="how-do-i-install-a-package-version-under-moderation"></a>
### How do I install a package version under moderation?
Related to the community package repository only (aka the default feed aka https://chocolatey.org/packages).

You can install a version of a package version that's still under moderation - however know that if the maintainer needs to fix the package version during the review process, you will never get those fixes locally since they are updating the ***SAME*** version. Package versions are not immutable until they are approved. The caveat for "never" is that if you know it changed (likely you won't and there is no notification, *what you have installed technically never existed*), you could force the reinstall of that same version of the package.

Another thing to consider: if the package version or the package as a whole is rejected (usually for renaming the package to something better to better meet naming standards), you are likely to get weird warnings later and won't see updates at all. Remember, you have installed something that technically never existed, so any thing you see related to choco not knowing about it is to be expected and not a bug.

To actually install, see the next question.

<a id="markdown-how-do-i-install-an-unlisted-package--package-version" name="how-do-i-install-an-unlisted-package--package-version"></a>
### How do I install an unlisted package / package version?
You need to specify name AND version to any package to install the unlisted/unapproved version. This goes for any NuGet compatible feed that understands unlisted packages.

<a id="markdown-how-do-i-install-a-rejected-package" name="how-do-i-install-a-rejected-package"></a>
### How do I install a rejected package?
Related to the community package repository only (aka the default feed aka https://chocolatey.org/packages), we have a concept of packages that have been rejected. You cannot install a rejected package. It could do bad things to your system so we don't allow install from the community repository.

<a id="markdown-how-do-i-self-reject-a-package" name="how-do-i-self-reject-a-package"></a>
### How do I self-reject a package?
**NOTE**: This applies during the moderation process only on the community repository. Once approved, there is no reject.

If you are a maintainer of a package and you would like to self-reject an older version of a package that is failing verification or validation, we support that. If however you just want to reject a working package because it is older, we don't support that. Rejected != Obsolete. It's really about when the underlying software has the same download url for every release so the older versions do not apply. If you are using checksums to verify the download (and you should be), then your older versions should start failing.

![image](https://cloud.githubusercontent.com/assets/63502/12429736/8c67689c-beb1-11e5-83e9-02fe1db91272.png)

* Failing verification -
![image](https://cloud.githubusercontent.com/assets/63502/12429697/509d2b94-beb1-11e5-9e1d-73a156117672.png)
* Failing validation - a message from the validator telling you it failed validation.

<a id="markdown-what-is-the-validator" name="what-is-the-validator"></a>
### What is the validator?
The [validator](https://github.com/chocolatey/package-validator) is a service that checks the quality of a package based on requirements, guidelines and suggestions for creating packages for Chocolatey’s community feed. Many of the validation items will automatically roll back into choco and will be displayed when packaging a package. We like to think of the validator as unit testing. It is validating that everything is as it should be and meets the minimum requirements for a package on the community feed.

What does the validator check? https://github.com/chocolatey/package-validator/wiki

<a id="markdown-what-is-the-verifier" name="what-is-the-verifier"></a>
### What is the verifier?
The [verifier](https://github.com/chocolatey/package-verifier) is a service that checks the correctness (that the package actually works), that it installs and uninstalls correctly, has the right dependencies to ensure it is installed properly and can be installed silently. The verifier runs against both submitted packages and existing packages (currently checking once a month that a package can still install and sending notice when it fails). We like to think of the verifier as integration testing. It’s testing all the parts and ensuring everything is good. On the site, you can see the current status of a package based on a little colored ball next to the title. If the ball is green or red, the ball is a link to the results (only on the package page, not in the list screen).

![Passing verification](https://cloud.githubusercontent.com/assets/63502/11872220/bf58f590-a499-11e5-84bb-6fcf6d320227.png)

* Green means good. The ball is a link to the results
* Orange if still pending verification (has not yet run).
* Red means it failed verification for some reason. The ball is a link to the results.
* Grey means unknown or excluded from verification (if excluded, a reason will be listed on the package page).

<a id="markdown-what-is-the-package-scanner" name="what-is-the-package-scanner"></a>
### What is the package scanner?
All packages (and the binaries they contain or download at runtime) on community repository are scanned by 50-60 antivirus scanners. We have partnered with [VirusTotal](https://virustotal.com) to provide this information back to the website so you can know when you are on a package page whether it is something you should be concerned with or not. It falls just under the files section of the package pages.

**NOTE**: Did you know that 60% or more of the sofware that is submitted to the community repository has its first scans by VirusTotal through Chocolatey's package scanner submissions? It's helped many of those anti-virus manufacturers get a clearer picture of heuristics and hopefully ends up in better anti-virus products with less false positives.

**NOTE**: Need runtime malware protection? Learn more about [[runtime malware protection|]]

<a id="markdown-what-is-the-package-cacher" name="what-is-the-package-cacher"></a>
### What is the package cacher?
On the community repository, we have a CDN cache for those files that would be downloaded by packages - those remote urls are overridden by default in licensed editions of Chocolatey to use those cached binaries. This is to avoid 404 errors you would normally see if those urls changed or were removed. See [[Customer CDN Download Cache|FeaturesPrivateCdn]] for more details.



<a id="markdown-comparison" name="comparison"></a>
## Comparison

<a id="markdown-how-is-chocolatey-different-than-onegetpowershell-package-management" name="how-is-chocolatey-different-than-onegetpowershell-package-management"></a>
### How is Chocolatey different than OneGet/PowerShell Package Management?
OneGet is a package manager ***manager***, which means [it is not really a package manager at all](http://blogs.msdn.com/b/garretts/archive/2015/05/05/10-things-about-oneget-that-are-completely-different-than-you-think.aspx). Chocolatey will have a provider that plugs right into OneGet. At the current time there is a CTP available, but it is based on 2 year old Chocolatey technology (we've had security fixes since then, plus a world of features), so we can't really recommend it. But if you must use it, make sure your PowerShell execution policy is set correctly and you are in an administrative console. See http://www.hanselman.com/blog/AptGetForWindowsOneGetAndChocolateyOnWindows10.aspx for more details.

Use ChocolateyGet for now.

<a id="markdown-how-is-chocolatey-different-than-ninite" name="how-is-chocolatey-different-than-ninite"></a>
### How is Chocolatey different than Ninite?
Great question, see [[Chocolatey vs Ninite|ChocolateyVsNinite]].

<a id="markdown-how-is-chocolatey-different-than-nuget-andor-openwrap" name="how-is-chocolatey-different-than-nuget-andor-openwrap"></a>
### How is Chocolatey different than NuGet and/or OpenWrap?
Chocolatey is a machine package manager. Where NuGet/OW are focused on developer library packages, Chocolatey is focused on applications and tools, and not necessarily developer focused.

A typical way of stating the difference is "Developers use NuGet to get 3rd party libraries that they use to build the .NET tools and applications that they release with Chocolatey!"

<a id="markdown-how-iswill-chocolatey-be-different-than-apt" name="how-iswill-chocolatey-be-different-than-apt"></a>
### How is/will Chocolatey be different than apt?

 * Chocolatey does not support the idea of source packages, which are packages that must be built to be used. For someone interested in that, check out https://github.com/Microsoft/vcpkg.
 * Library packages are not completely off the plate, but mostly. How would you link the library up to the application/tool?
