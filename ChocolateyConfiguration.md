# Configuración de Chocolatey

Hay configuraciones y características que pueden personalizar la forma en que Chocolatey funciona. La siguiente es una lista de las configuraciones y características de configuración y sus valores predeterminados.

<!-- TOC -->

- [Configuraciones globales](#config-settings)
  - [General](#general)
  - [Proxy](#proxy)
  - [Timeouts](#timeouts)
  - [Otros](#other)
- [Configuraciones globales - Edición con licencia](#config-settings---licensed-edition)
  - [Chocolatey Central Management](#chocolatey-central-management)
  - [Paquete acelerador](#package-throttle)
  - [Instalación de servicios de Windows](#windows-services-installation)
  - [Auto-servicio / Background Mode](#self-service--background-mode)
  - [Comprobación de virus](#virus-checking)
  - [Timeouts](#timeouts-1)
- [Características](#features)
  - [General](#general-1)
  - [Desinstalador automático](#automatic-uninstaller)
  - [Códigos de salida](#exit-codes)
  - [Control de flujo](#flow-control)
  - [Seguridad](#security)
  - [Otros](#other-1)
- [Características - Edición con licencia](#features---licensed-edition)
  - [General](#general-2)
  - [Control de Acceso/Seguridad](#access-control--security)
  - [Chocolatey Central Management](#chocolatey-central-management-1)
  - [Internalizador de paquetes](#package-internalizer)
  - [Reductor de paquetes](#package-reducer)
  - [Sincronización de paquetes](#package-synchronization)
  - [Autoservicio  / Background Mode](#self-service--background-mode-1)
  - [Comprobación de virus](#virus-checking-1)
  - [Otros](#other-2)

<!-- /TOC -->


## Configuraciones globales

Los ajustes de configuración se establecen usando `choco config set --name="'<nameFromBelow>'" --value="'<value>'"`y se reestablecen a los valores predeterminados con `choco config unset --name="'<nameFromBelow>'"`. Para más información, vea [[ choco configcommand | CommandsConfig]] o ejecute `choco config -?`.

### General
* `cacheLocation` = **' '** - Ubicación del caché cuando no se quiere utilizar la carpeta TEMP. Reemplaza el valor de `$env:TEMP`. Se recomienda encarecidamente que este ajuste se realice para que Chocolatey sea más determinista en la limpieza.

### Proxy
* `proxy` = **' '** - Ubicación de proxy explícita. Disponible desde la versión 0.9.9.9+.
* `proxyUser` = **' '** - Usuario proxy opcional. Disponible desde la versión 0.9.9.9+.
* `proxyPassword` = **' '**  - Contraseña de proxy opcional. Encriptada. Disponible desde la versión 0.9.9.9+.
* `proxyBypassList` = **' '** - Lista de omisión de proxy opcional. Separado por comas. Disponible desde la versión 0.10.4+.
* `proxyBypassOnLocal` = **'true '** - Omitir proxy para conexiones locales. Disponible desde la versión 0.10.4+.

### Timeouts
* `commandExecutionTimeoutSeconds` = **'2700'** - Tiempo de espera predeterminado para la ejecución del comando. '0' para infinito (Disponible desde la versión 0.10.4). Se recomienda que las organizaciones establezcan esto hasta por lo menos 4 horas (14400).
* `webRequestTimeoutSeconds` = **'45'** - Tiempo de espera predeterminado para solicitudes web. Disponible desde la versión 0.9.10+.

### Otros
* `containsLegacyPackageInstalls` = **'true'** - La instalación tiene paquetes instalados anteriores a la versión 0.9.9.

## Configuraciones para las ediciones con licencia
### Chocolatey Central Management
* `centralManagementServiceUrl` = **' '** - La URL que se debe utilizar para comunicarse con Chocolatey Central Management. Debería verse parecida a https://servicemachineFQDN:24020/ChocolateyCentralManagement. Más detalles en https://chocolatey.org/docs/features-chocolatey-central-management#fqdn-usage . Disponible en las ediciones de negocios v2.0.0 o superiores.

* `centralManagementReportPackagesTimerIntervalInSeconds` = **'1800'** - Cantidad de tiempo, en segundos, entre cada ejecución del servicio en segundo plano para informar los paquetes instalados y desactualizados a Chocolatey Central Management. Disponible en las ediciones de negocios v2.0.0 o superiores.

* `centralManagementReceiveTimeoutInSeconds` = **'30'** - Cantidad de tiempo, en segundos, que el agente en segundo plano debe esperar para recibir información de Chocolatey Central Management. Disponible en las ediciones de negocios v2.0.0 o superiores.

* `centralManagementSendTimeoutInSeconds` = **'30'** - la cantidad de tiempo, en segundos, que el agente en segundo plano debe esperar para enviar información a Chocolatey Central Management. Disponible en las ediciones de negocios v2.0.0 o superiores.

* `centralManagementCertificateValidationMode` = **'PeerOrChainTrust'** - el modo del certificado que se usa en la comunicación con Chocolatey Central Management. Disponible en las ediciones de negocios v2.0.0 o superiores.

### Acelerador
* `maximumDownloadRateBitsPerSecond` = **' '** - La velocidad máxima de descarga en bits por segundo. '0' o vacío significa que no hay límite máximo. Un número significa que será la velocidad de descarga máxima en bps. El valor predeterminado es ''. Disponible solo en ediciones licenciadas 1.10 o superiores. Más detalles en  https://chocolatey.org/docs/features-download-throttle

### Instalación de Windows Services
* `serviceInstallsDefaultUserName` = **'ChocolateyLocalAdmin'** - el nombre de usuario predeterminado que se utiliza al instalar servicios cuando no se especifica uno. El valor predeterminado es 'ChocolateyLocalAdmin'. La característica 'useLocalSystemForServiceInstalls' debe configurarse en 'falso' para usar este campo. Disponible en ediciones de negocios 1.12.0 o superiores.

* `serviceInstallsDefaultUserPassword` = **' '** La contraseña de usuario predeterminada que se utiliza para instalar servicios cuando no se especifica una. El valor predeterminado es ''. Cuando es '', se generará un valor como un hash cifrado específico de la máquina. No hay forma de conocer este valor. La característica 'useLocalSystemForServiceInstalls' debe configurarse en 'falso' para usar este campo. Disponible en ediciones de negocios 1.12.0 o superior.

### Auto-Servicio / Segundo plano
* `backgroundServiceAllowedCommands` = **'install,upgrade'** - Comandos permitidos del servicio en segundo plano: los diferentes comandos que se dirigirán a través del servicio en segundo plano separados por coma o punto y coma. Compatible con todos los comandos operativos. No compatible con comandos que cambian la configuración (config, source, feature, apikey, etc.) El valor predeterminado es 'install, upgrade'. Disponible solo en las ediciones de negocios 1.12.4 o superior.

### Comprobación de virus
* `virusCheckMinimumPositives` = **'4'** - Número mínimo de resultados positivos de escaneo antes de marcar un binario como un posible virus. Se utiliza cuando `virusScannerType` es `VirusTotal`. Disponible en versiones 0.9.10 o superiores, pero solo para ediciones con licencia. Más información en https://chocolatey.org/docs/features-virus-check

* `virusScannerType` = **'VirusTotal'** - Tipo de escáner de virus (Generic o VirusTotal). El valor predeterminado es VirusTotal para las ediciones Pro. Disponible en versiones 0.9.10 o superiores, pero solo para ediciones con licencia. Más información https://chocolatey.org/docs/features-virus-check

* `genericVirusScannerPath` = **' '** - La ruta completa al ejecutable del escáner de virus de la línea de comandos. Se utiliza cuando `virusScannerType` es `Generic`. Disponible en versiones 0.9.10 o superiores, pero solo para ediciones con licencia. Más información https://chocolatey.org/docs/features-virus-check

* `genericVirusScannerArgs` = **'[[File]]'** - los argumentos para pasar al analizador genérico de virus. Utilice [[File]] como marcador de posición de la ruta del archivo a analizar. Se utiliza cuando `virusScannerType` es `Generic`. Disponible en versiones 0.9.10 o superiores, pero solo para ediciones con licencia. Más información https://chocolatey.org/docs/features-virus-check

* `genericVirusScannerValidExitCodes` = **'0'** - los códigos de salida del antivirus genérico cuando un archivo no está marcado como virus. Puede separar una lista de valores con coma, el valor predeterminado es 0. Se utiliza cuando `virusScannerType` es `Generic`. Disponible en versiones 0.9.10 o superiores, pero solo para ediciones con licencia. Más información https://chocolatey.org/docs/features-virus-check

### Timeouts
0* `centralManagementReceiveTimeoutInSeconds` = **'30'** - la cantidad de tiempo, en segundos, que el agente de fondo debe esperar para recibir información de Chocolatey Central Management. Disponible en versiones 2.0.0 o superiores, pero solo para ediciones Bussiness.
* `centralManagementSendTimeoutInSeconds` = **'30'** -  la cantidad de tiempo, en segundos, que el agente de fondo debe esperar para enviar información a Chocolatey Central Management.  Disponible en versiones 2.0.0 o superiores, pero solo para ediciones Bussiness


## Caracteristicas

Las características se ajustan utilizando  `choco feature enable|disable --name="'<nameFromBelow>'"`. Para obtener más información, vea [`choco feature` command|CommandsFeature] o ejecute `choco feature -?`.

Una casilla de verificación significa que esta función está activada de forma predeterminada.

### General
* [ ] `logWithoutColor` - Registro sin color: no muestra colorización en la salida de registro. Disponible a partir de las versiones 0.10.9 o superior.
* [ ] `logEnvironmentValues` - Valores del entorno de registro: registrará los valores del entorno antes y después de la instalación (podría divulgar algunos datos confidenciales). Disponible a partir de las versiones 0.10.9 o superior.
* [x] `showNonElevatedWarnings` - Mostrar advertencias no elevadas - Mostrar advertencias no elevadas. Disponible a partir de las versiones 0.10.4 o superior.
* [x] `showDownloadProgress` - Mostrar progreso de descarga - Mostrar porcentajes de progreso de descarga en la CLI.  Disponible a partir de las versiones 0.10.4 o superior.
* [ ] `useRememberedArgumentsForUpgrades` - Usar argumentos recordados para actualizaciones: al ejecutar actualizaciones, usa los mismo argumentos para la actualización que se usaron para la instalación ("recordados"). Esto puede ser útil cuando se ejecuta la actualización para todos los paquetes. Disponible a partir de las versiones 0.10.4 o superior. Se activará de forma predeterminada en una versión futura.
* [ ] `logValidationResultsOnWarnings` - Registra los resultados de la validación en las advertencias - ¿Se deben registrar los resultados de validaciones si hay advertencias?  Disponible a partir de las versiones 0.10.12 o superior.

### Desinstalador automático
* [x] `autoUninstaller` -  Desinstalar desde programas y características sin requerir un script de desinstalación explícito.
* [ ] `failOnAutoUninstaller` - Fallar si el desinstalador automático también falla.

### Códigos de salida
* [x] `usePackageExitCodes` - Usar códigos de salida del paquete: los scripts del paquete pueden proporcionar códigos de salida. Con esto activado, los códigos de salida del paquete serán los que utilice Choco para salir cuando no el valor sea diferente de cero (este valor puede provenir de un paquete dependiente). Chocolatey define los códigos de salida válidos como 0, 1605, 1614, 1641, 3010. Con esta función desactivada, choco saldrá con 0, 1 o -1 (comportamiento anterior coincidente). Disponible a partir de las versiones 0.9.10 o superior.

* [ ] `useEnhancedExitCodes` - Usar códigos de salida mejorados: Chocolatey puede proporcionar códigos de salida mejorados que rodean la lista, búsqueda, información, comandos obsoletos y otros que se no tratan directamente con las operaciones de paquetes. Para ver los códigos de salida mejorados y sus significados, ejecute `choco [cmdname]-?`. Con esta función desactivada, choco finalizará con 0, 1 o -1 (coincidiendo con el comportamiento anterior). Disponible a partir de las versiones 0.10.12 o superior. Valor predeterminado desactivado en las versiones 0.10.14 o superior.

* [ ] `exitOnRebootDetected` - Salir en reinicio detectado: deja de ejecutar la instalación, actualización o desinstalación cuando se detecta una solicitud de reinicio pendiente. Requiere que la característica 'usePackageExitCodes' esté activada. Finalizará con 350 o 1604. Cuando finaliza con 350, significa que se debe reiniciar el sistema antes de ejecutar la operación. Cuando finaliza con 1604, significa que se ha completado algún trabajo antes de que se detectará la solicitud de reinicio. Disponible a partir de las versiones 0.10.12 o superior.

### Control de flujo
* [ ] `failOnInvalidOrMissingLicense` - Licencia no válida o faltante: permite saber cuándo una licencia está vencida o no se aplica a una máquina. Disponible a partir de las versiones 0.9.10 o superior.

* [x] `ignoreInvalidOptionsSwitches` - Ignorar opciones/interruptores no válidos - Si se pasa un interruptor o una opción que no se reconoce, ¿debería fallar choco? Disponible a partir de las versiones 0.9.10 o superior.

* [ ] `failOnStandardError` - Fallo si el proveedor de instalación escribe en stderr. No se recomienda su uso. Disponible a partir de las versiones 0.9.10 o superior.

* [ ] `failOnAutoUninstaller` - Fallar si falla el desinstalador automático.

* [ ] `stopOnFirstPackageFailure` - Detener en primer error de paquete: deja de ejecutar instalar, actualizar o desinstalar en el primer error de paquete en lugar de intentar continuar. Como esto afectará a la actualización de todos los paquetes, normalmente se recomienda dejarlo apagado. Disponible a partir de las versiones 0.10.4 o superior.

* [ ] `skipPackageUpgradesWhenNotInstalled` - Omitir paquetes no instalados durante la actualización: si un paquete no está instalado, no lo instale durante el proceso de actualización. Disponible a partir de las versiones 0.10.12 o superior.

* [ ] `ignoreUnfoundPackagesOnUpgradeOutdated` - Ignorar paquetes sin encontrar en actualizaciones desactualizadas: cuando se comprueban los datos obsoletos o de actualizaciones, si no se encuentra un paquete contra las fuentes especificadas, no informa el paquete en absoluto. Disponible a partir de las versiones 0.10.9 o superior.

### Seguridad
* [ ] `useFipsCompliantChecksums` - Usar sumas de control compatibles con FIPS - Asegúrese de que la suma de comprobación realizada por choco utiliza algoritmos compatibles con FIPS. No se recomienda a menos que sea requerido por el modo FIPS. La habilitación en una instalación existente podría tener consecuencias no deseadas relacionadas con las actualizaciones/desinstalaciones. Disponible en versiones 0.9.10 o superior.

* [x] `checksumFiles` - Verificar la suma de comprobación cuando se extraen datos de Internet (según el paquete).

* [ ] `allowEmptyChecksums` - Permitir que los paquetes tengan sumas de comprobación vacías/faltantes para los recursos descargados desde ubicaciones no seguras (HTTP, FTP). No se recomienda habilitar si se utilizan fuentes que descargan recursos de Internet. Disponible en versiones 0.10.0 o superior.

* [x] `allowEmptyChecksumsSecure` - Permitir que los paquetes tengan sumas de comprobación vacías/faltantes para los recursos descargados desde ubicaciones seguras (HTTPS). Disponible en versiones 0.10.0 o superior.

* [ ] `allowGlobalConfirmation` - Solicita la confirmación para la ejecución de scripts.

### Otros
* [x] `powershellHost` - Utilizar el host PowerShell incorporado de Chocolate. Disponible en versiones 0.9.10 o superior.

* [ ] `scriptsCheckLastExitCode` - Scripts Check $LastExitCode (comandos externos) - Déjelo apagado a menos que lo necesite absolutamente mientras arregla los scripts de su paquete  para usar `throw 'error message'` o `Set-PowerShellExitCode #` en lugar de  `exit #`. Este comportamiento comenzó en la versión 0.9.10 y produjo errores difíciles de encontrar. Si el último proceso externo finaliza exitosamente, pero con un código de salida que no es cero, podría causar fallas en la detección de errores en el paquete. Disponible en versiones 0.10.3 o superior. Will be removed in 0.11.0.

* [ ] `removePackageInformationOnUninstall` - Eliminar información almacenada del paquete en la desinstalación: cuando se desinstala un paquete, ¿también debería eliminarse la información almacenada del paquete? Disponible en versiones 0.10.9 o superior.

## Características - Ediciones con licencia
### General
* [x] `downloadCache` - Descargar caché: usar la caché de descarga privada si está disponible para el paquete. Disponible en versiones 0.9.10 o superior, pero solo para ediciones con licencia. Más información en  https://chocolatey.org/docs/features-private-cdn

* [ ] `failOnInvalidOrMissingLicense` - Fallar si la licencia no es válida o no se encuentra: permite saber cuándo una licencia está vencida o no se aplica a una máquina. Disponible en versiones 0.9.10 o superior.

* [x] `warnOnUpcomingLicenseExpiration` - Advertir sobre la próxima caducidad de la licencia: cuando llegue la fecha de caducidad de la licencia, ¿debería Chocolatey emitir una advertencia? Solo ediciones en MSP y Business 1.12.12 o superior. Configuración ignorada en las ediciones de prueba.

### Access Control / Security
* [ ] `adminOnlyExecutionForAllChocolateyCommands` - Limitar la ejecución de comandos de Chocolatey solo para administradores: si está habilitado, solo los administradores podrán ejecutar los comandos 'choco'. Disponible solo para ediciones de negocios en versiones 1.12.2 o superior.

* [ ] `adminOnlyExecutionForNewCommand` - Limitar a la ejecución del administrador solo para el nuevo comando: si está habilitado, solo los administradores podrán ejecutar `choco new`. Disponible solo para ediciones de negocios en versiones 1.10 o superior.

* [ ] `adminOnlyExecutionForDownloadCommand` - Limitar a la ejecución del administrador solo para el comando de descarga: si está habilitado, solo los administradores podrán ejecutar `choco download`. Disponible solo para ediciones de negocios en versiones 1.10 o superior.

* [ ] `useBackgroundServiceWithNonAdministratorsOnly` - Usar el servicio en segundo plano solo para usuario no administradores: cuando use el autoservicio, solo ejecute el modo en segundo plano para los no administradores. Disponible solo para ediciones de negocios en versiones 1.12 o superior.

* [x] `useLocalSystemForServiceInstalls` - Usar LocalSystem para instalaciones de servicio: cuando instale servicios que no indiquen un usuario/contraseña, use LocalSystem para esas instalaciones. Cuando está apagado, Chocolatey creará un administrador local con una contraseña única para la máquina, pero nunca sabrá la contraseña. Disponible solo para ediciones de negocios en versiones 1.12 o superior.

### Chocolatey Central Management
* [ ] `useChocolateyCentralManagement` - Usar Chocolatey Central Management - Las listas de paquetes instalados y desactualizados se informará al servidor elegido de Chocolatey Central Management. Disponible solo para ediciones de negocios en versiones 2.0 o superior. Más información en https://chocolatey.org/docs/features-chocolatey-central-management

### Internalizador de paquetes
* [x] `internalizeAppendUseOriginalLocation` - Agregar la ubicación original de uso con el internalizador de paquete: cuando `Install-ChocolateyPackage` se internaliza, agregue el parámetro `-UseOriginalLocation` a la función. Disponible solo en ediciones comerciales (versión 1.7.0+) y ediciones MSP (versión 1.12.1+). Requiere al menos Chocolatey v0.10.1 para que `Install-ChocolateyPackage` reconozca el interruptor adecuadamente. Más información en https://chocolatey.org/docs/features-automatically-recompile-packages

### Reductor de paquetes
* [x] `reduceInstalledPackageSpaceUsage` - Reducir el tamaño del paquete instalado (Package Reducer) - Reducir el tamaño del archivo nupkg a muy pequeño y eliminar los archivos extraídos y los instaladores. Disponible solo en ediciones con licencia (versión 1.12.0+). Más información en https://chocolatey.org/docs/features-package-reducer

* [ ] `reduceOnlyNupkgSize` - Reducir solo el tamaño del archivo Nupkg: reduzca solo el tamaño del archivo nupkg cuando se usa Package Reducer. Disponible solo en ediciones con licencia (versión 1.12.0+). También requiere que 'reduceInstalledPackageSpaceUsage' esté habilitado. Más información en https://chocolatey.org/docs/features-package-reducer

### Sincronización de paquetes
* [x] `allowSynchronization` - Sincronización: mantenga los paquetes Chocolatey instalados sincronizados con los cambios en Programas y características. Disponible en ediciones con licencia 0.9.10 o superior. Más información  https://chocolatey.org/docs/features-synchronize

* [ ] `showAllPackagesInProgramsAndFeatures` - Mostrar los paquetes del Sincronizador de paquetes en programas y características: muestra todos los paquetes en el Panel de control >> Programas y características, no solo los paquetes que usan un instalador nativo. Solo disponible en ediciones de negocios versión 1.10.0 o superior.

### Autoservicio / Servicio en segundo plano
* [x] `useBackgroundService` - Utilizar el servicio en segundo plano (autoservicio instalador): para algunos comandos como `install` y `upgrade`. Cuando se establece, utiliza un servicio en segundo plano en lugar de ejecutar el comando directamente. Disponible solo en ediciones comerciales con licencia 1.8.4 o superior. `Uninstall` requiere Chocolatey versión 0.10.4 o superior. También requiere el paquete chocolatey-agent (choco install chocolatey-agent). Más información en https://chocolatey.org/docs/features-agent-service

* [x] `useBackgroundServiceWithSelfServiceSourcesOnly` - Utilizar el servicio en segundo plano solo con fuentes de autoservicio: cuando se utiliza el autoservicio, se utilizan únicamente las fuentes que se configuran para ser utilizadas con el autoservicio. Esto permite otras fuentes que solo un administrador puede establecer o utilizar. Disponible en ediciones de negocios versión 1.10 o superiores. Requiere Chocolatey 0.10.4 o superior para habilitar las fuentes de autoservicio.

* [x] `useBackgroundServiceWithNonAdministratorsOnly` - Utilizar el servicio en segundo plano solo con usuarios no administradores: cuando se utiliza el autoservicio, se ejecuta el modo en segundo plano para usuarios no administradores. Disponible en solamente en ediciones de negocios con versión 1.12.0 o superior.

* [ ] `useBackgroundServiceInteractively` - Utilizar el servicio en segundo plano de manera interactiva (ACTUALMENTE NO FUNCIONA - NO LO UTILICE) - Cuando se utiliza el autoservicio y se instala software que no puede ser completamente silencioso, las instalaciones deberán ejecutarse en el entorno del escritorio actual. Establezca esta bandera para una mayor compatibilidad. Para usar esta función, debe utilizar la cuenta local 'ChocolateyLocalAdmin'. Disponible solo en ediciones de negocios versión 1.12.10 o superior.

* [x] `useBackgroundServiceWithEmptySessions` - Utilizar el servicio en segundo plano con sesiones vacías. A veces las sesiones vacías significan sesiones ejecutadas de forma remota, pero recientemente en Windows es normal ver sesiones vacías con uso interactivo. Deje este indicador a menos que sea absolutamente necesario (controle cómo las sesiones remotas utilizan el servicio en segundo plano habilitando la función `useBackgroundServiceWithNonAdministratorsOnly`). Disponible en ediciones de negocios con versión 1.12.11 o superior.

* [ ] `allowBackgroundServiceUninstallsFromUserInstallsOnly` - Permitir SOLAMENTE la desinstalación de paquetes instalados por un usuario de autoservicio desde el servicio en segundo plano. Permite que un usuario desinstale los paquetes que haya instalado -deben ser reportados como el usuario original con el comando choco -lo --audit. La configuración de configuración 'backgroundServiceAllowedCommands' debe tener agregada la 'desinstalación' para que esto funcione. Disponible solo ediciones de negocios con versión 2.0 o superior.

### Virus Checking
* [x] `virusCheck` - Virus Check: realiza la comprobación de virus en los archivos descargados. Disponible en versiones 0.9.10 o superior, pero solo ediciones con licencia. Más información en https://chocolatey.org/docs/features-virus-check

### Other
* [x] `allowPreviewFeatures` - Permitir características de vista previa - Activa las funciones de vista previa. Algunas funciones están disponibles para la vista previa antes de que se publiquen, solo con fines de prueba. Tenga en cuenta que no deben utilizarse para sistemas de producción, ya que podrían estropear un sistema. Disponible en ediciones con licencia versión 1.9.0 o superior.
