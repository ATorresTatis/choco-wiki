# La historia de Bob y Richard

Comencemos con una historia. Dos muchachos, Bob y Richard (cuyos nombres se han cambiado para proteger a los inocentes) necesitan preparar sus computadoras para hacer un trabajo de desarrollo con [Git](http://git-scm.org). Ni Bob ni Richard han trabajado con Git antes. Esta es la historia sobre el proceso por el que pasa cada uno para instalar Git.

Richard se dedica a investigar. Después de un tiempo, descubre que la herramienta que quiere instalar para Windows es Git para Windows. Él busca, descarga la última versión y la instala, pero se da cuenta que descargó la arquitectura incorrecta y entonces comienza de nuevo. Es posible que no tenga la configuración establecida de forma correcta. Entonces, pasa algún tiempo tratando de averiguar cuáles deberían ser los ajustes. Después de dedicar toda una mañana, finalmente tiene instalado Git y espera que esté configurado correctamente. Ahora Richard sabe un poco de Git pero nada acerca de otras herramientas que pudieran haberlo ayudado a usar Git.

Mientras tanto, Bob ha instalado recientemente una herramienta llamada Chocolatey.. Se dirige al repositorio de la comunidad en [chocolatey.org](http://chocolatey.org/packages) y busca a Git. Aprende que hay varias herramientas geniales para trabajar con Git en Windows. Decide que quiere usar Git Extensions para ayudarlo a visualizar parte del trabajo de Git. Abre una línea de comando, escribe `choco install gitextensions` y presiona Enter. Git Extensions depende de Git para Windows, por lo que Chocolatey lo descarga e instala silenciosamente en su máquina. Configura Git para el uso adecuado de Windows. Luego, Chocolatey descarga e instala silenciosamente Git Extensions en su máquina. En menos de diez minutos, Bob está listo para comenzar y tiene a su disposición algunas de las mejores herramientas para trabajar con Git.

¿Bob tuvo suerte? No. Es solo que Bob no tuvo que tomar tantas decisiones. Decidió que quería una herramienta. Luego Chocolatey hizo todo el trabajo, tomó todas las decisiones, obtuvo las aplicaciones dependientes e incluso configuró su máquina correctamente. Le queda poco por hacer para terminar de configurar la máquina para acceder a [GitHub](http://github.com).

¿La moraleja de la historia? Richard tardó de 3 a 4 horas en ponerse al día. Bob llegó a la velocidad máxima en menos de diez minutos. No seas un Richard.

Referencias

 * http://lostechies.com/jimmybogard/2012/02/01/improving-the-git-windows-experience-downloads/
