# StudioPilot 1.1 — versión de desarrollo integrada

**Estado:** proyecto conservado y ampliado desde StudioPilot 1.0 RC. Incluye el plugin fuente `StudioPilot.plugin.luau`, el servidor local `server.py`, el nuevo motor `studio_v11.py`, herramientas anteriores (`agent.py`, `visuals.py`, `visual_bridge.py`, `gallery.html`) y pruebas automatizadas. **No está validado aún ejecutándose dentro de Roblox Studio ni con claves comerciales reales.** Consulta `VALIDACION_1_1.md`.

## Instalar y abrir

1. Guarda una copia independiente de tu juego en Roblox Studio (`.rbxl` o `.rbxlx`) y descomprime el ZIP en tu PC. Necesitas Python 3.10+ y Roblox Studio para PC. No es una APK.
2. Configura en PowerShell la clave API del proveedor que elijas **solo en tu PC**, por ejemplo `$env:OPENAI_API_KEY = 'TU_CLAVE'`. También puedes utilizar `ANTHROPIC_API_KEY` o `GEMINI_API_KEY`. Son APIs externas con posibles cuotas/costos; no se incluyen créditos ilimitados.
3. Ejecuta `python server.py` desde la carpeta descomprimida. Copia la **clave temporal local** que muestra el programa (NO es tu clave API). El servidor escucha únicamente en `http://127.0.0.1:8765`.
4. Instala `StudioPilot.plugin.luau` como **plugin local de Roblox Studio**, nunca como Script normal en el juego. Autoriza únicamente la conexión HTTP local a `127.0.0.1:8765`. Abre el panel desde Plugins y pega la clave temporal en «CONEXIÓN PROTEGIDA».
5. Para desbloquear los botones de Play de StudioPilot, instala `luau-compile` oficial en el `PATH` o define `$env:LUAU_COMPILE_BIN` apuntando al ejecutable. El análisis estático no puede demostrar la ausencia de errores de ejecución.
6. Para las referencias visuales abre la galería local `http://127.0.0.1:8765/visual/gallery`, pega la misma clave y añade tus fotos o videos de ejemplo. Las capturas reales del viewport necesitan el permiso correspondiente de Roblox Studio.

## Las seis funciones nuevas (por etapas)

| Etapa | Función | Qué hace realmente en v1.1 |
|---|---|---|
| 1 | **Memoria avanzada** | `VER MEMORIA` y `GUARDAR NOTA` leen/guardan hasta 12 notas de 240 caracteres por ID de proyecto en un JSON privado del PC. No guarda el código del lugar ni permisos para aplicar cambios. Las notas se envían al proveedor **solo si pulsas EQUIPO IA**; revisa qué escribes. Para un lugar sin PlaceId, introduce un ID local único. |
| 2 | **Seguridad y optimización** | `AUDITAR JUEGO` busca heurísticamente credenciales, bucles, referencias a remotos y patrones que podrían afectar el rendimiento; informa la cobertura. No reescribe código ni certifica que el juego sea seguro. |
| 3 | **Constructor visual** | `PREPARAR HUD` ofrece un panel estático de título/estado; `PREPARAR ARENA` ofrece un suelo y cuatro muros. Ambas propuestas son acciones del motor existente, requieren **APLICAR CAMBIOS** después de la revisión y pueden deshacerse por historial. Para construir según fotografías o videos, conserva los botones de captura y galería anteriores. |
| 4 | **Laboratorio de ideas** | `IDEAS NUEVAS` muestra ejemplos para rondas, interfaces o proyectos generales y pruebas recomendadas. Para desarrollar una idea, escríbela en tu objetivo y genera una propuesta. El laboratorio **no** introduce extras por su cuenta. |
| 5 | **Equipo de agentes** | `EQUIPO IA · PLAN` realiza arquitectura, propuesta, crítica del resultado y auditoría local; la generación y revisión usan el modelo que elijas. Configura `STUDIOPILOT_REVIEW_MODEL` para usar **otro** modelo de revisión si tu API lo admite. Si no está configurado, la revisión usa el **mismo** modelo, y el panel no la declara independiente. El número de solicitudes y el costo pueden aumentar. |
| 6 | **Jugador automático limitado** | `PREPARAR BOT` crea una propuesta de `StudioPilot11_TestDriver`, un Script de prueba que **solo** se activa en Studio si la prueba recibe un argumento concreto; puedes dejar la meta vacía (comprobar aparición) o escribir el nombre de una `Part` directa de Workspace (comprobar `Humanoid:MoveTo`). Revisa su código y aplica el lote, instala el compilador, pulsa `REVISAR TODO` y luego `PRUEBA BOT`. El resultado muestra PASS/FAIL solo para ese escenario, no para el juego completo. **Retira el Script de prueba antes de publicar el juego.** |

## Cambios y pruebas: comportamiento seguro

- No se ejecutan archivos Python creados por la IA, no se publican experiencias, no se eliminan ni renombran objetos automáticamente. Se mantiene el contrato allowlist de v1.0. La opción «Extras: SÍ/NO» sigue separada del cambio principal y se requiere `APLICAR CAMBIOS` para ejecutar cualquier lote.
- El preflight calcula una huella del inventario y exige una comprobación reciente antes de iniciar Play. Los scripts nuevos empiezan desactivados y solo se habilitan después de una revisión sintáctica completa con `luau-compile`. El estado completo del juego puede tener elementos que el inventario limitado no detecte.
- **Límites heredados:** hasta 120 scripts, 2.500 objetos, 26.000 caracteres por script, 420 KB de inventario y 24 acciones por propuesta. Una tarea que exceda esos límites debe dividirse y validarse por etapas. El modo profundo consume más consultas de IA; no equivale a trabajo sin límites.
- El resultado de la prueba del bot verifica exclusivamente aparición del personaje o llegada al objetivo; si no hay un resultado reconocible, se indica **sin resultado verificable**. Comprueba también Output del servidor y clientes.
- **Memoria local:** por defecto, los archivos se guardan en `~/.studiopilot_v11`; puedes definir `STUDIOPILOT_DATA_DIR` para cambiar la carpeta. En un PC compartido, protégela. No incluyas claves, secretos ni datos privados en las notas ni en las capturas que envíes a la IA.

## Comprobar el paquete desde la carpeta descomprimida

```powershell
python -m unittest discover -s tests -v
python -m py_compile server.py agent.py visuals.py visual_bridge.py studio_v11.py
```

Consulta `VALIDACION_1_1.md` para ver qué se comprobó aquí y qué queda por realizar en Roblox Studio. `HISTORIAL_v1_0_RC.md` conserva las instrucciones de la versión anterior como referencia.