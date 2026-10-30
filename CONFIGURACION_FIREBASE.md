# Configuración del laboratorio en Firebase

## Punto 2: registrar la aplicación
Registrar Android con el paquete `com.example.makeitso` en el proyecto Firebase.
Descargar el archivo `google-services.json` y colocarlo en `start/app/`.
El archivo de configuración se mantiene local y no se incluye en Git.
Habilitar los proveedores Correo electrónico/contraseña y Anónimo en Authentication.
Estas acciones se realizan en la consola y no se aplican automáticamente al clonar.

## Punto 3: crear Cloud Firestore
Crear la base de datos en modo de producción y seleccionar su ubicación.
Las tareas se almacenan como documentos de la colección `tasks`.
Cada documento contiene el campo `userId` del propietario autenticado.
