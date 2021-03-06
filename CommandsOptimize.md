<!-- This file is automatically generated based on output from https://github.com/chocolatey/choco/tree/stable/src/chocolatey/infrastructure.app/commands/ChocolateyOptimizeCommand.cs using https://github.com/chocolatey/choco/tree/stable/GenerateDocs.ps1. Contributions are welcome at the original location(s). If the file is not found, it is not part of the open source edition of Chocolatey or the name of the file is different. -->

# Comando de optimización (choco optimize)

<!-- TOC -->

- [Optimizador de paquetes](#package-optimizer)
- [Uso](#usage)
- [Ejemplos](#examples)
- [Verlo en acción](#see-it-in-action)
- [Opciones y modificadores](#options-and-switches)

<!-- /TOC -->

<a name="package-optimizer"></a>
### Optimizador de paquetes

Disponible en las [ediciones licenciadas](https://chocolatey.org/compare) a partir de la versión 1.12.0.

Similar al Reductor de paquetes, pero reduce los paquetes existentes.
Con Package Optimizer/Reducer:

* Reduce los paquetes nupkg a 5 KB o menos, sin importar el tamaño.
* Los comprimidos/instaladores se eliminan automáticamente del directorio del paquete si se encuentran.
* Los comprimidos/instaladores se eliminan de la caché TEMP si se encuentran.

Las siguientes extensiones de archivo se eliminan automáticamente:

* 7z / zip / rar / gz / tar / sfx
* iso
* msi / msu / msp
* exe files if they are detected to be an installer


<a name="usage"></a>
## Uso

    choco optimize [<options/switches>]

<a name="examples"></a>
## Ejemplos

    choco optimize
    choco optimize --reduce-nupkg-only


<a name="see-it-in-action"></a>
## Verlo en acción

Próximamente

<a name="options-and-switches"></a>
## Opciones e interruptores

NOTA: Las opciones y los modificadores se aplican a todos los elementos aprobados, por lo que si está ejecutando un comando como instalar que permite instalar varios paquetes, y los usa `--version=1.0.0`, buscará e intentará instalar la versión 1.0.0 de cada paquete aprobado. Por lo tanto, divida varias llamadas de paquete cuando desee pasar opciones específicas.

Incluye  [[opciones/interruptores predeterminados|CommandsReference#default-options-and-switches]] (se incluyen a continuación para complementar).

~~~

 downloading multiple packages, and you use `--version=1.0.0`, it is
 going to look for and try to download version 1.0.0 of every package


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

     --reduce-nupkg-only, --deflate-nupkg-only
     Reduce Only Nupkg File Size - reduce only the size of nupkg file when
       using Package Optimizer. [Licensed editions](https://chocolatey.org/compare) only (version 1.12.0+).

     --id=VALUE
     Id - The package to optimize

~~~

[[Referencia de comandos|CommandsReference]]

***NOTA:*** Esta documentación ha sido generada automáticamente desde `choco optimize -h`.

