# AppBuscador - Sistema de Gestión de Doctorados

![Version](https://img.shields.io/badge/version-2.0-blue)
![Python](https://img.shields.io/badge/python-3.8+-blue)
![License](https://img.shields.io/badge/license-Apache--2.0-green)

## 📋 Descripción

**AppBuscador** es una aplicación de escritorio modular y escalable para la búsqueda y gestión de documentos de programas de doctorado y oficios administrativos de la Universidad Central del Ecuador.

La aplicación proporciona una interfaz intuitiva basada en **Tkinter** que permite a los usuarios autenticarse, buscar documentos de manera eficiente y acceder a oficios con filtros avanzados.

### 🎯 Propósito Principal
- Centralizar la búsqueda de documentos de doctorados
- Gestionar oficios administrativos  
- Facilitar el acceso a recursos desde Google Drive
- Proporcionar una interfaz segura con autenticación

---

## 🏗️ Estructura del Proyecto

```
AppBuscador/
├── main.py                          # Punto de entrada principal de la aplicación
├── AppBuscador.spec                 # Configuración PyInstaller para compilación
├── build.bat                        # Script automatizado para compilar ejecutable
├── clean.bat                        # Script para limpiar archivos temporales
│
├── config/
│   ├── __init__.py
│   └── settings.py                  # Configuración global, rutas y constantes
│
├── models/
│   └── __init__.py                  # Reservado para modelos de datos futuros
│
├── services/
│   ├── __init__.py
│   ├── auth_service.py              # Servicio de autenticación (SHA-256)
│   ├── file_service.py              # Gestión de descargas y apertura de archivos
│   └── search_service.py            # Lógica de búsqueda y filtrado
│
├── ui/
│   ├── __init__.py
│   ├── styles.py                    # Temas y estilos de UI
│   │
│   ├── components/
│   │   ├── __init__.py
│   │   ├── header.py                # Encabezado con logo y botones
│   │   ├── filters.py               # Componentes de filtros dinámicos
│   │   ├── results.py               # Vista de resultados en Treeview
│   │   └── details.py               # Panel de detalles de documentos
│   │
│   └── views/
│       ├── __init__.py
│       ├── login_view.py            # Pantalla de autenticación
│       ├── selection_view.py        # Pantalla de selección de módulo
│       ├── docentes_view.py         # Módulo de búsqueda de docentes
│       ├── oficios_view.py          # Módulo de gestión de oficios
│       ├── acerca_de_view.py        # Información de la aplicación
│       └── splash_view.py           # Pantalla de carga inicial
│
├── utils/
│   ├── __init__.py
│   ├── path_utils.py                # Búsqueda y validación de rutas Google Drive
│   └── file_utils.py                # Utilidades para recursos y archivos
│
├── data/
│   ├── cifrador.py                  # Herramienta para hashear contraseñas
│   └── usuarios.json                # Base de datos de usuarios (JSON)
│
├── imagenes/
│   └── logouce.png                  # Logo institucional
│
├── COMPILACION_RAPIDA.md            # Guía rápida de compilación
├── GUIA_EJECUTABLE.md               # Documentación completa del ejecutable
├── GUIA_LIMPIEZA.md                 # Guía de limpieza de archivos temporales
├── MEJORAS_INIT.md                  # Propuestas de mejora futuras
├── requerimientos.txt               # Requisitos funcionales pendientes
├── requirements-build.txt           # Dependencias para compilación
├── requirements.txt                 # Dependencias de ejecución
└── LICENSE                          # Licencia Apache 2.0
```

---

## 🔄 Flujo de Trabajo de la Aplicación

### 1. **Inicio de la Aplicación**
```
┌──────────────────────────────┐
│   Ejecución de main.py       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   Inicialización AppBuscador │
│   - Crear ventana principal  │
│   - Cargar configuración     │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   Mostrar Splash Screen      │
│   - Animación de carga       │
│   - Inicializar rutas        │
└──────────────┬───────────────┘
               │
               ▼
```

### 2. **Autenticación del Usuario**
```
┌──────────────────────────────┐
│   Vista de Login             │
│   Ingresar usuario/contraseña│
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   auth_service.py            │
│   - Hashear contraseña       │
│   - Validar en usuarios.json │
└──────────────┬───────────────┘
               │
       ┌───────┴───────┐
       │               │
    VÁLIDO          INVÁLIDO
       │               │
       ▼               ▼
┌──────────┐    ┌─────────────┐
│ Acceso   │    │ Error/Reint.│
│Concedido │    │   ento      │
└────┬─────┘    └─────────────┘
     │
     ▼
```

### 3. **Selección de Módulo**
```
┌──────────────────────────────────┐
│   selection_view.py              │
│   ┌────────────────────────────┐ │
│   │  Bienvenido: [Nombre User] │ │
│   ├────────────────────────────┤ │
│   │ ┌──────────┐  ┌──────────┐│ │
│   │ │ Docentes │  │ Oficios  ││ │
│   │ └──────────┘  └──────────┘│ │
│   │ ┌──────────────────────────┐│ │
│   │ │  Acerca de la Aplicación ││ │
│   │ └──────────────────────────┘│ │
│   └────────────────────────────┘ │
└──────────────┬───────────────────┘
               │
       ┌───────┼───────┐
       │       │       │
       ▼       ▼       ▼
    [DOC]  [OF]   [INFO]
```

### 4. **Flujo - Módulo de Docentes**
```
┌──────────────────────────────────────┐
│   docentes_view.py                   │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  ENCABEZADO                    │ │
│  │  Logo - Título - Botones       │ │
│  └────────────────────────────────┘ │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  FILTROS                       │ │
│  │  □ Universidad                 │ │
│  │  □ Programa                    │ │
│  │  □ Estudiante                  │ │
│  │  □ Año                         │ │
│  │  🔍 [Buscar...]               │ │
│  └────────────────────────────────┘ │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  RESULTADOS (Treeview)         │ │
│  │  ├─ [Expediente 1]             │ │
│  │  │  ├─ Documento 1             │ │
│  │  │  ├─ Documento 2             │ │
│  │  │  └─ Documento N             │ │
│  │  └─ [Expediente 2]             │ │
│  └────────────────────────────────┘ │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  ACCIONES                      │ │
│  │  [Abrir PDF] [Descargar]       │ │
│  │  [Descargar Expediente]        │ │
│  └────────────────────────────────┘ │
└──────────────────────────────────────┘
         │
         ▼
   search_service.py
     - Filtrar resultados
     - Buscar por criterios
         │
         ▼
   file_service.py
     - Abrir PDF (con visor externo)
     - Descargar archivo
     - Descargar expediente completo
```

### 5. **Flujo - Módulo de Oficios**
```
┌──────────────────────────────────────┐
│   oficios_view.py                    │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  ENCABEZADO                    │ │
│  │  Logo - Título - Botones       │ │
│  └────────────────────────────────┘ │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  FILTROS DE OFICIOS            │ │
│  │  □ Año                         │ │
│  │  □ Número Oficio               │ │
│  │  □ Remitente                   │ │
│  │  □ Asunto                      │ │
│  │  🔍 [Buscar...]               │ │
│  └────────────────────────────────┘ │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  LISTADO DE OFICIOS            │ │
│  │  ├─ Oficio 2025-001            │ │
│  │  ├─ Oficio 2025-002            │ │
│  │  └─ Oficio 2025-003            │ │
│  └────────────────────────────────┘ │
│                                      │
│  ┌────────────────────────────────┐ │
│  │  ACCIONES                      │ │
│  │  [Abrir PDF] [Descargar]       │ │
│  └────────────────────────────────┘ │
└──────────────────────────────────────┘
         │
         ▼
   search_service.py
     - Búsqueda por criterios
     - Filtrado avanzado
         │
         ▼
   file_service.py
     - Descarga de oficio
     - Apertura de PDF
```

### 6. **Ciclo de Búsqueda**
```
                          ┌─────────────┐
                          │ Usuario     │
                          │ Ingresa     │
                          │ Búsqueda    │
                          └──────┬──────┘
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │ search_service.py      │
                    │ • Aplicar filtros      │
                    │ • Validar criterios    │
                    │ • Buscar en Drive      │
                    └────────┬───────────────┘
                             │
                    ┌────────▼──────────┐
                    │ Resultados        │
                    │ Encontrados       │
                    └────────┬──────────┘
                             │
                 ┌────────────┼────────────┐
                 │            │            │
                 ▼            ▼            ▼
            [Abrir]      [Descargar]  [Expediente]
               │              │            │
               ▼              ▼            ▼
         file_service   file_service  file_service
         • PDF Viewer   • Descargar   • Zip múltiples
         • Externo      • Archivo       archivos
```

### 7. **Cierre de Sesión y Salida**
```
┌──────────────────────────────┐
│   Usuario elige:             │
│   - Cerrar sesión            │
│   - Salir de la aplicación   │
└──────────────┬───────────────┘
               │
       ┌───────┴────────┐
       │                │
    SESIÓN            SALIDA
       │                │
       ▼                ▼
    LOGIN            [Cerrar]
   (Volver)          Aplicación
```

---

## ⚙️ Componentes Principales

### **Services (Servicios)**

#### `auth_service.py`
- **Responsabilidad**: Autenticación y validación de credenciales
- **Métodos principales**:
  - `validar_usuario(usuario, contraseña)`: Verifica credenciales contra usuarios.json
  - Usa SHA-256 para hashear contraseñas

#### `search_service.py`
- **Responsabilidad**: Búsqueda y filtrado de documentos
- **Métodos principales**:
  - `buscar_por_criterios(filtros)`: Busca documentos aplicando filtros
  - `filtrar_por_universidad(datos)`: Filtra por institución
  - `filtrar_por_programa(datos)`: Filtra por programa académico

#### `file_service.py`
- **Responsabilidad**: Operaciones con archivos
- **Métodos principales**:
  - `descargar_archivo(origen, destino)`: Descarga desde Google Drive
  - `abrir_pdf(ruta)`: Abre PDF con visor externo
  - `descargar_expediente(archivos)`: Descarga múltiples archivos como ZIP

### **UI - Views (Vistas)**

#### `login_view.py`
- Pantalla de autenticación
- Validación de credenciales en tiempo real

#### `selection_view.py`
- Pantalla de selección de módulo (Docentes/Oficios/Acerca de)

#### `docentes_view.py`
- Vista completa del módulo de docentes
- Integra: encabezado, filtros, resultados, detalles y acciones

#### `oficios_view.py`
- Vista completa del módulo de oficios
- Interfaz específica para gestión de oficios

#### `splash_view.py`
- Pantalla de carga inicial
- Muestra progreso durante inicialización

### **UI - Components (Componentes Reutilizables)**

#### `header.py`
- Encabezado con logo y título
- Botones: Volver, Cerrar sesión

#### `filters.py`
- Componentes dinámicos de filtros
- Desplegables, campos de texto, checkboxes

#### `results.py`
- Treeview para mostrar resultados
- Soporta múltiples niveles (expedientes/documentos)

#### `details.py`
- Panel de información detallada
- Botones de acción (Abrir, Descargar)

### **Utils (Utilidades)**

#### `path_utils.py`
- Encuentra rutas de Google Drive montado
- Valida accesibilidad de paths

#### `file_utils.py`
- Gestiona rutas de recursos (imágenes, datos)
- Funciones auxiliares de archivos

---

## 🚀 Instalación y Uso

### **Requisitos Previos**
- Python 3.8+
- Google Drive montado o accesible
- Windows (para scripts .bat)

### **Instalación de Dependencias**

```bash
# Opción 1: Instalar desde requirements.txt
pip install -r requirements.txt

# Opción 2: Instalar manualmente
pip install tkinter pillow PyMuPDF
```

### **Ejecución de la Aplicación**

```bash
python main.py
```

### **Compilación a Ejecutable**

#### Método Rápido
```bash
# Ejecutar script de compilación
.\build.bat
```

El ejecutable estará en: `dist/AppBuscador.exe`

#### Documentación Completa
- 📄 [COMPILACION_RAPIDA.md](COMPILACION_RAPIDA.md)
- 📄 [GUIA_EJECUTABLE.md](GUIA_EJECUTABLE.md)

---

## 🧹 Mantenimiento del Proyecto

### **Limpiar Archivos Temporales**

```bash
# Ejecutar script de limpieza
.\clean.bat
```

Elimina:
- Directorio `__pycache__/`
- Directorios `.pytest_cache/`
- Archivos `.pyc`
- Directorio `build/` de compilaciones
- Directorios `.egg-info/`

📄 Documentación: [GUIA_LIMPIEZA.md](GUIA_LIMPIEZA.md)

---

## 📊 Características Principales

### ✅ Implementadas
- ✅ Sistema de autenticación con SHA-256
- ✅ Interfaz modular con Tkinter
- ✅ Módulo de búsqueda de docentes
- ✅ Módulo de gestión de oficios
- ✅ Descarga de documentos
- ✅ Apertura de PDFs
- ✅ Compilación a ejecutable
- ✅ Splash screen de carga

### 🚧 En Desarrollo
- 🔄 Mejora de filtros (disposición y espaciado)
- 🔄 Búsqueda avanzada por nombre de docente
- 🔄 Descarga completa de expedientes
- 🔄 Interfaz mejorada de oficios

### 📋 Futuras Mejoras
- [ ] Sistema de logging completo
- [ ] Tests unitarios
- [ ] Manejo robusto de errores
- [ ] Modelos de datos con clases
- [ ] Caché de búsquedas
- [ ] Exportación a Excel
- [ ] Búsqueda avanzada con operadores booleanos
- [ ] Sincronización automática con Google Drive
- [ ] Panel de administración
- [ ] Auditoría de accesos

---

## 🏛️ Ventajas de la Arquitectura Modular

### **Antes (Versión Monolítica)**
```
❌ 1392 líneas en un solo archivo
❌ 68 funciones mezcladas sin separación
❌ Variables globales dispersas
❌ Difícil de mantener y extender
❌ Imposible hacer testing
❌ Código duplicado
```

### **Ahora (Versión Modular)**
```
✅ Código distribuido en 20+ archivos especializados
✅ Separación clara de responsabilidades (MVC)
✅ Componentes reutilizables
✅ Fácil de mantener y extender
✅ Preparado para testing
✅ Código limpio y documentado
✅ Facilita trabajo colaborativo
```

---

## 👥 Equipo de Desarrollo

**Universidad Central del Ecuador**
- **Unidad de Gestión de Doctorados**
- **Facultad de Ingeniería y Ciencias Aplicadas**
- **Carrera de Ingeniería en Ciencias de la Computación**

### Versión Actual (2025-2026)
- Wulfer Quiguango
- Bryan Loya
- Dennis Trujillo
- Marielena Gonzalez
- Mariel Milan

### Versión Anterior (2024-2025)
- Kevin Pozo
- Jordy Chamba
- Freddy Tapia

---

## 📜 Licencia

Este proyecto está bajo la licencia **Apache 2.0**

Ver [LICENSE](LICENSE) para más detalles.

---

## 📞 Soporte y Contacto

Para reportar bugs, sugerir mejoras o hacer preguntas:
- 📧 Contactar a la Unidad de Gestión de Doctorados
- 🐛 Reportar issues en GitHub
- 📚 Consultar documentación en carpeta `/docs`

---

## 📝 Notas Importantes

1. **Google Drive**: La aplicación requiere acceso a Google Drive montado o sincronizado
2. **Contraseñas**: Las contraseñas se hashean con SHA-256, no se almacenan en texto plano
3. **Datos**: Base de datos de usuarios en `data/usuarios.json`
4. **Recursos**: Imágenes y assets en carpeta `imagenes/`
5. **Mantenimiento**: Ejecutar `clean.bat` regularmente para limpiar archivos temporales

---

**Última actualización**: 28/04/2026
**Versión**: 2.0
**Estado**: Activo en desarrollo
