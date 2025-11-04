<p align="center">
  <img src="./Antares.jpeg" style="max-width:100%"/>
</p>

# WebXR First Steps (Three.js + WebXR)

## Objetivo
Este repositorio está orientado a la presentación y aprendizaje inicial de conceptos de virtualización en tanto dispositivos, entornos y formatos de integración.

La instalación provee:
Frontend WebXR (Three.js) para demostrar y capacitar sobre experiencias inmersivas accesibles desde el navegador del visor (Quest/Pico, etc.). Ideal para difusión, formación y prototipado rápido de casos industriales, dejando el “runtime” XR al navegador.

## Por qué WebXR + Three.js
- Compatibilidad amplia: visores standalone soportan WebXR nativamente por Wi‑Fi.
- Sin dependencias de PC VR: funciona en Linux/Windows/macOS con navegador.
- Ecosistema web: integra con backends y servicios vía HTTP/WS.

## Pre‑instalación (requerimientos)
- Node.js 20+ y npm 10+.
  - Verifica versiones: `node -v` y `npm -v`.
  - Ubuntu (recomendado con nvm):
    - `curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash`
    - `source ~/.bashrc && nvm install 20 && nvm use 20`
  - macOS: `brew install node@20 && brew link node@20 --force`
  - Windows: `winget install OpenJS.NodeJS.LTS` (o instala desde https://nodejs.org)
- Git (para clonar el repositorio).
- Un visor con navegador WebXR (Meta Quest, Pico, etc.) en la misma red Wi‑Fi.
- Opcional (para desarrollo avanzado):
  - Google Chrome/Edge actualizados (DevTools).
  - ADB para port forwarding (USB):
    - Ubuntu: `sudo apt install adb`
    - macOS: `brew install android-platform-tools`
    - Windows: “platform-tools” de Android o `choco install adb`
  - Certificados de desarrollo confiables: `mkcert` para HTTPS local sin avisos.

## Documentación
- Índice general: `./DOCUMENTACION_INDICE.md`
- WebXR — visión general: `./Docs/webxr_overview.md`
- Monado (OpenXR, Linux) — visión general: `./Docs/monado_overview.md`
- Tutorial paso a paso (recomendado): `./Docs/tutorial_webxr_vrmeta.md`
- Cursos y slides: `./cursos/Indice.md`

## Instalación (3 pasos)
1) Clonar e instalar dependencias
```bash
git clone https://github.com/J2TechAntaresTechnologies/MetaQuest_FirstSteps_Antares.git
cd MetaQuest_FirstSteps_Antares
npm install
```
2) Ejecutar el servidor de desarrollo (HTTPS, 0.0.0.0:8081)
```bash
npm run dev
```
3) Abrir desde el visor/navegador
- PC: `https://localhost:8081`
- Visor en la misma red: `https://<IP-DE-TU-PC>:8081`
  - Acepta el certificado auto‑firmado si aparece un aviso.
  - Si la red bloquea acceso, usa ADB/port‑forwarding y entra por `https://localhost:8081` desde el visor.

Notas de HTTPS/Certificados
- WebXR requiere contexto seguro. Con auto‑firmado suele bastar aceptar el aviso; en entornos estrictos, usa un proxy HTTPS con certificado válido o instala una CA confiable en el visor.
- Para cambiar el puerto: `npm run dev -- --port 8443` (ejemplo).

## Endpoints
Este proyecto es frontend estático. No expone endpoints HTTP/WS propios. Para backend (MQTT/OPC‑UA/REST, etc.), integra servicios externos y consume APIs desde el cliente.

## Demo incluida (target practice)
- Disparo con controlador (gatillo), háptica y audio posicional.
- Puntuación con texto 3D y animaciones GSAP.
- Dianas reubicadas y detección por proximidad.

## Siguientes pasos industriales
- MQTT/OPC‑UA/REST: integrar datos de planta en el HUD/escena.
- MR/passthrough: overlays contextuales y anclajes espaciales.
- Multiusuario: sincronización y voz (WebRTC/servicios RT).
- QA/Performance: perfiles a 90 Hz, optimización de assets y materiales.

## Ruta nativa OpenXR (opcional, avanzada)
Si necesitas nativo en Linux/PC VR, usa un runtime OpenXR (p. ej., Monado) y un motor (Unity/Unreal) o C++. Este repo prioriza WebXR por simplicidad y portabilidad. Ver `./Docs/monado_overview.md`.

## Notas
- El dev‑server escucha en `0.0.0.0` con HTTPS y muestra la IP de tu equipo.
- Con otras emulaciones WebXR, desactívalas si interfieren. IWER/DevUI viene integrado y se activa si no hay WebXR nativo.

## Cliente WebXR de prueba
- URL (LAN): `https://<IP-DE-TU-PC>:8081`
- Pulsa “Enter VR” (VRButton). Si tu navegador no soporta WebXR, se activa la emulación IWER con controles desde teclado/ratón.

## Diapositivas (resumen)
- Markdown: `./Docs/vr_informe_slides.md`
- HTML listo: `./Docs/vr_informe_slides.html`
- Estilos y logo: `./Docs/slides.css`, `./Docs/assets/logo_antares.png`

## Piloto industrial (guía)
- Documento: `./Docs/piloto_industria4.md`
- Contiene objetivos, selección de caso, KPIs, integraciones, seguridad/MDM y plan de 8–10 semanas.

## Build y deploy
- Build de estáticos: `npm run build` → genera `./dist`.
- GitHub Pages: workflow en `.github/workflows/deploy.yml` (activar en Settings → Pages → GitHub Actions).

## Licencia y contribución
- Licencia: MIT (`./LICENSE`).
- Contribución: `./CONTRIBUTING.md` y `./CODE_OF_CONDUCT.md` (actualiza el email de contacto según tu organización).

---

Referencias oficiales WebXR (tecnología en evolución)
- W3C WebXR Device API: https://www.w3.org/TR/webxr/
- Immersive Web (grupo comunitario): https://immersive-web.github.io/
- MDN Web Docs (WebXR): https://developer.mozilla.org/docs/Web/API/WebXR_Device_API

WebXR es un estándar abierto en evolución. Aquí mostramos cómo implementarlo en procesos industriales y en el marco de Industria 5.0, priorizando acceso inmediato desde visor y prototipado ágil.


Autor: Juan Ignacio Martinez

<p align="center">
  <img src="./tutorial/assets/webxr-first-steps.png" style="max-width:188px"/>
</p>
