# Monitoreo de Sensores en Tiempo Real — Campus La María (UTEQ)

![Captura de la aplicación](./Captura.png)

Aplicación web desarrollada con **React + Vite** y **Firebase Realtime Database** para monitorear en tiempo real las mediciones ambientales de **10 sensores** ubicados en el campus La María de la **Universidad Técnica Estatal de Quevedo (UTEQ)**.

El sistema permite visualizar datos de **temperatura, humedad y presión atmosférica**, además de consultar la información de cada sensor y sus registros históricos.

## Estructura de datos en Firebase RTDB

```text
/ubicacionesSensores/{sensorId}
    → nombre, estudiante, campus, zona, ciudad,
      provincia, latitud, longitud, estado

/valorActual/{sensorId}
    → temperatura, humedad, presionAtmosferica, timestamp

/valoresHistoricos/{sensorId}/{timestamp}
    → temperatura, humedad, presionAtmosferica, timestamp
```

## Instalación y configuración

### 1. Configurar Firebase

Crear o utilizar un proyecto en [Firebase Console](https://console.firebase.google.com/) y habilitar **Firebase Realtime Database**.

Importar el archivo:

```text
firebase-rtdb-10-sensores-campus-la-maria.json
```

en el nodo raíz de la base de datos.

### 2. Configurar las reglas

Reemplazar las reglas de Firebase por las incluidas en:

```text
firebase-rules.json
```

Estas reglas incluyen el índice `.indexOn` para optimizar las consultas mediante `timestamp`.

### 3. Configurar las variables de entorno

Copiar el archivo `.env.example` como `.env` y colocar las credenciales de la aplicación web de Firebase:

```env
VITE_FIREBASE_API_KEY=TU_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=TU_AUTH_DOMAIN
VITE_FIREBASE_DATABASE_URL=TU_DATABASE_URL
VITE_FIREBASE_PROJECT_ID=TU_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=TU_STORAGE_BUCKET
VITE_FIREBASE_MESSAGING_SENDER_ID=TU_MESSAGING_SENDER_ID
VITE_FIREBASE_APP_ID=TU_APP_ID
```

### 4. Instalar dependencias

Desde la carpeta principal del proyecto ejecutar:

```bash
npm install
```

### 5. Ejecutar la aplicación

```bash
npm run dev
```

Luego abrir la dirección local proporcionada por Vite en el navegador.

## Rutas principales

| Ruta                | Contenido                                        |
| ------------------- | ------------------------------------------------ |
| `/`                 | Redirige al dashboard del sensor `sensor_001`    |
| `/sensor/:sensorId` | Dashboard dinámico del sensor indicado en la URL |
| `/ubicaciones`      | Directorio de los 10 sensores disponibles        |

## Prueba de funcionamiento en tiempo real

1. Abrir la ruta `/ubicaciones`.
2. Seleccionar un sensor, por ejemplo **Estación Ambiental 4**.
3. Comprobar que la aplicación abre `/sensor/sensor_004`.
4. Verificar que se muestran los datos correspondientes al sensor seleccionado.
5. Entrar a **Firebase Console** y modificar:

```text
valorActual/sensor_004/temperatura
```

6. Comprobar que el valor de temperatura se actualiza automáticamente en la aplicación **sin recargar la página**.
7. Agregar un nuevo registro dentro de:

```text
valoresHistoricos/sensor_004
```

utilizando un `timestamp` actual.
8. Verificar que el nuevo registro aparece automáticamente en la tabla de datos históricos.

## Tecnologías utilizadas

* **React**
* **Vite**
* **Firebase Realtime Database**
* **JavaScript**
* **HTML5**
* **CSS3**

## Objetivo del proyecto

El proyecto tiene como objetivo implementar una interfaz web para la **visualización y monitoreo de sensores ambientales en tiempo real**, facilitando el seguimiento de las condiciones ambientales dentro del campus **La María de la UTEQ** mediante una conexión directa con Firebase Realtime Database.
