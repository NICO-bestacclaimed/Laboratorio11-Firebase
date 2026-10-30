# Repositorio de entrega del laboratorio 11

Abrir la carpeta `start` en Android Studio.
La rama `main` organiza el trabajo por apartados del laboratorio.
Los commits de esta rama se organizaron al preparar esta entrega, sin alterar
sus fechas para simular una cronología de desarrollo. La rama
`historial-original` conserva el historial anterior. El proyecto de trabajo
original no fue modificado.

## Commits por apartado
```
ccb3ac9 build: preparar el proyecto Android y las versiones de Gradle
4cb9c8c feat: preparar la conexión Android con Firebase y documentar proveedores
69e4da4 docs: registrar la creación de Cloud Firestore y la colección de tareas
60b09ea feat: definir reglas de Firestore para proteger tareas por usuario
6fa04a1 feat: vincular la cuenta anónima con correo y contraseña
b9be0a4 feat: actualizar ajustes según el estado de autenticación
a51b816 feat: consultar y mostrar tareas del usuario en tiempo real
4df86f0 feat: medir la vinculación de cuentas con Performance Monitoring
f18ba3e feat: controlar la opción de editar tareas mediante Remote Config
```

Los SDK de Firebase y las trazas `saveTask` y `updateTask` ya formaban parte
del proyecto de inicio. El commit de Performance agrega la traza `linkAccount`;
el de Remote Config agrega la obtención y activación de la configuración y
la traza `fetchConfig`.

Las operaciones de la consola Firebase se documentan en
`CONFIGURACION_FIREBASE.md`; Git no registra su ejecución remota.
El informe y los videos se entregan por separado.

## Archivo local requerido
Copiar el `google-services.json` de tu proyecto Firebase a `start/app/`.
No está incluido en este paquete. Las versiones de Gradle y del plugin Android
se conservaron del proyecto que estás usando actualmente.

## Verificación
La entrega conserva el código Kotlin y los recursos del proyecto de trabajo.
No se volvió a compilar ni a ejecutar durante la reorganización de commits.
La verificación de compilación previa está descrita en `VERIFICACION.md`.
Este repositorio todavía no está publicado en GitHub y no tiene remoto configurado.
