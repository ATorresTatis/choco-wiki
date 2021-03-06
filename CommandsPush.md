<!-- This file is automatically generated based on output from https://github.com/chocolatey/choco/tree/stable/src/chocolatey/infrastructure.app/commands/ChocolateyPushCommand.cs using https://github.com/chocolatey/choco/tree/stable/GenerateDocs.ps1. Contributions are welcome at the original location(s). If the file is not found, it is not part of the open source edition of Chocolatey or the name of the file is different. -->

# Comando de publicación (choco push)

Chocolatey intentará publicar un paquete nupkg compilado. 
Algunos pueden preferir usar `cpush` como atajo para `choco push`.

**NOTA:** 100% compatible con clientes de chocolate más antiguos (0.9.8.32 y anteriores)
 con opciones e interruptores. La ubicación de inserción predeterminada está en desuso y será eliminada luego de la versión v1. 
 En la mayoría de los casos, aún puede utilizar las opciones y cambios especificando un guión (`-`). Para obtener más detalles, consulte
 [[cómo pasar argumentos|CommandsReference#how-to-pass-options--switches]] (`choco -?`).

Un feed puede ser una carpeta local, un recurso compartido de archivos, 
o el [feed de la comunidad](https://chocolatey.org/packages)
(https://push.chocolatey.org/), o un feed personalizado/privado. 
Para las fuentes web, tiene el requisito de implementar los puntos finales de OData necesarios para los paquetes NuGet..

<!-- TOC -->

- [Uso](#usage)
- [Ejemplos](#examples)
- [Solución de problemas](#troubleshooting)
- [Códigos de salida](#exit-codes)
- [Opciones y modificadores](#options-and-switches)

<!-- /TOC -->

<a name="usage"></a>
## Uso

    choco push [<path to nupkg>] [<options/switches>]
    cpush [<path to nupkg>] [<options/switches>]

**NOTE:** If there is more than one nupkg file in the folder, the command
 will require specifying the path to the file.

<a name="examples"></a>
## Ejemplos

    choco push --source https://chocolatey.org/
    choco push --source "'https://chocolatey.org/'" -t 500
    choco push --source "'https://chocolatey.org/'" -k="'123-123123-123'"

**NOTA:** Consulte las secuencias de comandos en [[cómo pasar argumentosCommandsReference#how-to-pass-options--switches]] (`choco -?`) para saber cómo escribir secuencias de comandos e integraciones adecuada


<a name="troubleshooting"></a>
## Solución de problemas

Para usar este comando, debe tener su clave API guardada para el feed de la comunidad (chocolatey.org) o para la fuente a la que desea enviar el paquete. También, puede pasar explícitamente el valor de apikey al comando. Consulte la ayuda del comando [[`apikey`|Commandsapikey]] para obtener instrucciones sobre cómo guardar su clave:

    choco apikey -?

Un error común es `Error al procesar la solicitud. 'La clave API especificada no proporciona la autoridad para enviar paquetes ". El servidor remoto devolvió un error: (403) Forbidden... `, cuando ocurre, generalmente significa que el paquete ya existe con un usuario diferente (clave de API) o el paquete podría no estar en la lista. Puede verificar yendo a https://push.chocolatey.org/packages/packageName. Póngase en contacto con los administradores de https://push.chocolatey.org/ si se encuentra con este comportamiento y no encuentra una buena razón para ello. 

<a name="exit-codes"></a>
## Códigos de salida

Códigos de salida que normalmente resultan de ejecutar este comando..

Normal:
 - 0: la operación fue exitosa, no se detectaron problemas
 - -1 o 1: se ha producido un error

Si encuentra otros códigos de salida que aún no hemos documentado, presente un ticket para que podamos documentarlo
 https://github.com/chocolatey/choco/issues/new/choose.

<a name="options-and-switches"></a>
## Opciones y Modificadores

NOTA: Las opciones y los modificadores se aplican a todos los elementos aprobados, por lo que si está ejecutando un comando como instalar que permite instalar varios paquetes, y los usa `--version=1.0.0`, buscará e intentará instalar la versión 1.0.0 de cada paquete aprobado. Por lo tanto, divida varias llamadas de paquete cuando desee pasar opciones específicas.

Incluye  [[opciones/interruptores predeterminados|CommandsReference#default-options-and-switches]] (se incluyen a continuación para complementar).

~~~

 -?, --help, -h
     Prints out the help menu.

 -d, --debug
     Debug - Show debug messaging.

 -v, --verbose
     Verbose - Show verbose messaging. Very verbose messaging, avoid using
       under normal circumstances.

     --trace
     Trace - Show trace messaging. Very, very verbose trace messaging. Avoid
       except when needing super low-level .NET Framework debugging. Available
       in 0.10.4+.

     --nocolor, --no-color
     No Color - Do not show colorization in logging output. This overrides
       the feature 'logWithoutColor', set to 'False'. Available in 0.10.9+.

     --acceptlicense, --accept-license
     AcceptLicense - Accept license dialogs automatically. Reserved for
       future use.

 -y, --yes, --confirm
     Confirm all prompts - Chooses affirmative answer instead of prompting.
       Implies --accept-license

 -f, --force
     Force - force the behavior. Do not use force during normal operation -
       it subverts some of the smart behavior for commands.

     --noop, --whatif, --what-if
     NoOp / WhatIf - Don't actually do anything.

 -r, --limitoutput, --limit-output
     LimitOutput - Limit the output to essential information

     --timeout, --execution-timeout=VALUE
     CommandExecutionTimeout (in seconds) - The time to allow a command to
       finish before timing out. Overrides the default execution timeout in the
       configuration of 2700 seconds. '0' for infinite starting in 0.10.4.

 -c, --cache, --cachelocation, --cache-location=VALUE
     CacheLocation - Location for download cache, defaults to %TEMP% or value
       in chocolatey.config file.

     --allowunofficial, --allow-unofficial, --allowunofficialbuild, --allow-unofficial-build
     AllowUnofficialBuild - When not using the official build you must set
       this flag for choco to continue.

     --failstderr, --failonstderr, --fail-on-stderr, --fail-on-standard-error, --fail-on-error-output
     FailOnStandardError - Fail on standard error output (stderr), typically
       received when running external commands during install providers. This
       overrides the feature failOnStandardError.

     --use-system-powershell
     UseSystemPowerShell - Execute PowerShell using an external process
       instead of the built-in PowerShell host. Should only be used when
       internal host is failing. Available in 0.9.10+.

     --no-progress
     Do Not Show Progress - Do not show download progress percentages.
       Available in 0.10.4+.

     --proxy=VALUE
     Proxy Location - Explicit proxy location. Overrides the default proxy
       location of ''. Available for config settings in 0.9.9.9+, this CLI
       option available in 0.10.4+.

     --proxy-user=VALUE
     Proxy User Name - Explicit proxy user (optional). Requires explicity
       proxy (`--proxy` or config setting). Overrides the default proxy user of
       '123'. Available for config settings in 0.9.9.9+, this CLI option
       available in 0.10.4+.

     --proxy-password=VALUE
     Proxy Password - Explicit proxy password (optional) to be used with
       username. Requires explicity proxy (`--proxy` or config setting) and
       user name.  Overrides the default proxy password (encrypted in settings
       if set). Available for config settings in 0.9.9.9+, this CLI option
       available in 0.10.4+.

     --proxy-bypass-list=VALUE
     ProxyBypassList - Comma separated list of regex locations to bypass on
       proxy. Requires explicity proxy (`--proxy` or config setting). Overrides
       the default proxy bypass list of ''. Available in 0.10.4+.

     --proxy-bypass-on-local
     Proxy Bypass On Local - Bypass proxy for local connections. Requires
       explicity proxy (`--proxy` or config setting). Overrides the default
       proxy bypass on local setting of 'True'. Available in 0.10.4+.

     --log-file=VALUE
     Log File to output to in addition to regular loggers. Available in 0.1-
       0.8+.

 -s, --source=VALUE
     Source - The source we are pushing the package to. Use https://pus-
       h.chocolatey.org/ to push to [community feed](https://chocolatey.org/packages).

 -k, --key, --apikey, --api-key=VALUE
     ApiKey - The api key for the source. If not specified (and not local
       file source), does a lookup. If not specified and one is not found for
       an https source, push will fail.

 -t=VALUE
     Timeout (in seconds) - The time to allow a package push to occur before
       timing out. Defaults to execution timeout 2700.

~~~

[[Referencia de comandos|CommandsReference]]

**NOTA:** Esta documentación ha sido generada automáticamente desde `choco optimize -h`.

