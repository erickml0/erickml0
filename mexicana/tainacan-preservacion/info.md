# Tainacan Digital Preservation (TDP) - Plugin WordPress

## Preservación Digital para Tainacan siguiendo el modelo OAIS (ISO 14721:2012)

[![WordPress Plugin](https://img.shields.io/badge/WordPress-5.8%2B-blue.svg)](https://wordpress.org/)
[![PHP Version](https://img.shields.io/badge/PHP-7.4%2B-purple.svg)](https://php.net/)
[![License](https://img.shields.io/badge/License-GPL%20v2%2B-green.svg)](https://www.gnu.org/licenses/gpl-2.0.html)
[![Version](https://img.shields.io/badge/Version-2.4.0-orange.svg)](https://github.com/)

---

## Índice

1. [Visión General](#visión-general)
2. [Requisitos](#requisitos)
3. [Instalación](#instalación)
4. [Estructura del Plugin](#estructura-del-plugin)
5. [Módulos](#módulos)
6. [Configuración](#configuración)
7. [Uso](#uso)
8. [API REST](#api-rest)
9. [Integración AtoM](#integración-atom)
10. [Estándares y Conformidad](#estándares-y-conformidad)
11. [Solución de Problemas](#solución-de-problemas)
12. [Changelog](#changelog)
13. [Licencia](#licencia)

---

## Visión General

El **Tainacan Digital Preservation (TDP)** es un plugin WordPress que implementa el modelo OAIS (Open Archival Information System - ISO 14721:2012) para preservación digital de largo plazo, integrado al repositorio digital Tainacan.

### Principales Funcionalidades

- **Gestión de Paquetes OAIS**: Generación y gestión de SIP, AIP y DIP
- **Verificación de Integridad**: Checksums SHA-256 con verificación periódica
- **Caracterización de Formatos**: Identificación vía Siegfried/PRONOM
- **Normalización**: Conversión a formatos de preservación (TIFF, PDF/A, WAV PCM)
- **Empaquetado BagIt**: Conformidad con RFC 8493
- **Metadatos PREMIS 3.0**: Registro completo de eventos de preservación
- **Manifiesto METS**: Estructura de metadatos descriptivos
- **Monitor de Obsolescencia**: Alertas sobre formatos en riesgo
- **Planificador de Migraciones**: Planificación y ejecución de migraciones de formato
- **Integración AtoM**: Sincronización bidireccional con Access to Memory (v2.4.0)
- **Múltiples Storage**: Local, FTP, SFTP, WebDAV, S3/MinIO

---

## Requisitos

### Obligatorios
- WordPress 5.8+
- PHP 7.4+ (8.0+ recomendado)
- MySQL 5.7+ / MariaDB 10.3+
- Plugin Tainacan 0.19+
- Extensiones PHP: `zip`, `json`, `mbstring`, `curl`

### Opcionales (para funcionalidades avanzadas)
- Siegfried (identificación de formatos)
- ExifTool (extracción de metadatos)
- FFmpeg/FFprobe (normalización de medios)
- ImageMagick (normalización de imágenes)
- LibreOffice headless (conversión a PDF/A)
- ClamAV (verificación antivirus)

---

## Instalación

### 1. Subida del Plugin

```bash
# Vía terminal
cd wp-content/plugins/
unzip tainacan-digital-preservation.zip

# O vía FTP/SFTP
# Suba la carpeta a wp-content/plugins/
```

### 2. Activación

1. Acceda a **Plugins → Plugins Instalados**
2. Localice "Tainacan Digital Preservation"
3. Haga clic en **Activar**

### 3. Configuración Inicial

1. Acceda a **Preservación Digital → Configuraciones**
2. Configure la ruta de almacenamiento
3. Verifique las herramientas disponibles
4. Guarde las configuraciones

---

## Estructura del Plugin

```
tainacan-digital-preservation/
├── tainacan-digital-preservation.php    # Archivo principal
├── readme.txt                           # Readme WordPress
├── uninstall.php                        # Rutinas de desinstalación
├── composer.json                        # Dependencias PHP
│
├── admin/
│   ├── class-tdp-admin.php              # Clase principal admin
│   ├── css/
│   │   └── tdp-admin.css                # Estilos del panel
│   ├── js/
│   │   └── tdp-admin.js                 # Scripts del panel
│   └── partials/                        # Plantillas de páginas
│       ├── dashboard.php
│       ├── packages.php
│       ├── integrity.php
│       ├── integrations.php
│       ├── security.php
│       ├── characterization.php
│       ├── metadata-extractor-admin.php
│       └── settings.php
│
├── includes/
│   ├── class-tdp-activator.php          # Activación del plugin
│   ├── class-tdp-deactivator.php        # Desactivación
│   ├── class-tdp-i18n.php               # Internacionalización
│   ├── class-tdp-loader.php            # Cargador de hooks
│   └── tdp-upgrade-240.php              # Script upgrade v2.4.0
│
├── public/
│   ├── class-tdp-public.php             # Funcionalidades públicas
│   ├── css/tdp-public.css
│   └── js/tdp-public.js
│
└── modules/
    ├── ingest/
    │   └── class-tdp-ingest.php         # Ingesta SIP
    │
    ├── aip-generator/
    │   └── class-tdp-aip-generator.php  # Generación AIP
    │
    ├── storage/
    │   └── class-tdp-storage.php        # Estrategias storage
    │
    ├── access/
    │   └── class-tdp-access.php         # Control de acceso
    │
    ├── characterization/
    │   ├── class-tdp-format-identifier.php
    │   └── class-tdp-characterization-schema.php
    │
    ├── normalization/
    │   ├── class-tdp-image-normalizer.php
    │   ├── class-tdp-document-normalizer.php
    │   ├── class-tdp-filename-normalizer.php
    │   └── *-admin.php
    │
    ├── packaging/
    │   ├── class-tdp-bagit-handler.php  # BagIt RFC 8493
    │   ├── class-tdp-mets-generator.php # METS v1.12
    │   ├── class-tdp-premis-generator.php # PREMIS 3.0
    │   └── *-admin.php
    │
    ├── preservation-planning/
    │   ├── class-tdp-obsolescence-monitor.php
    │   ├── class-tdp-migration-planner.php
    │   ├── class-tdp-migration-executor.php
    │   └── *-admin.php
    │
    ├── security/
    │   ├── class-tdp-antivirus.php
    │   └── class-tdp-integrity-check.php
    │
    └── integration/                     # NUEVO v2.4.0
        ├── class-tdp-atom-integration.php
        ├── atom-integration-admin.php
        ├── atom-integration-overview.php
        ├── atom-integration-instances.php
        ├── atom-integration-export.php
        ├── atom-integration-import.php
        ├── atom-integration-mapping.php
        ├── atom-integration-queue.php
        └── atom-integration-settings.php
```

---

## Módulos

### 1. Ingesta (SIP)

Captura archivos y metadatos del Tainacan para generar paquetes SIP.

```php
// Crear SIP programáticamente
$ingest = TDP_Ingest::get_instance();
$sip_id = $ingest->create_sip($item_id);
```

### 2. Generador AIP

Convierte SIPs en AIPs con metadatos técnicos y checksums.

### 3. Caracterización de Formatos

Identificación vía PRONOM usando Siegfried.

```php
$identifier = TDP_Format_Identifier::get_instance();
$result = $identifier->identify('/path/to/file.pdf');
// Retorna: puid, mime_type, format_name, version
```

### 4. Normalización

**Imágenes → TIFF**
```php
$normalizer = TDP_Image_Normalizer::get_instance();
$tiff_path = $normalizer->normalize('/path/to/image.jpg');
```

**Documentos → PDF/A**
```php
$normalizer = TDP_Document_Normalizer::get_instance();
$pdfa_path = $normalizer->convert_to_pdfa('/path/to/doc.docx');
```

### 5. BagIt (RFC 8493)

```php
$bagit = TDP_BagIt_Handler::get_instance();
$bag_path = $bagit->create_bag($aip_path, [
    'algorithm' => 'sha256',
    'include_fetch' => false
]);
```

### 6. PREMIS 3.0

```php
$premis = TDP_PREMIS_Generator::get_instance();
$premis->generate_event([
    'type' => 'ingestion',
    'outcome' => 'success',
    'linking_object_id' => $aip_id
]);
```

### 7. Monitor de Obsolescencia

Monitorea formatos en riesgo basado en PRONOM y alertas configurables.

### 8. Planificador de Migraciones

Planea y ejecuta migraciones de formato a formatos de preservación.

### 9. Integración AtoM (v2.4.0)

Sincronización bidireccional completa con Access to Memory.

---

## Configuración

### Almacenamiento

```
Preservación Digital → Configuraciones → Almacenamiento
```

| Opción | Descripción |
|--------|-------------|
| **Local** | Directorio en el servidor |
| **FTP/SFTP** | Servidor remoto |
| **WebDAV** | Protocolo WebDAV |
| **S3/MinIO** | Object Storage compatible S3 |

### Herramientas Externas

Configure las rutas en **Configuraciones**:

```
Siegfried: /usr/local/bin/sf
ExifTool: /usr/bin/exiftool
FFprobe: /usr/bin/ffprobe
ImageMagick: /usr/bin/convert
```

### Formatos de Preservación

| Tipo | Formato Original | Formato Preservación |
|------|------------------|----------------------|
| Imagen | JPEG, PNG, GIF, BMP | TIFF no comprimido |
| Documento | DOCX, ODT, RTF | PDF/A-2b |
| Audio | MP3, AAC, FLAC | WAV PCM 24-bit |
| Video | MP4, AVI, MOV | FFV1/MKV o MPEG-4 |

---

## Uso

### Dashboard

Acceda a **Preservación Digital** en el menú admin para visualizar:

- Estadísticas de preservación
- Colecciones e ítems
- Estado de la cola de procesamiento
- Alertas de integridad

### Crear SIP

1. Seleccione un ítem/colección
2. Haga clic en **Iniciar Preservación**
3. Configure opciones (ítems legados, nuevos ítems)
4. El SIP se crea automáticamente

### Verificar Integridad

```
Preservación Digital → Integridad → Verificar
```

### Generar DIP

1. Acceda a **Paquetes**
2. Localice el AIP deseado
3. Haga clic en **Generar DIP**
4. Descarga disponible por 7 días

---

## API REST

### Endpoints Principales

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/wp-json/tdp/v1/sips` | Listar SIPs |
| POST | `/wp-json/tdp/v1/sips` | Crear SIP |
| GET | `/wp-json/tdp/v1/aips` | Listar AIPs |
| GET | `/wp-json/tdp/v1/aips/{id}` | Detalles AIP |
| POST | `/wp-json/tdp/v1/dips` | Generar DIP |
| GET | `/wp-json/tdp/v1/integrity/{aip_id}` | Verificar integridad |
| GET | `/wp-json/tdp/v1/status` | Estado del sistema |

### Autenticación

```bash
# Cookie authentication (logged in)
curl -X GET "https://site.com/wp-json/tdp/v1/aips" \
  -H "X-WP-Nonce: $NONCE"

# Application Password
curl -X GET "https://site.com/wp-json/tdp/v1/aips" \
  -u "username:application_password"
```

---

## Integración AtoM

### Visión General (v2.4.0)

Integración bidireccional completa con AtoM (Access to Memory):

- **Exportar**: Enviar AIPs/DIPs como descripciones archivísticas
- **Importar**: Traer descripciones del AtoM para crear SIPs
- **Sincronizar**: Mantener ambos sistemas actualizados

### Instalación del Módulo AtoM

#### Archivos Necesarios

```
modules/integration/
├── class-tdp-atom-integration.php    # Clase principal
├── atom-integration-admin.php        # Interfaz admin (función)
├── atom-integration-overview.php     # Tab: Visión general
├── atom-integration-instances.php    # Tab: Instancias
├── atom-integration-export.php       # Tab: Exportar
├── atom-integration-import.php       # Tab: Importar
├── atom-integration-mapping.php      # Tab: Mapeo
├── atom-integration-queue.php        # Tab: Cola
└── atom-integration-settings.php     # Tab: Configuraciones

admin/
└── class-tdp-admin.php               # Actualizado con menú AtoM

tainacan-digital-preservation.php     # Actualizado v2.4.0
```

#### Paso a Paso

1. **Copie los archivos** a las carpetas correspondientes

2. **Reemplace `class-tdp-admin.php`** en `admin/`

3. **Reemplace `tainacan-digital-preservation.php`** en la raíz

4. **Acceda al WordPress** - las tablas se crearán automáticamente:
   - `wp_tdp_atom_instances`
   - `wp_tdp_atom_links`
   - `wp_tdp_atom_imports`
   - `wp_tdp_atom_queue`

### Configurar Instancia AtoM

1. Acceda a **Preservación Digital → Integración AtoM**
2. Haga clic en **Nueva Instancia**
3. Complete:
   - **Nombre**: Identificador
   - **URL**: `https://atom.ejemplo.com`
   - **API Key**: REST-API-Key del AtoM
   - **Cultura**: pt, pt_BR, en, es, fr
4. **Probar Conexión**
5. **Guardar**

### Mapeo Dublin Core → ISAD(G)

| Dublin Core | Campo AtoM (ISAD-G) |
|-------------|---------------------|
| dc:title | title |
| dc:creator | creators |
| dc:date | dates |
| dc:description | scopeAndContent |
| dc:subject | subjectAccessPoints |
| dc:identifier | referenceCode |
| dc:type | levelOfDescription |
| dc:format | extentAndMedium |
| dc:language | language |
| dc:rights | accessConditions |

### Exportar a AtoM

**Vía Interfaz:**
1. Pestaña **Exportar** → Seleccione AIPs
2. Elija instancia y descripción padre
3. Haga clic **Exportar**

**Vía Código:**
```php
$result = tdp_atom_export('aip_123', $instance_id, [
    'parent_slug' => 'fondo-principal',
    'level' => 'item'
]);
```

### Importar de AtoM

**Vía Interfaz:**
1. Pestaña **Importar** → Seleccione instancia
2. Configure filtros
3. Haga clic **Importar**

**Vía Código:**
```php
$result = tdp_atom_import($instance_id, [
    'query' => 'fotografias',
    'limit' => 50
]);
```

### Sincronización Automática

Configure en **Configuraciones**:
- Intervalo: hourly, daily, weekly
- Dirección: bidireccional, exportar, importar

### API REST AtoM

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/wp-json/tdp/v1/atom/instances` | Listar instancias |
| POST | `/wp-json/tdp/v1/atom/instances` | Crear instancia |
| POST | `/wp-json/tdp/v1/atom/instances/{id}/test` | Probar conexión |
| POST | `/wp-json/tdp/v1/atom/export/{aip_id}` | Exportar AIP |
| POST | `/wp-json/tdp/v1/atom/import` | Importar descripciones |
| POST | `/wp-json/tdp/v1/atom/sync` | Sincronizar |
| GET | `/wp-json/tdp/v1/atom/hierarchy/{id}` | Navegar jerarquía |

---

## Estándares y Conformidad

El TDP sigue los principales estándares de preservación digital:

| Estándar | Descripción | Estado |
|----------|-------------|--------|
| **ISO 14721:2012** | OAIS - Modelo de referencia | ✅ Implementado |
| **RFC 8493** | BagIt File Packaging | ✅ Implementado |
| **PREMIS 3.0** | Metadatos de preservación | ✅ Implementado |
| **METS 1.12** | Estructura de metadatos | ✅ Implementado |
| **PRONOM** | Registro de formatos | ✅ Vía Siegfried |
| **ISAD(G)** | Descripción archivística | ✅ Mapeo AtoM |
| **Dublin Core** | Metadatos descriptivos | ✅ Soportado |
| **NDSA Levels** | Niveles de preservación | 🔄 En progreso |

---

## Solución de Problemas

### Error "headers already sent"

**Causa**: Archivo admin cargado antes de que WordPress procese headers.

**Solución**: Asegúrese de usar la versión corregida del `class-tdp-admin.php` que carga el archivo admin vía callback del menú.

### Tablas no creadas

**Solución**:
1. Desactive el plugin
2. Reactive el plugin
3. O ejecute manualmente:
```php
do_action('tdp_create_tables');
```

### Error de conexión AtoM

1. Verifique URL y API Key
2. Confirme API REST habilitada en AtoM
3. Pruebe: `GET /api/informationobjects`

### Timeout en importaciones

1. Aumente timeout en las configuraciones
2. Reduzca tamaño del lote
3. Use WP-CLI para operaciones grandes

### Herramientas no detectadas

```bash
# Verificar instalación
which sf exiftool ffprobe convert

# Probar Siegfried
sf -version
sf /path/to/file.pdf
```

---

== Changelog ==

= 3.0.0 =
* Versión de producción estable
* Optimización de rendimiento
* Documentación completa
* Correcciones de codificación UTF-8

= 2.8.0 =
* Módulo de Conformidad ISO 16363
* Generación automática de políticas
* Análisis de brechas

= 2.7.0 =
* Módulo Disaster Recovery
* Backup y restauración

= 2.6.0 =
* Integration Bus
* OAI-PMH 2.0 Provider

= 2.5.0 =
* Integración Koha ILS

= 2.4.0 =
* Integración AtoM completa

== Upgrade Notice ==

= 3.0.0 =
Versión de producción con optimizaciones importantes. Haga backup antes de actualizar.

== Additional Info ==

Para documentación completa, visite: https://github.com/tainacan/tainacan-digital-preservation

Para soporte: https://github.com/tainacan/tainacan-digital-preservation/issues
