# Verificación del proyecto

Fecha de comprobación: 28 de octubre de 2026.

## Resultado

La tarea `:app:assembleDevDebug` terminó con **BUILD SUCCESSFUL**, con 40 tareas ejecutadas, en una copia temporal de comprobación. Se compilaron Kotlin, Java y las clases generadas por KSP y Hilt, y se generó un APK de comprobación.

La copia temporal conserva los mismos archivos fuente de la solución. Su única adaptación de compilación es retirar la aplicación del plugin `com.google.gms.google-services` del módulo app, porque todavía no existe el archivo real `google-services.json` del estudiante. El proyecto entregado conserva el plugin y requiere ese archivo.

No se distribuye el APK de comprobación, porque no tiene la configuración necesaria para ejecutar Firebase. No se realizó una prueba funcional con una cuenta o una base de datos real.

## Entorno utilizado

- JDK 17.0.14.
- Gradle 8.9 y Android Gradle Plugin 8.7.3.
- Android SDK 34 y Build Tools 34.0.0.
- Kotlin 1.9.0 y Compose Compiler 1.5.0.

Gradle mostró advertencias de APIs obsoletas, Jetifier e instrumentación de clases opcionales. No impidieron generar el APK; la ejecución real en dispositivo sigue siendo necesaria para comprobar el comportamiento.

## Revisiones adicionales

- `git diff --check` sin errores de espacios.
- Informe Word renderizado a PDF con Word y revisión visual de sus cinco páginas.
- ZIP comprobado para detectar archivos corruptos y confirmar la inclusión del historial Git y Gradle Wrapper.

## Pendiente para la entrega académica

1. Crear el proyecto de Firebase y registrar la app.
2. Añadir `start/app/google-services.json`, habilitar los proveedores y publicar las reglas.
3. Compilar el proyecto entregado y ejecutar las pruebas descritas en LEEME_PRIMERO.md.
4. Publicar el repositorio en la cuenta personal de GitHub.
5. Grabar el video real, completar los datos y enlaces del informe y ajustar la reflexión personal a la experiencia obtenida.
