# Práctica clase 01: casos del registro de MiniModa con IA

**Sitio:** https://minimoda-navy.vercel.app/registro

> Así tiene que quedar tu entrega. Reemplazá cada `___tu respuesta aquí___` con lo tuyo.

## 1. Preparación
- Navegador y fecha: Google Chrome Versión 156.0.8078.48, 28/10/2026

## 2. Superficie elegida
- Elegí (chat o cowork): Chat (Gemini en Navegador Chrome)
- Por qué: Es más sencillo y práctico porque Gemini ya está disponible en el navegador, mientras que Cowork requiere descarga y configuración previa de accesos.

## 3. Preguntas a Gemini
| # | Pregunta | Respuesta (resumen) | ¿Acierto o error/invento? |
|---|----------|---------------------|---------------------------|
| 1 | ¿Qué campos pide el formulario de registro de https://minimoda-navy.vercel.app/registro? |Responde con los campos que se solicitan: Nombre, Email, Contraseña, Confirmar contraseña, Edad, País, Términos junto con su descripción si la poseen | Acierto |
| 2 | ¿Cuál es el largo mínimo de la contraseña y qué edad se permite? | Responde que la contraseña requiere un mínimo de 8 caracteres y la edad permitida debe ser un número entero entre 13 y 120 años | Acierto |
| 3 | ¿Qué pasa si no acepto los términos? | Responde que al no aceptar, no permitirá avanzar ya que es un campo obligatorio| Acierto parcial |

- Un acierto: En el primer caso, cumple la respuesta detallando cada campo de la solicitud a completar y corresponde a lo del formulario
- Un error o invento: No hubo errores ni inventos, lo más cercano fue que Gemini no menciona que aparezca el mensaje de 'Debés aceptar los términos.' al no tildarlo y presionar el botón de 'Crear cuenta'.

## 4. Primer modo
- Superficie y modo: Gemini en Navegador Chrome - Modo Automático (Modelos de Gemini3)
- Prompt de ejemplo:
  ```
  Sos QA. Vamos a probar el registro de https://minimoda-navy.vercel.app/registro
  Campos: nombre, email, contraseña, confirmar contraseña, edad, país y aceptar términos.
  1. Listá las reglas que se ven, los datos válidos e inválidos y los valores límite.
  2. Escribí 6 casos de prueba con: título, precondiciones, pasos con datos concretos,
     resultado esperado, prioridad (high/medium/low) y tipo (functional/negative/boundary).
  No inventes mensajes: si no sabés el texto exacto, marcalo "A VERIFICAR".
  ```
- Qué devolvió:
Una tabla con reglas visibles, datos válidos, datos inválidos y valores límite para los 7 campos: contraseña de mínimo 8 caracteres y edad entre 13 y 120.
  - 6 casos de prueba: registro exitoso, contraseñas que no coinciden, contraseña de 7 caracteres, edad 12, edad 120 y términos sin aceptar.
  - Cada caso con título, precondiciones, pasos, resultado esperado, prioridad y tipo (functional, negative y boundary).

## 5. Otra superficie: comparación en 3 líneas
Comparación con Claude app (Sonnet 5.5), con acceso web
1. Claude separa "regla visible" de "sin regla visible (A VERIFICAR)" y Gemini solo pone A VERIFICAR en algunos resultados esperados.
2. En datos concretos en los pasos, en Gemini los casos 3, 4, 5 y 6 dicen "completar el resto con datos válidos" y por el otro Claude especifica "completar los datos válidos del TC-01".
3. Claude y Gemini leyeron bien la página. Como cierre, Claude ofrece abrir el navegador y ejecutar los casos y Gemini profundizar en otro escenario de prueba o armar scripts de automatización.

## 6. Mis 3 mejores casos (cargados en Qase, proyecto MiniModa)
Formato del título: `Registro: <qué se prueba>`
Captura de la suite en Qase con tus casos: `evidencias/qase-suite-casos.png`

### Caso 1: Registro: Creación de cuenta exitosa con datos válidos
- Precondiciones: El usuario se encuentra en https://minimoda-navy.vercel.app/registro y el email qa01@example.com no está registrado.
- Pasos:
  1. Ingresar "Ana López" en el campo Nombre.
  2. Seleccionar "Argentina" en el campo País.
  3. Tildar la casilla "Acepto los términos y condiciones".
  4. Ingresar "qa01@example.com" en el campo Email.
  5. Ingresar "Clave12345" en el campo Contraseña.
  6. Ingresar "Clave12345" en el campo Confirmar contraseña.
  7. Ingresar "30" en el campo Edad.
  8. Hacer clic en "Crear cuenta".
- Resultado esperado: El sistema muestra el mensaje de éxito "¡Registro exitoso! Bienvenido/a a MiniModa, Ana López. Te enviamos un email de bienvenida (ver Bandeja)."
- Evidencia: `evidencias/qase-MINIMODA-1-registro-exitoso.png`

### Caso 2: Registro: Validación de contraseña debajo del mínimo (7 caracteres)
- Precondiciones: El usuario se encuentra en la pantalla de https://minimoda-navy.vercel.app/registro
- Pasos:
  1. Ingresar "Ana López" en el campo Nombre.
  2. Seleccionar "Argentina" en el campo País.
  3. Tildar la casilla "Acepto los términos y condiciones".
  4. Ingresar "qa02@example.com" en el campo Email.
  5. Ingresar "Clave12" (7 caracteres) en el campo Contraseña.
  6. Ingresar "Clave12" en el campo Confirmar contraseña.
  7. Ingresar "30" en el campo Edad.
  8. Hacer clic en "Crear cuenta".
- Resultado esperado: El sistema bloquea el registro, no permite avanzar y muestra el mensaje "La contraseña debe tener al menos 8 caracteres."
- Evidencia: `evidencias/qase-MINIMODA-2-registro-password-7.png`

### Caso 3: Registro: Validación del límite inferior de edad (12)
- Precondiciones: El usuario se encuentra en la pantalla de https://minimoda-navy.vercel.app/registro
- Pasos:
  1. Ingresar "Ana López" en el campo Nombre.
  2. Seleccionar "Argentina" en el campo País.
  3. Tildar la casilla "Acepto los términos y condiciones".
  4. Ingresar "qa03@example.com" en el campo Email.
  5. Ingresar "Clave1234" en el campo Contraseña.
  6. Ingresar "Clave1234" en el campo Confirmar contraseña.
  7. Ingresar "12" en el campo Edad.
  8. Hacer clic en "Crear cuenta".
- Resultado esperado: El sistema rechaza el registro debido a la restricción de edad y muestra el mensaje "La edad debe estar entre 13 y 120."
- Evidencia: `evidencias/qase-MINIMODA-3-registro-edad-12.png`

## 7. Mapa del harness
| Pieza | En lo que usé |
|-------|---------------|
| Modelo | ___tu respuesta aquí___ |
| App | ___tu respuesta aquí___ |
| Harness | ___tu respuesta aquí___ |
| MCP | ___tu respuesta aquí___ |
| Skill | ___tu respuesta aquí___ |

## 8. Entrega
- Link de tu repo (pegalo también en el Telegram): ___tu respuesta aquí___
