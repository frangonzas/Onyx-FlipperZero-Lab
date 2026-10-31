# Historial de cambios

## 3.0.0 — Terminal de auditoría de campo · VERSIÓN FINAL

### Validación

- Compilación con el SDK oficial estable de Flipper.
- Instalación y pruebas documentadas en Flipper Zero físico.
- Estado del proyecto: **FINALIZADO / SOLO MANTENIMIENTO**.

### Funciones incorporadas

- Contador de muestras GPIO por sesión.
- Valores mínimo y máximo de tensión GPIO.
- RSSI mínimo/máximo de Sub-GHz por sesión.
- Referencia RSSI Sub-GHz fijada por el operador.
- Diferencia instantánea de RSSI y aviso simple por variación de ±12 dB.
- Contadores de señales IR, detecciones NFC y detecciones LF RFID.
- Pantalla de informe de sesión.
- Exportación de informe respetuoso con la privacidad a microSD.
- Documentación del formato de informe.

### Cambios internos y privacidad

- Versión de aplicación actualizada a 3.0.
- Mayor reserva de pila para la sesión ampliada.
- Documentación explícita del almacenamiento.
- Informe sin credenciales, UID NFC ni comandos IR.
- Módulos de radio y credenciales limitados a lectura o recepción.

## 2.0.0 — Herramientas de auditoría de hardware

Auditor GPIO ADC, monitor Sub-GHz RSSI/LQI en RX, estado Bluetooth, inspección IR, detector NFC y lector LF RFID.

## 1.0.0 — Primera versión

Generador de contraseñas con RNG de hardware, generador HEX aleatorio, consejos de seguridad, estructura inicial FAP y CI.
