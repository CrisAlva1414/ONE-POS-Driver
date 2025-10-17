# 🛠️ Guía de Desarrollo

## 📱 SDKs Disponibles

### Android
- **Archivo**: `Develop routine/Android SDK.zip`
- **Requisitos**: Android 5.0+ (API 21+)
- **Conexiones**: WiFi, Bluetooth, USB OTG

### iOS
- **Archivo**: `Develop routine/ios sdk.rar`
- **Requisitos**: iOS 10.0+
- **Conexiones**: WiFi, Bluetooth

### Windows
- **Archivo**: `Develop routine/windows SDK.rar`
- **Requisitos**: .NET Framework 4.5+
- **Conexiones**: USB, WiFi, Ethernet, Bluetooth

## 📋 Comandos ESC/POS Básicos

### Inicialización
```
ESC @ - Inicializar impresora
```

### Texto
```
ESC a 0 - Alinear izquierda
ESC a 1 - Centrar
ESC a 2 - Alinear derecha
```

### Formato
```
ESC ! 0x00 - Texto normal
ESC ! 0x08 - Doble altura
ESC ! 0x20 - Doble ancho
ESC ! 0x28 - Doble altura y ancho
```

### Corte de Papel
```
GS V 0 - Corte completo
GS V 1 - Corte parcial
```

## 🔧 Ejemplo de Implementación

### JavaScript (Web)
```javascript
class POSPrinter {
    constructor(ip, port = 9100) {
        this.ip = ip;
        this.port = port;
        this.socket = null;
    }
    
    async connect() {
        // Implementar conexión WebSocket o fetch
        this.socket = new WebSocket(`ws://${this.ip}:${this.port}`);
        return new Promise((resolve) => {
            this.socket.onopen = () => resolve(true);
        });
    }
    
    printText(text) {
        const buffer = new TextEncoder().encode(text + '\n');
        this.socket.send(buffer);
    }
    
    cutPaper() {
        const cutCommand = new Uint8Array([0x1D, 0x56, 0x00]);
        this.socket.send(cutCommand);
    }
}

// Uso
const printer = new POSPrinter('192.168.1.100');
await printer.connect();
printer.printText('Hola Mundo');
printer.cutPaper();
```

### Python
```python
import socket

class POSPrinter:
    def __init__(self, ip, port=9100):
        self.ip = ip
        self.port = port
        self.socket = None
    
    def connect(self):
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.socket.connect((self.ip, self.port))
    
    def print_text(self, text):
        self.socket.send((text + '\n').encode('utf-8'))
    
    def cut_paper(self):
        cut_command = bytes([0x1D, 0x56, 0x00])
        self.socket.send(cut_command)
    
    def disconnect(self):
        if self.socket:
            self.socket.close()

# Uso
printer = POSPrinter('192.168.1.100')
printer.connect()
printer.print_text('Hola Mundo')
printer.cut_paper()
printer.disconnect()
```

## 🧪 Testing

### Probar Conectividad
```bash
# Verificar puerto abierto
nc -zv 192.168.1.100 9100

# Enviar comando de prueba
echo -e "Prueba de impresion\n\n\n" | nc 192.168.1.100 9100
```

### Debugger de Comandos
```bash
# Capturar tráfico (Linux)
sudo tcpdump -i any -X port 9100

# Analizar comandos enviados
hexdump -C archivo_comandos.bin
```

## 📚 Recursos Adicionales

- [Comandos ESC/POS completos](https://reference.epson-biz.com/modules/ref_escpos/index.php)
- [Herramienta de test](../Tools/POS%20Printer%20Test%20V3.61C/)
- [Ejemplos de imágenes](../Tools/POS%20Printer%20Test%20V3.61C/Logo_Sample/)

## ⚠️ Mejores Prácticas

1. **Siempre cerrar** conexiones después de imprimir
2. **Manejar excepciones** de red apropiadamente
3. **Validar** datos antes de enviar a impresora
4. **Usar timeout** en conexiones de red
5. **Implementar retry** para comandos críticos