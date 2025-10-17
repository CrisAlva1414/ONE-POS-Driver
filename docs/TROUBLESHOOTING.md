# 🆘 Solución de Problemas

## 🚨 Problemas Comunes

### ❌ Error: "Impresora no encontrada"

#### Posibles Causas:
- Driver no instalado correctamente
- Puerto incorrecto
- Impresora apagada
- Cable defectuoso

#### Soluciones:
1. **Verificar alimentación**: LED de la impresora debe estar encendido
2. **Reinstalar driver**: Desinstalar y reinstalar como administrador
3. **Probar otro puerto**: USB diferente o cambiar cable
4. **Verificar en Administrador de dispositivos** (Windows)

### ❌ Error: "Puerto COM ocupado"

#### Solución en Windows:
```cmd
# Ver puertos en uso
netstat -an | findstr :9100

# Terminar proceso específico
taskkill /F /PID [numero_pid]
```

#### Solución en Linux:
```bash
# Ver procesos usando puerto serie
lsof /dev/ttyUSB0

# Liberar puerto
sudo killall -9 [nombre_proceso]
```

### ❌ Imprime caracteres extraños (ÿÿÿÿ, ��, etc.)

#### Causa: Codificación incorrecta
#### Soluciones:
1. **Cambiar codificación** a CP850 o UTF-8
2. **Configurar idioma** del sistema
3. **Verificar configuración** regional

```javascript
// Ejemplo de codificación correcta
const text = "Café con leche - $15.50";
const encoded = iconv.encode(text, 'cp850');
printer.send(encoded);
```

### ❌ No corta el papel automáticamente

#### Configuración manual:
1. **Herramienta de prueba** → Settings → Auto Cut
2. **Comando ESC/POS**: `GS V 0` (corte completo)
3. **Verificar** configuración de hardware

### ❌ IP de impresora cambia constantemente

#### Configurar IP estática:
1. **Acceder** panel web: `http://[ip_actual]`
2. **Network** → Static IP
3. **Configurar**:
   - IP: `192.168.1.100`
   - Máscara: `255.255.255.0`
   - Gateway: `192.168.1.1`

### ❌ Conexión WiFi intermitente

#### Diagnóstico:
```bash
# Probar conectividad
ping -c 10 192.168.1.100

# Verificar calidad de señal
iwconfig wlan0
```

#### Soluciones:
1. **Acercar** impresora al router
2. **Cambiar canal** WiFi (1, 6, 11)
3. **Actualizar** firmware de la impresora
4. **Usar frecuencia 2.4GHz** (más compatible)

## 🔧 Herramientas de Diagnóstico

### Windows - PowerShell
```powershell
# Test de conectividad avanzado
Test-NetConnection -ComputerName "192.168.1.100" -Port 9100 -InformationLevel Detailed

# Ver drivers instalados
Get-WmiObject Win32_SystemDriver | Where-Object {$_.Name -like "*pos*"}

# Información de puertos COM
Get-WmiObject Win32_SerialPort | Select-Object DeviceID, Description
```

### Linux - Terminal
```bash
# Información completa del sistema
sudo dmidecode

# Estado de puertos USB
lsusb -v

# Logs del sistema
sudo journalctl -f | grep -i printer

# Test de puerto de red
nmap -p 9100 192.168.1.100
```

### macOS - Terminal
```bash
# Información del sistema
system_profiler SPUSBDataType

# Estado de red
netstat -rn

# Logs del sistema
log show --predicate 'subsystem contains "printing"' --last 1h
```

## 📊 Códigos de Error Comunes

| Código | Descripción | Solución |
|--------|-------------|----------|
| 0x01 | Error de comunicación | Verificar conexión |
| 0x02 | Papel agotado | Cambiar rollo de papel |
| 0x03 | Tapa abierta | Cerrar tapa de la impresora |
| 0x04 | Temperatura alta | Esperar enfriamiento |
| 0x05 | Error de memoria | Reiniciar impresora |
| 0x06 | Comando inválido | Verificar sintaxis ESC/POS |

## 🛠️ Mantenimiento Preventivo

### Limpieza Regular
1. **Apagar** impresora y desconectar
2. **Limpiar** cabezal con alcohol isopropílico
3. **Remover** residuos de papel
4. **Verificar** sensores de papel

### Calibración
```bash
# Comando de auto-calibración
echo -e "\x1B\x40\x1D\x28\x4C\x02\x00\x30\x32" | nc 192.168.1.100 9100
```

### Actualización de Firmware
1. **Descargar** firmware del fabricante
2. **Usar herramienta** específica del modelo
3. **No interrumpir** proceso de actualización
4. **Verificar** versión después de actualizar

## 📞 Escalación de Soporte

### Información a Recopilar
Antes de contactar soporte técnico:

1. **Modelo exacto** de la impresora
2. **Sistema operativo** y versión
3. **Versión del driver** instalado
4. **Tipo de conexión** utilizada
5. **Mensaje de error** completo
6. **Pasos** que llevaron al problema
7. **Archivos de log** (si están disponibles)

### Generar Reporte de Sistema

#### Windows
```cmd
msinfo32 /report diagnostico.txt
dxdiag /t hardware.txt
ipconfig /all > red.txt
```

#### Linux
```bash
sudo lshw > hardware.txt
dmesg > kernel.txt
cat /var/log/syslog | grep printer > printer.log
```

#### macOS
```bash
system_profiler > sistema.txt
log show --last 1h > logs.txt
```

## 🔄 Reset de Fábrica

### Método 1: Botones Hardware
1. **Apagar** impresora
2. Mantener **FEED + POWER** por 10 segundos
3. **Soltar** botones cuando LED parpadee
4. **Esperar** reinicio automático

### Método 2: Comando Software
```bash
# Comando ESC/POS para reset
echo -e "\x1B\x40\x1D\x28\x45\x03\x00\x01\xFF\xFF" | nc [IP] 9100
```

### Método 3: Panel Web
1. **Acceder** a `http://[ip_impresora]`
2. **Settings** → Factory Reset
3. **Confirmar** operación
4. **Esperar** reinicio completo

## ⚡ Optimización de Rendimiento

### Configuración de Red
```bash
# Optimizar buffer TCP
echo 'net.core.rmem_max = 16777216' >> /etc/sysctl.conf
echo 'net.core.wmem_max = 16777216' >> /etc/sysctl.conf
```

### Configuración de Aplicación
```python
# Ejemplo de configuración optimizada
import socket

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
sock.setsockopt(socket.IPPROTO_TCP, socket.TCP_NODELAY, 1)
sock.settimeout(5.0)  # Timeout de 5 segundos
```

## 📋 Checklist de Verificación

### Antes de Reportar un Problema
- [ ] Impresora encendida y con papel
- [ ] Cable/conexión verificada
- [ ] Driver instalado correctamente
- [ ] Probado con herramienta oficial
- [ ] Reiniciado impresora y computadora
- [ ] Verificado configuración de red
- [ ] Consultado este documento
- [ ] Probado con otra aplicación

### Información de Contacto
Si después de seguir esta guía el problema persiste:
1. **Crear issue** en este repositorio
2. **Incluir** toda la información de diagnóstico
3. **Describir** pasos detallados para reproducir
4. **Adjuntar** capturas de pantalla si es relevante