# Política de seguridad

## Alcance

Se aceptan informes sobre problemas de seguridad de **Onyx Flipper Lab**. El proyecto está destinado a educación, ingeniería defensiva y auditorías explícitamente autorizadas de hardware.

## Comunicación responsable

Evita publicar detalles de explotación antes de que puedan evaluarse y corregirse. Un informe útil debe incluir versión/commit, pasos reproducibles, impacto previsto, demostración no destructiva con equipos autorizados y posibles medidas.

No publiques contraseñas, tokens, claves privadas ni datos personales.

## Límites operativos de la v3

Los módulos excluyen expresamente:

- Transmisión o reproducción Sub-GHz.
- Transmisión infrarroja.
- Emulación o escritura NFC y LF RFID.
- Fuerza bruta o interferencias.
- Cambio de perfiles Bluetooth o eliminación de dispositivos vinculados.
- Persistencia encubierta de identificadores observados.

El módulo GPIO solo utiliza **entrada/ADC**.

## Conservación de informes

La exportación voluntaria guarda un único resumen en el almacenamiento de la aplicación; el nuevo informe sustituye al anterior. Solo contiene contadores y medidas agregadas. Excluye UID NFC, datos LF RFID, direcciones/comandos IR, contraseñas y muestras RF reutilizables.

## Autorización

No se permite realizar pruebas sobre sistemas, credenciales, cerraduras, tarjetas, radios, vehículos, alarmas o infraestructuras de terceros sin autorización expresa.

Las investigaciones de buena fe y sin perjuicio realizadas sobre equipos propios o autorizados se consideran responsables dentro del alcance del proyecto. Esta política no concede autorización sobre sistemas ajenos.

© 2026 Fran Gonzas
