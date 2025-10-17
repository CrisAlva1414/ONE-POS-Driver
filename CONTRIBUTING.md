# 🤝 Guía de Contribución

¡Gracias por tu interés en contribuir al proyecto ONE-POS-Driver! 

## 🎯 Tipos de Contribuciones

### 📝 Documentación
- Corregir errores tipográficos
- Mejorar explicaciones existentes
- Agregar nuevos ejemplos
- Traducir a otros idiomas

### 🐛 Reportes de Errores
- Problemas de compatibilidad
- Errores en drivers
- Bugs en herramientas de prueba

### ✨ Nuevas Características
- Soporte para nuevos sistemas operativos
- Mejoras en herramientas existentes
- Nuevos ejemplos de código

## 📋 Proceso de Contribución

### 1. Fork del Repositorio
```bash
git clone https://github.com/[tu-usuario]/ONE-POS-Driver.git
cd ONE-POS-Driver
```

### 2. Crear Rama de Trabajo
```bash
git checkout -b feature/nombre-descriptivo
# o
git checkout -b fix/descripcion-del-fix
# o
git checkout -b docs/mejora-documentacion
```

### 3. Realizar Cambios
- Edita los archivos necesarios
- Mantén el estilo de documentación existente
- Prueba los cambios si aplica

### 4. Commit y Push
```bash
git add .
git commit -m "Descripción clara de los cambios"
git push origin nombre-de-tu-rama
```

### 5. Crear Pull Request
- Ve a GitHub y crea un Pull Request
- Describe claramente los cambios
- Incluye capturas de pantalla si es relevante

## 📏 Estándares de Código

### Documentación (Markdown)
- Usar emojis para títulos principales
- Código indentado con 3 espacios para ejemplos
- Incluir ejemplos prácticos
- Mantener estructura consistente

### Ejemplos de Código
```python
# ✅ Bueno: Comentarios claros
def connect_printer(ip, port=9100):
    """Conecta a la impresora POS por TCP/IP"""
    try:
        socket = create_connection((ip, port), timeout=5)
        return socket
    except ConnectionError as e:
        logger.error(f"Error conectando a {ip}:{port} - {e}")
        return None
```

```python
# ❌ Malo: Sin comentarios ni manejo de errores
def connect(ip, port):
    socket = create_connection((ip, port))
    return socket
```

## 🧪 Testing

### Documentación
- Verificar que todos los enlaces funcionen
- Probar ejemplos de código en diferentes sistemas
- Revisar ortografía y gramática

### Drivers/Software
- Probar en múltiples sistemas operativos
- Verificar compatibilidad con diferentes modelos
- Documentar limitaciones encontradas

## 📝 Estilo de Commits

### Formato Recomendado
```
tipo(ámbito): descripción corta

Descripción más detallada si es necesaria.

- Cambio específico 1
- Cambio específico 2
```

### Tipos de Commit
- **feat**: Nueva característica
- **fix**: Corrección de error
- **docs**: Cambios en documentación
- **style**: Cambios de formato (no afectan funcionalidad)
- **refactor**: Refactorización de código
- **test**: Agregar o modificar tests
- **chore**: Tareas de mantenimiento

### Ejemplos
```bash
feat(drivers): agregar soporte para Ubuntu 22.04

fix(docs): corregir enlaces rotos en README

docs(troubleshooting): agregar solución para error 0x06
```

## 🔍 Revisión de Pull Requests

### Criterios de Aceptación
- [ ] Código funciona correctamente
- [ ] Documentación actualizada si es necesario
- [ ] Estilo consistente con el proyecto
- [ ] No rompe funcionalidad existente
- [ ] Incluye ejemplos si agrega nueva funcionalidad

### Proceso de Revisión
1. **Revisión automática**: Verificar formato y enlaces
2. **Revisión técnica**: Probar cambios propuestos
3. **Revisión editorial**: Verificar claridad y consistencia
4. **Aprobación**: Merge del PR

## 🚫 Qué NO Hacer

### Cambios No Permitidos
- ❌ Modificar archivos binarios de drivers sin autorización
- ❌ Agregar archivos muy grandes (>10MB)
- ❌ Cambiar estructura de carpetas principales
- ❌ Eliminar documentación existente sin reemplazo

### Estilo No Recomendado
- ❌ Commits con mensajes poco descriptivos ("fix", "update")
- ❌ PRs muy grandes que cambien muchas cosas
- ❌ Documentación sin ejemplos prácticos
- ❌ Código sin comentarios o documentación

## 📚 Recursos Útiles

### Herramientas Recomendadas
- **Editor**: VS Code con extensiones de Markdown
- **Lint**: markdownlint para verificar formato
- **Git**: GitKraken o GitHub Desktop para interfaz gráfica

### Referencias
- [Guía de Markdown](https://www.markdownguide.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)

## 🏆 Reconocimientos

Los contribuidores serán reconocidos en:
- Lista de colaboradores en README principal
- Changelog de versiones
- Sección de agradecimientos

## 📞 Contacto

¿Tienes preguntas sobre cómo contribuir?
- 📧 Crear un issue con la etiqueta "question"
- 💬 Comentar en PRs existentes
- 📋 Revisar issues existentes por si ya fue respondida

---

¡Esperamos tus contribuciones! Cada aporte, por pequeño que sea, ayuda a mejorar este proyecto para toda la comunidad. 🎉