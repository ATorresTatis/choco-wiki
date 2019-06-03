# Empaquetado Automático para Mantenimiento
El empaquetado automático es un proceso que los **mantenedores de paquetes pueden ejecutar por su cuenta** para mantener actualizados sus paquetes. No es un paso forzoso para mantener los paquetes en la fuente de la comunidad (https://chocolatey.org/packages), pero se recomienda que encuentre una forma de automatizar el despliegue de paquetes cuando haya actualizaciones, si va a mantener más de 5 paquetes y usted no es el proveedor de software para estos paquetes.

**NOTA:** No debe confundirse con la función de creación automática de paquetes en [Chocolatey for Business](https://chocolatey.org/pricing) - esa función crea paquetes directamente desde los archivos del instalador. La funcionalidad descrita a continuación, es para el mantenimiento de paquetes de paquetes existentes en el feed de la comunidad.

<!-- TOC -->

- [Métodos de actualización automática](#automatic-update-methods)
- [Actualizador automático (AU)](#automatic-updater-au)
  - [Créditos](#credits)
  - [Requerimientos](#requirements)
  - [Preparación](#setup)
  - [Todo lo relacionado con UA](#everything-related-to-au)
- [Chocolatey Package Updater también conocido como chocopkgup [OBSOLETO]](#chocolatey-package-updater-aka-chocopkgup-deprecated)
  - [Licenciamiento](#licensing)
  - [Créditos](#credits-1)
  - [Requerimientos](#requirements-1)
  - [Preparación](#setup-1)
  - [Creación de un paquete automático](#create-an-automatic-package)
    - [Creación de un paquete para el empaquetado automático](#create-a-package-for-automatic-packaging)
    - [Ketarin](#ketarin)
  - [Notas sobre los tri-paquetes (meta/virtual aka *, * .install y * .portable)](#notes-about-tri-packages-metavirtual-aka--install-and-portable)
  - [Pruebas de Ketarin/ChocoPkgUp:](#testing-ketarinchocopkgup)
  - [Solución de problemas/Notas](#troubleshootingnotes)
  - [Notas importantes para los archivos alojados en SourceForge](#important-notes-for-files-hosted-on-sourceforge)

<!-- /TOC -->

## Métodos de actualización automática

Actualmente hay dos métodos que se pueden utilizar para mantener de forma automática los paquetes:

- RECOMENDADO - Usar solo Powershell a través del [módulo de actualización automática AU](https://github.com/majkinetor/au).
- OBSOLTEO - Usar  [Chocolatey Package Updater](https://chocolatey.org/packages/ChocolateyPackageUpdater) en combinación con la  herramienta de terceros [Ketarin](https://chocolatey.org/packages/ketarin).


## Actualizador automático (AU)

Puede obtener más información sobre el actualizador de AU a través de su [documentación](https://github.com/majkinetor/au/blob/master/README.md). Es un módulo de PowerShell, por lo que hará todo el trabajo utilizando scripts de PowerShell. También puede ejecutar todo en AppVeyor, por lo que no es necesario que programe el actualizador en su propia máquina.

### Créditos

[Miodrag Milic](https://github.com/majkinetor), miembro de la comunidad de Chocolatey, ofrece AU que se está volviendo cada vez más impresionante.

### Requerimientos

* PowerShell v5+.
* [El modulo AU](https://chocolatey.org/packages/au).

### Preparación

1. Bifurque  [`chocolatey-packages-template`](https://github.com/chocolatey/chocolatey-packages-template#fork-destination-box) y cámbiele el nombre a algo como `chocolatey-packages` (en GitHub: vaya a Configuración, nombre del repositorio, renombrar).
2. Clone el repositorio localmente.
3. Vaya a la carpeta de configuración y busque el archivo `au_setup.ps1`. Revíselo y luego ejecútelo.
4. Siga las instrucciones en el archivo [README](https://github.com/chocolatey/chocolatey-packages-template/blob/master/setup/README.md) en la carpeta de configuración.

Al crear los paquetes, no utilice `--auto`. AU no utiliza el reemplazo de tokens para actualizar paquetes. En su lugar, reemplaza los elementos xml y el código directamente.

### Todo lo relacionado con UA
AU mantiene su propia documentación [aquí](https://github.com/majkinetor/au/blob/master/README.md).


## Chocolatey Package Updater también conocido como chocopkgup [OBSOLETO]
<a name="chocolatey-package-updater-aka-chocopkgup"></a>
http://chocolatey.org/packages/ChocolateyPackageUpdater

La herramienta que realiza este proceso se conoce como [chocopkgup](https://chocolatey.org/packages/ChocolateyPackageUpdater) (Chocolatey Package Updater). Es una herramienta gratuita (a menos que desee utilizarla para cargar archivos a otro lugar que no sea chocolatey.org).

### Licenciamiento
Verifique la licencia en http://realdimensions.net/licenses/chocolateypackageupdater/license.txt para asegurarse de que le aplica.

Básicamente se reduce a esto: si desea utilizar chocopkgup en privado, tendrá que pagar. ¡Mientras este publicando en chocolatey.org, la herramienta es gratis! La licencia caduca de vez en cuando, pero si se mantiene al día con sus actualizaciones de chocolate localmente, ni lo notará (Utilizar `cup all` ¿recuerda?).

### Créditos
Esta herramienta hace uso de [Ketarin](https://chocolatey.org/packages/ketarin). Ketarin es una herramienta increíble que ayuda a chocopkgup a realizar sus tareas.

### Requerimientos

* Una ventana de tiempo en algún lugar - para ejecutar el actualizador
* [Ketarin](https://chocolatey.org/packages/ketarin)
* [Chocolatey Package Updater](https://chocolatey.org/packages/chocolateypackageupdater)

### Preparación

1. Bifurque  [`chocolatey-packages-template`](https://github.com/chocolatey/chocolatey-packages-template#fork-destination-box) y cámbiele el nombre a algo como `chocolatey-packages` (En GitHub: vaya a Configuración, nombre del repositorio y renombrar).
2. Clone el repositorio localmente.
3. Instale chocopkgup (que instalará ketarin y nuget.commandline). `choco install chocolateypackageupdater`.
4. Compruebe la configuración en `$env:ChocolateyInstall\lib\ChocolateyPackageUpdater\tools\chocopkgup\chocopkgup.exe.config`. La entrada `PackagesFolder` debe apuntar a donde se encuentra su repositorio.
5. Cree una tarea programada (en Windows). Este es el comando (editar la ruta de acceso de`cmd.exe` en consecuencia): `C:\Windows\System32\cmd.exe /c c:\tools\chocolateypackageupdater\ketarinupdate.cmd`
6. Alternativamente para evitar que la ventana de comandos se abra en Windows, puede crear un script de VBS y poner la ruta al archivo  `.vbs` en lugar de ejecutar el comando `ketarinupdate.cmd`.El archivo debe tener lo siguiente:

    ~~~vb
    Set objShell = WScript.CreateObject("WScript.Shell")
    objShell.Run("C:\tools\ChocolateyPackageUpdater\ketarinupdate.cmd"), 0, True
    ~~~

7. Elija un horario para la tarea. Algunas personas ejecutan la tarea aproximadamente una vez por hora para detectar las actualizaciones tan pronto como ocurren.
8. Abra Ketarin. Elija `File` –> `Settings`.
9. Ahora haga clic en Importar.
10. Elija [setup/KetarinSettings.xml](https://github.com/chocolatey/chocolatey-packages-template/blob/master/setup/KetarinSettings.xml) en la carpeta de repositorio. Esto agregará toda la configuración necesaria.
11. Haga clic en Variables globales y asegúrese de que todas las variables se configuran adecuadamente.
![Ketarin Global Variables](images/chocopkgup/KetarinGlobalVariables.png)

Esto hace que Ketarin se configure con un comando global para todos los paquetes que creamos.

*NOTA*: Esto ha configurado comandos globales para "Antes de actualizar una aplicación" y "Después de actualizar una aplicación". No debería necesitar ajustes adicionales, sin embargo, si lo hace, asegúrese de volver a exportar la configuración.

### Crear un paquete de forma automática
Preferiblemente, tomar un paquete existente que ya se ha probado y convirtiéndolo en un paquete automático.

#### Crear un paquete para el empaquetado automático
Cuando esté creando paquetes, debe asegurarse de estar en la última versión de Chocolatey. Esto significa que tiene las últimas correcciones para las plantillas de empaquetado y las mejores formas de automatización.

1. Asegurándose de que esta en la última versión de Chocolatey - `choco upgrade chocolatey`.
2. Abra PowerShell (o cmd.exe) y diríjase a la carpeta de paquetes que este automatizando. Algo como "repolocation\automatic".
3. Ejecute `choco new <name> --auto [options]`. Puede usar una plantilla de paquete diferente si las tiene instaladas - vea https://chocolatey.org/docs/commands-new para listar todas las opciones o ejecute `choco new -?`. Para plantillas de paquetes vea https://chocolatey.org/docs/how-to-create-custom-package-templates.
4. Inspeccione la salida. Combine la lógica de su paquete existente si tiene uno que está convirtiendo.
5. Asegúrese que `checksumType` y `checksumType64` está configurado como `sha256` ya que este es el tipo de actualización que generará.
6. Realice los ajustes que necesite en el paquete para preparar el empaquetado.

#### Ketarin

1. Abrir Ketarin. Choose `File` –> `Import…`
2. Elija [ketarin/_KetarinChocolateyTemplate.xml](https://github.com/chocolatey/chocolatey-packages-template/blob/master/ketarin/_KetarinChocolateyTemplate.xml) de la carpeta repo.
3. Responda a las preguntas. Esto creará un nuevo trabajo para verificar en Ketarin.
4. Una cosa importante a tener en cuenta es que el nombre del trabajo **debe coincidir *exactamente* con el nombre de la carpeta del paquete y nuspec**.
5. Haga clic derecho en ese nuevo trabajo y seleccione `Edit`. Verifique lo siguiente
![Ketarin Job Main](images/chocopkgup/KetarinMain.png "Ketarin Job Main")
6. Clic en `Variables` a la derecha de la URL
![Ketarin Job Variables](images/chocopkgup/KetarinSetVariables.png "Ketarin Job Variables")
7. En el lado izquierdo debería ver una variable para la **versión** y una para **url64** . Haga clic en **versión**
8. Elija el método apropiado para usted. En este ejemplo he elegido **Content from URL (start/end)**.
9. Ingrese la URL para obtener información sobre las versiones.
![Ketarin Job Variables](images/chocopkgup/KetarinVariables.png "Ketarin Job Variables")
10. En el contenido en sí, resalte suficiente información para evaluar antes de una versión y de esta forma poder seleccionarla únicamente durante las actualizaciones (pero no tanta información como para que se detecte un cambio cada vez que cambia la página). Haga clic en **Usar selección como punto de inicio**.
11. Ahora observe que no fue demasiado lejos.
12. Haga lo mismo con la parte final, teniendo en cuenta que este lado no necesita ser demasiado porque se encuentra DESPUÉS del comienzo. Una vez seleccionado, haga clic en **Usar selección como punto final**.
13. Debería parecer algo similar a lo que se presenta en la imagen de arriba.
14. Si tiene una URL de 64 bits que desea procesar, haga lo mismo con la variable url64.
15. Cuando haya finalizado, haga clic en **OK**.
16. Haga clic en **OK** de nuevo.


### Notas sobre los tri-paquetes (meta/virtual aka *, * .install y * .portable)

**ACTUALIZACIÓN AGO 2016:** Esto ya no puede ser cierto. Sólo configure tres trabajos.

Cuando tenga los tres paquetes, debe configurar solo dos trabajos, uno para _*.install_ y otro para _*.portable_.

En cualquiera de los trabajos a los que apunte el paquete meta, debe agregar un comando como lo hizo para la configuración de todos los trabajos en ketarin.

1. Haga clic en la pestaña **Comandos** y establezca el comando **Editar evento para "Antes de actualizar una aplicación"**.
![Ketarin Settings](images/chocopkgup/KetarinJobSettings.png "Ketarin Settings")
2. Agregue el siguiente texto (reemplace `name` con  real de la carpeta del meta paquete)::

    ~~~cmd
    chocopkgup /p name /v {version} /u "{preupdate-url}" /u64 "{url64}" /pp "{file}" /c "{Checksum}" /c64 "{Checksumx64}"
    REM /disablepush
    ~~~

3. Revise la parte inferior de esta sección para asegurarse de que esté establecido en **Comando**.
![Ketarin Settings Command](images/chocopkgup/KetarinCustomCommand.png "Ketarin Settings Command")

### Prueba de Ketarin/ChocoPkgUp:

1. Necesitamos tener una buena idea de si esto funcionará o no.
2. Abra la línea de comando y escriba ketarin.
3. Una vez que se abre Ketarin, abra las opciones globales (pasos 8 y 11), vaya a Variables globales y configúralo `cscript` para `1` en lugar de `2` para que solo llegue hasta la creación de paquetes.
4. Encuentre su trabajo y haga clic derecho -> Actualizar. Si todo está bien configurado, en un momento tendrá un paquete Chocolatey en la carpeta que configuró `{PackagesFolder}\_output`, donde `{PackagesFolder}` está la ruta que estableció en la sección 5 de configuración de este artículo.
6. Inspeccione el (los) paquete (s) resultante de Chocolatey para cualquier problema.
7. También debe probar las tareas programadas de forma adecuada.

### Solución de problemas/Notas

* Ketarin viene con una instalación de registro para que pueda ver lo que está haciendo. Está en el menú Ver -> Mostrar registro.
* En la carpeta de nivel superior para chocopkgup (en datos del programa o program data), también se registra lo que  se recibe de Ketarin durante el proceso de armar un paquete.
* Verifique que el nombre de la aplicación en ketarin coincide exactamente con el de la carpeta que se encuentra en la carpeta de paquetes automáticos.
* De vez en cuando busque en Ketarin para ver qué trabajos podrían estar fallando. Averigue el por qué.
* De vez en cuando, querrá inspeccionar la carpeta `chocopkgup` para ver si hay algún paquete que no haya sido creado por alguna razón u otra y luego cargarlos.
* Si la aplicación/instalador descargado no ha cambiado, el paquete no se generará. Elimine los archivos en la ubicación de descarga especificada en [*Ketarin*](#ketarin) e intente nuevamente.

### Notas importantes para los archivos alojados en SourceForge
Pruebe esto primero:
* En la configuración avanzada, asegúrese de que el agente de usuario es chocolatey command line. Esto permitirá que ketarine se comporte de manera similar a como lo hace Chocolatey.
![Ketarin Job Advanced Settings](https://cloud.githubusercontent.com/assets/63502/7350038/b1928aaa-ecc2-11e4-8abe-af9e7c65c82a.png)

No es raro que ciertos espejos de SorceForge se desconecten o sean extremadamente lentos debido a la sobrecarga. Por lo tanto, no se recomienda utilizar enlaces directos de espejo (por ejemplo, http://heanet.dl.sourceforge.net/project/…) en su archivo `chocolateyInstall.ps1`, ya que con frecuencia esto romperá su paquete y lo hará poco confiable. 

Para evitar esto, use la siguiente convención para los archivos alojados en SourceForge:

No use `{{DownloadUrl}}` y `{{DownloadUrlx64}}` en su archivo `chocolateyInstall.ps1`, en esto su lugar (ejemplo de nomacs de la aplicación): $url = 'http://sourceforge.net/projects/nomacs/files/nomacs-{{PackageVersion}}/nomacs-setup-{{PackageVersion}}-x86.exe/download' y $url64 = 'http://sourceforge.net/projects/nomacs/files/nomacs-{{PackageVersion}}/nomacs-setup-{{PackageVersion}}-x64.exe/download' para otras aplicaciones, obviamente, tiene que usar los nombres reales de la aplicación/archivo. Es importante que use {{PackageVersion}} y no use ningún enlace directo que incluya los espejos de SourceForge.
