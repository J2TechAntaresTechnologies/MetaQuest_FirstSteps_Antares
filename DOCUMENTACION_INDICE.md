# Índice de Documentación y Estructura del Proyecto

Este índice resume la documentación existente y los componentes principales del proyecto, con la ubicación de cada elemento y una breve descripción de su propósito.

## Documentación principal

- `webxr-first-steps/README.md`
  Guía principal del proyecto. Explica el objetivo del tutorial (crear un mini‑juego WebXR con Three.js), requisitos (Node 20+, npm 10+), instalación y ejecución (`npm install`, `npm run dev`), desarrollo con visor (IP/ADB), emulación integrada con IWER/@iwer/devui, índice de capítulos, y despliegue (GitHub Pages o `npm run build`).

- `webxr-first-steps/CONTRIBUTING.md`
  Proceso de contribución: flujo de PRs, CLA, issues, estilo de código con ESLint/Prettier y consejos para VS Code.

- `webxr-first-steps/CODE_OF_CONDUCT.md`
  Código de conducta basado en Contributor Covenant: lenguaje inclusivo, responsabilidades y canal de reporte.

- `webxr-first-steps/LICENSE`
  Licencia MIT.

## Tutorial (capítulos)

- `webxr-first-steps/tutorial/chapter1.md`
  Objetos simples en Three.js. Crea geometrías básicas (suelo, cono, cubo, esfera) y aplica transformaciones (posición/rotación/escala).

- `webxr-first-steps/tutorial/chapter2.md`
  Controladores XR y spawns. Lee entradas con `gamepad-wrapper` y genera balas desde el ray del controlador con posición/orientación correctas.

- `webxr-first-steps/tutorial/chapter3.md`
  Animación de balas. Calcula dirección (forward rotado por quaternion), aplica velocidad, TTL y limpia al expirar.

- `webxr-first-steps/tutorial/chapter4.md`
  Modelos GLTF. Carga estación espacial, bláster y dianas con `GLTFLoader`. Acopla bláster al controlador y usa un “bullet” embebido como prototipo.

- `webxr-first-steps/tutorial/chapter5.md`
  Lógica de juego. Detección de impactos por proximidad, respawn de dianas y marcador con `troika-three-text`.

- `webxr-first-steps/tutorial/chapter6.md`
  Acabado. Audio posicional (disparo/puntuación), hápticos (si disponible) y efectos de escala con GSAP; sincronización del ticker.

## Código fuente (aplicación)

- `webxr-first-steps/src/index.html`
  Página HTML mínima: banner de créditos/licencia y carga `src/index.js` como módulo.

- `webxr-first-steps/src/init.js`
  Bootstrap de la escena Three.js y del runtime XR. Detecta soporte WebXR; si no hay, activa emulación con IWER (`iwer` + `@iwer/devui`). Configura escena, cámara, entorno, renderer con XR, grupo `player`, controladores (ray/grip) y `VRButton`. Expone `init(setupScene, onFrame)` que llama a los callbacks del tutorial.

- `webxr-first-steps/src/index.js`
  Implementación del juego final: constantes de balas, grupo del bláster, dianas, marcador `troika-three-text`, audio posicional (laser/score), hápticos en el gatillo y animaciones con GSAP. Maneja spawn/movimiento/TTL de balas y detección de impactos.

- `webxr-first-steps/src/assets/`
  Recursos utilizados por la escena: modelos GLB (`spacestation.glb`, `blaster.glb`, `target.glb`), fuentes (`SpaceMono-Bold.ttf`) y sonidos (`laser.ogg`, `score.ogg`).

## Infraestructura y tooling

- `webxr-first-steps/package.json`
  Dependencias (`three`, `troika-three-text`, `gsap`, `iwer`, `@iwer/devui`, `gamepad-wrapper`) y `devDependencies` de build (Webpack/Dev Server, ESLint, Prettier). Scripts: `dev` (servidor local), `build` (bundle a `dist`), `format` (Prettier en `src/`).

- `webxr-first-steps/webpack.config.cjs`
  Configuración de Webpack para empaquetar `src/` y servir en desarrollo.

- `webxr-first-steps/eslint.config.cjs`
  Reglas de linting: `eslint:recommended` + `prettier`, `sort-imports`, `no-unused-vars` con patrón de ignore, separación entre miembros de clase.

- `webxr-first-steps/prettier.config.cjs`
  Estilo de formato: LF, tabs, comas finales, `arrowParens: always`, comillas simples.

- `webxr-first-steps/.github/workflows/deploy.yml`
  Workflow para construir y desplegar a GitHub Pages: Node 20.x, `npm install`, `npm run build`, subida de `dist` y publicación.

## Activos del tutorial

- `webxr-first-steps/tutorial/assets/*`
  Imágenes y GIFs ilustrativos de cada capítulo, incluyendo capturas y recursos gráficos.

## Uso rápido

1. Requisitos: Node 20.x+, npm 10.x+
2. Instalar dependencias: `npm install`
3. Desarrollo: `npm run dev` (abre `https://localhost:8081` y acepta el certificado en el visor si es necesario)
4. Emulación (opcional): sin WebXR nativo, IWER se activa automáticamente desde `src/init.js`.
5. Build: `npm run build` (genera `dist/` para hosting estático o GitHub Pages).

## Notas

- Para pruebas en visor por red local, usa la IP del PC y el puerto indicado por `webpack-dev-server`. Si hay advertencia de certificado, confírmalo en el navegador del visor.
- Si usas otras extensiones/emuladores WebXR en el navegador de escritorio, desactívalos para evitar conflictos con IWER.
