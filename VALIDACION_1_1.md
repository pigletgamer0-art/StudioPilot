# Validación de StudioPilot 1.1

## Comprobaciones que pueden realizarse en este entorno

- Ejecutar todos los tests unitarios existentes y nuevos de Python, incluyendo HTTP local autenticado, propuestas de HUD/arena, memoria local, separación de proyectos, rechazo de credenciales evidentes, auditoría heurística, contrato del equipo de agentes y generación del script de prueba. **No se hace una llamada comercial de IA durante estos tests.**
- Comprobar sintaxis de los archivos Python y del JavaScript de la galería (`node --check gallery.js` si se extrae de HTML). Comprobar integridad del ZIP de distribución.
- Revisar que los nuevos botones llaman a rutas permitidas del servidor y que el motor de v1.0 aún exige aprobación antes de aplicar acciones.

## Pruebas pendientes que **sí** requieren Roblox Studio

1. Instalar el plugin como plugin local; verificar que abre el panel, conecta al servidor con la clave temporal y conserva las funciones de v1.0.
2. Compilar `StudioPilot.plugin.luau` y el script Luau generado para el bot. **No se dispone de compilador Luau ni de Roblox Studio en el entorno de creación del paquete**. Los tests Python no sustituyen esas comprobaciones.
3. En un lugar de pruebas con respaldo: preparar un HUD y una arena, comparar antes/después, comprobar propiedades en móvil, probar Undo y que las otras funciones del lugar sigan intactas.
4. Crear y aplicar el controlador del bot, ejecutar `REVISAR TODO` y probar `PRUEBA BOT` primero sin meta y después con una Part directa de Workspace. Comprobar si la prueba devuelve `StudioPilot11:PASS:` o `StudioPilot11:FAIL:`, el tiempo límite y los registros reales de Output. **No publicar el controlador del bot como componente permanente.**
5. Usar claves de API reales en cuentas autorizadas para validar cada proveedor/modelo disponible, el modo de equipo, los costos y la revisión independiente cuando exista.
6. Confirmar autorización de capturas reales, referencias de fotos/video, diagnósticos, reparación y test de dos jugadores tras instalar el nuevo plugin, sin dar por válidas pruebas del servidor Python como tests funcionales del juego.

**Clasificación actual:** v1.1 de desarrollo integrada. No hay evidencia suficiente para declararla 1.1 estable, «100% autónoma», universalmente compatible ni capaz de demostrar que todos los errores del juego fueron corregidos.