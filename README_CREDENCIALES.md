# 🔐 GUÍA DE CAMBIO DE CREDENCIALES

## ⚠️ CREDENCIALES ACTUALES EXPUESTAS

### 1. TURN Server (pptturn.html)
```
Servidor:   140.82.25.249:3478
Usuario:    reportero
Contraseña: mundial2026
```

---

## 📝 CÓMO MODIFICAR LAS CREDENCIALES

### OPCIÓN 1: Cambio Directo en el Archivo (Simple)

#### Archivo: `streventos/pptturn.html`

**Busca esta sección:**
```javascript
TURN_SERVERS = [
    {
        urls: 'turn:140.82.25.249:3478',
        username: 'reportero',
        credential: 'mundial2026'
    },
    {
        urls: 'turn:140.82.25.249:3478?transport=tcp',
        username: 'reportero',
        credential: 'mundial2026'
    }
]
```

**Reemplaza por:**
```javascript
TURN_SERVERS = [
    {
        urls: 'turn:TU_IP_O_DOMINIO:3478',
        username: 'TU_USUARIO',
        credential: 'TU_CONTRASEÑA'
    },
    {
        urls: 'turn:TU_IP_O_DOMINIO:3478?transport=tcp',
        username: 'TU_USUARIO',
        credential: 'TU_CONTRASEÑA'
    }
]
```

**Ejemplo:**
```javascript
TURN_SERVERS = [
    {
        urls: 'turn:turnserver.micompany.com:3478',
        username: 'operador2026',
        credential: 'MiContraseña123Segura!'
    },
    {
        urls: 'turn:turnserver.micompany.com:3478?transport=tcp',
        username: 'operador2026',
        credential: 'MiContraseña123Segura!'
    }
]
```

---

### OPCIÓN 2: Cambio de MQTT Broker

#### Archivos afectados: TODOS los que usan MQTT
- `51933847353.html`
- `baradero.html`
- `hub-video.html`
- `call/index.html`
- `thn/index.html`
- Y otros...

**Busca:**
```javascript
const MQTT_BROKER = 'wss://broker.emqx.io:8084/mqtt';
// O
const MQTT_CONFIG = { host: 'broker.emqx.io', port: 8084, path: '/mqtt' };
```

**Reemplaza por tu broker:**
```javascript
// Opción A: Mosquitto en tu servidor
const MQTT_BROKER = 'wss://mqtt.micompany.com:8084/mqtt';

// Opción B: Broker comercial
const MQTT_BROKER = 'wss://broker.tu-proveedor.io:8083/mqtt';

// Opción C: Con autenticación
const MQTT_CONFIG = { 
    host: 'mqtt.micompany.com',
    port: 8084,
    path: '/mqtt',
    username: 'usuario_mqtt',
    password: 'contraseña_mqtt'
};
```

---

### OPCIÓN 3: Cambio de PeerJS Server

#### Cambiar servidor P2P (Menos Común)

**Busca en archivos:**
```javascript
const peer = new Peer(myPeerId, PEER_CONFIG);
// O
const PEER_CONFIG = { host: '0.peerjs.com', port: 443 }
```

**Para usar servidor propio:**
1. Instala PeerJS Server:
```bash
npm install -g peerjs-server
peerjs --port 9000
```

2. Reemplaza en archivos:
```javascript
PEER_CONFIG = {
    host: 'tuserver.com',
    port: 9000,
    path: '/'
}
```

---

### OPCIÓN 4: Cambio de STUN Servers

#### Para mejorar conectividad P2P

**Busca:**
```javascript
'iceServers': [
    { urls: 'stun:stun.l.google.com:19302' },
    { urls: 'stun:stun1.l.google.com:19302' }
]
```

**Reemplaza por otros STUN públicos:**
```javascript
'iceServers': [
    { urls: 'stun:stun.l.google.com:19302' },
    { urls: 'stun:stun1.l.google.com:19302' },
    { urls: 'stun:stun2.l.google.com:19302' },
    { urls: 'stun:stun3.l.google.com:19302' },
    { urls: 'stun:stun4.l.google.com:19302' }
]
```

**O servidores alternativos:**
```javascript
'iceServers': [
    { urls: 'stun:stun.stunprotocol.org:3478' },
    { urls: 'stun:stun.xten.com:3478' },
    { urls: 'stun:stun.sipgate.net:3478' }
]
```

---

## 🔄 CÓMO CAMBIAR EN TODOS LOS ARCHIVOS A LA VEZ

### Script de Reemplazo Global (PowerShell)

```powershell
# Cambiar MQTT Broker en todos los archivos
$old = "wss://broker.emqx.io:8084/mqtt"
$new = "wss://mqtt.micompany.com:8084/mqtt"

Get-ChildItem -Path "d:\stream-tropa" -Filter "*.html" -Recurse | ForEach-Object {
    (Get-Content $_.FullName) -replace [regex]::Escape($old), $new | Set-Content $_.FullName
}

Write-Host "✅ MQTT broker actualizado globalmente"
```

### Script para TURN Server

```powershell
# Cambiar TURN credentials
$old_user = "reportero"
$new_user = "tu_usuario"

$old_pass = "mundial2026"
$new_pass = "tu_contraseña_nueva"

Get-ChildItem -Path "d:\stream-tropa" -Filter "*.html" -Recurse | ForEach-Object {
    $content = Get-Content $_.FullName
    $content = $content -replace [regex]::Escape($old_user), $new_user
    $content = $content -replace [regex]::Escape($old_pass), $new_pass
    Set-Content -Path $_.FullName -Value $content
}

Write-Host "✅ Credenciales TURN actualizadas globalmente"
```

---

## ✅ VERIFICACIÓN POST-CAMBIO

### Verificar cambios realizados:

```powershell
# Ver todos los MQTT brokers definidos
Select-String -Path "d:\stream-tropa\**\*.html" -Pattern "mqtt.*emqx|MQTT_BROKER" -Recurse

# Ver credenciales TURN
Select-String -Path "d:\stream-tropa\**\*.html" -Pattern "username|credential" -Recurse

# Ver PEER_CONFIG
Select-String -Path "d:\stream-tropa\**\*.html" -Pattern "PEER_CONFIG|0.peerjs.com" -Recurse
```

---

## 🛠️ CONFIGURACIONES RECOMENDADAS

### Para Ambiente Local (Testing)
```javascript
// MQTT: Mosquitto en localhost
MQTT_BROKER = 'wss://localhost:8084/mqtt'

// PeerJS: Servidor local
PEER_CONFIG = { host: 'localhost', port: 9000 }

// STUN: Google (mantener)
'iceServers': [{ urls: 'stun:stun.l.google.com:19302' }]
```

### Para Producción (Empresa)
```javascript
// MQTT: Servidor propio
MQTT_BROKER = 'wss://mqtt.micompany.com:8084/mqtt'
// Con autenticación
clientId: `app_${Date.now()}`,
username: 'app_streaming',
password: 'GenerarContraseñaSegura123!ABC'

// PeerJS: Servidor propio
PEER_CONFIG = { host: 'peerjs.micompany.com', port: 443 }

// STUN: Múltiples servidores
'iceServers': [
    { urls: 'stun:stun.l.google.com:19302' },
    { urls: 'stun:stun.micompany.com:3478' },
    { urls: 'turn:turn.micompany.com:3478', username: 'appuser', credential: 'pass' }
]
```

### Para Nube (AWS/Azure/GCP)
```javascript
// MQTT: Broker SaaS
MQTT_BROKER = 'wss://mqtt-broker.azure.com:8084/mqtt'

// PeerJS: CDN
PEER_CONFIG = { host: 'peerjs.example.com', port: 443 }

// STUN/TURN: Servidores SaaS (Twilio, AWS, etc)
'iceServers': [
    { urls: 'stun:stun.twilio.com:3478' },
    { 
        urls: 'turn:turn.twilio.com:3478',
        username: 'tu-account-sid',
        credential: 'tu-auth-token'
    }
]
```

---

## 📋 CHECKLIST DE SEGURIDAD

- [ ] Cambiar credenciales TURN de `reportero/mundial2026`
- [ ] Cambiar MQTT Broker a servidor propio si es producción
- [ ] Usar HTTPS/WSS (no HTTP)
- [ ] Agregar autenticación MQTT si es acceso remoto
- [ ] Usar contraseñas complejas (min 16 caracteres)
- [ ] Limitar acceso por firewall/IP
- [ ] Rotar credenciales cada 90 días
- [ ] Monitorear logs de conexión
- [ ] Usar certificados SSL válidos

---

## 🆘 TROUBLESHOOTING

### "No puedo conectarme al servidor MQTT"
```
1. Verificar URL en código: ✓
2. Verificar puerto (8084/8083): ✓
3. Verificar WSS/MQTT: ✓
4. Verificar firewall: ✓
5. Verificar DNS: ✓
```

### "No puedo conectarme al TURN Server"
```
1. Verificar IP/Dominio: ✓
2. Verificar puerto (3478): ✓
3. Verificar credenciales: ✓
4. Verificar que TURN esté habilitado en router: ✓
5. Probar con: $ turnutils_stunclient IP 3478
```

### "PeerJS no conecta"
```
1. Verificar host es accesible: ✓
2. Verificar puerto 443 abierto: ✓
3. Verificar certificado SSL válido: ✓
4. Verificar STUN servers funcionan: ✓
```

---

## 📚 RECURSOS ÚTILES

- [MQTT.org - Brokers Públicos](https://mqtt.org/software/brokers/public)
- [PeerJS - Deploy propio](https://github.com/peers/peerjs-server)
- [TURN Servers públicos](https://gist.github.com/zziuni/3741933)
- [Verificar STUN](https://www.3cx.com/pbx/test-stun-server/)

---

**Última actualización:** 2026-04-29
**Versión:** 1.0
