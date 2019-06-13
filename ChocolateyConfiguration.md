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
* [x] `downloadCache` - Download Cache - use the private download cache if available for a package. Available in 0.9.10+. Licensed editions only. See https://chocolatey.org/docs/features-private-cdn
* [ ] `failOnInvalidOrMissingLicense` - Fail On Invalid Or Missing License - allows knowing when a license is expired or not applied to a machine. Available in 0.9.10+.
* [x] `warnOnUpcomingLicenseExpiration` - Warn On Upcoming License Expiration - When a license expiration date is upcoming, should Chocolatey provide a warning? MSP and Business editions only (version 1.12.12+). Setting ignored in trial editions.

### Access Control / Security
* [ ] `adminOnlyExecutionForAllChocolateyCommands` - Limit to Administrator Execution Only for All Chocolatey Commands - If enabled, only administrators will be able to run 'choco' commands. Business editions only (version 1.12.2+).
* [ ] `adminOnlyExecutionForNewCommand` - Limit to Administrator Execution Only for New Command - If enabled, only administrators will be able to run 'choco new'. Business editions only (version 1.10.0+).
* [ ] `adminOnlyExecutionForDownloadCommand` - Limit to Administrator Execution Only for Download Command - If enabled, only administrators will be able to run 'choco download'. Business editions only (version 1.10.0+).
* [ ] `useBackgroundServiceWithNonAdministratorsOnly` - Use Background Service With Non-Administrators Only - When using Self-Service, only execute background mode for non-administrators. Business editions only (version 1.12.0+).
* [x] `useLocalSystemForServiceInstalls` - Use LocalSystem For Service Installs - When installing services that don't indicate a user/password, use the LocalSystem for those installations. When turned off, Chocolatey will manage a local admin with a password unique to the machine but will never know it. Business editions only (version 1.12.0+).

### Chocolatey Central Management
* [ ] `useChocolateyCentralManagement` - Use Chocolatey Central Management - Lists of installed and outdated packages will be reported to the chosen Chocolatey Central Management server.  Business editions only (version 2.0.0+). See https://chocolatey.org/docs/features-chocolatey-central-management

### Package Internalizer
* [x] `internalizeAppendUseOriginalLocation` - Append UseOriginalLocation with Package Internalizer - When `Install-ChocolateyPackage` is internalized, append the `-UseOriginalLocation` parameter to the function. Business editions (version 1.7.0+) and MSP editions (version 1.12.1+) only. Requires at least Chocolatey v0.10.1 for `Install-ChocolateyPackage` to recognize the switch appropriately. See https://chocolatey.org/docs/features-automatically-recompile-packages

### Package Reducer
* [x] `reduceInstalledPackageSpaceUsage` - Reduce Installed Package Size (Package Reducer) - Reduce size of the nupkg file to very small and remove extracted archives and installers. Licensed editions only (version 1.12.0+). See https://chocolatey.org/docs/features-package-reducer
* [ ] `reduceOnlyNupkgSize` - Reduce Only Nupkg File Size - reduce only the size of nupkg file when using Package Reducer. Licensed editions only (version 1.12.0+). Also requires 'reduceInstalledPackageSpaceUsage' to be enabled. See https://chocolatey.org/docs/features-package-reducer

### Package Synchronization
* [x] `allowSynchronization` - Synchronization - Keep installed Chocolatey packages in sync with changes in Programs and Features. Available in 0.9.10+. Licensed editions only. See https://chocolatey.org/docs/features-synchronize
* [ ] `showAllPackagesInProgramsAndFeatures` - Package Synchronizer's Packages In Programs And Features Synchronization - Show all packages in Programs and Features, not just packages that use a native installer. Business editions only (version 1.10.0+).

### Self-Service / Background Mode
* [x] `useBackgroundService` - Use Background Service (Self-Service Installer) - For some commands like install and upgrade, use a background service instead of running the command directly. Business editions only (licensed version 1.8.4+). Uninstall requires Chocolatey v0.10.4. Requires the package chocolatey-agent (choco install chocolatey-agent). See https://chocolatey.org/docs/features-agent-service
* [x] `useBackgroundServiceWithSelfServiceSourcesOnly` - Use Background Service With Self-Service Sources Only - When using Self-Service, opt-in only sources configured to be used with self-service. This allows for other sources only an admin can use. Business editions only (version 1.10+). Requires Chocolatey 0.10.4+ for enabling sources with self-service only.
* [x] `useBackgroundServiceWithNonAdministratorsOnly` - Use Background Service With Non-Administrators Only - When using Self-Service, only execute background mode for non-administrators. Business editions only (version 1.12.0+).
* [ ] `useBackgroundServiceInteractively` - Use Background Service Interactively (BROKEN CURRENTLY - DO NOT USE) - When using Self-Service and installing software that cannot be completely silent, installs will need to be executed against the current desktop environment. Set this flag on for the most compatibility. To use this feature, you must be using the local 'ChocolateyLocalAdmin' account. Business editions only (version 1.12.10+).
* [x] `useBackgroundServiceWithEmptySessions` - Use Background Service With Empty Sessions - Sometimes empty sessions mean remotely run sessions, but in in newer Windows it is much more normal to see empty sessions with interactive use. Leave this flag on unless you absolutely need it off (control how remote sessions use background service by enabling the feature 'useBackgroundServiceWithNonAdministratorsOnly'). Business editions only (version 1.12.11+).
* [ ] `allowBackgroundServiceUninstallsFromUserInstallsOnly` - Allow ONLY Uninstall of Packages Installed By a Self-service User in Background Service - Allow a user to uninstall packages they've installed - they must be reported as the original user in a choco list -lo --audit. The config setting 'backgroundServiceAllowedCommands' must must have 'uninstall' added as well for this to work. Business editions only (version 2.0+).

### Virus Checking
* [x] `virusCheck` - Virus Check - perform virus checking on downloaded files. Available in 0.9.10+. Licensed editions only. See https://chocolatey.org/docs/features-virus-check

### Other
* [x] `allowPreviewFeatures` - Allow Preview Features - Turns on Preview Features. Some features become available for preview before they are released for testing purposes. Please note these should not be used for production systems as they could mess up a system.  Licensed editions only (version 1.9.0+).
