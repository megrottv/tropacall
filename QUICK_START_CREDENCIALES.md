# ⚡ GUÍA RÁPIDA - CAMBIAR TUS CREDENCIALES

## 🎯 OBJETIVO
Reemplazar las credenciales actuales de Stream-Tropa por las tuyas propias en **5-10 minutos**.

---

## 📋 ANTES DE EMPEZAR

**Prepara esta información:**

```
MQTT:
  ☐ URL/IP: _______________
  ☐ Puerto: _______________
  ☐ Usuario: _______________
  ☐ Contraseña: _______________

TURN Server:
  ☐ IP/Dominio: _______________
  ☐ Puerto: _______________
  ☐ Usuario: _______________
  ☐ Contraseña: _______________

PeerJS (Opcional):
  ☐ Host: _______________
  ☐ Puerto: _______________
```

---

## 🚀 MÉTODO RÁPIDO (5 minutos)

### Opción A: Cambiar MQTT Broker Globalmente

1. **Abre PowerShell** en carpeta `d:\stream-tropa`

2. **Copia y ejecuta este comando:**
```powershell
$old = "wss://broker.emqx.io:8084/mqtt"
$new = "wss://TU_SERVIDOR:8084/mqtt"

Get-ChildItem -Path . -Filter "*.html" -Recurse | ForEach-Object {
    (Get-Content $_.FullName) -replace [regex]::Escape($old), $new | Set-Content $_.FullName
}

Write-Host "✅ MQTT actualizado: $old -> $new"
```

3. **Reemplaza:**
   - `TU_SERVIDOR` por tu host/IP real
   - `8084` por tu puerto (si es diferente)

4. **¡Listo!** Todos los archivos usan tu MQTT

---

### Opción B: Cambiar TURN Server (pptturn.html)

1. **Abre** `streventos/pptturn.html` con editor de texto

2. **Busca:**
```
username: 'reportero'
credential: 'mundial2026'
140.82.25.249
```

3. **Reemplaza por:**
```
username: 'TU_USUARIO'
credential: 'TU_CONTRASEÑA'
TU_IP_O_DOMINIO
```

**Ejemplo:**
```javascript
// ANTES
{
    urls: 'turn:140.82.25.249:3478',
    username: 'reportero',
    credential: 'mundial2026'
}

// DESPUÉS
{
    urls: 'turn:turnserver.micompany.com:3478',
    username: 'operador2026',
    credential: 'MiPass123Segura!'
}
```

4. **Guarda archivo** (Ctrl+S)

---

## ✅ VERIFICAR CAMBIOS

**Abre PowerShell** y ejecuta:

```powershell
# Ver MQTT brokers definidos
Select-String -Path "**\*.html" -Pattern "mqtt|MQTT_BROKER" -Recurse | Select-Object Path, Line

# Ver credenciales TURN
Select-String -Path "**\*.html" -Pattern "username|credential|140.82" -Recurse | Select-Object Path, Line

# Ver PEER_CONFIG
Select-String -Path "**\*.html" -Pattern "PEER_CONFIG|0.peerjs.com" -Recurse | Select-Object Path, Line
```

**Verifica:**
- ✓ No aparezca `emqx.io` (si cambiaste MQTT)
- ✓ Aparezca tu servidor
- ✓ Desaparezcan credenciales antiguas

---

## 🧪 PROBAR LOS CAMBIOS

### Test 1: MQTT
```
1. Abre http://localhost:8000/hub-video.html
2. Abre Browser Console (F12)
3. Deberías ver: "MQTT Conectado" (verde)
4. Si falla: rojo error
```

### Test 2: TURN
```
1. Abre http://localhost:8000/streventos/pptturn.html
2. Intenta conectar desde dos navegadores diferentes
3. Verifica que se establezca conexión P2P
4. Prueba video/audio bidireccional
```

### Test 3: Integración
```
1. Abre hub-video.html
2. Copia código de sala
3. Abre en otra pestaña con mismo código
4. Presiona INICIAR TRANSMISIÓN
5. Verifica que aparezca video remoto
```

---

## 📝 LISTA DE ARCHIVOS IMPORTANTES

**Contienen configuraciones:**
```
51933847353.html          → MQTT
atem.html                 → (Sin config sensible)
baradero.html            → MQTT, PEER
call/index.html          → MQTT, PEER
hub-video.html           → MQTT, PEER
strp/index.html          → PEER
streventos/pptturn.html  → TURN (⚠️ IMPORTANTE)
thn/index.html           → MQTT
```

---

## 🔧 CAMBIOS AVANZADOS (Opcional)

### Cambiar PeerJS Server Propio

**En todos los archivos, busca:**
```javascript
PEER_CONFIG = { host: '0.peerjs.com', port: 443 }
```

**Reemplaza por:**
```javascript
PEER_CONFIG = { 
    host: 'tuserver.com',     // Tu dominio
    port: 9000,              // Tu puerto
    path: '/'
}
```

---

### Agregar Autenticación MQTT

**En archivos que usan MQTT, busca:**
```javascript
mqtt.connect(MQTT_BROKER)
```

**Reemplaza por:**
```javascript
mqtt.connect(MQTT_BROKER, {
    username: 'mi_usuario',
    password: 'mi_contraseña',
    clientId: `app_${Date.now()}`
})
```

---

### Usar HTTPS/WSS

**Todos los archivos:**

**Busca:**
```javascript
'wss://broker.emqx.io'
'http://localhost'
```

**Reemplaza por:**
```javascript
'wss://broker.seguro.com'  // WebSocket Seguro
'https://localhost'         // HTTPS
```

---

## 🆘 SI ALGO FALLA

### "Los cambios no funcionan"

**Checklist:**
```
☐ ¿Guardaste el archivo? (Ctrl+S)
☐ ¿Recargaste página? (Ctrl+Shift+R)
☐ ¿Limpió caché? (Settings → Clear cache)
☐ ¿Servidor nuevo está online?
☐ ¿Credenciales son correctas?
☐ ¿Firewall permite conexión?
☐ ¿Puerto es accesible?
```

### "Puedo ver el cambio pero no conecta"

```
1. Abre Console (F12)
2. Busca errores en rojo
3. Copia el error completo
4. Verifica:
   - URL correcta
   - Puerto correcto
   - Credenciales correctas
   - Servidor online
   - Firewall abierto
```

### "¿Cómo revierto los cambios?"

```
Opción 1: Git
  git checkout <archivo>

Opción 2: Reemplazar todo
  $old = "tu_servidor"
  $new = "broker.emqx.io:8084/mqtt"
  Get-ChildItem -Path . -Filter "*.html" -Recurse | ...

Opción 3: Restaurar desde backup
  (Si tienes backup)
```

---

## 📞 OBTENER CREDENCIALES

### Broker MQTT Público
```
Broker:     broker.emqx.io
Puerto:     8084 (WebSocket)
Usuario:    (ninguno)
Contraseña: (ninguno)
```

### Broker MQTT Gratuito
```
HiveMQ:     broker.hivemq.com:8884
Mosquitto:  test.mosquitto.org:8884
Insomnia:   broker.insomnia.im:8884
```

### TURN Server Público
```
Google:     stun.l.google.com:19302
Twilio:     global.stun.twilio.com:3478
Xten:       stun.xten.com:3478
```

### TURN Server Gratuito con Credenciales
```
WebRTC Samples:
  https://webrtc.github.io/samples/
```

### Crear tu propio TURN Server

**Ubuntu/Debian:**
```bash
sudo apt-get install coturn

# Configurar /etc/coturn/turnserver.conf
echo "user=mi_usuario:mi_contraseña" >> /etc/coturn/turnserver.conf

# Iniciar
sudo systemctl start coturn
```

---

## ✨ BUENAS PRÁCTICAS

### Contraseñas Seguras
```
✓ Mínimo 16 caracteres
✓ Mayúsculas + minúsculas
✓ Números + símbolos
✓ No reutilizar en otros servicios
✓ Cambiar cada 90 días

Generador: https://www.password-generator.com/
```

### Cambio Regular
```
Recomendación: cada 90 días
Proceso:
  1. Generar nuevas credenciales
  2. Actualizar en archivos (este procedimiento)
  3. Verificar en console
  4. Documentar cambio y fecha
```

### Documentación
```
Mantén archivo CREDENCIALES_BACKUP.txt (encriptado):
  Broker MQTT: [IP] [Puerto] [Usuario] [Pass] [Fecha]
  TURN Server: [IP] [Puerto] [Usuario] [Pass] [Fecha]
  PeerJS:      [Host] [Puerto] [Fecha]
```

---

## 🎓 PRÓXIMOS PASOS

Después de cambiar credenciales:

1. **Prueba:** Sigue los tests de la sección "PROBAR LOS CAMBIOS"
2. **Documenta:** Guarda credenciales en lugar seguro
3. **Monitorea:** Observa logs del servidor nuevo
4. **Comunica:** Avisa al equipo sobre cambios
5. **Backup:** Haz copia de archivos actualizados

---

## 📚 MÁS INFORMACIÓN

- Detalles técnicos: [README_CREDENCIALES.md](README_CREDENCIALES.md)
- Configuración general: [README_GENERAL.md](README_GENERAL.md)
- Troubleshooting: Cada README específico
- Índice de docs: [INDICE.md](INDICE.md)

---

## ✅ CHECKLIST FINAL

```
☐ Identifiqué qué cambiar (MQTT/TURN/PeerJS)
☐ Preparé credenciales nuevas
☐ Ejecuté comandos PowerShell
☐ Verifiqué cambios (Select-String)
☐ Recargué páginas (Ctrl+Shift+R)
☐ Probé en Console (F12)
☐ Hice prueba de conexión
☐ Documenté cambios
☐ Backup de archivos
☐ Comunicé al equipo
```

---

**¡Listo! 🎉 Tus credenciales ahora son propias**

---

**Última actualización:** 2026-04-29
**Versión:** 1.0
