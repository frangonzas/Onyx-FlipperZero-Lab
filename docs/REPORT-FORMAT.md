# Formato del informe de auditoría

## Archivo generado

La última exportación se escribe en:

~~~text
/ext/apps_data/onyx_flipper_lab/last_audit_report.txt
~~~

Cada exportación sustituye la anterior para reducir la acumulación innecesaria de observaciones.

## Ejemplo del formato real

**Los nombres de campos se conservan en inglés porque forman parte del formato que escribe la aplicación. No deben traducirse dentro de los archivos exportados.**

~~~text
ONYX FLIPPER LAB - FIELD AUDIT REPORT
Version: 3.0
Operator: Fran Gonzas
Scope: defensive / authorized / read-only radio

Session start: 2026-09-27 12:00:00
Report time:   2026-09-27 12:15:00

[GPIO]
samples=42
min_mv=0
max_mv=3294

[SUBGHZ_RX]
samples=105
min_rssi_dbm=-103.4
max_rssi_dbm=-44.7
tx_performed=false

[SIGNAL_INVENTORY]
ir_signals=4
nfc_detection_events=2
lf_rfid_detection_events=1

[PRIVACY]
credential_payloads_saved=false
ir_commands_saved=false
nfc_uid_saved=false
lf_rfid_bytes_saved=false

END OF REPORT
~~~

## Privacidad

El informe resume medidas, **no crea una base de datos de credenciales**. No almacena UID NFC, sectores de aplicación NFC, bytes LF RFID, direcciones/comandos IR, contraseñas generadas ni capturas Sub-GHz reproducibles.

## Interpretación de los datos

El RSSI depende del entorno, distancia, orientación de antena, interferencias y configuración del receptor. La diferencia respecto a una referencia es un indicador comparativo: **no demuestra** la identidad de un dispositivo ni un comportamiento malicioso.

© 2026 Fran Gonzas
