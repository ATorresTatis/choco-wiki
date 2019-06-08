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
* `centralManagementReceiveTimeoutInSeconds` = **'30'** - The amount of time, in seconds, that the background agent should wait to receive information from Chocolatey Central Management.  Available in business editions v2.0.0+ only.
* `centralManagementSendTimeoutInSeconds` = **'30'** - The amount of time, in seconds, that the background agent should wait to send information to Chocolatey Central Management.  Available in business editions v2.0.0+ only.


## Features

Features are adjusted using `choco feature enable|disable --name="'<nameFromBelow>'"`. For more information see [[`choco feature` command|CommandsFeature]] or run `choco feature -?`.

A checkbox means this feature is turned on by default.

### General
* [ ] `logWithoutColor` - Log without color - Do not show colorization in logging output. Available in 0.10.9+.
* [ ] `logEnvironmentValues` - Log Environment Values - will log values of environment before and after install (could disclose sensitive data). Available in 0.9.10+.
* [x] `showNonElevatedWarnings` - Show Non-Elevated Warnings - Display non-elevated warnings. Available in 0.10.4+.
* [x] `showDownloadProgress` - Show Download Progress - Show download progress percentages in the CLI. Available in 0.10.4+.
* [ ] `useRememberedArgumentsForUpgrades` - Use Remembered Arguments For Upgrades - when running upgrades, use arguments for upgrade that were used for installation ('remembered'). This is helpful when running upgrade for all packages. Available in 0.10.4+. This is considered in preview for 0.10.4 and will be flipped to on by default in a future release.
* [ ] `logValidationResultsOnWarnings` - Log validation results on warnings - Should the validation results be logged if there are warnings? Available in 0.10.12+.

### Automatic Uninstaller
* [x] `autoUninstaller` - Uninstall from programs and features without requiring an explicit uninstall script.
* [ ] `failOnAutoUninstaller` - Fail if automatic uninstaller fails.

### Exit Codes
* [x] `usePackageExitCodes` - Use Package Exit Codes - Package scripts can provide exit codes. With this on, package exit codes will be what choco uses for exit when non-zero (this value can come from a dependency package). Chocolatey defines valid exit codes as 0, 1605, 1614, 1641, 3010. With this feature off, choco will exit with 0, 1, or -1 (matching previous behavior). Available in 0.9.10+.
* [ ] `useEnhancedExitCodes` - Use Enhanced Exit Codes - Chocolatey is able to provide enhanced exit codes surrounding list, search, info, outdated and other commands that don't deal directly with package operations. To see enhanced exit codes and their meanings, please run `choco [cmdname] -?`. With this feature off, choco will exit with 0, 1, or -1  (matching previous behavior). Available in 0.10.12+. Default off in 0.10.14+.
* [ ] `exitOnRebootDetected` - Exit On Reboot Detected - Stop running install, upgrade, or uninstall when a reboot request is detected. Requires 'usePackageExitCodes' feature to be turned on. Will exit with either 350 or 1604. When it exits with 350, it means pending reboot discovered prior to running operation. When it exits with 1604, it means some work completed prior to reboot request being detected. Available in 0.10.12+.

### Flow Control
* [ ] `failOnInvalidOrMissingLicense` - Fail On Invalid Or Missing License - allows knowing when a license is expired or not applied to a machine. Available in 0.9.10+.
* [x] `ignoreInvalidOptionsSwitches` - Ignore Invalid Options/Switches - If a switch or option is passed that is not recognized, should choco fail? Available in 0.9.10+.
* [ ] `failOnStandardError` - Fail if install provider writes to stderr. Not recommended for use. Available in 0.9.10+.
* [ ] `failOnAutoUninstaller` - Fail if automatic uninstaller fails.
* [ ] `stopOnFirstPackageFailure` - Stop On First Package Failure - stop running install, upgrade or uninstall on first package failure instead of continuing with others. As this will affect upgrade all, it is normally recommended to leave this off. Available in 0.10.4+.
* [ ] `skipPackageUpgradesWhenNotInstalled` - Skip Packages Not Installed During Upgrade - if a package is not installed, do not install it during the upgrade process. Available in 0.10.12+.
* [ ] `ignoreUnfoundPackagesOnUpgradeOutdated` - Ignore Unfound Packages On Upgrade Outdated - When checking outdated or upgrades, if a package is not found against sources specified, don't report the package at all. Available in 0.10.9+.

### Security
* [ ] `useFipsCompliantChecksums` - Use FIPS Compliant Checksums - Ensure checksumming done by choco uses FIPS compliant algorithms. Not recommended unless required by FIPS Mode. Enabling on an existing installation could have unintended consequences related to upgrades/uninstalls. Available in 0.9.10+.
* [x] `checksumFiles` - Checksum files when pulled in from internet (based on package).
* [ ] `allowEmptyChecksums` - Allow packages to have empty/missing checksums for downloaded resources from non-secure locations (HTTP, FTP). Enabling is not recommended if using sources that download resources from the internet. Available in 0.10.0+.
* [x] `allowEmptyChecksumsSecure` - Allow packages to have empty/missing checksums for downloaded resources from secure locations (HTTPS). Available in 0.10.0+.
* [ ] `allowGlobalConfirmation` - Prompt for confirmation in scripts or bypass.

### Other
* [x] `powershellHost` - Use Chocolatey's built-in PowerShell host. Available in 0.9.10+.
* [ ] `scriptsCheckLastExitCode` - Scripts Check $LastExitCode (external commands) - Leave this off unless you absolutely need it while you fix your package scripts  to use `throw 'error message'` or `Set-PowerShellExitCode #` instead of `exit #`. This behavior started in 0.9.10 and produced hard to find bugs. If the last external process exits successfully but with an exit code of not zero, this could cause hard to detect package failures. Available in 0.10.3+. Will be removed in 0.11.0.
* [ ] `removePackageInformationOnUninstall` - Remove Stored Package Information On Uninstall - When a package is uninstalled, should the stored package information also be removed?  Available in 0.10.9+.

## Features - Licensed Edition
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
