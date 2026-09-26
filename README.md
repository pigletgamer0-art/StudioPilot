# StudioPilot 1.2 DEV

Asistente de IA para Roblox Studio. Esta rama contiene la documentación de la nueva versión 1.2 mientras el paquete completo se valida antes de pasar a main.

## Novedades

- Project Brain y grafo local de dependencias.
- Auto-Test Loop con reparación preparada tras un FAIL, sin aplicar cambios a escondidas.
- Visual Diff / UI Autopilot.
- Watchtower, contratos estructurales y checkpoints locales.
- Security + Performance Lab, Device Audit y Release Doctor.
- Equipo de 7 roles, Debate IA, modo Experimento y contexto inteligente.
- Issue Tracker, replays declarativos, documentación y asesor de migraciones.
- Toolbox revisable para Decal, Texture, Sound, ParticleEmitter, PointLight y Highlight.

## Estado real

El motor Python supera 118 pruebas automatizadas en el entorno de desarrollo. El plugin Luau, StudioTestService, StudioCaptureService y la carga de assets todavía deben probarse dentro de Roblox Studio antes de marcar 1.2 como estable.

El Toolbox nunca aplica un asset directamente: genera una propuesta que conserva el preflight, la aprobación y ChangeHistoryService.
