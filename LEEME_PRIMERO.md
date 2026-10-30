# Laboratorio 11 Firebase

Solución de código basada en el repositorio del docente: https://github.com/BparejaTec/Lab11_Start. Se conservan los avisos de licencia del código original. Los commits nuevos corresponden a los cambios realizados con ayuda de IA.

## Qué incluye

- Vinculación de la cuenta anónima con correo y contraseña, conservando el UID y sus tareas.
- Navegación al terminar el registro y actualización reactiva de Settings.
- Lectura de tareas por usuario mediante Firestore, Flow y collectAsStateWithLifecycle.
- Opciones de editar, marcar y eliminar tareas conectadas a la pantalla.
- Reglas que validan el propietario al crear y evitan cambiarlo al actualizar.
- Remote Config y traza de vinculación como avance adicional. Esto no acredita los puntos adicionales hasta probar y grabar la app.
- Historial Git con commits por avance, conservando los commits originales del docente.

## 1 Crear tu proyecto de Firebase

1. Entra con tu cuenta en https://console.firebase.google.com/ y crea un proyecto llamado, por ejemplo, Laboratorio11Firebase.
2. Habilita Google Analytics según lo solicitado por la guía y completa la creación.
3. Añade una aplicación Android. El paquete debe ser exactamente `com.example.makeitso`.
4. Descarga `google-services.json` y colócalo dentro de `start/app/`. No se necesita SHA para los proveedores de este laboratorio.
5. En Authentication > Sign-in method habilita **Email/Password** y **Anonymous**.
6. Esta solución conserva Firebase BoM 32.5.0 del proyecto docente. Para reproducir el flujo antiguo de vinculación, sigue la indicación de la guía sobre desactivar la protección de enumeración de correo en Authentication > Settings. Limita esa configuración al proyecto de práctica; antes de usarlo en producción, actualiza el SDK y revisa la protección con la documentación oficial.
7. En Firestore Database crea la base `(default)`, de edición Standard, en modo producción. Selecciona una región disponible apropiada.
8. En Rules reemplaza el contenido por `firestore.rules` de este repositorio y pulsa Publish. No dejes reglas abiertas.
9. No necesitas crear manualmente `tasks`: el primer guardado crea la colección.
10. Para Remote Config puedes crear el parámetro booleano `show_task_edit_button` con valor `true` y publicar. Hay un valor predeterminado local en `remote_config_defaults.xml`.

## 2 Abrir y ejecutar

1. En Android Studio abre la carpeta **start**, donde está `settings.gradle.kts`.
2. En Settings > Build, Execution, Deployment > Build Tools > Gradle selecciona **JDK 17**. En esta computadora existe `C:\Users\ASUS\.jdks\jbr-17.0.14`. El JBR 25 del Android Studio instalado no es compatible con Gradle 8.9.
3. Sincroniza Gradle. La configuración utiliza AGP 8.7.3, Gradle 8.9, Kotlin 1.9.0 y Compose Compiler 1.5.0. No cambies solo una de esas versiones sin revisar compatibilidad.
4. Selecciona la variante **devDebug** en Build Variants.
5. En Device Manager inicia un emulador con Google APIs/Google Play o conecta un teléfono con depuración USB. Ejecuta `app`.
6. Si falta Android SDK 34, instálalo desde SDK Manager.

Desde PowerShell, dentro de `start`, con JAVA_HOME apuntando al JDK 17 y el SDK configurado:

```powershell
.\gradlew.bat :app:assembleDevDebug
```

El APK se genera en `start/app/build/outputs/apk/dev/debug/`. La configuración real de Firebase es necesaria para ejecutar correctamente la app. No omitas `processDevDebugGoogleServices`: otras tareas dependen de sus recursos. Para revisar el código antes de disponer del archivo se utiliza una copia temporal sin el plugin Google Services; esa comprobación no demuestra conexión con Firebase y no sustituye la compilación del proyecto completo.

## 3 Comprobar la parte guiada y el ejercicio

1. Abre la app: se crea una cuenta anónima. En Authentication > Users comprueba que aparezca.
2. Pulsa + y crea una tarea, por ejemplo `Entregar laboratorio 11`. Comprueba en Firestore que tenga `userId` igual al UID de esa cuenta.
3. En Settings > Create account introduce un correo tuyo y una contraseña que cumpla la validación de la app. No muestres la contraseña en el video.
4. Comprueba que Settings muestre Sign out y Delete your account. Verifica en Authentication que el UID se conserve y el proveedor ya sea correo/contraseña.
5. Vuelve a tareas: la tarea creada antes del registro debe continuar disponible.
6. Edita la tarea, cambia el estado de completado y elimina una tarea de prueba mediante el menú.
7. Cambia el título de una tarea desde Firestore: con la app abierta y conectada debe actualizarse sin recargar manualmente.
8. Si tienes dos dispositivos, entra con la misma cuenta y comprueba sincronización. Con otra cuenta, la lista debe mostrar solo las tareas de ese otro usuario.
9. Para comprobar reglas usa Rules Playground: acceso sin autenticar denegado; propietario permitido; otro UID denegado; crear con `userId` ajeno y cambiar propietario denegados. No afirmes que estas pruebas pasaron antes de ejecutarlas.

## 4 Repositorio personal y commits

El repositorio local ya tiene commits reales por avance. Aún no está publicado en tu cuenta. Crea un repositorio vacío en GitHub, sin README ni licencia añadida, y desde esta carpeta ejecuta lo siguiente sustituyendo TU_USUARIO:

```powershell
git remote rename origin docente
git remote add origin https://github.com/TU_USUARIO/Laboratorio11-Firebase.git
git push -u origin main
git log --oneline -8
```

Si vuelves a ejecutar esos comandos, revisa primero `git remote -v` porque el cambio de nombre se hace una sola vez. No hagas push al repositorio del profesor. `google-services.json` está excluido de Git; cada persona debe conectar su propio proyecto. Después de añadir el informe y evidencias, crea otro commit descriptivo y haz push.

## 5 Guion para el video de 2 a 3 minutos

- Presentación: nombre, laboratorio, Kotlin, Compose y Firebase.
- Muestra una tarea anónima y su documento en Firestore.
- Registra la cuenta sin mostrar la contraseña. Explica que `linkWithCredential` conserva el UID.
- Muestra el cambio de opciones de Settings y que la tarea se conserva.
- Crea, edita, completa y elimina una tarea de prueba.
- Cambia un título en Firestore y muestra la actualización en la app.
- Enseña el historial de commits del repositorio personal y menciona el uso de IA.

Graba desde los controles extendidos del emulador en Record and Playback, si tu versión lo permite, o desde la grabadora del teléfono. Adjunta el video solicitado y pega el enlace en el informe. No se incluye un video simulado.

## Problemas frecuentes

- `google-services.json is missing`: el archivo debe ir en `start/app`, no en la raíz del repositorio.
- `No matching client found`: registraste un paquete distinto de `com.example.makeitso`.
- Error `25.0.4` al arrancar Gradle: selecciona JDK 17.
- `OPERATION_NOT_ALLOWED`: revisa ambos proveedores de Authentication.
- `PERMISSION_DENIED`: publica las reglas y comprueba el UID, el nombre `tasks` y el campo `userId`.
- La pantalla no lista tareas: comprueba que estás usando la misma cuenta y que el usuario tiene conexión; consulta Logcat para errores del listener.
- No se puede eliminar la cuenta por inicio de sesión antiguo: vuelve a iniciar sesión antes de eliminarla.
- Eliminar una cuenta de Authentication no elimina automáticamente sus documentos de Firestore; esta versión conserva ese comportamiento de la base docente.

## Fuentes

- Guía GLAB S11 proporcionada por el estudiante.
- Repositorio del docente: https://github.com/BparejaTec/Lab11_Start
- Codelab oficial: https://firebase.google.com/codelabs/build-android-app-with-firebase-compose
- Vinculación de cuentas: https://firebase.google.com/docs/auth/android/anonymous-auth
- Condiciones de reglas: https://firebase.google.com/docs/firestore/security/rules-conditions
- Protección de enumeración: https://docs.cloud.google.com/identity-platform/docs/admin/email-enumeration-protection
