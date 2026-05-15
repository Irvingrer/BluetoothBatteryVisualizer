# BluetoothBatteryVisualizer🔋✨
APK para visualización de porcentaje de batería de dispositivos conectados por bluetooth BLE o HID, con una burbuja que se superpone a las demás aplicaciones abiertas, permitiendo predecir el desgaste de la pila en entornos industriales (Handhelds y PDA)

[![Android](https://img.shields.io/badge/Platform-Android-3DDC84?style=flat-square&logo=android&logoColor=white)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Language-Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white)](https://kotlinlang.org)
[![Department](https://img.shields.io/badge/Department-Evolución%20Tecnológica-00BCD4?style=flat-square)](#)

**BT Battery Monitor** es una aplicación nativa para Android diseñada para optimizar y auditar las operaciones logísticas en centros de distribución. Su función principal es supervisar en tiempo real el nivel de batería de los periféricos Bluetooth conectados (como ring scanners, lectores portátiles y wearables de marcas como Honeywell, Netum, COZEK o Steren) mediante una interfaz dinámica y un **overlay (burbuja flotante) persistente**.

Esta herramienta elimina la incertidumbre operativa provocada por descargas inesperadas de hardware de escaneo, garantizando la continuidad del flujo de trabajo en almacén.

---

## 🚀 Características Principales

* **Burbuja Flotante HUD (Heads-Up Display):** Un globo interactivo que permanece visible sobre cualquier pantalla o aplicación de escaneo del PDA.
* **Gestos Avanzados:** El globo cuenta con físicas de arrastre suave para reposicionarlo en cualquier área de la pantalla y soporta **doble toque rápido** para regresar instantáneamente a la app principal.
* **Semáforo de Alertas Inteligente:** El texto del porcentaje en el globo cambia de color dinámicamente según el rango de carga para una auditoría visual inmediata:
    * 🟢 **100% - 70%:** Estado Óptimo (Verde)
    * 🟡 **69% - 30%:** Estado Moderado (Amarillo)
    * 🔴 **29% - 1%:** Alerta Crítica / Requiere Cambio (Rojo)
* **Efecto Frosted Glass:** Interfaz moderna con un fondo un 30% translúcido (`#4DFFFFFF`) y tipografía gruesa optimizada para una legibilidad perfecta en entornos de alta movilidad.
* **Monitoreo Reactivo e Inmediato:** Sincronización bidireccional en tiempo real mediante *BroadcastReceivers* que detectan la conexión, desconexión (`ACL_DISCONNECTED`) y nivel exacto del hardware, incluyendo un escaneo de bienvenida retroactivo si el dispositivo ya estaba enlazado.
* **Panel de Control Minimalista:** Interfaz limpia y centrada con un solo botón de acción inmediata: `INICIAR` y `APAGAR`.

---

## 🛠️ Arquitectura y Tecnologías

El proyecto se construyó bajo estándares nativos de Android enfocados en bajo consumo de memoria y rendimiento en entornos industriales:

* **Language:** Kotlin 
* **Asincronía y Eventos:** `BroadcastReceiver` dinámicos para capturar intents del sistema como `BATTERY_LEVEL_CHANGED` y cambios de estado del adaptador Bluetooth.
* **Componentes de Fondo:** `Foreground Service` respaldado por notificaciones persistentes (`NotificationChannel`) para asegurar que Android no destruya el proceso de monitoreo en segundo plano.
* **UI Dinámica:** `WindowManager` con tipos de capa `TYPE_APPLICATION_OVERLAY` y control manual de layouts a través de `MotionEvent` y `GestureDetector`.
* **Reflexión de Clases:** Invocación de métodos ocultos del SDK de Android (`device.javaClass.getMethod("isConnected")`) para garantizar la compatibilidad de lectura en PDAs industriales (ej. Urovo, iData).

---

## 📦 Estructura del Código Clave

* **`MainActivity.kt`:** Gestiona el ciclo de vida de la pantalla principal, solicitudes dinámicas de permisos en tiempo real (`BLUETOOTH_CONNECT` para Android 12+) y el renderizado del listado de hardware activo con un retraso estratégico de seguridad (500ms) para evitar falsos positivos de carga.
* **`BatteryOverlayService.kt`:** Servicio encargado de instanciar la burbuja en la ventana global del sistema, procesar la lógica del semáforo de colores y controlar los gestos táctiles.
* **`rounded_background.xml`:** Recurso vectorial que define la geometría oval (`android:shape="oval"`) para mantener un diseño de burbuja perfectamente simétrico y estético.

---

## ⚙️ Requisitos de Instalación

1. **Permisos Requeridos:**
   * Al iniciar la aplicación por primera vez, otorgar el permiso de **"Aparecer encima de otras aplicaciones"** (Overlay Permission).
   * Permitir los accesos de **Dispositivos cercanos (Bluetooth)**.
2. **Dispositivos Compatibles:** Diseñado para smartphones y terminales PDA Android (probado con éxito en entornos operativos Android M hasta Android S+).

---

<p align="center">
  <b>Desarrollado por el Departamento de Evolución Tecnológica</b>
</p>
