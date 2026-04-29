# 🎬 SPLITEO DE VIDEO & GRÁFICOS - GUÍA COMPLETA

## Aplicaciones Incluidas

### Spliteo (Mezcla de Video)
- `atem.html` - StreamSplitter V25 (Grilla 2x2)
- `strp/index.html` - Streamcall Power
- `strp/4g.html` - Optimizado 4G
- `strp/4ghn.html` - Con TURN Honduras

### Control de Gráficos
- `51933847353.html` - StreamCommand (QR, Cronómetro, Cards)
- `thn/index.html` - Zapping Master V12 (Noticias)

---

## 🎯 DESCRIPCIÓN GENERAL

### Spliteo de Video
Permite ver **múltiples fuentes de video simultáneamente** en:
- Grilla 2x2 (4 fuentes)
- Modo director (principal + miniatura)
- Modo limpio para OBS

### Control de Gráficos
Permite mostrar **elementos dinámicos** en transmisión:
- Códigos QR generados en vivo
- Cronómetros y timers
- Tarjetas de citas/noticias
- Alertas flash
- Gráficos de noticias

---

## 🚀 INICIO RÁPIDO - SPLITEO

### Escenario: Ver 4 Cámaras Simultáneamente

1. **Abrir maestro (atem.html):**
   ```
   http://localhost:8000/atem.html
   ```
   - Genera grilla 2x2
   - Panel flotante en inferior

2. **En 4 navegadores separados (cámaras):**
   ```
   http://localhost:8000/strp/index.html?mode=camera&slot=1
   http://localhost:8000/strp/index.html?mode=camera&slot=2
   http://localhost:8000/strp/index.html?mode=camera&slot=3
   http://localhost:8000/strp/index.html?mode=camera&slot=4
   ```

3. **OBS captura atem.html:**
   - Browser source → URL de atem.html
   - Captura grilla 2x2 limpia

**¡Resultado:** 4 cámaras en pantalla dividida ✅

### Escenario Principal: Stream Call 3 Cámaras + Audio + StreamCommand

1. **Abrir control gráfico (StreamCommand):**
    ```
    http://localhost:8000/51933847353.html
    ```
    - QR, cronómetro, cards y avisos en vivo

2. **Levantar las 3 cámaras:**
    ```
    http://localhost:8000/strp/index.html?mode=camera&slot=1
    http://localhost:8000/strp/index.html?mode=camera&slot=2
    http://localhost:8000/strp/index.html?mode=camera&slot=3
    ```
    - Mantener audio activo en cada fuente

3. **Si la red móvil es inestable, usar la variante 4G:**
    ```
    http://localhost:8000/strp/4g.html
    ```
    - Pensado para operación liviana en Argentina

4. **Capturar el resultado final en OBS:**
    - Browser source → `atem.html` o el layout que corresponda
    - Combinar con el panel de StreamCommand según la producción

**Resultado:** Stream Call de 3 cámaras con audio, control gráfico separado y enfoque 4G ✅

---

## 🎛️ INTERFAZ USUARIO

### atem.html (StreamSplitter)
```
┌────────────────────────────────┐
│  ┌──────────┬──────────┐       │
│  │ VIDEO 1  │ VIDEO 2  │       │
│  │          │          │       │
│  ├──────────┼──────────┤       │
│  │ VIDEO 3  │ VIDEO 4  │       │
│  │          │          │       │
│  └──────────┴──────────┘       │
│                                │
│  ┌──────────────────────────┐  │
│  │ [UP] [DOWN] [LEFT][RIGHT]│  │
│  │ [SELECT] [MODE]          │  │
│  └──────────────────────────┘  │
└────────────────────────────────┘
```

### Controles Flotantes
```
┌─────────────────────────┐
│ 🎮 CONTROL PANEL        │
├─────────────────────────┤
│ ▲                       │
│◄───┼───►                │
│ ▼                       │
│ [SELECT] [CLEAN MODE]   │
│ [CALIBRATE]             │
└─────────────────────────┘
```

### 51933847353.html (StreamCommand)
```
┌─────────────────────────────────┐
│ StreamCommand Dashboard         │
├─────────────────────────────────┤
│                                 │
│ ┌─────────────────────────────┐ │
│ │  QR GENERATOR               │ │
│ │  URL: https://google.com    │ │
│ │  [MOSTRAR QR] [COPIAR URL]  │ │
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │  CRONÓMETRO                 │ │
│ │  00:05:23                   │ │
│ │  [START] [STOP] [RESET]     │ │
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │  CITA DESTACADA             │ │
│ │  \"La innovación...\"        │ │
│ │  - Gustavo Eppel            │ │
│ │  [MOSTRAR] [EDITAR]         │ │
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │  ALERTA FLASH               │ │
│ │  EN VIVO                    │ │
│ │  [ACTIVAR]                  │ │
│ └─────────────────────────────┘ │
│                                 │
└─────────────────────────────────┘
```

### thn/index.html (Zapping Master)
```
┌─────────────────────────────────┐
│ Zapping Master V12              │
├─────────────────────────────────┤
│                                 │
│ ◆ NOTICIA 1                     │
│   Títular principal             │
│   Animación: PULSE              │
│                                 │
│ ◇ NOTICIA 2                     │
│   Subtítulo                     │
│   Estado: Esperando             │
│                                 │
│ [ADD NEWS] [CLEAR] [AUTO MODE]  │
│ [SPEED: NORMAL]                 │
│                                 │
└─────────────────────────────────┘
```

---

## 📡 FUNCIONAMIENTO DETALLADO

### Spliteo - Flujo de Video
```
Cámara 1 ─┐
          │
Cámara 2 ─┤   ATEM.html (Mezclador)  ─→  OBS Capture  ─→  Transmisión
          │       ↓
Cámara 3 ─┤   Grilla 2x2
          │   (4 ventanas)
Cámara 4 ─┘
```

### Control de Gráficos - Arquitectura
```
Panel Principal (51933847353.html)
    ├─ QR Generator
    │   ├─ Entrada URL
    │   ├─ Genera QR automático
    │   └─ Overlay en URL
    │
    ├─ Timer/Cronómetro
    │   ├─ Startwatch/Countdown
    │   └─ Overlay en URL
    │
    ├─ Featured Card
    │   ├─ Cita + Autor
    │   └─ Overlay en URL
    │
    └─ Flash Alert
        ├─ Texto EN VIVO
        └─ Overlay pulsante

        Todos generan URLs separadas para OBS
```

---

## 🎚️ CASOS DE USO REALES

### Caso 1: Programa de TV Multi-Cámara
```
Setup:
  - ATEM.html: Mezclador central
  - 4 cámaras en strp/index.html
  - OBS captura ATEM limpio
  - Overlay adicional de cronómetro

Flujo:
  1. Inicio programa: Timer en 00:00:00
  2. Director elige cámara (click en grilla)
  3. Cambios en tiempo real
  4. Cada 10min: Card con slogan

Resultado: Programa multi-cámara profesional
```

### Caso 2: Noticiario Automatizado
```
Setup:
  - thn/index.html (Zapping Master)
  - 5 noticias cargadas
  - OBS captura como browser source
  - Auto-scroll cada 30s

Flujo:
  1. Sistema carga noticias
  2. Muestra cada 30 segundos
  3. Animación pulse
  4. Director puede adelantar/atrasar

Resultado: Gráficos dinámicos en vivo
```

### Caso 3: Presentación Interactiva
```
Setup:
  - 51933847353.html (StreamCommand)
  - QR para votación
  - Cronómetro para preguntas
  - Alertas flash para resultados

Flujo:
  1. Presentador muestra QR (audiencia vota)
  2. Timer de 2min
  3. Resultado: Flash \"¡VOTACIÓN CERRADA!\"
  4. Muestra cita motivacional
  5. Siguiente pregunta

Resultado: Presentación dinámica + engagement
```

---

## 🔧 CONFIGURACIÓN AVANZADA

### Cambiar Modo de Grilla
**Archivo:** `atem.html`

Busca:
```javascript
const gridConfig = { columns: 2, rows: 2 }; // Grilla 2x2
```

Reemplaza por:
```javascript
// Opción 1: Grilla 2x3 (6 fuentes)
const gridConfig = { columns: 2, rows: 3 };

// Opción 2: Grilla 3x3 (9 fuentes)
const gridConfig = { columns: 3, rows: 3 };

// Opción 3: Modo maestro (1 grande + 3 mini)
const gridConfig = { 
    type: 'master',
    main: { w: 0.7, h: 1.0 },
    pips: [{ w: 0.3, h: 0.33 }, { w: 0.3, h: 0.33 }, { w: 0.3, h: 0.33 }]
};
```

### Agregar más Noticias
**Archivo:** `thn/index.html`

Busca:
```javascript
const newsArray = [
    { title: 'NOTICIA 1', subtitle: 'Contenido...' },
    { title: 'NOTICIA 2', subtitle: 'Contenido...' }
];
```

Reemplaza:
```javascript
const newsArray = [
    { title: 'NOTICIA 1', subtitle: 'Contenido 1', type: 'rect' },
    { title: 'NOTICIA 2', subtitle: 'Contenido 2', type: 'capsule' },
    { title: 'NOTICIA 3', subtitle: 'Contenido 3', type: 'modern' },
    { title: 'NOTICIA 4', subtitle: 'Contenido 4', type: 'glass' },
    { title: 'NOTICIA 5', subtitle: 'Contenido 5', type: 'rect' }
];
```

### Tipos de Animación
```javascript
// thn/index.html - Estilos disponibles
{
    type: 'rect',          // Rectángulo simple
    type: 'capsule',       // Cápsula redondeada
    type: 'modern',        // Moderno con degradado
    type: 'glass',         // Glassmorphism
    animation: 'pulse',    // Pulse glow
    animation: 'radar',    // Radar sweep
    animation: 'slide'     // Slide in
}
```

### Cambiar Duración de Timer
**Archivo:** `51933847353.html`

Busca:
```javascript
const initialState = {
    timer: { visible: false, label: "TIEMPO RESTANTE", mode: "stopwatch", running: false }
};
```

Para countdown con duración:
```javascript
const initialState = {
    timer: { 
        visible: false, 
        label: "TIEMPO RESTANTE", 
        mode: "countdown",  // Cambia a countdown
        duration: 300,      // 5 minutos (en segundos)
        running: false 
    }
};
```

---

## 🎨 PERSONALIZACIÓN VISUAL

### Cambiar Colores de Grilla
**Archivo:** `atem.html`

```css
/* Busca */
.cell {
    background: #111; 
    border: 1px dashed #444;
}

/* Reemplaza */
.cell {
    background: #1a1a1a;  /* Más oscuro */
    border: 2px solid #666;  /* Borde más visible */
}

.cell.selected {
    border: 3px solid #ff6600;  /* Naranja en selección */
}
```

### Cambiar Colores de Noticias
**Archivo:** `thn/index.html`

```css
/* Busca */
.news-box.rect {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Reemplaza */
.news-box.rect {
    background: linear-gradient(135deg, #ff6b6b 0%, #ff8e53 100%);  /* Rojo-naranja */
}
```

---

## 📊 CONSUMO DE RECURSOS

### Spliteo (ATEM)
```
Resolución: 1920x1080 (4 videos 960x540)
Bitrate:    ~8-10 Mbps
CPU:        15-25% (RTX 2060+)
RAM:        500-800 MB
Red:        WiFi 5GHz recomendado
```

### Gráficos (Zapping)
```
Resolución: 1920x1080
Bitrate:    ~500 Kbps (solo gráficos)
CPU:        5-10%
RAM:        200-300 MB
Red:        3G+ suficiente
```

---

## 🐛 TROUBLESHOOTING

### "Videos no aparecen en grilla"
```
1. ✓ Verifica cámaras están conectadas
2. ✓ Verifica slots son accesibles
3. ✓ Recarga página (atem.html)
4. ✓ Verifica permisos de cámara
```

### "Gráficos se ven pixelados"
```
1. ✓ Aumenta resolución de fuente
2. ✓ Verifica zoom no está reducido
3. ✓ Recarga página
4. ✓ Usa resolución 1080p
```

### "Timer no se ve en OBS"
```
1. ✓ Verifica URL con ?mode=overlay
2. ✓ Verifica browser source en OBS
3. ✓ Clickea en OBS source para activar
4. ✓ Aumenta tamaño del source
```

### "Noticias no cambian automáticamente"
```
1. ✓ Verifica auto-mode está activado
2. ✓ Verifica duración está configurada
3. ✓ Abre consola (F12) para errores
4. ✓ Recarga página
```

---

## 🔒 PRIVACIDAD

### Datos en URL
```
URLs públicas para gráficos:
- ?mode=overlay&module=qr
- ?mode=overlay&module=timer
- ?mode=overlay&module=card

⚠️ Cualquiera con la URL puede ver el gráfico
✓ Cambiar URL regularmente si es sensible
```

---

## 📚 REFERENCIAS

- [Grid CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [React Animations](https://react.dev/reference/react-dom/components/common#react-event-handler)
- [WebRTC Video Rendering](https://www.w3.org/TR/webrtc/#dom-rtcpeerconnection)

---

**Última actualización:** 2026-04-29
**Versión:** 1.0
