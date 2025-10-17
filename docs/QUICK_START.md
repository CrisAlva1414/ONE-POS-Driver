# 🚀 Guía de Inicio Rápido

## ⚡ Configuración en 5 minutos

### 1. Descargar Driver
- **Windows**: `Driver/Windows Driver/POS Printer Driver Setup V8.203.exe`
- **Mac**: `Driver/Mac Driver/prt.pos.drv_3.8.1.pkg`
- **Linux**: `Driver/Linux Driver/printer-driver-pos_3.13.1_all.deb`

### 2. Instalar
- Ejecutar como administrador
- Seguir el asistente de instalación
- Reiniciar si es necesario

### 3. Conectar Impresora
#### USB
- Conectar cable y esperar detección automática

#### WiFi
- Mantener presionado botón WiFi hasta que parpadee
- Conectar a red temporal de la impresora
- Ir a `192.168.4.1` y configurar tu red WiFi

#### Ethernet
- Conectar cable de red
- La impresora obtendrá IP automática

### 4. Probar
- Usar `Tools/POS Printer Test.exe`
- Seleccionar tipo de conexión
- Hacer clic en "Print Test"

## 🔧 Solución Rápida de Problemas

| Problema | Solución |
|----------|----------|
| No detecta impresora | Reinstalar driver como administrador |
| Caracteres extraños | Cambiar codificación a UTF-8 |
| No corta papel | Activar "Auto Cut" en configuración |
| IP cambia | Configurar IP estática en panel web |

¿Necesitas ayuda? Consulta el [README completo](../README.md)