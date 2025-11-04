---
titulo: "Curso 2 – Fundamentos WebXR con Three.js"
duracion: "1 semana (5 sesiones x 3h)"
nivel: "Intermedio"
---

# Curso 2 – Fundamentos WebXR con Three.js

Programa intensivo de 1 semana para adquirir bases sólidas de WebXR con Three.js y buenas prácticas de desarrollo, culminando en un mini‑proyecto funcional.

## Objetivos
- Configurar entornos de desarrollo WebXR y emulación.
- Construir escenas 3D con Three.js y controles XR.
- Cargar modelos GLTF, gestionar assets, audio y texto.
- Interacción: raycasting, gamepad, haptic feedback.
- Optimización básica y despliegue.

## Audiencia
- Desarrolladores front‑end/Full‑stack con nociones de JS/ES6.

## Requisitos previos
- JavaScript moderno (ES6+), npm, nociones de gráficos 3D deseables.

## Estructura semanal (5×3h)

### Día 1 – Introducción y Setup (3h)
- WebXR, runtimes y emulación (IWER/DevUI)
- Repaso Three.js, escena/cámara/renderer
- Controles, OrbitControls, RoomEnvironment
- Laboratorio: levantar `npm run dev` y render simple

### Día 2 – Interacción y movimiento (3h)
- Controladores XR y GamepadWrapper
- Raycasting y eventos básicos
- Animación con `clock` y GSAP
- Laboratorio: mover/rotar objetos, disparo básico

### Día 3 – Assets y UI (3h)
- GLTF/GLB: carga y gestión de modelos
- Texto 3D con `troika-three-text`
- Audio posicional (THREE.Audio)
- Laboratorio: UI de puntuación y sonidos

### Día 4 – Colisiones y estado (3h)
- Proximidad y detección de choques simple
- Gestión de estado y TTL
- Optimización ligera (materiales, tamaños, bundling)
- Laboratorio: juego de dianas con score

### Día 5 – Despliegue y QA (3h)
- Webpack, `mode`, Pages/hosting
- Certificados y acceso desde visor en LAN
- Revisión final y demo del mini‑proyecto

## Entregables
- Mini‑proyecto: juego WebXR con disparos, score, audio/haptics.
- Slides (`curso_2_sliders.html`).

## Evaluación
- Checkpoints diarios (breves) + demo final funcional.

## Materiales
- Repositorio `webxr-first-steps` (src/index.js, init.js).
- Documentación del tutorial y Docs del repo.

