# ONYX FLIPPER LAB — v3.0.0

**Terminal de auditoría defensiva para Flipper Zero**  
**Creador: Fran Gonzas · Lenguaje: C · Formato: aplicación externa FAP**

## Estado del proyecto

| Campo | Estado |
|---|---|
| Versión | **3.0.0 — final** |
| Plataforma | Flipper Zero |
| Compilación | uFBT y SDK oficial de Flipper |
| Validación | Compilación superada y versión probada en hardware físico, según documentación del proyecto |
| Mantenimiento | Correcciones de compatibilidad, seguridad y documentación |
| Uso | Auditorías autorizadas, observación pasiva y generación de informes |

> **Limitación importante:** el proyecto no transmite por Sub-GHz, no reproduce señales, no clona credenciales ni realiza interferencias de radiofrecuencia.

## Funciones de la versión final

La v3 consolida las herramientas en una **sesión de auditoría de campo** que acumula contadores y medidas:

- Conteo y rango de tensión mínimo/máximo por GPIO.
- Monitor de RSSI/LQI Sub-GHz en recepción, con referencia configurable y diferencia en directo.
- Indicador simple de variaciones mayores de ±12 dB respecto al nivel de referencia.
- Contadores de señales IR y detecciones NFC/LF RFID.
- Informe resumido de sesión exportable a microSD.
- Utilidades de contraseñas y hexadecimal basadas en el generador aleatorio del hardware.

## Módulos

| Módulo | Información | Límite |
|---|---|---|
| **Auditor GPIO** | ADC, tensión, muestras y valores mínimo/máximo | No configura salidas GPIO |
| **Sub-GHz RSSI** | RSSI/LQI, máximo, línea base y diferencia | Solo recepción, sin transmisión |
| **Bluetooth** | Estado local del controlador y enlace | No cambia perfiles |
| **Inspección IR** | Recepción, decodificación y tiempos | No transmite infrarrojos |
| **Detector NFC** | Familia de protocolo mediante API oficial | No emula ni escribe |
| **Lector LF RFID** | Tipo ASK/PSK y vista temporal de datos | No escribe ni emula |
| **Informe de sesión** | Contadores y medidas agregadas | Solo escribe el informe |
| **Contraseñas aleatorias** | Caracteres mediante RNG hardware | Ejecución local |
| **HEX aleatorio** | Ocho bytes mediante RNG hardware | Ejecución local |

## Controles físicos

- **Arriba / Abajo:** navegar por el menú.
- **Izquierda / Derecha:** cambiar pin GPIO o banda Sub-GHz.
- **OK en Sub-GHz:** registrar el RSSI actual como referencia.
- **OK en Informe de sesión:** exportar el resumen.
- **Atrás:** detener el módulo y volver al menú.

## Privacidad de los informes

La ruta del último informe es:

~~~text
/ext/apps_data/onyx_flipper_lab/last_audit_report.txt
~~~

Solo se almacenan métricas agregadas y contadores. **No se guardan** UID de NFC, datos LF RFID, comandos IR, contraseñas generadas ni muestras RF reutilizables. Cada exportación sustituye al informe anterior.

[Especificación del informe](docs/REPORT-FORMAT.md) · [Política de seguridad](SECURITY.md)

## Compilación e instalación

Necesitas Flipper Zero, microSD, conexión USB y Python compatible con uFBT.

**macOS/Linux:**

~~~bash
python3 -m pip install --upgrade ufbt
git clone https://github.com/frangonzas/Onyx-FlipperZero-Lab.git
cd Onyx-FlipperZero-Lab
ufbt
~~~

**Windows PowerShell:**

~~~powershell
py -m pip install --upgrade ufbt
git clone https://github.com/frangonzas/Onyx-FlipperZero-Lab.git
cd Onyx-FlipperZero-Lab
ufbt
~~~

Para compilar, transferir y ejecutar en un dispositivo conectado:

~~~bash
ufbt launch
~~~

GitHub Actions compila con el SDK oficial y ofrece el archivo \`.fap\` como artefacto, cuando la ejecución termina correctamente.

[Manual de compilación](docs/BUILD.md) · [Arquitectura](docs/ARCHITECTURE.md) · [Módulos de auditoría](docs/AUDIT-MODULES.md)

## Nota técnica sobre Bluetooth

La API pública para aplicaciones externas de Flipper ofrece información útil del estado Bluetooth, pero **no proporciona un escáner genérico estable de anuncios BLE** para todas las FAP. El módulo utiliza las funciones públicas disponibles sin depender de componentes internos inestables.

## Política de uso

Solo para dispositivos, sistemas y radiofrecuencias propios o con autorización expresa. El indicador de variación de señal **no prueba** la identidad de un emisor ni la existencia de un ataque.

[Estado final del proyecto](FINAL_STATUS.md) · [Historial](CHANGELOG.md) · [Seguridad](SECURITY.md)

**© 2026 Fran Gonzas · v3.0.0 final · Mantenimiento.**
