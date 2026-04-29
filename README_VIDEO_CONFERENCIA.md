# 🎥 VIDEO CONFERENCIA - GUÍA COMPLETA

## Aplicaciones Incluidas
- `hub-video.html` - StreamVideo V2.0 (Recomendado)
- `baradero.html` - StreamCall Pro
- `call/index.html` - StreamCall V10
- `mau.html` - MAU StreamCall
- `tves.html` - TVES StreamCall

---

## 🎯 DESCRIPCIÓN GENERAL

Las aplicaciones de video conferencia permiten comunicación de **video bidireccional en tiempo real** con múltiples roles:
- **Transmisor (Transmitter)**: Envía video/audio
- **Director (Receiver)**: Recibe video y controla
- **OBS Mode**: Recibe limpio para OBS sin UI
- **Guest**: Participa en video conferencia

---

## 🚀 INICIO RÁPIDO

### Escenario 1: Video Simple Dos Personas

1. **Abrir en navegador 1:**
   ```
   http://localhost:8000/hub-video.html
   ```
   - Se genera un código de sala automático (ej: `A4K2`)
   - Click en **INICIAR TRANSMISIÓN**

2. **Abrir en navegador 2:**
   ```
   http://localhost:8000/hub-video.html?mode=receiver&room=A4K2
   ```
   - Ingresa el mismo código de sala
   - Permite recibir video automáticamente

**¡Resultado:** Video bidireccional activo ✅

---

### Escenario 2: Director + 3 Cámaras

1. **Navegador del Director:**
   - Abre: `baradero.html`
   - Modo: `director`
   - Click: **PANEL DIRECTOR**

2. **Navegadores de Cámaras (3x):**
   - Abre: `baradero.html`
   - Modo: `guest`
   - Mismo código de sala
   - Click: **ENTRAR**

**Resultado:** Director ve grid con 3 cámaras, control de tally ✅

---

## 🎛️ INTERFAZ USUARIO

### Panel Principal (Dashboard)
```
┌─────────────────────────────────┐
│  StreamVideo V2.0               │
│  ─────────────────────────────  │
│  Código Sala: [________]        │
│  Nombre: [_____]                │
│                                 │
│  [INICIAR TRANSMISIÓN]          │
│  [ENTRAR COMO RECEPTOR]         │
└─────────────────────────────────┘
```

### Panel Transmisor (TX)
```
┌──────────────────────────────┐
│  CÁMARA (Preview)            │
│  ────────────────────────────│
│  📷 Dispositivo: [Seleccionar]│
│  🎤 Micrófono: [Seleccionar]  │
│  📊 Resolución: 720p [▼]      │
│                              │
│  [🔴 INICIAR TRANSMISIÓN]    │
└──────────────────────────────┘
```

### Panel Receptor (RX)
```
┌──────────────────────────────┐
│  TRANSMISORES ACTIVOS        │
│  ────────────────────────────│
│  ┌────────────┬────────────┐ │
│  │  CAM 1     │  CAM 2     │ │
│  │ [VIDEO]    │ [VIDEO]    │ │
│  │ 🔊 ONLINE  │ 🔊 OFFLINE │ │
│  └────────────┴────────────┘ │
│  ┌────────────┐              │
│  │  CAM 3     │              │
│  │ [VIDEO]    │              │
│  │ 🔊 ONLINE  │              │
│  └────────────┘              │
└──────────────────────────────┘
```

### Sistema de Tally (Indicador ON-AIR)
```
Estado Idle:   ⬜ Gris (PARADO)
Estado Preview: 🟢 Verde (PREVENIDO)
Estado LIVE:   🔴 Rojo (AL AIRE)
```

---

## 📱 FUNCIONALIDADES PRINCIPALES

### Control de Dispositivos
```
✓ Seleccionar cámara (frontal/trasera en móviles)
✓ Seleccionar micrófono
✓ Cambiar resolución (360p/720p/1080p)
✓ Muteado de audio/video individual
✓ Cambio de cámara sin cortar stream
```

### Calidad de Video
```
360p  → 640x360   @ ~1Mbps    (Bajo ancho banda)
720p  → 1280x720  @ ~2.5Mbps  (Estándar recomendado)
1080p → 1920x1080 @ ~5Mbps    (Alta calidad, requiere fibra)
4K    → 3840x2160 @ ~12Mbps   (Extremo, no recomendado)
```

### Control Remoto (Director)
```
✓ Ver todos los transmisores simultáneamente
✓ Cambiar indicador Tally (ON-AIR/PREVIEW/IDLE)
✓ Enviar retorno (Talkback) al guest
✓ Copiar URL para OBS
✓ Modo limpio para producción
```

### OBS Integration
```
1. Director genera URL limpia: ?mode=obs&room=SALA
2. Copia URL en OBS → Browser source
3. Guest se conecta en ?mode=guest&room=SALA
4. Video aparece limpio en OBS (sin UI)
```

---

## 🔌 CONEXIÓN TÉCNICA

### Flujo de Datos
```
Transmisor (TX)
    ↓ GetUserMedia() → captura cámara/micrófono
    ↓ PeerJS.call() → inicia llamada P2P
    ↓ MQTT.publish() → notifica conexión
    ↓
BROKER (MQTT) → Distribuye estado
    ↓
Receptor (RX)
    ↓ Recibe stream P2P directamente
    ↓ MQTT.subscribe() → escucha cambios
    ↓ Renderiza video
```

### Protocolos Utilizados
```
WebRTC (P2P)        → Video/Audio bidireccional
MQTT (Pub/Sub)      → Control y estado
DNS                 → Resolución de nombres
STUN (NAT Traversal)→ Descubrimiento de IP pública
TURN (Fallback)     → Relay si NAT bloquea
```

---

## 🎥 CASOS DE USO REALES

### Caso 1: Reunión de Trabajo Virtual
```
Participantes: 4 personas
Configuración:
  - Hub-video.html
  - Código sala: MEET-2026
  - Resolución: 720p
  - Micrófono: Integrado de laptop
Resultado: Video conferencia 4-way sin software especial
```

### Caso 2: Transmisión Profesional (Director + 3 Cámaras)
```
Setup:
  - Director en Laptop (Baradero director mode)
  - 3 cámaras en teleprompters/móviles
  - OBS para captura
Flujo:
  1. Director abre: baradero.html?mode=director&room=SHOW1
  2. Cámara 1,2,3 abren: baradero.html?mode=guest&room=SHOW1
  3. Director ve grid 3x cámaras
  4. Director activa TALLY LIVE en Cám 2
  5. Cám 2 ve borde rojo indicando ON-AIR
  6. OBS captura con: baradero.html?mode=obs&room=SHOW1
```

### Caso 3: Retransmisión a Internet
```
Cadena:
  Cámara física
     ↓
  OBS (captura + codifica)
     ↓
  Upload a YouTube/Facebook
     ↓
  Audience ve en vivo

Paralelo con Stream-Tropa:
  Director recibe y monitorea
  Cámaras remotas se conectan
  Sistema redundante de backup
```

---

## ⚙️ CONFIGURACIÓN AVANZADA

### Cambiar MQTT Broker
**Archivo:** Todos los que tienen `MQTT_BROKER`

Busca:
```javascript
const MQTT_BROKER = 'wss://broker.emqx.io:8084/mqtt';
```

Reemplaza:
```javascript
const MQTT_BROKER = 'wss://mqtt.micompany.com:8084/mqtt';
```

### Cambiar Resolución Predeterminada
**Archivo:** `hub-video.html`

Busca:
```javascript
const [selectedRes, setSelectedRes] = useState('720');
```

Reemplaza por:
```javascript
const [selectedRes, setSelectedRes] = useState('1080'); // 1080p por defecto
```

### Aumentar Bitrate (Para mejor calidad)
**Archivo:** `hub-video.html`

Busca:
```javascript
const VIDEO_PROFILES = {
    '720': { w: 1280, h: 720, bps: 2500000, label: '720p HD' }
}
```

Reemplaza:
```javascript
const VIDEO_PROFILES = {
    '720': { w: 1280, h: 720, bps: 5000000, label: '720p HD Extra' }
}
```

---

## 🐛 TROUBLESHOOTING

### "No veo video del otro"
```
1. ✓ Verifica código de sala coincida
2. ✓ Verifica permisos de cámara: Settings → Site settings → Camera
3. ✓ Intenta en otra pestaña
4. ✓ Reinicia navegador
5. ✓ Verifica firewall no bloquee puertos
```

### "Audio con lag/retraso"
```
1. ✓ Reduce resolución (720p → 360p)
2. ✓ Cierra otras aplicaciones usando internet
3. ✓ Verifica conexión WiFi (mejor si es Ethernet)
4. ✓ Usa otro navegador (Chrome es óptimo)
```

### "Video pixelado/cortado"
```
1. ✓ Aumenta ancho banda (reduce otras apps)
2. ✓ Cambia a resolución más baja (1080p → 720p)
3. ✓ Acércate al router WiFi
4. ✓ Usa cable Ethernet si es posible
```

### "No funciona en OBS"
```
1. ✓ Verifica URL correcta: ?mode=obs&room=CODIGO
2. ✓ Guest debe estar conectado ANTES de iniciar OBS source
3. ✓ Usa navegador Chromium (mejor compatibilidad)
4. ✓ Permisos de cámara en Windows: Settings → Privacy → Camera
```

---

## 📊 ESTADÍSTICAS DE RED

### Consumo de Datos Típico
```
Resolución | Bitrate | Datos/min | Datos/hora
-----------|---------|-----------|----------
360p       | 1 Mbps  | 7.5 MB    | 450 MB
720p       | 2.5 Mbps| 18.75 MB  | 1.1 GB
1080p      | 5 Mbps  | 37.5 MB   | 2.2 GB
```

### Latencia Esperada
```
WiFi local:     50-100ms
Internet local: 100-200ms
Internet remoto: 200-500ms
Aceptable:      <400ms
No aceptable:   >600ms
```

---

## 🔒 PRIVACIDAD Y SEGURIDAD

### Datos Transmitidos
- ✓ Video (Encriptado en WebRTC)
- ✓ Audio (Encriptado en WebRTC)
- ✓ Código de sala (Público en URL)
- ✓ Estado (Público en MQTT)

### Recomendaciones
- ✓ Usar HTTPS siempre (no HTTP)
- ✓ Cambiar código de sala regularmente
- ✓ Usar contraseña en MQTT si es acceso remoto
- ✓ Limitar acceso por firewall
- ✓ Desconectar cuando no uses

### Encriptación
```
✓ WebRTC P2P:   DTLS-SRTP (automático)
✓ MQTT:         WSS/TLS (si es wss://)
✓ Entre peers:   Encriptada punto-a-punto
✓ Broker MQTT:   Ve mensajes sin cifrar
```

---

## 🎓 MODO EDUCATIVO

### Ventajas sobre Zoom/Meet
- ✓ Sin límites de usuarios
- ✓ Bajo latencia (P2P directo)
- ✓ Controlable completamente
- ✓ Gratuito (open source)
- ✓ Personalizable

### Desventajas
- ✗ No tiene grabación built-in
- ✗ No tiene chat de texto
- ✗ Requiere TURN para NAT simétrico
- ✗ Sin email/verificación

---

## 📚 REFERENCIAS TÉCNICAS

- [WebRTC.org](https://webrtc.org/)
- [PeerJS Documentation](https://peerjs.com/)
- [MQTT Protocol](https://mqtt.org/)
- [RFC 5245 - ICE](https://tools.ietf.org/html/rfc5245)

---

**Última actualización:** 2026-04-29
**Versión:** 1.0
