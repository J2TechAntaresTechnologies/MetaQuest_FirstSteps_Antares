# Presentación del Proyecto – WebXR First Steps

## Resumen ejecutivo
WebXR First Steps es un proyecto educativo y demostrativo que acelera la adopción de experiencias inmersivas en la web (VR/MR) usando Three.js y el estándar WebXR. Incluye una demo interactiva, tutorial por capítulos, material de cursos y guías de despliegue, facilitando tanto la difusión y capacitación como la exploración de casos de uso industriales.

- Demo/juego WebXR: target practice con controladores, sonido, haptics y detección de impactos.
- Emulación integrada: IWER + DevUI para desarrollar y probar sin visor físico.
- Formación estructurada: tres cursos (2h, 1 semana, 3 semanas) con slides.
- Despliegue sencillo: Webpack + GitHub Pages u hosting propio.

## Objetivos
- Presentar y difundir el potencial de WebXR en contextos industriales y comerciales.
- Capacitar equipos técnicos y no técnicos mediante tutoriales y cursos guiados.
- Proveer una base de código mínima pero completa para prototipado rápido.
- Trazar una hoja de ruta de evolución hacia POCs y productos XR robustos.

## ¿Qué es WebXR y por qué ahora?
WebXR es el estándar web para experiencias inmersivas (VR/MR/AR) directamente en el navegador, sin instalar apps nativas. Permite:
- Prototipar y distribuir con rapidez (URLs, CI/CD, control de versiones).
- Integrarse con ecosistema web (APIs, seguridad, redes, analítica).
- Usar hardware moderno (p. ej., Meta Quest 3) con buen tracking y passthrough.

Referencias: `Docs/webxr_overview.md` y `Docs/monado_overview.md`.

## Tecnologías empleadas
- Three.js (render 3D) y addons (GLTFLoader, VRButton, etc.).
- WebXR + emulación IWER (`iwer`, `@iwer/devui`).
- Troika-Three-Text (texto 3D), GSAP (animaciones), Audio posicional.
- Tooling: Webpack/Dev Server (HTTPS), ESLint/Prettier.

## Componentes del proyecto
- Código principal: `src/`
  - `index.js`: lógica del juego (disparos, colisiones, score, audio, haptics).
  - `init.js`: inicialización XR, emulación IWER, controladores y render loop.
  - `index.html` y assets (GLB/OGG/TTF).
- Tutorial paso a paso: `tutorial/` (capítulos 1–6 con imágenes y GIFs).
- Documentación de apoyo: `Docs/` (slides Reveal.js y notas técnicas).
- Cursos y slides: `cursos/` (3 programas con materiales y presentaciones).

## Demo y experiencia incluida
El repositorio incluye una experiencia WebXR de tiro al blanco lista para ejecutar:
- Control con gatillo del controlador derecho, vibración y sonido.
- HUD de puntuación con texto 3D y animaciones.
- Targets reubicados dinámicamente y colisión por proximidad.

Ejecución local:
1) `npm install`  2) `npm run dev`  3) Abrir `https://localhost:8081` (aceptar certificado). 
Acceso desde visor: por IP o con ADB/port‑forwarding (ver `README.md`).

## Casos de uso industriales (ejemplos)
- Formación y SOPs 3D (procedimientos, seguridad, primeros auxilios).
- Mantenimiento asistido (diagnóstico/soporte remoto, guías interactivas).
- Gemelos digitales y visualización de KPIs operativos en tiempo real.
- Planificación de layout y ergonomía (pruebas virtuales previas).
- Preventa/ventas técnicas (demo inmersiva de soluciones y configuraciones).

Beneficios: reducción de tiempos de entrenamiento, menor costo de iteración, mejor comprensión espacial, mayor retención y colaboración.

## Seguridad, privacidad y gobernanza
- HTTPS en LAN, control de acceso y manejo de datos sensibles.
- MDM/Quest for Business para gestión de dispositivos.
- Revisión de permisos (cámara/passthrough), privacidad y cumplimiento interno.

## Roadmap de evolución (proyección a futuro)
- Integración de datos industriales: WebSocket, MQTT, OPC‑UA o REST.
- Interacción avanzada: hand tracking, gestos y haptics enriquecidos.
- MR/passthrough: anclajes espaciales, oclusión y UX contextual.
- Multiusuario: sincronización de estado (WebRTC/servicios de tiempo real).
- Performance: materiales/instancias, culling y optimización de assets.
- QA/Observabilidad: métricas de sesión, tiempo en tarea y trazas.
- Despliegue: CI/CD a Pages/edge/on‑prem; automatización y control de versiones.
- Transición/compatibilidad con OpenXR nativo si se requiere mayor rendimiento.

## Formación y materiales
- Cursos: `cursos/Indice.md`
  - Curso 1 (2h): panorama sin programación para toma de decisiones.
  - Curso 2 (1 semana): bases de desarrollo con Three.js/WebXR.
  - Curso 3 (3 semanas): POC industrial end‑to‑end.
- Tutorial por capítulos: `tutorial/` (de objetos simples a experiencia completa).
- Slides listos para exponer (Reveal.js) en `Docs/` y `cursos/`.

## Métricas y KPIs sugeridos
- Adopción: asistentes a sesiones, tiempo de uso, repetición.
- Eficacia: tiempo hasta la primera demo/POC, tasa de errores en tareas.
- Rendimiento técnico: FPS, tiempos de carga, tamaño de bundle.
- Valor de negocio: reducción de tiempos y costos, satisfacción de usuarios (NPS).

## Contribución y gobernanza del repo
- Guía de contribución: `CONTRIBUTING.md`.
- Conducta: `CODE_OF_CONDUCT.md` (basado en Contributor Covenant).
- Licencia: `LICENSE` (MIT).

## Próximos pasos
1. Ejecutar la demo local y validar acceso desde el visor.
2. Seleccionar 1–2 casos de alto valor para un piloto.
3. Completar el tutorial y/o cursar el programa de 1 semana.
4. Definir datos a integrar y KPIs de medición.
5. Plan de despliegue (Pages/on‑prem) y gobernanza (MDM, seguridad).

---

Para dudas o mejoras, abre un issue/PR en el repositorio y consulta el material de `Docs/` y `cursos/` para clases y presentaciones.
