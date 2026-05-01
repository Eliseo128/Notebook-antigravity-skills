Viewed usuario_model.dart:49-69
Ran command: `flutter pub get`
Ran command: `Get-ChildItem lib\*.dart`
Viewed main.dart:1-26

¡Exacto! Ya puedes ejecutar la aplicación directamente. He preparado todo (dependencias, configuración de Firebase y corrección de errores) para que funcione a la primera.

Para ejecutarla, abre una terminal en la carpeta de tu proyecto (`c:\antigravityproyecto\navacontroescolar`) y usa cualquiera de estos comandos dependiendo de dónde quieras probarla:

### 1. En el Navegador (Web) - La opción más rápida para probar el layout:
```powershell
flutter run -d chrome
```

### 2. En Windows (Escritorio):
```powershell
flutter run -d windows
```

### 3. En Android (Emulator o Dispositivo físico):
```powershell
flutter run
```

---

### 💡 Notas antes de iniciar:
1.  **Google Sign-In:** Recuerda que para que el inicio de sesión con Google funcione en **Android**, deberás agregar la huella SHA-1 de tu máquina en la consola de Firebase más adelante si aún no lo has hecho. En **Web**, debería funcionar tras configurar el dominio autorizado.
2.  **Firestore:** Asegúrate de que las reglas de tu base de datos en Firebase Console permitan la lectura/escritura (puedes usar "modo prueba" para desarrollo inicial).

**¿Quieres que te ayude con algo más o prefieres probar la app ahora mismo?**
Notas antes de iniciar:
Google Sign-In: Recuerda que para que el inicio de sesión con Google funcione en Android, deberás agregar la huella SHA-1 de tu máquina en la consola de Firebase más adelante si aún no lo has hecho. En Web, debería funcionar tras configurar el dominio autorizado.
Firestore: Asegúrate de que las reglas de tu base de datos en Firebase Console permitan la lectura/escritura (puedes usar "modo prueba" para desarrollo inicial).
#### pasos a seguir
¡Claro! Este es un paso fundamental para que Google reconozca tu aplicación Android como segura y permita que los usuarios inicien sesión.

Aquí tienes la guía paso a paso:

### Paso 1: Obtener tu huella SHA-1 (Desde tu computadora)

La forma más sencilla en Flutter es usar el comando de Gradle que genera un reporte de firmas.

1.  Abre una terminal en la raíz de tu proyecto.
2.  Ejecuta el siguiente comando (si estás en Windows):
    ```powershell
    cd android
    ./gradlew signingReport
    ```
3.  Espera a que termine. Busca en la salida de texto la sección llamada `Variant: debug` (o `task :android:signingReport`).
4.  Copia el código que aparece al lado de **SHA1**. Se ve algo como esto:
    `5E:8F:16:06:2E:A3:CD:2C:4A:0D:54:74:68:A4:71:32:00:00:00:00`

---

### Paso 2: Agregar la huella en la Consola de Firebase

1.  Entra a la [Consola de Firebase](https://console.firebase.google.com/).
2.  Selecciona tu proyecto: **controlescolarcbtis128-997d4**.
3.  Haz clic en el icono de engranaje (⚙️) junto a "Project Overview" y selecciona **Configuración del proyecto**.
4.  Baja hasta la sección **Tus apps** y asegúrate de seleccionar la pestaña de **Android** (`com.cbtis128.nava_control_escolar`).
5.  Busca el botón que dice **Agregar huella digital**.
6.  Pega el código **SHA1** que copiaste en el Paso 1 y haz clic en **Guardar**.

---

### Paso 3: Actualizar la configuración en tu proyecto

Una vez agregada la huella en la consola, la configuración de Firebase ha cambiado. Debes actualizarla en tu código local:

1.  Regresa a tu terminal en la raíz del proyecto.
2.  Vuelve a ejecutar el comando de configuración:
    ```powershell
    flutterfire configure --project=controlescolarcbtis128-997d4 --platforms=android,web,windows --android-package-name=com.cbtis128.nava_control_escolar --yes
    ```
    *Esto descargará automáticamente el nuevo archivo `google-services.json` que ya contiene la información de la firma.*

---

### Paso 4: (Opcional pero recomendado) SHA-256
Te recomiendo repetir el **Paso 2** pero copiando también la huella **SHA-256** que aparece en el mismo reporte de Gradle. Esto es necesario para funciones avanzadas como el "Enlace de cuentas" o la verificación por SMS de Firebase Auth.

**¡Listo!** Con esto, el botón de "Iniciar sesión con Google" ya no debería dar error en Android y te permitirá seleccionar tu cuenta de Google correctamente.

¿Pudiste obtener el código SHA1 con el comando de Gradle?
