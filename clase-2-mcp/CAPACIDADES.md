# Capacidades del agente con MCP

## 1. Playwright MCP

**Qué pudo hacer:**
Codex abrió la página de MiniModa, recorrió la tienda, seleccionó un producto (Body Manga Larga Estrellitas), lo agregó al carrito y abrió el carrito con el producto seleccionado. También generó por su cuenta las capturas `01-tienda.png` y `02-carrito.png`. En su respuesta detalló cada paso y la duración de la tarea.

| | Tiempo (estimado) |
|---|---|
| Agente | 55 s (con capturas; el primer recorrido, sin capturas, tardó 42 s) |
| A mano | ~2-3 min |
| Ahorro | ~1-2 min por recorrido |

## 2. Mi MCP «casos-de-prueba»

**Qué pudo hacer:**
Codex creó el caso de prueba con el formato requerido y lo guardó en la carpeta correspondiente (`casos/minimoda-agregar-producto-con-stock-al-carrito.md`). Por su cuenta agregó "minimoda" al inicio del nombre del archivo, aunque no se lo pedí.

| | Tiempo (estimado) |
|---|---|
| Agente | 25 s |
| A mano | ~8-10 min (redactar y guardar el `.md`) |
| Ahorro | ~8 min por caso |

## 3. Límites encontrados

- **Setup:** tuve inconvenientes de acceso y configuración que me demoraron al inicio. Codex no podía resolverlos solo: me ofrecía hacerlo manualmente, indicándome qué agregar y en qué lugar. Después de algunos prompts logré que me dijera concretamente todo lo que faltaba y cómo resolverlo.
- **Sandbox:** Codex no pudo instalar las dependencias ni registrar el servidor por sí solo, porque su entorno no tenía red ni permisos de escritura en la configuración. Esos pasos los hice yo desde la terminal.
- **Supervisión:** tuve que estar atenta a la ejecución para aceptar los accesos que solicitaba Codex, por lo que no es un proceso del todo desatendido.

## 4. Conclusión

El agente con MCP sirve para ejecutar y generar evidencia de flujos repetitivos y habituales. Cuando una pantalla presenta múltiples casos de prueba, ayuda mucho a generarlos y organizarlos. Para una prueba puntual o exploratoria conviene hacerla manualmente, porque el tiempo de configuración y supervisión pesa más que el ahorro.