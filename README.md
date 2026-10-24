# Worksheet Studio

Fichas de práctica de tiempos verbales en inglés para clases individuales con adultos.
Funciona en el celular y en el computador.

**Abrir la app:** https://cvargas-bubba.github.io/worksheet-studio/

## Qué hace

- **Alumnos (sin cuenta):** abren el link y practican. Escriben la respuesta y la revisan,
  marcan alternativas o usan el modo clase, que muestra una pregunta grande por vez.
- **Banco de fichas:** 12 fichas listas de present simple y continuous, past simple y continuous,
  present perfect (simple y continuous), past perfect, futuro, used to / would y repasos mixtos.
- **Profesora (con correo y contraseña):**
  - Crea fichas nuevas con una IA gratuita: la app copia las instrucciones, la profesora las
    pega en ChatGPT, Claude o Gemini, y después pega la respuesta en la app.
  - Guarda las fichas en la biblioteca, donde las ven todos los alumnos.
  - Ve el solucionario y copia el link de cada ficha para enviarlo.

## Cuenta y datos

La profesora ingresa con **Firebase Authentication** (correo y contraseña). Las fichas se guardan
en **Cloud Firestore**, en la colección `fichas`. Cualquiera puede leerlas, pero solo la
profesora puede guardar o borrar.

La configuración de Firebase que aparece en `index.html` no es secreta: identifica al proyecto,
y el acceso a los datos lo controlan las reglas. Este repositorio no contiene datos personales.

Reglas de Firestore (`firestore.rules`):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /fichas/{id} {
      allow read: if true;
      allow write: if request.auth != null
        && request.auth.token.email == "CORREO_DE_LA_PROFESORA";
    }
  }
}
```
