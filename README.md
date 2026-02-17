# CitySpots - Módulo 4: Hardware & Maps

**CitySpots** es una aplicación nativa de Android desarrollada con **Kotlin** y **Jetpack Compose** que permite a los usuarios capturar momentos especiales vinculándolos a una ubicación geográfica. La app utiliza la cámara del dispositivo, el GPS y Google Maps para crear una experiencia de "diario de viaje" visual.

---

## Características Principales

* ** Captura de Fotos:** Integración con CameraX para tomar fotografías dentro de la app.
* ** Geolocalización:** Uso de FusedLocationProvider para obtener coordenadas GPS precisas.
* ** Google Maps:** Visualización de los "Spots" guardados como marcadores en un mapa interactivo.
* ** Persistencia de Datos:** Base de datos local con Room (SQLite) para guardar la información del lugar.
* ** Gestión de Almacenamiento:** Sistema inteligente para guardar y eliminar imágenes del almacenamiento interno.

---

## Parte 1: Configuración de Google Maps API

El primer desafío del laboratorio fue configurar la seguridad y el acceso al SDK de Google Maps para Android.

### Pasos Realizados:
1.  **Seguridad de API Key:** Se configuró el archivo `local.properties` (el cual es ignorado por Git) para almacenar la variable `MAPS_API_KEY`.
2.  **Inyección con Gradle:** Se modificó el archivo `build.gradle.kts` para leer esta propiedad segura e inyectarla en el Manifiesto durante la compilación.
3.  **Metadata en Manifest:** Se configuró el `AndroidManifest.xml` para consumir la clave inyectada, permitiendo que el mapa cargue correctamente sin exponer la clave en el control de versiones.

---

## Parte 2: Funcionalidad de Borrado (Spot Deletion)

Se implementó la funcionalidad completa para eliminar registros, cumpliendo con la **Definition of Done** requerida. Esta característica abarca todas las capas de la arquitectura Clean/MVVM.

### Criterios Cumplidos:

- [x] **DAO (Data Access Object):**
  - Se agregó la consulta `@Query("DELETE FROM spots WHERE id = :id")` en `SpotDao`.

- [x] **Repository & Limpieza de Archivos:**
  - Se creó la función `deleteSpot` en el Repositorio.
  - **Lógica Clave:** No solo se borra el registro de la base de datos, sino que también se elimina el archivo físico (`.jpg`) del almacenamiento interno del teléfono para evitar "archivos basura".

- [x] **ViewModel:**
  - Gestión de Corrutinas para realizar el borrado en segundo plano (Background Thread) y actualizar el estado de la UI automáticamente mediante `StateFlow`.

- [x] **Interfaz de Usuario (UI):**
  - **Interacción:** Se implementó un gesto de **Pulsación Larga (Long Press)** en la ventana de información del marcador (`onInfoWindowLongClick`).
  - **Confirmación:** Se diseñó un `AlertDialog` nativo que pregunta "¿Estás seguro?" antes de proceder, evitando borrados accidentales.

---

## Arquitectura y Tecnologías

El proyecto sigue una arquitectura **MVVM (Model-View-ViewModel)** recomendada por Google:

* **UI:** Jetpack Compose (Material 3).
* **State Management:** StateFlow & ViewModel.
* **Dependency Injection:** Koin.
* **Async:** Kotlin Coroutines.
* **Image Loading:** Coil.
* **Maps:** Maps SDK for Android (Maps Compose Library).

---

## Video Explicativo

[https://youtu.be/yquQuXq41XM]

---
