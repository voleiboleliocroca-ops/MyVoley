# MyVoley — proyecto Android

Primera versión funcional de una app de gestión de voleibol, offline y con datos guardados localmente.

## Incluido en esta versión
- Acceso local con creación de contraseña en el primer inicio.
- Verificación de contraseña mediante PBKDF2-HMAC-SHA256 (210.000 iteraciones y salt aleatorio de 16 bytes).
- Base de datos SQLite local.
- Alta, consulta, edición y eliminación de jugadoras.
- Nombre, dorsal, posición, anotaciones técnicas.
- Estadísticas acumuladas por jugadora: saques ganadores, ataques, bloqueos, recepciones y errores.
- Resumen estadístico del equipo.
- Interfaz Android con Jetpack Compose.
- No solicita permisos de internet ni sincroniza datos con servidores.

## Requisitos para compilar
- Android Studio actualizado.
- JDK 17.
- Android SDK Platform 35 y las herramientas de compilación que proponga Android Studio.
- Conexión a internet en el ordenador durante la primera compilación para descargar Gradle y dependencias. La aplicación instalada funciona sin internet.

## Generar el APK
1. Descomprime `MyVoley-proyecto.zip`.
2. Abre Android Studio y selecciona **Open**; elige la carpeta `MyVoley` (la que contiene `settings.gradle.kts`).
3. Espera a que termine la sincronización de Gradle e instala las plataformas SDK que solicite.
4. Selecciona **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
5. El APK de depuración quedará normalmente en `app/build/outputs/apk/debug/app-debug.apk`.
6. Pasa el archivo al móvil e instálalo. Android puede pedir permiso para instalar aplicaciones desde esa fuente.

Para crear un APK firmado para distribuirlo, usa **Build > Generate Signed Bundle / APK** en Android Studio y crea un keystore que guardes en un lugar seguro.

## Primer uso
Al abrir la aplicación por primera vez, crea una contraseña de al menos 8 caracteres. Después podrás añadir jugadoras desde la pestaña **Plantilla**. La contraseña no se puede recuperar desde esta versión; si se olvida, será necesario borrar los datos de la app, lo que también elimina la base de datos local.

## Alcance y siguientes mejoras
Esta versión registra estadísticas acumuladas manualmente en la ficha de cada jugadora. Todavía no incluye registro por partido, temporadas, exportación/copias de seguridad, fotos, recuperación de contraseña ni cifrado completo de la base de datos. Los datos permanecen en el almacenamiento privado de la app, pero no están cifrados como base de datos; evita almacenar información especialmente sensible hasta añadir cifrado y copias de seguridad seguras.

## Compilar el APK sin instalar programas en tu ordenador (GitHub Actions)

Este proyecto incluye un flujo automático en `.github/workflows/build-apk.yml`.

1. En GitHub, crea un repositorio nuevo llamado `MyVoley` (puede ser privado).
2. Sube el contenido de esta carpeta al repositorio, manteniendo también la carpeta oculta `.github`.
3. Abre la pestaña **Actions** del repositorio y selecciona **Construir APK MyVoley**.
4. Pulsa **Run workflow** y espera a que termine el proceso en verde.
5. En la ejecución completada, baja a **Artifacts** y descarga `MyVoley-apk-debug`.
6. Descomprime el ZIP descargado: dentro estará `app-debug.apk`. Pásalo al móvil e instálalo. Android puede pedir permiso para instalar aplicaciones desde esa fuente.

Es un APK de depuración para pruebas, no una versión firmada para publicar en Google Play. La compilación depende de que GitHub Actions complete correctamente el proceso.
