# 🖨️ Tutorial Completo de Impresoras POS - Guía paso a paso

## 📋 Índice
1. [Introducción](#introducción)
2. [Instalación de Drivers](#instalación-de-drivers)
3. [Configuración por Tipo de Conexión](#configuración-por-tipo-de-conexión)
4. [Herramientas de Prueba](#herramientas-de-prueba)
5. [Desarrollo con SDKs](#desarrollo-con-sdks)
6. [Solución de Problemas](#solución-de-problemas)
7. [Preguntas Frecuentes](#preguntas-frecuentes)

---

## 🚀 Introducción

Este repositorio contiene todo lo necesario para configurar y usar impresoras POS (Point of Sale) en diferentes sistemas operativos. Las impresoras POS son dispositivos especializados para imprimir recibos, tickets y comprobantes de venta.

### ¿Qué encontrarás aquí?
- **Drivers** para Windows, Mac y Linux
- **Herramientas de configuración** para diferentes tipos de conexión
- **SDKs** para desarrollo de aplicaciones
- **Guías detalladas** para configuración paso a paso

---

## 💾 Instalación de Drivers

### 🪟 Windows

#### Opción 1: Driver Completo (Recomendado)
1. **Descargar**: Busca el archivo `POS Printer Driver Setup V8.203.exe` en la carpeta `Driver/Windows Driver/`
2. **Ejecutar**: Haz clic derecho → "Ejecutar como administrador"
3. **Seguir el asistente**: Acepta los términos y condiciones
4. **Reiniciar**: Reinicia tu computadora cuando se complete la instalación

#### Opción 2: Driver Simplificado
1. **Descargar**: `POSPrinterSimple80DriveSetup V2.1R.exe`
2. **Instalar**: Mismo proceso que la opción 1
3. **Uso**: Ideal para impresoras de 80mm de ancho

#### ⚡ Driver para Puerto Virtual COM
Si tu impresora se conecta por USB pero necesitas que aparezca como puerto COM:

**Para procesadores Intel/AMD de 64 bits:**
1. Ve a `Driver/Virtual com driver/ST/x64/`
2. Ejecuta `VCP_V1.3.1_Setup_x64.exe`

**Para procesadores Intel/AMD de 32 bits:**
1. Ve a `Driver/Virtual com driver/ST/x86/`
2. Ejecuta el instalador correspondiente

### 🍎 macOS

1. **Localizar**: Archivo `prt.pos.drv_3.8.1.pkg` en `Driver/Mac Driver/`
2. **Instalar**: Doble clic en el archivo .pkg
3. **Permisos**: Si aparece "Desarrollador no identificado":
   - Ve a Preferencias del Sistema → Seguridad y Privacidad
   - Haz clic en "Abrir de todas formas"
4. **Completar**: Sigue las instrucciones en pantalla

### 🐧 Linux (Ubuntu/Debian)

1. **Abrir terminal**: Presiona `Ctrl + Alt + T`
2. **Navegar**: 
   ```bash
   cd ruta/a/Driver/Linux\ Driver/
   ```
3. **Instalar**:
   ```bash
   sudo dpkg -i printer-driver-pos_3.13.1_all.deb
   ```
4. **Resolver dependencias** (si es necesario):
   ```bash
   sudo apt-get install -f
   ```

---

## 🔧 Configuración por Tipo de Conexión

### 📱 Bluetooth

#### Preparación
1. **Activar Bluetooth** en tu computadora
2. **Encender** la impresora
3. **Modo emparejamiento**: Mantén presionado el botón de la impresora hasta que parpadee

#### Configuración en Windows
1. **Panel de Control** → Dispositivos e impresoras
2. **Agregar impresora** → Buscar impresoras Bluetooth
3. **Seleccionar** tu impresora de la lista
4. **Emparejar**: Introduce el PIN (generalmente 0000 o 1234)

#### Configuración en Mac
1. **Preferencias del Sistema** → Bluetooth
2. **Buscar dispositivos**
3. **Conectar** con la impresora
4. **Agregar impresora**: Sistema → Impresoras y escáneres

#### Configuración en Linux
```bash
# Escanear dispositivos
bluetoothctl scan on

# Emparejar (reemplaza XX:XX:XX con la dirección de tu impresora)
bluetoothctl pair XX:XX:XX:XX:XX:XX

# Conectar
bluetoothctl connect XX:XX:XX:XX:XX:XX
```

### 📶 WiFi

#### Configuración Inicial
1. **Encender** la impresora
2. **Botón WiFi**: Mantén presionado hasta que parpadee
3. **Buscar red**: La impresora creará una red temporal

#### Conectar a tu Red WiFi
1. **Conectar** tu computadora a la red temporal de la impresora
2. **Abrir navegador**: Ve a `192.168.4.1`
3. **Configurar WiFi**:
   - Selecciona tu red WiFi
   - Introduce la contraseña
   - Guarda la configuración
4. **Reiniciar**: La impresora se conectará automáticamente

#### Configurar Dirección IP Fija
Para evitar que la IP cambie:
1. **Acceder** al panel de configuración: `192.168.1.xxx` (IP de la impresora)
2. **Configuración de red**:
   - IP: `192.168.1.100` (ejemplo)
   - Máscara: `255.255.255.0`
   - Gateway: `192.168.1.1` (IP de tu router)
3. **Guardar** y reiniciar

### 🌐 Ethernet (Cable de Red)

#### Conexión Física
1. **Conectar** cable Ethernet de la impresora al router/switch
2. **Encender** la impresora
3. **Esperar**: La impresora obtendrá IP automáticamente

#### Encontrar la IP de la Impresora
**Método 1: Imprimir configuración**
- Mantén presionado el botón FEED por 3 segundos
- Se imprimirá la configuración actual

**Método 2: Escanear red**
```bash
# En Linux/Mac
nmap -sn 192.168.1.0/24

# En Windows (PowerShell)
1..254 | ForEach-Object {Test-NetConnection -ComputerName "192.168.1.$_" -Port 9100 -InformationLevel Quiet}
```

### 🔌 USB

#### Windows
1. **Conectar** cable USB
2. **Esperar**: Windows detectará automáticamente
3. **Si no detecta**: Ir a Administrador de dispositivos → Actualizar driver

#### Mac
1. **Conectar** USB
2. **Preferencias del Sistema** → Impresoras y escáneres
3. **Agregar** → La impresora aparecerá automáticamente

#### Linux
```bash
# Verificar detección
lsusb

# Ver impresoras disponibles
lpstat -p -d
```

---

## 🛠️ Herramientas de Prueba

### Herramienta de Prueba Oficial

En la carpeta `Tools/POS Printer Test V3.61C/` encontrarás la herramienta oficial de prueba.

#### Cómo usar:
1. **Ejecutar**: `POS Printer Test.exe`
2. **Seleccionar conexión**:
   - COM (para USB/Serial)
   - TCP/IP (para WiFi/Ethernet)
   - Bluetooth
3. **Configurar parámetros**:
   - Puerto COM o dirección IP
   - Velocidad (generalmente 9600 baudios)
4. **Probar conexión**: Botón "Connect"
5. **Imprimir prueba**: Botón "Print Test"

#### Funciones Disponibles
- ✅ **Imprimir texto** simple
- ✅ **Imprimir códigos QR**
- ✅ **Imprimir imágenes**
- ✅ **Probar caracteres especiales**
- ✅ **Configurar tamaño de papel**

### Comandos de Prueba Manual

#### Texto Simple
```
Hola Mundo
Este es un recibo de prueba
------------------------
Fecha: 2024-10-17
Hora: 14:30:25
------------------------
Total: $123.45
Gracias por su compra!
```

#### Código QR
La herramienta puede generar códigos QR con cualquier texto o URL.

---

## 🔧 Personalización Avanzada

### Especificaciones de Papel

#### Anchos Estándar
- **58mm**: Común en pequeños comercios
- **76mm**: Uso intermedio
- **80mm**: Más común, mejor legibilidad

#### Configurar Ancho Personalizado
1. **Abrir herramienta de prueba**
2. **Settings** → Paper Settings
3. **Introducir** ancho en milímetros
4. **Guardar** configuración

### Configuración de Puertos de Red

#### Agregar Puerto IP Manual
**Windows:**
1. **Panel de Control** → Dispositivos e impresoras
2. **Agregar impresora** → La impresora que quiero no está en la lista
3. **Agregar por dirección TCP/IP**:
   - Tipo: TCP/IP
   - Nombre del host o IP: `192.168.1.100`
   - Puerto: `9100`
   - Nombre del puerto: `IP_192.168.1.100`

#### Puertos Comunes
- **9100**: Puerto estándar para impresión directa
- **515**: LPR/LPD (Line Printer Daemon)
- **631**: IPP (Internet Printing Protocol)

---

## 💻 Desarrollo con SDKs

### SDKs Disponibles

En la carpeta `Develop routine/` encontrarás:
- **Android SDK** (`.zip`)
- **iOS SDK** (`.rar`)
- **Windows SDK** (`.rar`)

### Instalación de SDKs

#### Android
1. **Extraer**: `Android SDK.zip`
2. **Importar** en Android Studio como módulo
3. **Agregar dependencia** en `build.gradle`:
   ```gradle
   implementation project(':pos-printer-sdk')
   ```

#### iOS
1. **Extraer**: `ios sdk.rar`
2. **Arrastrar** archivos `.framework` a tu proyecto Xcode
3. **Configurar**: Build Settings → Framework Search Paths

#### Windows
1. **Extraer**: `windows SDK.rar`
2. **Agregar referencia** en Visual Studio
3. **Incluir** archivos de cabecera (.h) y librerías (.lib)

### Ejemplo de Código Básico

#### Android (Java)
```java
// Inicializar impresora
POSPrinter printer = new POSPrinter();
printer.connect("192.168.1.100", 9100);

// Imprimir texto
printer.printText("Hola Mundo");
printer.printText("Total: $123.45");
printer.cutPaper();

// Desconectar
printer.disconnect();
```

#### iOS (Swift)
```swift
// Conectar impresora
let printer = POSPrinter()
printer.connect(host: "192.168.1.100", port: 9100)

// Imprimir
printer.printText("Hola Mundo")
printer.printText("Total: $123.45")
printer.cutPaper()

// Desconectar
printer.disconnect()
```

#### Windows (C#)
```csharp
// Crear instancia
var printer = new POSPrinter();
printer.Connect("192.168.1.100", 9100);

// Imprimir
printer.PrintText("Hola Mundo");
printer.PrintText("Total: $123.45");
printer.CutPaper();

// Desconectar
printer.Disconnect();
```

---

## 🚨 Solución de Problemas

### Problemas Comunes y Soluciones

#### ❌ La impresora no se conecta

**Verificar conexión física:**
- ✅ Cable USB bien conectado
- ✅ Cable de red con luces indicadoras
- ✅ Impresora encendida (luz LED activa)

**Verificar red (WiFi/Ethernet):**
```bash
# Probar conectividad
ping 192.168.1.100

# Probar puerto de impresión
telnet 192.168.1.100 9100
```

#### ❌ Imprime caracteres extraños

**Causa:** Codificación incorrecta
**Solución:**
1. **Configurar codificación** a UTF-8 o CP850
2. **Verificar** configuración regional en el sistema
3. **Probar** con diferentes configuraciones de caracteres

#### ❌ No corta el papel automáticamente

**Configurar corte automático:**
1. **Herramienta de prueba** → Settings
2. **Auto Cut** → Enabled
3. **Guardar** configuración

#### ❌ Error de puerto COM ocupado

**Windows:**
1. **Administrador de dispositivos** → Puertos COM
2. **Verificar** qué programa usa el puerto
3. **Cerrar** aplicaciones que puedan estar usando el puerto

**Linux:**
```bash
# Ver procesos usando el puerto
lsof /dev/ttyUSB0

# Liberar puerto (cambiar PID por el proceso)
kill -9 [PID]
```

#### ❌ Driver no se instala en Windows

**Modo de compatibilidad:**
1. **Clic derecho** en el instalador
2. **Propiedades** → Compatibilidad
3. **Ejecutar en modo de compatibilidad** para Windows 7/8
4. **Ejecutar como administrador**

#### ❌ IP de la impresora cambia constantemente

**Configurar IP estática:**
1. **Acceder** panel web de la impresora
2. **Network Settings** → Static IP
3. **Configurar**:
   - IP: `192.168.1.100`
   - Subnet: `255.255.255.0`
   - Gateway: `192.168.1.1`
   - DNS: `8.8.8.8`

---

## ❓ Preguntas Frecuentes

### 🤔 ¿Qué diferencia hay entre los drivers?

**Driver Completo (V8.203):**
- ✅ Soporte completo para todas las funciones
- ✅ Múltiples tipos de conexión
- ✅ Herramientas de configuración avanzada
- ❌ Archivo más grande

**Driver Simple (V2.1R):**
- ✅ Instalación rápida
- ✅ Archivo más pequeño
- ✅ Ideal para uso básico
- ❌ Funciones limitadas

### 🤔 ¿Puedo usar una impresora con múltiples computadoras?

**Sí, hay varias opciones:**

**Conexión de red (Recomendado):**
- Conecta la impresora por WiFi o Ethernet
- Todas las computadoras pueden acceder por IP
- No hay límite de usuarios simultáneos

**Compartir por USB:**
- Conecta a una computadora principal
- Comparte la impresora en la red
- Limitado por la computadora anfitriona

### 🤔 ¿Qué ancho de papel debo usar?

**Para pequeños comercios:** 58mm
- Recibos compactos
- Menor costo de papel
- Ideal para cafeterías, pequeñas tiendas

**Para comercios medianos:** 80mm
- Mejor legibilidad
- Más espacio para información
- Estándar en supermercados

### 🤔 ¿Cómo imprimo logos o imágenes?

**Requisitos:**
- Imagen en formato BMP o PNG
- Resolución máxima: 576 píxeles de ancho
- Colores: Blanco y negro únicamente

**Proceso:**
1. **Convertir** imagen a escala de grises
2. **Redimensionar** al ancho de la impresora
3. **Usar** herramienta de prueba para cargar imagen
4. **Imprimir** desde la aplicación

### 🤔 ¿La impresora funciona con tablets y smartphones?

**Android:** Sí
- Usar SDK de Android
- Conexión por WiFi, Bluetooth o USB OTG
- Aplicaciones específicas disponibles

**iOS:** Sí
- Usar SDK de iOS
- Principalmente por WiFi o Bluetooth
- Certificación MFi requerida para algunos modelos

### 🤔 ¿Qué hacer si se atasca el papel?

**Pasos para resolver:**
1. **Apagar** la impresora
2. **Abrir** la tapa superior
3. **Retirar** papel atascado con cuidado
4. **Verificar** que no queden restos
5. **Cerrar** tapa y encender
6. **Probar** con papel nuevo

---

## 📞 Soporte Técnico

### 🔧 Información del Sistema

Antes de solicitar soporte, ten a mano:
- **Sistema operativo** y versión
- **Modelo** de la impresora
- **Tipo de conexión** (USB, WiFi, Ethernet, Bluetooth)
- **Mensaje de error** específico
- **Archivos de log** (si están disponibles)

### 📋 Generar Reporte de Diagnóstico

**Windows:**
```cmd
# Información del sistema
systeminfo > diagnostico.txt

# Dispositivos conectados
devmgmt.msc

# Estado de red
ipconfig /all >> diagnostico.txt
```

**Linux:**
```bash
# Información del sistema
uname -a > diagnostico.txt
lsb_release -a >> diagnostico.txt

# Dispositivos USB
lsusb >> diagnostico.txt

# Estado de red
ifconfig >> diagnostico.txt
```

### 🌐 Recursos Adicionales

- **Documentación técnica:** Archivos PDF en las carpetas correspondientes
- **Herramientas de diagnóstico:** Carpeta `Tools/`
- **Ejemplos de código:** Carpeta `Develop routine/`
- **Actualizaciones:** Revisa periódicamente este repositorio

---

## 📝 Notas Importantes

### ⚠️ Compatibilidad
- **Windows:** 7, 8, 10, 11 (32 y 64 bits)
- **macOS:** 10.12 o superior
- **Linux:** Ubuntu 16.04+, Debian 9+, CentOS 7+

### 🔒 Seguridad
- Mantén los drivers actualizados
- Usa contraseñas seguras en conexiones WiFi
- Configura firewalls apropiadamente para conexiones de red

### 💡 Consejos de Mantenimiento
- **Limpia** regularmente el cabezal de impresión
- **Usa** papel de calidad para evitar atascos
- **Mantén** la impresora en ambiente libre de polvo
- **Actualiza** firmware cuando esté disponible

---

## 📄 Licencia y Términos de Uso

Este repositorio contiene software y documentación de terceros. Consulta los términos de licencia específicos en cada carpeta de drivers.

### Uso Comercial
- ✅ Permitido para uso comercial
- ✅ Redistribución permitida
- ❌ No modificar archivos de driver sin autorización

---

## 🚀 ¡Contribuye!

Si encuentras errores o mejoras para esta documentación:
1. **Fork** este repositorio
2. **Crea** una rama para tus cambios
3. **Envía** un Pull Request
4. **Describe** claramente los cambios realizados

---

*Última actualización: Octubre 2024*
*Versión del tutorial: 2.0*

---

## 📊 Estado de Compatibilidad

| Característica | Windows | macOS | Linux | Android | iOS |
|---------------|---------|-------|-------|---------|-----|
| USB | ✅ | ✅ | ✅ | ✅ | ❌ |
| WiFi | ✅ | ✅ | ✅ | ✅ | ✅ |
| Ethernet | ✅ | ✅ | ✅ | ✅ | ✅ |
| Bluetooth | ✅ | ✅ | ✅ | ✅ | ✅ |
| Códigos QR | ✅ | ✅ | ✅ | ✅ | ✅ |
| Imágenes | ✅ | ✅ | ✅ | ✅ | ✅ |
| Corte automático | ✅ | ✅ | ✅ | ✅ | ✅ |

---

¡Esperamos que esta guía te sea útil! Si tienes alguna pregunta, no dudes en abrir un issue en el repositorio. 🎉