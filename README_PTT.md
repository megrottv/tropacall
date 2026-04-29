# 📡 COMUNICACIÓN PTT (PUSH-TO-TALK) - GUÍA COMPLETA

## Aplicaciones Incluidas
- `test.html` - StreamTalk V9.0 (Pocket Mode)
- `talktotalk.html` - StreamTalk V9.0 (Full)
- `talkok.html` - StreamTalk V9.1 (Listen Only)

---

## 🎯 QUÉ ES PTT

**Push-To-Talk (PTT)** es un sistema de comunicación tipo **walkie-talkie** donde:
- **Un usuario habla** (presiona botón)
- **Todos escuchan** (reciben audio)
- **Alternancia** (no simultáneo)
- **Claridad** (mejor que radios tradicionales)

**Casos de uso:**
- Equipo de producción en TV
- Coordinación en eventos en vivo
- Comunicación de seguridad
- Retransmisión de noticias

---

## 🚀 INICIO RÁPIDO

### Setup Básico: 1 Director + 6 Crew

1. **En navegador del DIRECTOR:**
   ```
   http://localhost:8000/test.html
   ```
   - Se generan 6 botones: CAM 1, CAM 2, CAM 3, CAM 4, SONIDO, PISO
   - Click en cualquiera = envía audio al crew
   - No recibe audio del crew

2. **En navegadores de CREW (3-6 personas):**
   ```
   http://localhost:8000/talkok.html
   ```
   - Ven estado conectado
   - Escuchan automáticamente
   - No pueden transmitir

**¡Resultado:** Walkie-talkie funcionando ✅

---

## 🎛️ INTERFAZ USUARIO

### Panel Director (test.html)
```
┌────────────────────────────────┐
│  StreamTalk V9.0               │
│  ──────────────────────────────│
│  DIRECCION DE AUDIO            │
│                                │
│  ┌──────┐ ┌──────┐ ┌──────┐   │
│  │ CAM1 │ │ CAM2 │ │ CAM3 │   │
│  └──────┘ └──────┘ └──────┘   │
│  ┌──────┐ ┌──────┐ ┌──────┐   │
│  │ CAM4 │ │SONIDO│ │ PISO │   │
│  └──────┘ └──────┘ └──────┘   │
│                                │
│  Estado: 🟢 CONECTADO          │
│  Crew activos: 4               │
└────────────────────────────────┘
```

### Panel Crew (talkok.html)
```
┌────────────────────────────────┐
│  StreamTalk V9.1 - LISTEN      │
│  ──────────────────────────────│
│  DIRECTOR TRANSMITIENDO        │
│                                │
│  📡 Escuchando...              │
│  🎤 Micrófono: Habilitado      │
│  🔊 Volumen: ▰▰▰▰▰             │
│                                │
│  Estado: 🟢 CONECTADO          │
│  Última transmisión: 2s ago    │
└────────────────────────────────┘
```

### Panel Bidireccional (talktotalk.html)
```
┌────────────────────────────────┐
│  StreamTalk V9.0 - FULL        │
│  ──────────────────────────────│
│                                │
│  MODO DIRECTOR     │ MODO CREW │
│  ┌──────┐ ┌──────┐│┌────────┐ │
│  │ CAM1 │ │ CAM2 │││Escuchar│ │
│  └──────┘ └──────┘│└────────┘ │
│  ┌──────┐ ┌──────┐│┌────────┐ │
│  │ CAM3 │ │ CAM4 │││ Status │ │
│  └──────┘ └──────┘│└────────┘ │
│                                │
│  Estado: 🟢 ONLINE             │
│  Modo: DIRECTOR                │
└────────────────────────────────┘
```

---

## 📡 FLUJO DE COMUNICACIÓN

### Arquitectura P2P
```
Director
    │ (transmite audio)
    ├─ Crew 1 (escucha)
    ├─ Crew 2 (escucha)
    ├─ Crew 3 (escucha)
    ├─ Crew 4 (escucha)
    ├─ Crew 5 (escucha)
    └─ Crew 6 (escucha)
```

### Secuencia de Conexión
```
1. Crew inicia → Se conecta a PeerJS
2. Director inicia → Se conecta a PeerJS
3. Director presiona botón → Captura micrófono
4. Director transmite → Audio llega a todos
5. Crew recibe → Se reproduce automáticamente
6. Director suelta → Transmission termina
```

---

## 🎙️ FUNCIONAMIENTO DETALLADO

### Modo Director (test.html / talktotalk.html)
```
┌─────────────────────────────────┐
│ DIRECTOR - StreamTalk V9.0      │
├─────────────────────────────────┤
│ Funciones:                      │
│ ✓ Transmitir a crew (6 canales) │
│ ✓ Seleccionar canal con botones │
│ ✓ Ver estado de crew            │
│ ✓ Recibir confirmación de audio │
│ ✓ Alternancia entre canales     │
│                                 │
│ No puede:                       │
│ ✗ Escuchar crew                 │
│ ✗ Recibir audio                 │
│ ✗ Ver video                     │
└─────────────────────────────────┘
```

**Canales disponibles:**
```
1. CAM 1      → Cámara frontal
2. CAM 2      → Cámara lateral
3. CAM 3      → Cámara B
4. CAM 4      → Cámara C
5. SONIDO     → Ingeniero de sonido
6. PISO       → Asistente de piso
```

### Modo Crew Listen-Only (talkok.html)
```
┌─────────────────────────────────┐
│ CREW - StreamTalk V9.1          │
├─────────────────────────────────┤
│ Funciones:                      │
│ ✓ Escuchar transmisiones        │
│ ✓ Ver indicador de transmisión  │
│ ✓ Ajustar volumen               │
│ ✓ Status de conexión            │
│                                 │
│ No puede:                       │
│ ✗ Transmitir                    │
│ ✗ Cambiar canal                 │
│ ✗ Interrumpir director          │
└─────────────────────────────────┘
```

### Modo Bidireccional (talktotalk.html con role=crew)
```
┌─────────────────────────────────┐
│ CREW BIDIRECCIONAL              │
├─────────────────────────────────┤
│ Funciones:                      │
│ ✓ Escuchar director (pasivo)    │
│ ✓ Transmitir al director        │
│ ✓ Cambiar entre RX/TX           │
│ ✓ Confirmación de recepción     │
│                                 │
│ Casos:                          │
│ • Comunicación de doble vía      │
│ • Feedback en vivo              │
│ • Coordinación en tiempo real   │
└─────────────────────────────────┘
```

---

## 🎚️ CONTROLES Y AJUSTES

### Botones del Director
```
CAM 1-4     → Selecciona destinatario
SONIDO      → Habla al ingeniero
PISO        → Habla al asistente
            → Presionar = transmitir
            → Soltar = detener
```

### Panel del Crew
```
🔊 Volumen  → +/- para ajustar
🎤 Mic      → Muteado/Habilitado
📡 Status   → Conectado/Desconectado
🕐 Timer    → Tiempo desde última TX
```

---

## 🔊 CALIDAD DE AUDIO

### Configuración de Audio
```javascript
// Captura desde micrófono
{
    audio: {
        echoCancellation: true,     // Quita eco
        noiseSuppression: true,     // Quita ruido
        autoGainControl: true       // Normaliza volumen
    }
}
```

### Recomendaciones
```
✓ Micrófono profesional (USB)
✓ Auriculares sin micrófono (loop feedback)
✓ Sin otros audios reproduciendo
✓ Habitación silenciosa
✓ Latencia: <200ms aceptable
```

### Problemas de Audio Comunes
```
Eco/Feedback    → Usar auriculares
Silencio        → Verificar micrófono habilitado
Distorsión      → Alejarse del micrófono
Retraso         → Cerrar otras apps
Ruido fondo     → Activar noiseSuppression
```

---

## 🌐 ARQUITECTURA TÉCNICA

### Tecnologías
```
PeerJS 1.5.2    → Llamadas VoIP P2P
WebRTC          → Audio bidireccional
React 18        → UI
Babel           → Transpilación JSX
```

### Flujo de Datos
```
Micrófono
    ↓
getUserMedia()
    ↓
Encode audio
    ↓
PeerJS.call()
    ↓
Network P2P
    ↓
Decode audio
    ↓
Altavoz/Headphones
```

### Conexión P2P
```
ID Director: "ptt_director_{ROOM}"
ID Crew:     "ptt_crew_{ROOM}_{INDEX}"

Cuando Director presiona botón:
  1. Captura micrófono
  2. Abre llamada P2P a cada crew
  3. Transmite stream de audio
  4. Actualiza UI (Transmitiendo)

Cuando crew escucha:
  1. Recibe stream P2P
  2. Renderiza en altavoz
  3. Muestra indicador (Transmisión activa)
```

---

## 🚀 CONFIGURACIÓN AVANZADA

### Agregar Más Canales
**Archivo:** `test.html`

Busca:
```javascript
const roles = ['CAM 1', 'CAM 2', 'CAM 3', 'CAM 4', 'SONIDO', 'PISO'];
```

Reemplaza:
```javascript
const roles = [
    'CAM 1', 'CAM 2', 'CAM 3', 'CAM 4',  // 4 Cámaras
    'SONIDO', 'PISO',                    // Crew
    'DIRECCIÓN', 'CONTROL'               // Nuevos canales
];
```

### Cambiar STUN Server
**Archivo:** Todos

Busca:
```javascript
'iceServers': [{ urls: 'stun:stun.l.google.com:19302' }]
```

Reemplaza:
```javascript
'iceServers': [
    { urls: 'stun:stun.l.google.com:19302' },
    { urls: 'stun:stun1.l.google.com:19302' },
    { urls: 'stun:stun.xten.com:3478' }
]
```

### Ajustar Bitrate de Audio
```javascript
// Por defecto WebRTC ajusta automáticamente
// Para forzar bitrate:
const constraints = {
    audio: {
        echoCancellation: true,
        noiseSuppression: true,
        bitrate: 128000  // 128 kbps
    }
};
```

---

## 📊 CASOS DE USO REALES

### Caso 1: Transmisión TV en Vivo
```
Setup:
  - Director: laptop con 6 botones para canales
  - Crew: 6 personas con headphones
  - Conexión: WiFi 5GHz

Flujo:
  1. Director transmite: "En 10 segundos cámara 2"
  2. Op Cám 2 se prepara
  3. Director: "¡Cámara 2!" → Op Cám 2 activa
  4. Studio ve en vivo
  5. Director coordina cambios

Latencia: <100ms (tiempo real)
Usuarios: 7 (1 Director + 6 Crew)
```

### Caso 2: Event Coordinator
```
Setup:
  - Coordinador en mesa de control
  - 5 asistentes en piso
  - WiFi celular (4G/5G)

Flujo:
  1. Coordinador: "Asistentes, ¿listos?"
  2. Crew responde (bidireccional)
  3. Coordinador da instrucciones
  4. Crew confirma recepción

Latencia: 100-300ms
Escalabilidad: Hasta 20 usuarios
```

### Caso 3: Seguridad de Evento
```
Setup:
  - Centro de control (Director)
  - 8 guardias en puntos
  - Radiofrecuencia VoIP

Flujo:
  1. Guardia 3 reporta: "Situación anormal"
  2. Control recibe
  3. Control notifica resto de equipo
  4. Respuesta coordinada

Latencia crítica: <500ms
Redundancia: Dual path (WiFi + 4G)
```

---

## 🐛 TROUBLESHOOTING

### "No escucho nada"
```
1. ✓ Verifica conexión a internet
2. ✓ Verifica micrófono está habilitado
3. ✓ Verifica volumen no está al 0
4. ✓ Verifica dirección está transmitiendo
5. ✓ Recarga página (talkok.html)
```

### "Eco/Feedback"
```
1. ✓ Usa auriculares en lugar de altavoz
2. ✓ Aleja micrófono del altavoz
3. ✓ Baja volumen
4. ✓ Cierra otras llamadas de audio
```

### "Director no recibe la llamada"
```
1. ✓ Verifica PeerJS está conectado
2. ✓ Verifica STUN accesible
3. ✓ Recarga talkok.html
4. ✓ Verifica firewall permite puerto 443
```

### "Latencia muy alta (retraso)"
```
1. ✓ Usa WiFi 5GHz si disponible
2. ✓ Acércate al router
3. ✓ Cierra aplicaciones usando internet
4. ✓ Usa conexión cableada (Ethernet)
5. ✓ Verifica no hay ataques DDoS
```

---

## 🔒 PRIVACIDAD Y SEGURIDAD

### Datos Transmitidos
- ✓ Audio (encriptado en WebRTC)
- ✓ Código de sala (público)
- ✓ Estado de conexión

### Encriptación
```
WebRTC:     DTLS-SRTP (automático)
P2P:        Encriptación E2E
Broker:     Certificado SSL/TLS
```

### Recomendaciones
- ✓ Cambiar código de sala entre sesiones
- ✓ Usar HTTPS siempre
- ✓ Verificar identidad de crew
- ✓ Grabar con consentimiento previo
- ✓ Limitar acceso por red corporativa

---

## 📚 REFERENCIAS

- [WebRTC Audio](https://www.w3.org/TR/webrtc/)
- [PeerJS Calls](https://peerjs.com/docs/#api)
- [VoIP Standards](https://tools.ietf.org/html/rfc3550)

---

**Última actualización:** 2026-04-29
**Versión:** 1.0
