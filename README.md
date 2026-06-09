# Votacion por rondas en tiempo real

Aplicacion estatica con Firebase Realtime Database para elegir un ranking por rondas.

Archivos:

- `index.html`: vista de participantes.
- `organizador.html`: vista del organizador.
- `firebase-rules.json`: reglas recomendadas para Realtime Database.

## Enlaces al publicarla

Si subes estos archivos a GitHub Pages:

- Participantes: `https://TU_USUARIO.github.io/TU_REPO/`
- Organizador: `https://TU_USUARIO.github.io/TU_REPO/organizador.html`

## Firebase

La app viene conectada al proyecto Firebase usado en otras apps:

```js
databaseURL: "https://pulsadorconcurso-default-rtdb.europe-west1.firebasedatabase.app/"
```

Usa la rama de datos:

```text
voting/current
```

Si quieres usar otro Firebase, cambia el bloque `firebaseConfig` en:

- `index.html`
- `organizador.html`

## Configuracion desde cero

1. Entra en [Firebase Console](https://console.firebase.google.com/).
2. Crea un proyecto o usa uno existente.
3. Activa **Realtime Database**.
4. Elige una ubicacion cercana.
5. En **Reglas**, pega el contenido de `firebase-rules.json`.
6. Publica las reglas.
7. Si usas otro proyecto, copia el bloque `firebaseConfig` de tu app web y pegalo en ambos HTML.

## Uso

1. Abre `organizador.html`.
2. Abre `index.html` en los dispositivos de participantes.
3. Cada participante escribe su nombre y envia solicitud.
4. El organizador acepta o rechaza cada solicitud.
5. Cuando esten todos, pulsa **Empezar**.
6. En cada ronda, cada participante aceptado elige exactamente dos personas.
7. No se puede votar a uno mismo.
8. No se puede votar dos veces a la misma persona.
9. No se puede votar a personas ya elegidas en rondas anteriores.
10. Los ya elegidos siguen pudiendo votar, pero no pueden volver a ser candidatos.
11. El organizador pulsa **Cerrar ronda** para calcular el elegido.
12. Pulsa **Siguiente ronda** para elegir el siguiente puesto.
13. Pulsa **Finalizar** para cerrar la votacion.

## Regla de desempate

En cada ronda gana:

1. Quien reciba mas votos.
2. Si hay empate, quien haya recibido antes su primer voto en esa ronda.
3. Si siguiera el empate, se resuelve por orden alfabetico.

## Finalizacion

La app finaliza cuando:

- el organizador pulsa **Finalizar**;
- o ya no quedan candidatos suficientes para que cada participante pueda elegir dos personas validas.

## Limitaciones de seguridad

Esta version esta pensada para aula, concurso o evento controlado. No usa Firebase Authentication.

Eso significa:

- Cualquiera con el enlace podria abrir `organizador.html`.
- Las reglas validan forma de datos, pero no roles reales.
- Para una votacion formal haria falta autenticacion, roles y reglas mas estrictas.

## Archivos que subir a GitHub

Sube estos tres archivos a la raiz del repositorio:

- `index.html`
- `organizador.html`
- `firebase-rules.json`

`README.md` es opcional, pero recomendable.
