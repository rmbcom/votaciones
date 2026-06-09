# Subasta en tiempo real

Aplicacion web estatica con Firebase Realtime Database.

Archivos:

- `index.html`: app de participantes.
- `subastador.html`: app del subastador.
- `firebase-rules.json`: reglas recomendadas para Realtime Database.

## Enlaces al abrirla

Si subes la carpeta a GitHub Pages:

- Participantes: `https://TU_USUARIO.github.io/TU_REPO/`
- Subastador: `https://TU_USUARIO.github.io/TU_REPO/subastador.html`

## Configuracion de Firebase

La app ya usa la configuracion del proyecto `pulsadorconcurso`:

```js
databaseURL: "https://pulsadorconcurso-default-rtdb.europe-west1.firebasedatabase.app/"
```

Si quieres usar otro proyecto, cambia el bloque `firebaseConfig` en:

- `index.html`
- `subastador.html`

## Crear Firebase desde cero

1. Entra en [Firebase Console](https://console.firebase.google.com/).
2. Crea un proyecto.
3. Entra en **Realtime Database**.
4. Pulsa **Crear base de datos**.
5. Elige una ubicacion cercana, por ejemplo Europa.
6. Para probar rapido, empieza en modo prueba.
7. En **Configuracion del proyecto > Tus apps**, crea una app web.
8. Copia el bloque `firebaseConfig`.
9. Pegalo en `index.html` y `subastador.html`.
10. En **Realtime Database > Reglas**, pega el contenido de `firebase-rules.json` y publica.

## Uso

1. Abre `subastador.html`.
2. Escribe nombre, descripcion, precio inicial y contrasena de acceso.
3. Sube una imagen del articulo.
4. Pulsa **Iniciar subasta**.
5. Abre `index.html` en los dispositivos de los participantes.
6. Cada participante escribe su nombre y la contrasena indicada por el subastador.
7. Los participantes pueden pujar con:
   - `+0,01 EUR`
   - `+0,03 EUR`
   - `+0,05 EUR`
   - `+0,10 EUR`
8. Cada puja reinicia el temporizador a 30 segundos.
9. Si llega a cero, se muestra:

`Adjudicado a [nombre] por [precio]`

## Notas tecnicas

- El precio se guarda internamente como centimos (`currentPriceCents`) para evitar errores con decimales.
- Las pujas usan `runTransaction()` para que dos pujas simultaneas no pisen mal el precio.
- La imagen se guarda como base64 dentro de Firebase. Para clase o pruebas va bien; para uso serio es mejor Firebase Storage o una URL publica de imagen.
- El temporizador se calcula con `endsAt`. Cada cliente lo pinta localmente, pero el valor sale de Firebase.
- La pantalla del subastador o cualquier participante abierto puede marcar la subasta como finalizada si el tiempo llega a cero.
- La contrasena se guarda como `accessCode` en Firebase para filtrar entradas de participantes.

## Limitaciones de seguridad

Esta version prioriza sencillez y uso en aula/evento. No tiene login real ni roles de Firebase Authentication.

Eso significa:

- Cualquiera con el enlace podria abrir `subastador.html`.
- Cualquiera con el enlace podria escribir en la base si las reglas estan abiertas.
- Las reglas incluidas validan formas de datos, pero no distinguen realmente entre subastador y participante.
- La contrasena de acceso no sustituye a Firebase Authentication: evita entradas casuales, pero no es una medida fuerte.

Para una subasta real con dinero de verdad haria falta:

- Firebase Authentication.
- Reglas con roles.
- Backend/Cloud Functions para validar pujas.
- Almacenamiento de imagenes en Firebase Storage.
- Registro de auditoria no editable por clientes.
