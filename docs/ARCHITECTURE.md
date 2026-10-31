# Arquitectura — Onyx Flipper Lab v3.0.0

## Objetivos de diseño

La aplicación prioriza la observación pasiva, las API públicas y estables del SDK de Flipper, el tratamiento de datos con límites, el ciclo de vida explícito de cada módulo y la ausencia de persistencia encubierta. No implementa reproducción de capturas, clonación de credenciales, interferencias ni fuerza bruta.

## Modelo de ejecución

~~~text
Botones
  │
  ▼
Callback de entrada
  │
  ▼
FuriMessageQueue
  │
  ▼
Bucle principal ──────────► Ciclo de vida del módulo
  │                             │
  ▼                             ├── GPIO ADC
Estado con mutex                ├── Sub-GHz RX
  │                             ├── Bluetooth HAL
  ▼                             ├── Trabajador IR
Callback gráfico                ├── Escáner NFC
                                └── Trabajador LF RFID
~~~

El callback de entrada solo encola eventos. **El hilo principal** controla el inicio y la parada de recursos físicos.

## Concurrencia

Los módulos IR, NFC y LF RFID utilizan trabajadores y callbacks del firmware. Estos callbacks copian únicamente datos acotados, no dibujan directamente, adquieren el mutex de aplicación antes de modificar el estado compartido y no guardan credenciales. El dibujo de la interfaz también protege las instantáneas con el mismo mutex.

## Ciclo de vida del hardware

Al abrir una pantalla se obtienen únicamente los recursos necesarios. Al pulsar **Atrás**:

1. Se vuelve al menú.
2. Se detiene el recurso de radio, trabajador o escáner correspondiente.
3. Se libera la memoria y los objetos asociados.

Esto evita mantener activos módulos que el operador ya ha cerrado.

## Sub-GHz

El CC1101 interno se inicializa, restablece, configura con la modulación OOK asíncrona oficial, ajusta a una frecuencia admitida, pasa a **RX** y permite consultar RSSI/LQI. **No se llama a una función de transmisión.**

## GPIO

Se consultan los metadatos del firmware para seleccionar pines con ADC que no estén reservados para depuración. El pin se configura como entrada analógica, se muestrea y se calcula su tensión en milivoltios. No se fuerza un nivel de salida.

## Bluetooth

La API pública de aplicaciones externas ofrece información del estado del controlador/enlace, pero no un escáner genérico estable de anuncios BLE. El proyecto evita las API privadas del firmware.

## Modelo de amenazas

**Activos:** integridad de Flipper, expectativas de observación pasiva, datos temporales de señales y etiquetas, y valores aleatorios generados.

**Límite de confianza:** las señales y etiquetas externas son entradas no fiables.

**Fuera del alcance:** atacar terceros, superar controles de acceso, obtener sectores NFC protegidos, clonar credenciales, reproducir transmisiones y conservar credenciales a largo plazo.

La v3 añade métricas por sesión e informes agregados; consulta [Formato de informe](REPORT-FORMAT.md).

© 2026 Fran Gonzas
