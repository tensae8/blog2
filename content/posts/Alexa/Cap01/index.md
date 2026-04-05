---
author: Tensae
title: Como cambiar el sistema operativo a Alexa
date: 2026-04-05
description: Como cambiarle el Sistema Operativo a Alexa
categorías: [Guía]
etiquetas: [Experimentos]
series: ["Alexa"]
series_order: 1
---
Esta guía se basa en el proceso de [`esta`](https://xdaforums.com/t/unlock-root-twrp-unbrick-amazon-echo-show-5-2nd-gen-2021-cronos.4772596/) web y [`este`](https://www.youtube.com/watch?v=5CCRIzcgKuM&t=90s) video. Son las fuentes en las que me he basado para hacer el proceso. También hay ciertos aspectos que he hecho diferente a ellos y cosas en las que yo no había caído hasta que las he hecho.

En cualquier caso, si algo de lo que explico no queda claro, recurriendo a estas dos guías seguro que se acaba solucionando. 

{{< alert cardColor="#e63946" iconColor="#1d3557" >}}
Hay un resigo considerable de transformar el dispositivo en un ladrillo inutilizable si alguno de los pasos no se sigue correctamente. Si procedes a hacer todo esto ten en cuenta que lo haces bajo tu propia responsabilidad y riesgo.
{{< /alert >}}

Antes de comenzar a tocar a Alexa necesitaremos descargarnos unos cuantos programas.

## Programas necesarios

Lo primero que necesitaremos para permitir que nuestro ordenador se comunique con Alexa serán los drivers del USB en [`esta`](https://developer.amazon.com/docs/fire-tablets/connecting-adb-to-device.html#install_usb_driver) web:

![Kindle_fire_usb_driver.png](../../../_resources/Alexa/91eb6d8b1b2cb63e2a18aef234decae8.png)

El proceso de instalación es bastante sencillo, simplemente extraeremos el .zip, ejecutaremos el .exe, e instalaremos siguiendo los pasos de la interfáz gráfica que se nos deplegará.

Lo siguiente que necesitaremos será [`esto`](https://xdaforums.com/attachments/amonet-cronos-v1-1-2-zip.6325109/). Con lo cual se nos descargará un .zip que al descomprimirlo, dentro de `amonet-checkers-v1.1.2/amonet/` tendremos todos los scripts necesarios:

![Amonet_scripts.png](../../../_resources/Alexa/0e95dd8b7527d1543da3fe563ab6bd89.png)

Por último, para la instalación del nuevo sistema operativo usaremos ADB, el cual podemos descargar desde la página oficial de google [`aquí`](https://developer.android.com/tools/releases/platform-tools#downloads):

![ADB.png](../../../_resources/Alexa/zen_QdaPObs21u.png)

Al descomprimirlo nos encontraremos con una carpeta donde encontraremos la herramienta para poder modificar el dispositivo miedante el ordenador, a esta recomiendo cambiarle el nombre a ADB para evitar confusiones. 

## Desbloquear el bootloader


{{< alert >}}
Si después del proceso queremos usar el FireOS debemos estar registrados con una cuenta de amazon antes de comenzar.
De otra manera el menú de inicio por defecto crashearía y no se podría completar la configuración de inicio.
{{< /alert >}}

Antes de nada confirmaremos que estamos en la versión de alexa adecuada (Las únicas válidas son FireOS 6.5.4.4, 6.5.4.8, 6.5.5.0, 6.5.6.4, 6.5.7.0, o cualquier versión más reciente que la 6.5.7.0 )
Si encontramos que no la tenemos en la versión deseada la actualizamos y ya.

De esta manera también podemos comprobar que modelo de Alexa tenemos:

![alexa_version.jpg](../../../_resources/Alexa/IMG_20260401_133717_874.jpg)

Después de haber instalado los drivers para el USB nos dirigiremos a la carpeta de amonet. En mi caso (ya que estoy en Windows) el archivo que me interesa es `fastbrick.bat`, si estuvieramos en linux buscaríamos el .sh. Después de localizarlo lo ejecutaremos, nos saltará una alerta advirtiendonos de que el autor no ha podido ser verificado pero lo ejecutaremos igual (no es ningún virus). Nos aparecerá una terminal con lo siguiente:

![amonet_exec.png](../../../_resources/Alexa/651ddf18c5d730e21bf7b0af5ded7e20.png)

Al presionar cualquier tecla el propio script nos dará instrucciones para poner Alexa en modo fastboot, lo cual es manteniendo los tres botones superiores durante el inicio del dispositivo hasta tener el logo en la parte inferior izquierda:

![FASTBOOT_mode.jpg](../../../_resources/Alexa/IMG_20260402_101911_175.jpg)

En el momento que la tengamos en este estado es momento para conectarlo al ordenador por cable (no importa si la enchufamos antes o después). El script detectará el dispositivo y pasaremos al siguiente paso:

![Amonet_work.png](../../../_resources/Alexa/WindowsTerminal_vkUouXf9iF.png)

Aquí introduciremos "yes" y enter para que el script empieze a trabajar. En la propia terminal de nuestro ordenador no veremos mucho cambio pero si miramos en Alexa sí que veremos procesos. 
Una vez termine se reiniciará automáticamente (Es normal si tarda unos minutos):

![amonet_work_alexa.jpg](../../../_resources/Alexa/IMG_20260402_101950_562.jpg)

Al terminar debería iniciar de nuevo Alexa pero en el menú de TWRP (Team Win Recovery Proyect) el cual es una imagen de recuperación de código abierto para android.

![TWRP_menu.jpg](../../../_resources/Alexa/IMG_20260402_104149_929.jpg)

## Copia de seguridad

Por si en algún momento deseamos volver a tener Fire OS necesitamos hacer una copia de seguridad, la cual se hace de forma muy rápida y no cuesta nada.

Para hacerla buscaremos en la carpeta amonet el archivo `backup.bat` y lo ejecutaremos siguiendo las instrucciones hasta tener un resultado similar a este:

![backup_script.png](../../../_resources/Alexa/6bfd79371334092d596cdf13fa34619f.png)

## Limpieza de los datos antiguos

Para poder instalar el nuevo sistema operativo necesitaremos limpiar los datos del antiguo para que no se produzcan conflictos.

Esto se puede realizar muy fácilmente mediante la nueva GUI de TWRP.

En la página principal nos dirigiremos a la parte superior derecha donde pone "wipe":

![TWRP_Wipe.png](../../../_resources/Alexa/183ba7c691ecddc74516420e1269a5c6.png)

Dentro del nuevo menú que se nos desplegará seleccionaremos "Advanced Wipe" en la parte inferior izquierda. Después de presionar el botón se nos desplegará un último menú en el cual deberemos de seleccionar cuidadosamente: "System", "Data" y "Caché". Por último, deslizaremos la barra inferior y esperaremos:

![wipe_settings.jpg](../../../_resources/Alexa/IMG_20260402_104107_341.jpg)

Este proceso no debería tardar más de unos cuantos segundos y al acabar podemos darle back y despues a la casa en el menú de navegación.

## Instalación de LineageOS

En este punto es donde más importa que modelo de Alexa tengamos, ya que la versión que instalaremos de LineageOS dependerá de ello.
En mi caso ya que tengo a "Amazon Echo Show 5 (2021)" es decir, la segunda generación, debo descargarme la versión "cronos" [aquí](https://github.com/amazon-oss/releases/releases/tag/lineage-18.1-cronos-v0.1). En caso de que tuvieramos la 1ra generación (2019) nos decargaríamos la versión "checkers" [aquí](https://github.com/amazon-oss/releases/releases/tag/lineage-18.1-checkers-v0.4).
Más adelante muestro que me equivoqué en este paso introduciendo la versión que no era, pero no pasó nada grave.

Este archivo que descargemos debemos guardarlo en la carpeta del ADB, en la que abrimos la terminal, para poder hacer referencia a él de manera más sencilla (Yo tengo dos archivos por error):

![ADB_with_LineageOS.png](../../../_resources/Alexa/b55ced27309079152c115c5f85fa232f.png)

Como paso final para comenzar la magia necesitamos poner a alexa en modo receptivo para ser capaces de instalarle Lineage OS. Esto lo conseguimos navegando en el menú principal a "Advanced" en la parte inferior izquierda:

![TWRP_advanced.png](../../../_resources/Alexa/8c01893fa6ed4497168f7c9674f6fd64.png)

Después seleccionaremos "ADB sideload" en el mismo lugar:

![ADB_sideload_option.png](../../../_resources/Alexa/02aced78ed29fc65dd4886e233946b80.png)

y solamente deslizaremos la barra. Esto cambiará el estado de Alexa de "recovery" a "sideloading":

![ADB_sideload_alexa_slide.jpg](../../../_resources/Alexa/IMG_20260402_104215_540.jpg)

Si ya hemos llegado a este paso tenemos a Alexa desbloqueada lista para instalarle el nuevo sistema operativo, para cuyo proceso utilizaremos ADB.

Dentro de la carepta que extragimos al principio encontraremos otra carpeta (La que cambiamos el nombre a ADB) abriremos una terminal en ella, para ello haremos click derecho en cualquier parte y seleccionaremos la opción:

![Terminal_lunch.png](../../../_resources/Alexa/017f91fb2d0f8e5457407f9dcc47ee86.png)

Dado que no tenemos el comando añadido al PATH, tendremos que poner la ruta para llegar a él en cada comando, como estamos en la misma carperta pues solamente con poner:
```Powershell
.\adb.exe
```
en la terminal debería aparecernos el manual:

![ADB_man.png](../../../_resources/Alexa/dac35646aab2006d47af773a629c0cb0.png)

Si es así, podemos continuar.

Ahora ejecutaremos:
```Powershell
.\adb.exe devices
```
Lo que nos debería devolver a uno (Alexa) y seguidamente ejecutaremos el comando: 
```Powershell
.\adb.exe sideload lineage-18.1-20251220-UNOFFICIAL-cronos.zip
```
No hace falta poner todo el nombre del paquete, con empezar poniendo lineage y pulsar el tabulador se autocompleta.

Tuve un fallo a la hora de seleccionar la versión de lineageOS, elegí la versión checkers (que es para la alexa de 1ra generación):

![sideload_error.png](../../../_resources/Alexa/0ddf663d614c4ff34c656ec6ddf00dda.png)

Al correr el comando me dió un error en Alexa y en la propia terminal, diciendome que la versión no era correcta. 
Lo corregí instalando la versión cronos (que es para la 2nda generación) y ya todo funcionó correctamente:

![sideload_def.png](../../../_resources/Alexa/417e2b75c7f4708b3423bc80278ecc9c.png)

Deberíamos ver en nuestra Alexa algo similar a esto (si todo ha ido bien al finalizar):

![ADB_complete.png](../../../_resources/Alexa/968097a7b22d937599b3c62b8b77e711.png)

Con esto ya tendríamos LineageOS instalado, y solo nos quedaría reiniciar el sistema dandole a "Reboot system":
Donde el sistema arrancará con el logo de amazon convencional y después aparecerá LineageOS:

![LineageOS.jpg](../../../_resources/Alexa/IMG_20260402_105644_474.jpg)

Los pasos de aquí en adelante son los típicos que se hacen al configurar un móvil android por primera vez, nada que no sepamos hacer todos. Al acabar tendremos un sistema operativo Android 11 completamente funcional y libre:

![LineageOS_home.jpg](../../../_resources/Alexa/IMG_20260402_110102_502.jpg)

