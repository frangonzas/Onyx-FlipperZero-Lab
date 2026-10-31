# Compilación e instalación

## Requisitos

Flipper Zero con tarjeta microSD, cable USB, Python 3.8 o superior para instalar uFBT y el entorno **uFBT**.

## Instalar uFBT

**macOS/Linux:**

~~~bash
python3 -m pip install --upgrade ufbt
~~~

**Windows:**

~~~powershell
py -m pip install --upgrade ufbt
~~~

## Obtener y compilar el proyecto

~~~bash
git clone https://github.com/frangonzas/Onyx-FlipperZero-Lab.git
cd Onyx-FlipperZero-Lab
ufbt
~~~

Cuando la compilación termina correctamente, la FAP se coloca en \`dist/\`.

## Ejecutar en Flipper conectado

~~~bash
ufbt launch
~~~

El comando compila, transfiere el archivo por USB y abre la aplicación.

## Compatibilidad con el SDK

uFBT obtiene un SDK del canal de firmware elegido. Si el dispositivo informa de incompatibilidad de API/SDK, actualiza el SDK local o compila contra la misma familia de firmware instalada.

## Transferencia manual

Puedes copiar el archivo FAP desde el ordenador a la microSD utilizando el gestor de archivos de qFlipper. La carpeta base de aplicaciones es:

~~~text
/ext/apps/
~~~

La categoría específica se establece mediante \`fap_category\` en \`application.fam\`.

## Registros técnicos

La aplicación utiliza los mensajes de ciclo de vida de Furi. Con el dispositivo conectado:

~~~bash
ufbt cli
~~~

Selecciona el nivel de registro pertinente desde la consola de Flipper. No publiques registros con datos sensibles.

© 2026 Fran Gonzas
