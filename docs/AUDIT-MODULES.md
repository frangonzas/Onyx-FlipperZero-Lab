# Módulos de auditoría

## Auditor GPIO

Mide tensión analógica de pines externos compatibles con ADC **sin activar salidas**.

- Enumera pines ADC no reservados por el firmware.
- Configura entrada analógica.
- Obtiene valor de ADC de 12 bits y tensión calibrada en milivoltios.
- Cuenta muestras de la sesión.
- Conserva mínimo y máximo registrados.

**Límite:** nunca configura el pin como salida ni modifica su nivel lógico.

## Monitor RSSI Sub-GHz

Evalúa pasivamente la presencia de señales RF con el CC1101 interno.

- Usa la configuración RX OOK asíncrona oficial.
- Permite seleccionar frecuencias admitidas por el hardware.
- Presenta RSSI actual/máximo y LQI.
- Registra mínimos y máximos por sesión.
- Permite fijar el nivel RSSI actual como referencia.
- Calcula la diferencia en directo e indica cambios mayores de **±12 dB**.

El umbral es un indicador de campo sencillo, no un sistema de clasificación RF. **No hay transmisión, reproducción, codificación ni gestión de claves.**

## Auditoría Bluetooth

Consulta el estado local del controlador utilizando API HAL públicas:

- Controlador disponible.
- Publicidad o conexión activa.
- Capacidades GATT/GAP.
- Indicador de modo de pruebas.
- RSSI de enlace cuando hay Bluetooth activo.

La API pública de FAP no expone un escáner general de anuncios BLE estable; no se utilizan API internas no documentadas.

## Inspección infrarroja

Recibe señales de equipos autorizados, utiliza el decodificador del firmware, identifica protocolos compatibles, presenta dirección/comando y repetición **solo en memoria**, informa de tiempos cuando no hay decodificación y aumenta el contador de señales. **No transmite IR.**

## Detector NFC

Utiliza el escáner \`NfcScanner\` oficial para identificar familias de protocolos; muestra hasta cuatro identificadores detectados y contabiliza eventos durante la sesión. Los datos quedan en RAM.

No autentica, emula, escribe ni accede a sectores de aplicación protegidos. El informe exportado incluye únicamente el **contador de detecciones**, nunca UID.

## Lector LF RFID

Permite identificar protocolos ASK/PSK de credenciales propias o autorizadas. Muestra un máximo temporal de ocho bytes y contabiliza detecciones.

No invoca escritura ni emulación RFID. El informe guarda únicamente el recuento de eventos, no los bytes de la credencial.

## Informe de sesión

La pantalla muestra muestras y rango GPIO, muestras y rango RSSI Sub-GHz, contadores IR/NFC/LF RFID y estado de la última exportación.

Al pulsar **OK** escribe \`last_audit_report.txt\` en el directorio de datos de la aplicación. El archivo sustituye al anterior y contiene solo valores agregados.

## Aleatoriedad

El generador de contraseñas y el generador HEX utilizan el RNG de hardware del firmware. La selección de caracteres emplea *rejection sampling* para evitar el sesgo simple de módulo.

© 2026 Fran Gonzas
