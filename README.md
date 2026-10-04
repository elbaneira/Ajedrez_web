
### 🕹️ Proyecto Destacado / Easter Egg   

#### ♟️ [Ajedrez Cyberpunk (2 Jugadores)](https://elbaneira.github.io/Ajedrez_web/)
Un juego de ajedrez interactivo diseñado con estética neón / cyberpunk. Permite partidas locales para dos jugadores con validación de movimientos y un diseño moderno e interactivo  en un único `index.html`, con estética Dark Sci-Fi / neón y lógica completa de reglas..

* **Demo en vivo:** [Ver Ajedrez Cyberpunk ↗](https://elbaneira.github.io/Ajedrez_web/)

---

Abrir `index.html` directo en el navegador. Sin servidor, sin build.

---

## Arquitectura

Un solo archivo, tres capas separadas:

- **HTML**: contenedor, panel de estado (`#infoPanel` / `#status-text`), tablero (`#myBoard`), botón (`#newGameBtn`), overlay `GAME OVER`, canvas `#particles`.
- **CSS**: tema cyberpunk (fondo `#050510` + cian `#00f0ff` / verde `#39ff14` / púrpura `#bf00ff` / rojo `#ff073a`), casillas con degradado metálico, glow neón, animaciones `@keyframes` (scan, flicker, pulse-neon, checkBlink, kingShake, flashOut, burst, loadShine, btnPulse, glitch, buildBlocks).
- **JS**: Vanilla JS + CDN:
  - `jQuery 3.5.1` (requerido por chessboard.js)
  - `chess.js 0.10.3` — reglas, validación, jaque/mate/tablas, FEN
  - `chessboard.js 1.0.0` — render + drag and drop (`moveSpeed: 'slow'`)
  - `pieceTheme` Wikipedia + filtros CSS neón (compatibilidad total con drag and drop)

## Funciones JS

| Función | Qué hace |
|---|---|
| `onDragStart(source, piece)` | Bloquea arrastre si terminó la partida o si la pieza no es del turno. Marca la casilla origen con `.selected`. |
| `onDrop(source, target)` | Valida con `game.move({from, to, promotion:'q'})`. Ilegal → `'snapback'`. Captura → `captureEffect(target)` + sonido grave; normal → blip. Llama `updateStatus()`. |
| `onSnapEnd()` | Sincroniza vista con `board.position(game.fen())` (enroque, paso, coronación). |
| `updateStatus()` | Turno Blancas/Negras, Jaque (panel `.check` + rey con `.king-in-check`), Mate (overlay `GAME OVER` glitch), Tablas (ahogado, repetición triple, material insuficiente → overlay `DRAW`). |
| `startNewGame()` | `game.reset()` + `board.start()` + limpia overlay/marcas + sonido. |
| `squareEl(sq)` | Localiza la casilla del DOM (`.square-e4` o `[data-square]`). |
| `findKing(color)` | Recorre `game.board()` para ubicar el rey del turno (temblor en jaque). |
| `captureEffect(sq)` | Flash radial + 14 partículas + blip. |
| `playBlip(freq)` | Sonido WebAudio (oscilador square, sin archivos). |
| Bucle partículas | 65 partículas cian/púrpura/verde flotando en `#particles` vía `requestAnimationFrame`. |

## Efectos visuales

- Hover en casilla: glow verde neón.
- Selección: pulso neón cian constante.
- Movimiento: slide suave (`moveSpeed: 'slow'` + transición CSS).
- Captura: explosión de partículas + flash.
- Panel: fuente mono tech con escaneado y parpadeo; en jaque parpadea en rojo.
- Fin: texto glitch `GAME OVER` / `DRAW` con bloques de luz.
- Botón: shine de carga en hover, pulso al presionar, sonido al clic.

## Uso

1. Blancas mueven primero, arrastrar y soltar.
2. Coronación automática a Reina.
3. `Nueva Partida` reinicia lógica y vista.
4. Clic en el overlay de fin lo oculta.

## Estructura del repo

- `index.html` — juego completo.
- `Ajedrez.bat` — lanzador local.
- `GIT_RULES.md` — reglas Git del proyecto.
- `README.md` — este archivo.
