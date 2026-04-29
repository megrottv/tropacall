# 📡 STREAM-TROPA - DOCUMENTACIÓN GENERAL

## Visión General
Stream-Tropa es una colección de aplicaciones HTML para streaming de video en tiempo real, construidas con **React 18**, **PeerJS (WebRTC)** y **MQTT**. Las aplicaciones permiten:
- Video conferencias multiusuario
- Control de producción (director/guest)
- Streaming para OBS
- Overlay de gráficos (QR, cronómetros, noticias)
- Audio bidireccional y PTT

---

## 📂 Estructura General

```
stream-tropa/
├── [Archivos raíz] - Aplicaciones principales
│   ├── 51933847353.html  → StreamCommand (Panel de Control)
│   ├── atem.html         → StreamSplitter (Divisor de Video)
│   ├── baradero.html     → StreamCall Pro (Video Director)
│   ├── hub-video.html    → StreamVideo V2.0 (Conferencia)
│   ├── talkok.html       → StreamTalk (PTT)
│   └── test.html         → StreamTalk Pocket
│
├── call/                 → StreamCall Pro (Director/Guest)
│   ├── index.html       → Control principal
│   └── vdo.html         → Meshcast Studio
│
├── call3/                → BARADERO StreamCall 3
│
├── avndi/                → NDI Tools (Calculadora delay)
│
├── strp/                 → Streamcall Power (Optimizado 4G)
│   ├── index.html
│   ├── 4g.html
│   ├── 4g1.html
│   ├── 4ghn.html        → Con TURN Honduras
│   └── hn.html
│
├── retorno/              → Visualizador de retorno
│   ├── index.html
│   └── pc.html
│
├── tablet/               → iPad Screen Share
│   ├── ipad.html        → Transmisor
│   └── obs.html         → Receptor
│
├── tablet3/              → iPad Screen Share (Moderno)
│
├── thn/                  → Zapping Master (Gráficos)
│   ├── index.html
│   └── index2.html
│
├── streventos/           → PPT Call (Eventos)
│   ├── pptevent.html    → LAN puro
│   └── pptturn.html     → Con TURN fallback
│
└── streventos/           → Archivos de configuración
    └── leame.txt
```

---

## 🔧 Arquitectura Técnica

### Tecnologías Principales
```
Frontend:      React 18 + Babel (JSX transpilation)
P2P Video:     PeerJS 1.5.2 (WebRTC wrapper)
Mensajería:    MQTT 4.3.7 (pub/sub para estado)
Estilos:       Tailwind CSS (CDN)
Navegación:    Query parameters (?mode=, ?room=)
```

### Flujo de Conexión
```
1. Navegador carga HTML
2. React se monta y detecta parámetros URL
3. PeerJS se conecta a broker (0.peerjs.com:443)
4. MQTT se conecta (opcional, para estado)
5. Usuarios se intercambian streams P2P directamente
6. Sistema de tally/control vía MQTT
```

---

## 🔐 Configuraciones Actuales

### MQTT Broker
```javascript
// Configuración estándar en TODOS los archivos
MQTT_BROKER = 'wss://broker.emqx.io:8084/mqtt'
```
**Características:**
- Público (sin autenticación)
- WebSocket Seguro (WSS)
- Topics por sala: `sc_video_v4/{roomName}/...`

### PeerJS Configuration
```javascript
PEER_CONFIG = {
    config: {
        'iceServers': [
            { urls: 'stun:stun.l.google.com:19302' },
            { urls: 'stun:stun1.l.google.com:19302' }
        ]
    }
}
```
**Host:** `0.peerjs.com:443`

### ⚠️ CREDENCIALES EXPUESTAS

**Archivo: `streventos/pptturn.html`**
```javascript
username: 'reportero'
password: 'mundial2026'
TURN Server: 140.82.25.249:3478
```

---

## 🌐 URLs de Funcionamiento

### Local
```
file:///d:/stream-tropa/hub-video.html
```

### HTTP Server (Recomendado)
```
http://localhost:8000/hub-video.html
```

### IMPORTANTE
- Las aplicaciones requieren **HTTPS** o **localhost** para acceso a cámara
- WebRTC P2P funciona desde cualquier origen
- MQTT requiere servidor con WebSocket

---

## ✅ Requisitos Previos

1. **Navegador moderno** (Chrome, Firefox, Edge, Safari)
2. **Permisos de cámara/micrófono** (solicitados al acceder)
3. **Conexión a internet** (para STUN/MQTT/PeerJS)
4. **Servidor local** (para testing, si es necesario)

---

## 📋 Categorías de Aplicaciones

### 1️⃣ **VIDEO CONFERENCIA**
Comunicación multiusuario bidireccional
- `hub-video.html` - StreamVideo V2.0
- `baradero.html` - StreamCall Pro
- `call/index.html` - StreamCall V10

### 2️⃣ **COMUNICACIÓN PTT**
Push-to-Talk para equipos (Walkie-Talkie)
- `test.html` - StreamTalk V9.0
- `talktotalk.html` - StreamTalk V9.0
- `talkok.html` - StreamTalk V9.1 (Listen Only)

### 3️⃣ **SPLITEO DE VIDEO**
Mezcla y división de fuentes
- `atem.html` - StreamSplitter (Grilla 2x2)
- `strp/index.html` - Streamcall Power

### 4️⃣ **PANEL DE CONTROL**
Overlays y gráficos para transmisiones
- `51933847353.html` - StreamCommand (QR, Cronómetro, Cards)
- `thn/index.html` - Zapping Master (Gráficos dinámicos)

### 5️⃣ **CAPTURA DESDE iPad**
Screen sharing desde dispositivos móviles
- `tablet/ipad.html` - Transmisor
- `tablet/obs.html` - Receptor
- `tablet3/` - Versión mejorada

### 6️⃣ **HERRAMIENTAS**
Utilidades para streaming
- `avndi/index.html` - Calculadora de Delay NDI
- `retorno/index.html` - Visualizador retorno

---

## 🎯 Casos de Uso Típicos

### Caso 1: Video Conferencia Simple
```
1. Abrir hub-video.html en dos navegadores
2. Ambos ingresan el mismo código de sala
3. Presionan INICIAR
4. Se establece conexión P2P automática
```

### Caso 2: Director + Múltiples Cámaras
```
1. Operador abre baradero.html en modo director
2. Cámaras se conectan en modo guest
3. Director ve todas las fuentes en grid
4. Sistema de tally (ON-AIR/PREVIEW) controla indicadores
```

### Caso 3: Captura OBS
```
1. Abrir tablet/obs.html en navegador (receptor limpio)
2. OBS agrega como Browser source
3. iPad se conecta en tablet/ipad.html
4. Pantalla del iPad se captura en OBS
```

### Caso 4: Control de Gráficos
```
1. Abrir 51933847353.html en navegador
2. Configurar QR, cronómetro, cards
3. Copiar URLs de overlay
4. Agregar como Browser source en OBS
5. Actualizar desde panel principal en tiempo real
```

### Caso 5: Stream Call 3 Cámaras + Audio para 4G en Argentina
```
1. Abrir strp/index.html o strp/4g.html según la red disponible
2. Conectar 3 cámaras con audio activo
3. Usar 51933847353.html para QR, timer y avisos en vivo
4. Capturar el resultado final en OBS o en el destino de emisión
5. Priorizar strp/4g.html cuando la red móvil sea inestable
```

Este flujo está pensado para producciones móviles en Argentina donde se necesita una salida liviana, estable y fácil de operar con control de gráficos separado.

---

## 🚀 Primeros Pasos

1. **Verificar navegador**: Chrome/Firefox/Edge con soporte WebRTC
2. **Verificar permisos**: Permitir cámara y micrófono cuando se pida
3. **Elegir aplicación**: Según el caso de uso (arriba)
4. **Compartir URL**: Enviar link a otros participantes
5. **Conectar**: Ingresar código de sala común

---

## ⚙️ Siguiente: LEE LOS README ESPECÍFICOS POR CATEGORÍA

- `README_VIDEO_CONFERENCIA.md` - Sistemas multiusuario
- `README_PTT.md` - Comunicación walkie-talkie
- `README_SPLITEO.md` - Mezcla de video
- `README_OVERLAYS.md` - Gráficos y controles
- `README_CAPTURA_IPAD.md` - Screen sharing
- `README_CREDENCIALES.md` - Cómo cambiar configuraciones

---

**Última actualización:** 2026-04-29
**Versiones de componentes:** React 18, PeerJS 1.5.2, MQTT 4.3.7
