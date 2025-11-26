# 1. Descripción general del proyecto

MetaQuest_FirstSteps_Antares (repositorio `webxr-first-steps`) es un proyecto educativo y demostrativo centrado en WebXR y Three.js, orientado a visores standalone como Meta Quest. El objetivo principal es ofrecer una demo completa de práctica de tiro en VR, junto con un tutorial por capítulos, documentación técnica y materiales de curso para acelerar la adopción de experiencias inmersivas en contextos industriales.

La aplicación es 100% frontend y se ejecuta en el navegador del visor o del PC mediante WebXR. El foco está en:
- Mostrar una experiencia WebXR lista para usar (target practice con controladores, score, audio y hápticos).
- Servir como base mínima para prototipar POCs industriales (HUD, datos, escenas XR).
- Proveer material de formación estructurado (cursos de distinta duración, slides Reveal.js, tutorial paso a paso).

**Contexto de uso:**
- Visores standalone (Meta Quest, Pico, etc.) en entornos industriales, educativos o comerciales.
- Demos rápidas, pilotos de Industria 4.0 e introducción a WebXR para equipos técnicos y de negocio.

**Stack tecnológico principal:**
- WebXR (API del navegador para VR) con soporte de emulación cuando no hay runtime nativo.
- Three.js como motor 3D principal (escena, cámara, render, controladores, audio, GLTF, etc.).
- Herramientas de soporte: `iwer` y `@iwer/devui` para emulación XR en escritorio, `gamepad-wrapper` para entrada, `troika-three-text` para texto 3D y `gsap` para animaciones.
- Tooling de build: Webpack + Webpack Dev Server (HTTPS), Node.js + npm, ESLint y Prettier.

---

# 2. Estructura del repositorio

La raíz del repositorio `webxr-first-steps` contiene tanto el código de la demo WebXR como la documentación y materiales de curso. Las carpetas más relevantes son:

- `src/`
  - Código fuente principal de la aplicación WebXR (Three.js + WebXR).
  - Contiene el punto de entrada (`index.js`), el bootstrap XR (`init.js`), la plantilla HTML (`index.html`) y los assets 3D/audio (`assets/`).

- `tutorial/`
  - Tutorial por capítulos (markdown) que recorre paso a paso la construcción de la demo, desde objetos simples hasta la experiencia completa con audio y hápticos.
  - Incluye imágenes y GIFs en `tutorial/assets/` que ilustran cada capítulo.

- `Docs/`
  - Documentación conceptual y materiales de soporte:
    - Visión general de WebXR y de Monado/OpenXR.
    - Guía de piloto industrial (Industria 4.0).
    - Tutorial alternativo apoyado en un backend externo (`vrmeta_app`).
    - Slides Reveal.js y recursos gráficos (CSS, logos, imágenes, videos).

- `cursos/`
  - Materiales de tres cursos (2h, 1 semana, 3 semanas) con temarios detallados en markdown y slides HTML asociados.
  - Sirve como base para impartir formación usando el propio repositorio como entorno práctico.

- `.github/workflows/`
  - Workflows de GitHub Actions para build y deploy automático a GitHub Pages.

- `dist/`
  - Carpeta de salida generada por Webpack (`npm run build`) con los archivos estáticos listos para deploy.

- `MetaQuest_FirstSteps_Antares/`
  - Copia interna del mismo proyecto (estructura similar a la raíz: `src/`, `Docs/`, `cursos/`, etc.). En el contexto de este documento, la referencia principal es la raíz `webxr-first-steps`; la carpeta interna se puede considerar como un espejo / proyecto anidado.

**Archivos importantes en la raíz:**
- `README.md`
  - Guía principal en español. Explica objetivo del proyecto, requisitos (Node 20+, npm 10+, Git, visor WebXR), instalación (`npm install`), ejecución (`npm run dev`), acceso desde visor (HTTPS en LAN), y enlaces a documentación.
- `DOCUMENTACION_INDICE.md`
  - Índice detallado de documentación y componentes del proyecto (código, tutorial, tooling, workflow de deploy), con descripciones por archivo.
- `PRESENTACION_PROYECTO.md`
  - Presentación ejecutiva del proyecto: resumen, objetivos, tecnologías, componentes, casos de uso industriales, roadmap y materiales formativos.
- `Indice.md`
  - Resumen del repositorio y listado de documentos clave en `Docs/`, orientado a navegación rápida.
- `CONTRIBUTING.md`
  - Guía de contribución (PRs, estilo de código con ESLint/Prettier, uso de VS Code, etc.).
- `CODE_OF_CONDUCT.md`
  - Código de conducta basado en Contributor Covenant.
- `LICENSE`
  - Licencia MIT.
- `package.json`
  - Definición de dependencias y scripts de build/dev/format.
- `webpack.config.cjs`
  - Configuración de Webpack y del servidor de desarrollo.
- `eslint.config.cjs` y `prettier.config.cjs`
  - Configuración de estilo y reglas de lint/format.

---

# 3. Configuración de build, dev y deploy

## Desarrollo (entorno local)

El flujo de desarrollo está basado en Node.js y Webpack Dev Server:

- Requisitos previos:
  - Node.js 20+ y npm 10+.
  - Git para clonar el repositorio.
  - Un visor con navegador WebXR en la misma red que el PC (para pruebas en dispositivo real).

- Instalación:
  ```bash
  git clone https://github.com/J2TechAntaresTechnologies/MetaQuest_FirstSteps_Antares.git
  cd MetaQuest_FirstSteps_Antares
  npm install
  ```

- Comando de desarrollo:
  ```bash
  npm run dev
  ```

- Configuración de Webpack Dev Server (`webpack.config.cjs`):
  - `host: '0.0.0.0'` → accesible desde la LAN.
  - `server: 'https'` → el servidor utiliza HTTPS (requisito típico para WebXR en producción y en muchos navegadores).
  - `port: 8081` → el dev server escucha en el puerto 8081.
  - `static.directory: 'dist'` → contenido estático servido desde la carpeta de salida.

- Acceso a la app:
  - Desde el PC: `https://localhost:8081`.
  - Desde un visor en la misma red: `https://<IP-DE-TU-PC>:8081` (el visor debe aceptar el certificado auto‑firmado).

- HTTPS y certificados:
  - El README sugiere aceptar el certificado auto‑firmado en el visor.
  - Para entornos más estrictos, se recomienda generar certificados confiables (por ejemplo, mediante `mkcert`) o poner la app detrás de un proxy HTTPS con TLS válido.

## Build (generación de estáticos)

- Script de build:
  ```bash
  npm run build
  ```

- Salida:
  - Webpack genera los archivos estáticos en la carpeta `dist/`:
    - Bundle JS (`index.bundle.js`), HTML generado a partir de `src/index.html`, y copia de assets desde `src/assets`.

- Configuración clave de Webpack:
  - `entry: './src/index.js'` como punto de entrada.
  - `output.path: ./dist` con limpieza (`clean: true`).
  - `HtmlWebpackPlugin` para generar el HTML final.
  - `CopyPlugin` para copiar `src/assets` a `dist/assets`.
  - `ESLintPlugin` integrado en el proceso de build/desarrollo.

## Deploy (GitHub Pages / hosting estático)

- Workflow principal: `.github/workflows/deploy.yml`.
- Disparadores:
  - `push` a la rama `main`.
  - `workflow_dispatch` para ejecuciones manuales.

- Pasos del pipeline:
  - Checkout del repo.
  - Setup de Node.js 20.x.
  - `npm install`.
  - `npm run build`.
  - Upload del artefacto (`./dist`) como contenido de la página.
  - Deploy a GitHub Pages usando `actions/deploy-pages@v4`.

- Patrón de uso previsto:
  - Rama principal (`main`) como fuente de verdad.
  - Cada push a `main` reconstruye y publica el sitio WebXR en GitHub Pages.
  - También es posible tomar la carpeta `dist/` y desplegarla en otro hosting estático con HTTPS.

---

# 4. Arquitectura de la aplicación WebXR

## Punto de entrada y bootstrap XR

- **Punto de entrada principal:** `src/index.js`.
- **Bootstrap WebXR/Three.js:** `src/init.js`.
- **Plantilla HTML:** `src/index.html` (carga el bundle, muestra créditos/licencia y un contenedor mínimo para la app).

### `src/init.js` — Inicialización de escena y XR

Este módulo encapsula la inicialización de Three.js y del runtime XR, y expone una función asíncrona:

```js
export async function init(setupScene = () => {}, onFrame = () => {}) { ... }
```

Responsabilidades principales:
- **Detección de soporte WebXR nativo:**
  - Comprueba `navigator.xr.isSessionSupported('immersive-vr')`.
  - Si no hay soporte nativo, inicializa IWER (`XRDevice`, `metaQuest3`) para emular un dispositivo Meta Quest 3.
  - Configura parámetros del dispositivo emulado (FOV, IPD, posición/quaternions de controladores) y lanza la `DevUI` de `@iwer/devui` para depuración.

- **Creación de escena Three.js:**
  - `Scene` con color de fondo gris.
  - `PerspectiveCamera` con altura típica de usuario (1.6 m) y rango de visión adecuado.
  - `OrbitControls` para navegación con mouse en escritorio (útil para depurar sin visor).

- **Renderer y entorno:**
  - `WebGLRenderer` con antialias, XR habilitado (`renderer.xr.enabled = true`).
  - Resolución ajustada a `window.innerWidth/Height` y `window.devicePixelRatio`.
  - Entorno físico con `RoomEnvironment` y `PMREMGenerator` para iluminación basada en entorno.

- **Player y controladores:**
  - Crea un grupo `player` que contiene la cámara y los espacios de controladores.
  - Configura controladores XR usando `XRControllerModelFactory`:
    - Para cada mano (`left` y `right`), crea `raySpace` (`renderer.xr.getController(i)`) y `gripSpace` (`renderer.xr.getControllerGrip(i)`).
    - Asocia un modelo 3D de controlador a `gripSpace`.
    - Escucha eventos `connected` / `disconnected` en `gripSpace` para registrar o limpiar un objeto `controller` que agrupa:
      - `raySpace`, `gripSpace`, `mesh` y un `GamepadWrapper` con el gamepad XR subyacente.

- **Loop de render:**
  - Gestiona `resize` para mantener el aspect ratio correcto.
  - Crea un `Clock` para obtener `delta` (tiempo entre frames) y `time` (tiempo acumulado).
  - En cada frame (`animate`):
    - Actualiza todos los `GamepadWrapper` de los controladores conectados.
    - Llama a `onFrame(delta, time, globals)` donde `globals` contiene `{ scene, camera, renderer, player, controllers }`.
    - Renderiza la escena (`renderer.render(scene, camera)`).
  - Usa `renderer.setAnimationLoop(animate)` para integrarse con el frame loop XR.

- **Interfaz de usuario VR:**
  - Añade el botón `VRButton` al `document.body` → permite iniciar sesión WebXR (`Enter VR`) en navegadores compatibles.

En resumen, `init.js` es el módulo de “infraestructura XR”: se encarga del entorno 3D, la detección/emulación de XR, la gestión de controladores y el loop de render, delegando la lógica de juego a `setupScene` y `onFrame`.

### `src/index.js` — Lógica del juego WebXR (target practice)

Este módulo implementa la experiencia de práctica de tiro:

Elementos principales:
- **Colecciones y constantes:**
  - `const bullets = {}`: mapa de balas activas en la escena.
  - `const forwardVector = new THREE.Vector3(0, 0, -1)`: vector base de avance (hacia adelante desde el gatillo).
  - `const bulletSpeed = 10`, `const bulletTimeToLive = 1`: parámetros de velocidad y tiempo de vida de las balas.
  - `const blasterGroup = new THREE.Group()`: grupo que contendrá el modelo del bláster, acoplado al controlador.
  - `const targets = []`: arreglo de dianas.

- **Marcador de puntuación:**
  - `let score = 0` y `const scoreText = new Text()` de `troika-three-text`.
  - Configuración de fuente (`SpaceMono-Bold.ttf`), tamaño, color y anclajes.
  - Función `updateScoreDisplay()` que:
    - Limita el score entre 0 y 9999.
    - Lo formatea como número de 4 dígitos con ceros a la izquierda.
    - Actualiza el texto (`scoreText.text`) y llama a `scoreText.sync()`.

- **Audio posicional:**
  - Variables `laserSound` y `scoreSound` definidas a nivel de módulo.
  - Dentro de `setupScene`, se crea un `AudioListener` asociado a la cámara.
  - Con `AudioLoader` se cargan:
    - `laser.ogg` (positional audio agregado al `blasterGroup`).
    - `score.ogg` (positional audio agregado al `scoreText`).

#### `setupScene({ scene, camera, renderer, player, controllers })`

Responsabilidades:
- Carga de modelos GLTF con `GLTFLoader`:
  - `spacestation.glb`: entorno/estación espacial.
  - `blaster.glb`: modelo del bláster, añadido a `blasterGroup`.
  - `target.glb`: modelo de la diana, clonado 3 veces y distribuido en el espacio con posiciones aleatorias (en X e Y/Z) para generar la experiencia de tiro.
- Inserción del texto de score en la escena:
  - Posicionamiento frontal, ligeramente inclinado hacia el jugador.
- Configuración de audio posicional (laser y score) como se describe arriba.

#### `onFrame(delta, time, { scene, camera, renderer, player, controllers })`

Lógica frame a frame:
- **Acople del bláster al controlador:**
  - Si existe `controllers.right` (controlador derecho conectado):
    - Toma `raySpace`, `mesh` y `gamepad`.
    - Si `blasterGroup` aún no es hijo de `raySpace`, lo agrega y oculta el modelo estándar del controlador (`mesh.visible = false`).

- **Disparo (entrada de usuario):**
  - Detecta el clic del gatillo con `gamepad.getButtonClick(XR_BUTTONS.TRIGGER)`.
  - Intenta disparar hápticos con `gamepad.getHapticActuator(0).pulse(0.6, 100)` dentro de un `try/catch` (para tolerar dispositivos sin hápticos).
  - Reproduce el sonido de disparo (`laserSound`), reiniciándolo si ya estaba sonando.
  - Busca un objeto llamado `bullet` dentro del `blasterGroup` (incluido en el modelo GLTF) y lo clona:
    - Añade la bala a la escena.
    - Copia posición y rotación desde el prototipo (`getWorldPosition`, `getWorldQuaternion`).
    - Calcula la dirección de avance aplicando el quaternion de la bala al `forwardVector` y escala por `bulletSpeed`.
    - Guarda en `bullet.userData` su `velocity` y `timeToLive`.
    - Añade la bala al diccionario `bullets` indexada por `uuid`.

- **Actualización de balas:**
  - Itera sobre todas las balas activas:
    - Si `timeToLive < 0`, elimina la bala de la escena y del mapa.
    - Si sigue viva, calcula el desplazamiento `deltaVec = velocity * delta` y actualiza la posición.
    - Decrementa `timeToLive` por `delta`.

- **Detección de impactos con dianas:**
  - Para cada bala viva, recorre las `targets` visibles.
  - Calcula `distance = target.position.distanceTo(bullet.position)`.
  - Si la distancia es menor que un umbral (1 unidad), se considera impacto:
    - Elimina la bala de la escena.
    - Aplica animación de escala con `gsap` para hacer desaparecer la diana (escalado a 0 en 0.3s).
    - Marca la diana como no visible; tras un timeout, la vuelve a mostrar, la reposiciona aleatoriamente en X y Z, y la escala de vuelta a 1 (animación inversa con `gsap`).
    - Incrementa el `score` en 10 puntos, actualiza el marcador con `updateScoreDisplay()` y reproduce el sonido de puntuación (`scoreSound`).

- **Ticker de GSAP:**
  - `gsap.ticker.tick(delta)` se llama al final del frame para integrar el delta de tiempo con las animaciones.

En conjunto, `index.js` implementa un pequeño “engine” de juego sobre el bootstrap XR de `init.js`, construyendo una experiencia de tiro al blanco con feedback visual, sonoro y háptico.

## Especificidad para Meta Quest y otros visores

- El código no está limitado a Meta Quest, pero:
  - Está pensado para visores standalone con compatibilidad WebXR.
  - Usa perfiles de entrada estándar (`XR_BUTTONS`) y gamepads XR.
  - Integra la emulación IWER (`metaQuest3`) para simular un visor Quest 3 en escritorio, lo que facilita el desarrollo sin hardware.
- El acceso desde visor se hace mediante la IP del PC (`https://<IP-DE-TU-PC>:8081`) con HTTPS.

---

# 5. Documentación y materiales de soporte

## Documentos clave en `Docs/`

- `Docs/webxr_overview.md`
  - Visión general de WebXR: definición, capacidades, posibilidades, costes, comunidad y repositorios clave. Incluye buenas prácticas (HTTPS, optimización de glTF, etc.) y una sección “Probarlo con este ecosistema” donde se describe cómo ejecutar este cliente WebXR y, opcionalmente, un backend complementario (`vrmeta_app`).

- `Docs/monado_overview.md`
  - Documento técnico sobre Monado como runtime OpenXR FOSS para Linux: capacidades, dispositivos soportados, repositorios clave y consideraciones prácticas. Está orientado a entornos nativos OpenXR (C++/C#/Rust, motores como Godot/Unreal).

- `Docs/piloto_industria4.md`
  - Guía de plan de piloto VR para Automatización Industrial: objetivos, selección de caso, KPIs, integraciones (telemetría MQTT/OPC‑UA, backend Python), arquitectura recomendada, seguridad/MDM, plan de trabajo 8–10 semanas, roles, costes, riesgos y entregables.

- `Docs/tutorial_webxr_vrmeta.md`
  - Tutorial paso a paso centrado en el proyecto complementario `vrmeta_app` (no incluido en este repo). Describe cómo levantar un backend FastAPI con WebSocket, servir un cliente WebXR y conectar telemetría (incluye mención a MQTT/OPC‑UA mediante `MQTTBridge` y `OPCUABridge`). Importante: deja claro que `vrmeta_app` no forma parte de este repositorio y debe clonarse aparte.

- `Docs/vr_informe_slides.html`
  - Slides Reveal.js del informe VR (presentación en HTML lista para exponer). Utiliza estilos de `Docs/slides.css` y recursos de `Docs/assets`.

- `Docs/vr_informe_slides_test.html`
  - Variante de prueba de las slides.

- `Docs/slides.css`
  - Estilos personalizados para slides Reveal.js (colores, tipografías, branding, etc.).

- `Docs/assets/*`
  - Recursos gráficos para documentación y slides (logos, placeholders, imágenes varias).

- `Docs/videos/*`
  - Colección de videos relacionados con el proyecto/cursos (intros, demos, etc.). No son necesarios para entender el código, pero aportan material audiovisual de soporte.

## Presentaciones y contexto de proyecto

- `PRESENTACION_PROYECTO.md`
  - Documento de presentación ejecutiva con resumen del proyecto, objetivos, tecnologías, componentes, demo incluida, casos de uso industriales, seguridad/MDM, roadmap, formación, métricas y contribución.

- `Indice.md`
  - Índice resumido que referencia los documentos clave en `Docs/` y `DOCUMENTACION_INDICE.md`.

## Materiales de cursos (`cursos/`)

- `cursos/Indice.md`
  - Índice de cursos. Resume los tres cursos y sus objetivos:
    - Curso 1: Panorama WebXR e Industria (2h).
    - Curso 2: Fundamentos WebXR con Three.js (1 semana).
    - Curso 3: Proyecto WebXR Industrial (3 semanas).
  - Incluye temas clave (ecosistema XR, WebXR vs OpenXR, Three.js, interacción XR, assets, rendimiento, despliegue, gobernanza).

- `cursos/curso_1.md`
  - Temario del **Curso 1 – Panorama WebXR e Industria**. Nivel introductorio, sin foco en código. Cubre conceptos XR, capacidades de hardware, casos de uso industriales, seguridad/gobernanza y despliegue. Incluye actividades de demostración con la propia demo del repositorio.

- `cursos/curso_2.md`
  - Temario del **Curso 2 – Fundamentos WebXR con Three.js**. Programa intensivo de 1 semana orientado a desarrolladores. Recorrido desde setup y emulación hasta interacción, assets, audio, colisiones y deploy. Se apoya en el código de `src/index.js` e `init.js`.

- `cursos/curso_3.md`
  - Temario del **Curso 3 – Proyecto WebXR Industrial (end‑to‑end)**. Programa de 3 semanas para construir un POC industrial completo, integrando datos, UX, performance y despliegue.

- `cursos/curso_1_sliders.html`, `curso_2_sliders.html`, `curso_3_sliders.html`
  - Slides HTML para cada curso, listas para usar en formación.

En conjunto, los documentos y cursos complementan la app WebXR ofreciendo contexto conceptual, guías prácticas y materiales docentes.

---

# 6. Estándares de código y convenciones

El proyecto utiliza ESLint y Prettier para estandarizar el estilo de código JavaScript.

## Herramientas de estilo

- `eslint.config.cjs`:
  - Entorno: `browser: true`, `es2021: true`.
  - Extiende `eslint:recommended` y `prettier` (ESLint delega formateo a Prettier).
  - Reglas relevantes:
    - `sort-imports`: obliga a ordenar imports de forma consistente.
    - `no-unused-vars`: marca variables y argumentos no usados (permite ignorar argumentos con prefijo `_`).
    - `lines-between-class-members`: fuerza líneas en blanco entre miembros de clase.

- `prettier.config.cjs`:
  - `endOfLine: 'lf'` (saltos de línea estilo Unix).
  - `useTabs: true` (usa tabs en lugar de espacios).
  - `trailingComma: 'all'` (comas finales donde sea posible).
  - `arrowParens: 'always'`.
  - `singleQuote: true` para cadenas en JS.

- Scripts en `package.json`:
  - `npm run format` → `prettier --write ./src/**/*` (formatea el código fuente de `src/`).

## Organización y patrones de código

A partir del código existente se puede inferir:
- Uso de **módulos ES** (`import`/`export`) y estructura modular sencilla:
  - `init.js` expone `init` como bootstrap genérico.
  - `index.js` importa `init` y define callbacks de escena/loop.
- Estilo de imports:
  - Primero imports de librerías externas (Three.js, GSAP, troika, gamepad-wrapper, iwer).
  - Luego imports relativos (`./init.js`).
  - Los imports están ordenados y agrupados, en línea con `sort-imports`.
- Paradigma:
  - Basado en funciones y objetos de Three.js; no usa clases propias complejas.
  - Lógica de juego expresada con estructuras simples (`const`, `let`, arrays, mapas) y un loop explícito (`onFrame`).
- Convención XR:
  - `controllers.left` / `controllers.right` almacenan estado de cada mano.
  - `player` contiene cámara y controladores; la escena 3D se organiza alrededor de este grupo.

No se observan convenciones estrictas adicionales (por ejemplo, arquitectura Redux o similar); el diseño se mantiene intencionalmente simple para fines educativos.

---

# 7. Integración con entornos industriales (si aplica)

El código de este repositorio es puramente frontend y no incluye integraciones directas con sistemas industriales, pero la documentación describe claramente la orientación y posibles integraciones.

## Integraciones descritas en la documentación

- `Docs/piloto_industria4.md` y `PRESENTACION_PROYECTO.md` mencionan:
  - **MQTT u OPC‑UA** como canales de telemetría industrial (lectura/escritura) para conectar con SCADA/MES/PLCs.
  - **Backends en Python** (por ejemplo, FastAPI + WebSocket) como base para servicios de datos.
  - Integración con sistemas de planta, KPIs operativos (OEE, MTTR, etc.) y dashboards XR.

- `Docs/tutorial_webxr_vrmeta.md` presenta un proyecto complementario (`vrmeta_app`) que **no forma parte de este repo**, pero que ejemplifica:
  - Un backend FastAPI con WebSocket para mensajería en tiempo real (`/ws`).
  - Un cliente WebXR simple servido desde el backend.
  - Extensiones avanzadas con `MQTTBridge` y `OPCUABridge` para conectar con MQTT y OPC‑UA, reenviando eventos hacia clientes WebXR.

En este repositorio:
- No hay código de conexión directa a OPC‑UA, MQTT o REST.
- La app WebXR está pensada como cliente estático que podría consumir APIs externas vía WebSocket/REST.

Por lo tanto, la **integración industrial** está actualmente en estado de **planificación / ejemplo conceptual**, pero hay rutas claras para:
- Extender el cliente WebXR para consumir datos en tiempo real (KPIs, alarmas, estados de máquina) desde un backend como `vrmeta_app`.
- Usar WebXR como front-end de gemelos digitales y paneles 3D basados en datos de planta.

Cualquier integración concreta deberá implementarse en un proyecto de backend separado (por ejemplo, `vrmeta_app`) y enlazarse desde el cliente WebXR mediante HTTP/WS/REST, tal como sugiere la documentación.

---

# 8. Notas para otras IAs

Este documento (`Docs/AI_CONTEXT_WEBXR.md`) fue generado leyendo el contenido real del repositorio local `webxr-first-steps` (MetaQuest_FirstSteps_Antares). Está diseñado para que otra IA, sin acceso al código fuente, pueda entender la estructura, objetivos y arquitectura del proyecto.

Si en el futuro otro agente vuelve a tener acceso al código, los archivos más importantes a consultar son:
- `src/index.js` → lógica del juego WebXR (disparos, targets, score, audio, hápticos).
- `src/init.js` → bootstrap XR (Three.js + WebXR + IWER, controladores y loop de render).
- `src/index.html` → estructura HTML base y carga del bundle JS.
- `Docs/webxr_overview.md` → contexto técnico de WebXR y ecosistema.
- `Docs/piloto_industria4.md` → guía de piloto industrial y posibles integraciones.
- `Docs/tutorial_webxr_vrmeta.md` → tutorial alternativo con backend complementario (`vrmeta_app`).
- `tutorial/*.md` → explicación paso a paso del código y del diseño de la demo.
- `cursos/*.md` e `Indice.md` → programas de cursos y cómo usar el repo en formación.
- `README.md`, `DOCUMENTACION_INDICE.md` y `PRESENTACION_PROYECTO.md` → visión global, índice de documentación y presentación ejecutiva.

Otras IAs deberían tomar este documento como guía de alto nivel y, si tienen acceso al repo, usar los archivos listados para profundizar en:
- La arquitectura WebXR/Three.js.
- El flujo de build/dev/deploy.
- La alineación con casos de uso industriales y rutas de integración futuras.

