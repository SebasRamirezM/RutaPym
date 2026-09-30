# Feature 1 — Guion del pitch (7 min de demo + 3 min de preguntas)

**Expositor asignado:** _(registrar el nombre antes de iniciar la feature; nadie repite hasta que todos expongan)_

Antes de empezar: `python main.py` encendido, navegador en `http://127.0.0.1:8000` con la red vacía
y una terminal lista para `python pruebas/aceptacion_feature1.py`.

| Minuto | Tema | Qué decir / mostrar |
|--------|------|---------------------|
| 0:00–0:45 | Problema y usuario | RutaPyme decide rutas por intuición y a veces usa conexiones cerradas. Usuario de esta feature: el **coordinador logístico**, que necesita registrar su red. |
| 0:45–2:00 | Modelado | Nodos = puntos con tipo. Aristas = trayectos **dirigidos** (calle de un solo sentido; subir ≠ bajar). Peso = **minutos, > 0**. Mostrar el diagrama de `modelado.md`. |
| 2:00–3:00 | Estructura y complejidad | **Lista de adyacencia** `{punto: {destino: costo}}`. Vecinos en O(grado) vs O(V) en matriz; memoria O(V+E) vs O(V²). La red es dispersa. Registrar punto o conexión: O(1) promedio. |
| 3:00–5:00 | Demo en vivo | 1) Registrar `BOD-CENTRO` y `BAR-NORTE`. 2) Conexión `BOD-CENTRO → BAR-NORTE` (12). 3) Consultar `BAR-NORTE`: **no** tiene salida de regreso. 4) Registrar el regreso con 15. 5) Cargar la red de ejemplo y mostrar la imagen de NetworkX y la lista de adyacencia. |
| 5:00–6:00 | Caso borde | Intentar `BOD-CENTRO → BAR-OESTE` (404, punto inexistente), costo `0` (400) y repetir la conexión (409). Mostrar que la red no cambió. |
| 6:00–7:00 | Evidencia y equipo | Ejecutar el script: **37/37 PASÓ**. Mostrar PRs, commits y la bitácora de IA; explicar qué hizo cada integrante. |

## Preguntas probables y respuesta corta

| Pregunta | Respuesta |
|----------|-----------|
| ¿Por qué no un grafo no dirigido? | Porque A→B no garantiza B→A; el sistema inventaría regresos inexistentes. |
| ¿Por qué no matriz de adyacencia? | La operación principal es pedir vecinos; en matriz cuesta O(V) y gasta O(V²) memoria en una red dispersa. |
| ¿Dónde usan NetworkX? | Solo en `backend/visualizacion.py`, para dibujar la red que ya construyó y validó `red.py`. |
| ¿Qué pasa si el costo es 0 o negativo? | Se rechaza con 400: ningún trayecto tarda 0 min, y la Feature 3 (ruta de menor costo) necesita pesos positivos. |
| ¿Se pueden repetir identificadores? | No; se guardan en mayúsculas, así que `bod-centro` y `BOD-CENTRO` son el mismo punto (409). |
| ¿Se permiten ciclos? | Sí; en una red de calles es normal ir y volver. No es un problema de dependencias. |
| ¿Qué hizo la IA y cómo lo verificaron? | Ver `docs/ia/bitacora-feature-1.md`: cada propuesta con decisión y forma de verificación. |
