# 📚 ÍNDICE GENERAL - DOCUMENTACIÓN STREAM-TROPA

## 🎯 ¿Por dónde empezar?

### Si eres nuevo en Stream-Tropa:
0. **Abre primero:** [index.html](index.html)
   - Portal central integrado
   - Punto único de acceso a todas las apps

1. **Lee primero:** [README_GENERAL.md](README_GENERAL.md)
   - Visión general del proyecto
   - Estructura de aplicaciones
   - Requisitos previos

2. **Luego, elige tu caso de uso:**
   - [Videoconferencia](#-video-conferencia)
   - [Comunicación PTT](#-comunicación-ptt)
   - [Spliteo de Video](#-spliteo-de-video)
   - [Captura desde iPad](#-captura-desde-ipad)
   - [Gráficos y Overlays](#-gráficos-y-overlays)

3. **Finalmente:** [README_CREDENCIALES.md](README_CREDENCIALES.md)
   - Cómo cambiar configuraciones sensibles
   - Migración a servidores propios

---

## 📖 DOCUMENTOS DISPONIBLES

### 📋 GENERAL
| Documento | Contenido | Leer si... |
|-----------|----------|-----------|
| [index.html](index.html) | Portal central integrado | Quieres operar todo desde una sola pantalla |
| [README_GENERAL.md](README_GENERAL.md) | Introducción al proyecto | Eres nuevo en Stream-Tropa |
| [README_CREDENCIALES.md](README_CREDENCIALES.md) | Cómo cambiar configuraciones | Necesitas personalizar servidores |

---

### 🎥 VIDEO CONFERENCIA
**Documentos:**
- [README_VIDEO_CONFERENCIA.md](README_VIDEO_CONFERENCIA.md)

**Aplicaciones incluidas:**
| App | Archivo | Uso |
|-----|---------|-----|
| StreamVideo V2.0 | `hub-video.html` | Conferencia multiusuario |
| StreamCall Pro | `baradero.html` | Director + múltiples cámaras |
| StreamCall V10 | `call/index.html` | Conferencia avanzada |
| MAU StreamCall | `mau.html` | Comunicación remota |
| TVES StreamCall | `tves.html` | Dirección profesional |

**Casos de uso:**
- ✓ Video conferencias (2-20 personas)
- ✓ Transmisión director + cámaras remotas
- ✓ OBS integration
- ✓ Sistema de tally (ON-AIR/PREVIEW)

---

### 📡 COMUNICACIÓN PTT
**Documentos:**
- [README_PTT.md](README_PTT.md)

**Aplicaciones incluidas:**
| App | Archivo | Uso |
|-----|---------|-----|
| StreamTalk V9.0 | `test.html` | Walkie-talkie director |
| StreamTalk V9.0 Full | `talktotalk.html` | Bidireccional completo |
| StreamTalk V9.1 | `talkok.html` | Listen-only (solo escucha) |

**Casos de uso:**
- ✓ Equipos de producción (TV/eventos)
- ✓ Comunicación de seguridad
- ✓ Coordinación en eventos en vivo
- ✓ Push-to-talk (6-20 usuarios)

---

### 🎬 SPLITEO DE VIDEO & GRÁFICOS
**Documentos:**
- [README_SPLITEO.md](README_SPLITEO.md)

**Aplicaciones incluidas:**

**Spliteo (Mezcla de Video):**
| App | Archivo | Uso |
|-----|---------|-----|
| StreamSplitter V25 | `atem.html` | Grilla 2x2 de 4 fuentes |
| Streamcall Power | `strp/index.html` | Sistema flexible |
| Streamcall Power 4G | `strp/4g.html` | Optimizado para 4G en Argentina |
| Streamcall Power Honduras | `strp/4ghn.html` | Con TURN Honduras |

**Control de Gráficos:**
| App | Archivo | Uso |
|-----|---------|-----|
| StreamCommand | `51933847353.html` | QR + Cronómetro + Cards + alertas |
| Zapping Master V12 | `thn/index.html` | Gráficos de noticias |

**Casos de uso:**
- ✓ Programas multi-cámara (TV)
- ✓ Divulgación de información (QR dinámicos)
- ✓ Cronómetros en vivo
- ✓ Gráficos de noticias automatizados
- ✓ Alertas flash

---

### 📱 CAPTURA DESDE iPAD
**Documentos:**
- [README_CAPTURA_IPAD.md](README_CAPTURA_IPAD.md)

**Aplicaciones incluidas:**
| App | Archivo | Uso |
|-----|---------|-----|
| iPad Transmisor | `tablet/ipad.html` | Captura pantalla |
| OBS Receptor | `tablet/obs.html` | Recibe en OBS |
| iPad Moderno | `tablet3/ipad.html` | Versión mejorada |
| OBS Receptor V3 | `tablet3/obs.html` | Recibe versión 3 |

**Casos de uso:**
- ✓ Presentaciones desde iPad
- ✓ Captura de apps
- ✓ Compartir documentos
- ✓ Demo de software
- ✓ Streaming de juegos

---

### 🛠️ HERRAMIENTAS ADICIONALES
| App | Archivo | Uso | Referencia |
|-----|---------|-----|-----------|
| NDI Delay Calculator | `avndi/index.html` | Calcular delay FPS | `README_GENERAL.md` |
| Visualizador Retorno | `retorno/index.html` | Ver retorno en vivo | `README_GENERAL.md` |
| Laptop-to-Laptop | `retorno/pc.html` | Video entre laptops | `README_GENERAL.md` |
| PPT Call Eventos | `streventos/pptevent.html` | Eventos LAN | `README_GENERAL.md` |
| PPT Call Híbrido | `streventos/pptturn.html` | Con TURN fallback | `README_CREDENCIALES.md` ⚠️ |

---

## 🔑 CREDENCIALES Y CONFIGURACIÓN

### ⚠️ INFORMACIÓN SENSIBLE ACTUAL

**TURN Server (pptturn.html):**
```
Servidor:    140.82.25.249:3478
Usuario:     reportero
Contraseña:  mundial2026
```

**MQTT Broker:**
```
URL:  wss://broker.emqx.io:8084/mqtt
Tipo: Público (sin autenticación)
```

**PeerJS Server:**
```
Host: 0.peerjs.com:443
Tipo: Público CDN
```

### ✅ CAMBIAR CREDENCIALES

**Lee:** [README_CREDENCIALES.md](README_CREDENCIALES.md)

**Pasos rápidos:**
1. Identifica qué cambiar (TURN/MQTT/PeerJS)
2. Copia la sección de código correspondiente
3. Reemplaza valores
4. Guarda archivos
5. Verifica con `Select-String` (PowerShell)

---

## 🚀 GUÍAS RÁPIDAS POR CASO DE USO

### 1️⃣ Quiero Conferencia de Video Simple
**Pasos:**
1. Abre `hub-video.html` en dos navegadores
2. Ambos ingresan código de sala igual
3. Click: INICIAR
4. ✅ Video activo

**Referencia:** [README_VIDEO_CONFERENCIA.md](README_VIDEO_CONFERENCIA.md)

---

### 2️⃣ Quiero Transmisión TV (Director + Cámaras)
**Pasos:**
1. Director: `baradero.html?mode=director&room=SHOW1`
2. Cámaras (3x): `baradero.html?mode=guest&room=SHOW1`
3. OBS Source: `baradero.html?mode=obs&room=SHOW1`
4. Director controla Tally
5. ✅ Transmisión completa

**Referencia:** [README_VIDEO_CONFERENCIA.md](README_VIDEO_CONFERENCIA.md)

---

### 3️⃣ Quiero Walkie-Talkie para Equipo
**Pasos:**
1. Director: `test.html` (transmite)
2. Crew (6x): `talkok.html` (escucha)
3. Director presiona botón para hablar
4. ✅ Audio coordinado

**Referencia:** [README_PTT.md](README_PTT.md)

---

### 4️⃣ Quiero 4 Cámaras Simultáneas
**Pasos:**
1. Abre: `atem.html` (grilla 2x2)
2. Conecta 4 cámaras: `strp/index.html`
3. OBS captura: `atem.html`
4. ✅ Multi-cámara en OBS

**Referencia:** [README_SPLITEO.md](README_SPLITEO.md)

---

### 5️⃣ Quiero Stream Call 3 Cámaras + Audio para 4G Argentina
**Pasos:**
1. Abre: `51933847353.html` (StreamCommand)
2. Conecta 3 cámaras con audio: `strp/index.html` o `strp/4g.html`
3. Usa la variante `strp/4g.html` si la red móvil está débil
4. Captura la salida final en OBS o en el destino de emisión
5. ✅ Flujo liviano para operación móvil

**Referencia:** [README_SPLITEO.md](README_SPLITEO.md)

---

### 6️⃣ Quiero Compartir Pantalla del iPad
**Pasos:**
1. OBS: Browser source → `tablet/obs.html?room=STREAM1`
2. iPad: `tablet/ipad.html` → Código: STREAM1
3. iPad: Compartir Pantalla
4. ✅ Pantalla iPad en OBS

**Referencia:** [README_CAPTURA_IPAD.md](README_CAPTURA_IPAD.md)

---

### 7️⃣ Quiero Mostrar QR y Cronómetro
**Pasos:**
1. Abre: `51933847353.html` (StreamCommand)
2. Configura QR, Cronómetro, Cards
3. Copia URLs de overlay
4. OBS Browser sources
5. ✅ Gráficos dinámicos

**Referencia:** [README_SPLITEO.md](README_SPLITEO.md)

---

### 8️⃣ Quiero Noticias Automáticas
**Pasos:**
1. Abre: `thn/index.html` (Zapping Master)
2. Agrega noticias
3. Modo Auto
4. OBS captura
5. ✅ Gráficos rotando automáticamente

**Referencia:** [README_SPLITEO.md](README_SPLITEO.md)

---

## 🔧 TAREAS DE CONFIGURACIÓN

### Cambiar MQTT Broker a Propio
**Dificultad:** ⭐⭐⭐

**Archivo:** [README_CREDENCIALES.md](README_CREDENCIALES.md) - Sección OPCIÓN 2

**Pasos:**
1. Instala Mosquitto o broker MQTT
2. Obtén URL/IP:puerto
3. Usa Find & Replace global en archivos
4. Verifica con `Select-String`
5. Prueba conexión

---

### Cambiar TURN Server
**Dificultad:** ⭐⭐

**Archivo:** [README_CREDENCIALES.md](README_CREDENCIALES.md) - Sección OPCIÓN 1

**Pasos:**
1. Obtén servidor TURN (Twilio, AWS, etc)
2. Modifica `streventos/pptturn.html`
3. Reemplaza IP/usuario/contraseña
4. Guarda y prueba

---

### Usar PeerJS Server Propio
**Dificultad:** ⭐⭐⭐⭐

**Archivo:** [README_CREDENCIALES.md](README_CREDENCIALES.md) - Sección OPCIÓN 3

**Pasos:**
1. Instala PeerJS Server: `npm install -g peerjs-server`
2. Ejecuta: `peerjs --port 9000`
3. Modifica todos los archivos
4. Cambia host a tu servidor
5. Verifica certificado SSL

---

## 🆘 SOLUCIÓN DE PROBLEMAS

### "No conecta"
**Verificar:**
1. ¿Navegador soporta WebRTC? (Chrome/Firefox/Safari)
2. ¿Permisos de cámara/micrófono activados?
3. ¿Conexión a internet estable?
4. ¿Firewall permite puertos?
5. Abre Console (F12) para ver errores

**Referencia:** Cada README tiene sección "Troubleshooting"

---

### "Audio con retraso"
**Solución rápida:**
1. Reduce resolución de video
2. Cierra otras aplicaciones
3. Usa WiFi 5GHz si es posible
4. Intenta cable Ethernet
5. Recarga página

**Referencia:** [README_VIDEO_CONFERENCIA.md](README_VIDEO_CONFERENCIA.md#-troubleshooting)

---

### "OBS no recibe video"
**Verificar:**
1. URL en OBS es correcta
2. `?mode=obs` está en parámetros
3. Transmisor está conectado
4. Firewall permite conexión
5. Verifica en consola (F12)

**Referencia:** [README_CAPTURA_IPAD.md](README_CAPTURA_IPAD.md#-troubleshooting)

---

## 📊 MATRIZ DE COMPATIBILIDAD

### Navegadores
```
Chrome      ✓ Soporto completo (recomendado)
Firefox     ✓ Soporto completo
Safari      ✓ Soporto completo (15.1+)
Edge        ✓ Soporto completo
Opera       ✓ Soporto completo
```

### Dispositivos
```
Laptop      ✓ Óptimo
Desktop     ✓ Óptimo
Tablet      ✓ Bueno
Móvil       ⚠️ Limitado (pantalla pequeña)
iPad        ✓ Excelente
```

### Sistemas Operativos
```
Windows     ✓ Completo
macOS       ✓ Completo
Linux       ✓ Completo
iOS 15.1+   ✓ Completo
Android 6+  ✓ Completo
```

---

## 📈 ROADMAP (Mejoras Futuras)

- [ ] Grabación de sesiones
- [ ] Chat de texto integrado
- [ ] Soporte de pantalla virtual
- [ ] Autenticación con contraseña
- [ ] Dashboard de administración
- [ ] Estadísticas en tiempo real
- [ ] Soporte de subtítulos
- [ ] Integración con YouTube/Twitch

---

## 📞 CONTACTO Y SOPORTE

**Problemas técnicos:**
1. Verifica Console (F12) para errores
2. Busca en el README correspondiente
3. Prueba en navegador diferente
4. Verifica conectividad de red

**Reporte de bugs:**
- Captura pantalla del error
- Abre Console (F12) y copia texto rojo
- Describe pasos para reproducir

---

## 📝 FORMATO DE DOCUMENTOS

Cada README incluye:
- 🎯 Descripción general
- 🚀 Inicio rápido
- 🎛️ Interfaz usuario
- 📡 Funcionamiento técnico
- 🔧 Configuración avanzada
- 🎬 Casos de uso reales
- 🐛 Troubleshooting
- 🔒 Privacidad y seguridad
- 📚 Referencias

---

## 🎓 TUTORIALES RECOMENDADOS

### Para Principiantes
1. Lee: README_GENERAL.md
2. Elige: Caso de uso simple
3. Sigue: Guía Rápida del caso
4. Prueba: Copia exacta de URLs

### Para Intermedios
1. Lee: README específico de categoría
2. Modifica: Configuraciones básicas
3. Integra: Con OBS
4. Personaliza: Colores y textos

### Para Avanzados
1. Modifica: Servidores MQTT/TURN/PeerJS
2. Deployea: En servidor propio
3. Desarrolla: Extensiones propias
4. Optimiza: Para producción

---

## 📜 CONTROL DE VERSIONES

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0 | 2026-04-29 | Documentación inicial |
| 1.1 | TBD | Agregar soporte de grabación |
| 2.0 | TBD | Rediseño UI |

---

## 🙏 CRÉDITOS

**Desarrollo:** Stream-Tropa Team
**Tecnologías:** React 18, PeerJS, MQTT, WebRTC
**Hosting:** Community driven
**Licencia:** Open Source

---

**Última actualización:** 2026-04-29
**Versión:** 1.0
**Estado:** ✅ Producción
