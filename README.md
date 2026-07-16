# 📡 Implementación de una Red Privada LTE con soporte IoT mediante SDR

Este repositorio contiene la documentación y configuración para el despliegue de una **Red Privada LTE (4G)** con soporte para dispositivos del Internet de las Cosas (IoT), implementada mediante **Radio Definido por Software (SDR)**. 

Proyecto desarrollado para el curso de Comunicaciones Móviles de la **Universidad Nacional Mayor de San Marcos (UNMSM)**.

## 🚀 Acerca del Proyecto

El objetivo principal de este proyecto es el diseño, despliegue y validación de una estación base de comunicaciones móviles funcional con capacidad de recibir y procesar datos de dispositivos IoT. Para ello, se utiliza la suite de código abierto **srsRAN 4G** para virtualizar las funciones de red (EPC y eNodeB) interactuando con hardware SDR **USRP B200**. 

El sistema fue validado mediante un caso de uso real de IoT: la transmisión periódica de datos de sensores (temperatura, humedad y batería) desde un smartphone conectado a la red celular privada hacia un dashboard de monitoreo en tiempo real.

## 🏗️ Arquitectura del Sistema

La topología de la red se divide en cuatro bloques principales:

1. **Dispositivo IoT (UE):** Smartphone Samsung Galaxy J6+ (Banda 7) equipado con una SIM programable. Ejecuta la aplicación IoT MQTT Panel para publicar telemetría.
2. **Estación Base (eNodeB):** Hardware USRP B200 conectado vía USB 3.0 a la PC host. Utiliza el módulo `srsENB` para implementar la capa física y de acceso radio.
3. **Núcleo de Red (EPC):** Implementado con `srsEPC` en Ubuntu 24.04 LTS. Gestiona el MME, HSS (con autenticación Milenage), S-GW y P-GW.
4. **Servidor de Monitoreo (Stack IoT):** Compuesto por un Broker MQTT (Mosquitto), un script de integración en Python, InfluxDB para almacenar las métricas temporales y Grafana para la visualización.

## 🛠️ Requisitos

### Hardware
* PC/Servidor Host (Recomendado: procesador multicore y puertos USB 3.0 dedicados).
* SDR **USRP B200** (Ettus Research).
* Lector de tarjeta SIM USB y tarjeta SIM programable (LTE/Milenage).
* Equipo de Usuario (UE) compatible con LTE Banda 7 (2600 MHz).

### Software
* **Sistema Operativo:** Ubuntu 24.04 LTS.
* **Stack Móvil:** [srsRAN 4G](https://github.com/srsran/srsRAN_4G) (versión 25.10.0) y controladores UHD (v4.6).
* **Stack IoT:** Eclipse Mosquitto, InfluxDB, Grafana (v13.1.0), Python 3.
* **Herramientas SIM:** SIM Personalize Tools (o equivalente) para la grabación de parámetros (IMSI, KI, OPC).

## ⚙️ Parámetros de Red (Configuración)

La red está configurada para operar con los siguientes parámetros de radiofrecuencia e identificación:

* **Banda de Operación:** Banda 7 LTE (FDD)
* **Frecuencia Downlink (DL):** 2680 MHz (EARFCN 3350)
* **Frecuencia Uplink (UL):** 2560 MHz
* **Ancho de Banda:** 10 MHz (50 PRBs)
* **Identificadores:** MCC: `001`, MNC: `01`
* **APN IoT:** `srsapn`

## 📊 Resultados y KPIs

* **Attach LTE 100% Exitoso:** Se logró completar todas las etapas del protocolo NAS, incluyendo el acceso aleatorio RACH, autenticación Milenage y establecimiento del bearer de datos.
* **Estabilidad del Plano de Datos:** Conectividad IP extremo a extremo verificada (0% de pérdida de paquetes) con una latencia mínima de 19.8 ms.
* **Telemetría E2E:** Recepción exitosa y continua de datos MQTT en el dashboard de Grafana con tasas de actualización de 5 segundos a través del enlace de radiofrecuencia privado.

## 👥 Autor

* **Alexis Cosme Romero** 

---
*Facultad de Ingeniería Electrónica y Eléctrica - Escuela Profesional de Ingeniería de Telecomunicaciones | UNMSM - Julio 2026*
