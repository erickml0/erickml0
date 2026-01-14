# Funcionalidades del Dashboard - Tainacan Digital Preservation

## Descripción General

El dashboard del plugin **Tainacan Digital Preservation (TDP)** proporciona una interfaz centralizada para gestionar todos los aspectos del sistema de preservación digital basado en el modelo OAIS (ISO 14721:2012). A continuación se describen las principales funcionalidades organizadas por sección.

---

## 1. Inicio (Dashboard)

### Descripción
El panel de inicio proporciona una visión general del estado del sistema de preservación digital, mostrando estadísticas clave y alertas importantes.

### Funcionalidades Principales

- **Estadísticas de Preservación**
  - Total de paquetes SIP creados
  - Total de paquetes AIP almacenados
  - Total de paquetes DIP generados
  - Espacio total utilizado en almacenamiento
  - Tasa de éxito de ingestas

- **Estado del Sistema**
  - Estado de las herramientas externas (Siegfried, ExifTool, FFmpeg, etc.)
  - Estado de conexión con sistemas de almacenamiento
  - Estado de las integraciones (AtoM, Koha, OAI-PMH)
  - Alertas de salud del sistema

- **Actividad Reciente**
  - Últimos eventos de preservación registrados
  - Últimas verificaciones de integridad
  - Últimas migraciones ejecutadas
  - Últimas exportaciones/importaciones

- **Alertas y Notificaciones**
  - Alertas de integridad fallida
  - Formatos en riesgo de obsolescencia
  - Errores en procesamiento
  - Tareas pendientes

- **Accesos Rápidos**
  - Crear nuevo SIP
  - Verificar integridad
  - Generar DIP
  - Configurar pipeline automático

---

## 2. Pipeline Automático

### Descripción
El pipeline automático permite configurar flujos de trabajo automatizados para el procesamiento de preservación digital, desde la ingesta hasta el almacenamiento final.

### Funcionalidades Principales

- **Configuración de Flujos de Trabajo**
  - Definir secuencia de pasos de procesamiento
  - Configurar reglas de activación automática
  - Establecer condiciones y filtros
  - Programar ejecución periódica

- **Pasos del Pipeline**
  - **Ingesta**: Captura automática de ítems del Tainacan
  - **Caracterización**: Identificación automática de formatos
  - **Normalización**: Conversión automática a formatos de preservación
  - **Validación**: Verificación de integridad y seguridad
  - **Empaquetado**: Creación automática de paquetes BagIt
  - **Generación de Metadatos**: Creación de METS y PREMIS
  - **Almacenamiento**: Transferencia a sistemas de almacenamiento

- **Monitoreo del Pipeline**
  - Estado de ejecución en tiempo real
  - Logs de procesamiento
  - Estadísticas de rendimiento
  - Manejo de errores y reintentos

- **Gestión de Colas**
  - Visualización de tareas pendientes
  - Priorización de tareas
  - Pausa/reanudación de procesamiento
  - Cancelación de tareas

---

## 3. Repositorio

### Descripción
El módulo de repositorio gestiona los paquetes OAIS (SIP, AIP, DIP) y las verificaciones de integridad de los objetos preservados.

### 3.1. Paquetes (SIP/AIP/DIP)

#### Funcionalidades

- **Gestión de SIP (Submission Information Package)**
  - Visualización de todos los SIPs creados
  - Detalles de cada SIP (metadatos, archivos, estado)
  - Búsqueda y filtrado de SIPs
  - Exportación de SIPs

- **Gestión de AIP (Archival Information Package)**
  - Listado de todos los AIPs almacenados
  - Información detallada de cada AIP
  - Verificación de checksums
  - Visualización de estructura BagIt
  - Acceso a metadatos METS y PREMIS

- **Gestión de DIP (Dissemination Information Package)**
  - Generación de DIPs bajo demanda
  - Listado de DIPs generados
  - Control de acceso y descargas
  - Gestión de expiración de enlaces

- **Operaciones**
  - Crear nuevo SIP desde ítem/colección
  - Convertir SIP a AIP
  - Generar DIP desde AIP
  - Eliminar paquetes (con confirmación)
  - Descargar paquetes completos

### 3.2. Verificación de Integridad

#### Funcionalidades

- **Verificación de Checksums**
  - Verificación individual de AIPs
  - Verificación masiva programada
  - Comparación de checksums SHA-256
  - Detección de corrupción de archivos

- **Reportes de Integridad**
  - Historial de verificaciones
  - Estadísticas de integridad
  - Alertas de fallos
  - Recomendaciones de acción

- **Reparación Automática**
  - Detección de archivos corruptos
  - Restauración desde réplicas
  - Regeneración de checksums
  - Notificaciones de problemas

---

## 4. Procesamiento

### Descripción
El módulo de procesamiento incluye todas las herramientas para analizar, caracterizar, normalizar y validar los objetos digitales antes de su preservación.

### 4.1. Caracterización

#### Funcionalidades

- **Identificación de Formatos**
  - Identificación automática vía Siegfried/PRONOM
  - Detección de PUID (PRONOM Unique Identifier)
  - Identificación de MIME types
  - Detección de versiones de formato

- **Análisis de Archivos**
  - Análisis de estructura de archivos
  - Detección de formatos comprimidos
  - Identificación de formatos contenedores
  - Análisis de metadatos embebidos

- **Reportes de Caracterización**
  - Reportes por formato
  - Estadísticas de formatos detectados
  - Alertas de formatos no identificados
  - Recomendaciones de normalización

### 4.2. Metadatos Técnicos

#### Funcionalidades

- **Extracción de Metadatos**
  - Extracción automática con ExifTool
  - Metadatos EXIF de imágenes
  - Metadatos de documentos (Office, PDF)
  - Metadatos de audio/video (MediaInfo)

- **Gestión de Metadatos**
  - Visualización de metadatos extraídos
  - Edición manual de metadatos
  - Validación de metadatos
  - Exportación de metadatos técnicos

- **Esquemas de Metadatos**
  - Dublin Core
  - PREMIS 3.0
  - METS 1.12
  - Esquemas personalizados

### 4.3. Normalización

#### Funcionalidades

- **Normalización de Imágenes**
  - Conversión a TIFF no comprimido
  - Preservación de resolución y color
  - Validación de calidad
  - Generación de derivados

- **Normalización de Documentos**
  - Conversión a PDF/A-2b
  - Preservación de estructura y metadatos
  - Validación de conformidad PDF/A
  - Generación de versiones accesibles

- **Normalización de Audio**
  - Conversión a WAV PCM 24-bit
  - Preservación de calidad de audio
  - Normalización de metadatos
  - Validación de formato

- **Normalización de Video**
  - Conversión a formatos de preservación (FFV1/MKV, MPEG-4)
  - Preservación de calidad
  - Extracción de pistas de audio
  - Generación de subtítulos

- **Gestión de Normalización**
  - Configuración de perfiles de normalización
  - Programación de normalizaciones masivas
  - Monitoreo de procesos
  - Gestión de archivos originales vs normalizados

### 4.4. Seguridad/Antivirus

#### Funcionalidades

- **Escaneo Antivirus**
  - Escaneo con ClamAV
  - Escaneo con VirusTotal (opcional)
  - Detección de malware
  - Cuarentena de archivos infectados

- **Validación de Seguridad**
  - Verificación de firmas digitales
  - Detección de archivos sospechosos
  - Análisis de comportamiento
  - Reportes de seguridad

- **Políticas de Seguridad**
  - Configuración de reglas de escaneo
  - Políticas de cuarentena
  - Notificaciones de amenazas
  - Integración con sistemas de seguridad

---

## 5. Empaquetamiento

### Descripción
El módulo de empaquetamiento gestiona la creación de paquetes conforme a estándares internacionales (BagIt, METS, PREMIS) para garantizar la preservación a largo plazo.

### 5.1. BagIt (RFC 8493)

#### Funcionalidades

- **Creación de Paquetes BagIt**
  - Generación automática de bags
  - Validación de estructura BagIt
  - Generación de manifestos (SHA-256)
  - Inclusión de metadatos opcionales

- **Gestión de Bags**
  - Visualización de estructura de bags
  - Validación de integridad
  - Verificación de checksums
  - Reparación de bags corruptos

- **Configuración**
  - Selección de algoritmo de checksum
  - Configuración de metadatos
  - Opciones de compresión
  - Validación de conformidad RFC 8493

### 5.2. METS (v1.12)

#### Funcionalidades

- **Generación de Manifiestos METS**
  - Creación automática de documentos METS
  - Estructura conforme a METS 1.12
  - Inclusión de metadatos descriptivos
  - Vinculación con archivos y metadatos técnicos

- **Gestión de METS**
  - Visualización de documentos METS
  - Validación de esquemas
  - Edición de metadatos
  - Exportación de METS

- **Secciones METS**
  - Header: Información del paquete
  - Descriptive Metadata: Metadatos Dublin Core
  - Administrative Metadata: Metadatos PREMIS
  - File Section: Lista de archivos
  - Structural Map: Estructura lógica

### 5.3. PREMIS 3.0

#### Funcionalidades

- **Registro de Eventos PREMIS**
  - Registro automático de eventos de preservación
  - Conformidad con PREMIS 3.0
  - Vinculación de eventos con objetos
  - Registro de agentes y derechos

- **Tipos de Eventos**
  - Ingesta (ingestion)
  - Migración (migration)
  - Verificación de integridad (fixity check)
  - Validación (validation)
  - Acceso (access)
  - Eliminación (deletion)

- **Gestión de PREMIS**
  - Visualización de eventos registrados
  - Búsqueda y filtrado de eventos
  - Exportación de registros PREMIS
  - Validación de conformidad

---

## 6. Preservación

### Descripción
El módulo de preservación incluye herramientas para garantizar la preservación a largo plazo, incluyendo monitoreo de obsolescencia, planificación de migraciones, replicación y recuperación ante desastres.

### 6.1. Replicación Geográfica

#### Funcionalidades

- **Configuración de Réplicas**
  - Configuración de múltiples ubicaciones de almacenamiento
  - Sincronización automática de AIPs
  - Verificación de réplicas
  - Gestión de políticas de replicación

- **Monitoreo de Réplicas**
  - Estado de sincronización
  - Detección de desincronizaciones
  - Alertas de fallos de replicación
  - Estadísticas de replicación

### 6.2. Monitor de Obsolescencia

#### Funcionalidades

- **Detección de Formatos en Riesgo**
  - Monitoreo basado en PRONOM
  - Alertas de formatos obsoletos
  - Evaluación de riesgo de obsolescencia
  - Recomendaciones de migración

- **Reportes de Obsolescencia**
  - Listado de formatos en riesgo
  - Estadísticas por formato
  - Historial de alertas
  - Planes de acción recomendados

### 6.3. Planificador de Migraciones

#### Funcionalidades

- **Planificación de Migraciones**
  - Identificación de objetos a migrar
  - Selección de formatos destino
  - Configuración de estrategias de migración
  - Programación de migraciones

- **Ejecución de Migraciones**
  - Ejecución automática de migraciones
  - Validación de migraciones
  - Preservación de versiones originales
  - Actualización de metadatos

- **Monitoreo de Migraciones**
  - Estado de migraciones en curso
  - Logs de ejecución
  - Estadísticas de éxito/fallo
  - Gestión de errores

### 6.4. Disaster Recovery

#### Funcionalidades

- **Backup y Restauración**
  - Generación de paquetes de recuperación
  - Backup de metadatos y configuraciones
  - Restauración desde backups
  - Validación de backups

- **Planificación de Recuperación**
  - Documentación de procedimientos
  - Planes de contingencia
  - Pruebas de recuperación
  - Evaluación de RTO/RPO

---

## 7. Integraciones

### Descripción
El módulo de integraciones permite conectar el sistema de preservación con otros sistemas de gestión de información (AtoM, Koha, OAI-PMH, Barramento de integración).

### 7.1. AtoM (Access to Memory)

#### Funcionalidades

- **Configuración de Instancias**
  - Creación de múltiples instancias AtoM
  - Configuración de conexión (URL, API Key)
  - Prueba de conectividad
  - Gestión de credenciales

- **Exportación a AtoM**
  - Exportación de AIPs como descripciones archivísticas
  - Mapeo de metadatos (Dublin Core → ISAD(G))
  - Creación de jerarquías archivísticas
  - Vinculación de objetos digitales

- **Importación desde AtoM**
  - Importación de descripciones archivísticas
  - Creación automática de SIPs
  - Sincronización de metadatos
  - Gestión de relaciones jerárquicas

- **Sincronización**
  - Sincronización bidireccional automática
  - Resolución de conflictos
  - Logs de sincronización
  - Gestión de cola de sincronización

### 7.2. Koha

#### Funcionalidades

- **Integración con ILS**
  - Conexión con sistema Koha
  - Importación de registros bibliográficos
  - Sincronización de metadatos
  - Vinculación con objetos digitales

### 7.3. OAI-PMH

#### Funcionalidades

- **Proveedor OAI-PMH 2.0**
  - Exposición de metadatos vía OAI-PMH
  - Configuración de sets y metadatos
  - Soporte para múltiples formatos de metadatos
  - Gestión de identificadores persistentes

### 7.4. Barramento de Integración

#### Funcionalidades

- **Integración con Sistemas Externos**
  - API REST para integraciones
  - Webhooks para eventos
  - Transformación de datos
  - Gestión de flujos de trabajo

---

## 8. Conformidad

### Descripción
El módulo de conformidad permite evaluar y documentar el cumplimiento del sistema con estándares internacionales de preservación digital.

### Funcionalidades Principales

- **Evaluación de Conformidad**
  - Matriz de conformidad ISO 16363
  - Evaluación de requisitos OAIS
  - Análisis de brechas
  - Generación de reportes

- **Documentación de Políticas**
  - Generación automática de políticas
  - Documentación de procedimientos
  - Registro de decisiones de preservación
  - Mantenimiento de documentación

- **Auditoría**
  - Logs de auditoría
  - Trazabilidad de acciones
  - Reportes de cumplimiento
  - Certificaciones

---

## 9. Configuraciones

### Descripción
El módulo de configuraciones permite personalizar todos los aspectos del sistema de preservación digital.

### Funcionalidades Principales

- **Configuración General**
  - Rutas de almacenamiento
  - Configuración de herramientas externas
  - Configuración de logs
  - Configuración de notificaciones

- **Configuración de Almacenamiento**
  - Almacenamiento local
  - FTP/SFTP
  - WebDAV
  - S3/MinIO

- **Configuración de Procesamiento**
  - Perfiles de normalización
  - Configuración de caracterización
  - Políticas de seguridad
  - Configuración de pipeline

- **Configuración de Integraciones**
  - Configuración de AtoM
  - Configuración de Koha
  - Configuración de OAI-PMH
  - Configuración de barramento

- **Configuración de Preservación**
  - Políticas de replicación
  - Configuración de migraciones
  - Configuración de disaster recovery
  - Configuración de obsolescencia

---

## Navegación y Accesos Rápidos

### Menú Principal
El menú principal del dashboard está organizado en secciones lógicas que facilitan el acceso a todas las funcionalidades:

- **Inicio**: Panel de control principal
- **Pipeline Automático**: Configuración de flujos de trabajo
- **Repositorio**: Gestión de paquetes y verificación de integridad
- **Procesamiento**: Caracterización, metadatos, normalización y seguridad
- **Empaquetamiento**: BagIt, METS y PREMIS
- **Preservación**: Replicación, obsolescencia, migraciones y recovery
- **Integraciones**: AtoM, Koha, OAI-PMH y barramento
- **Conformidad**: Evaluación y documentación de conformidad
- **Configuraciones**: Personalización del sistema

### Atajos de Teclado
- `Ctrl+K`: Búsqueda global
- `Ctrl+N`: Crear nuevo SIP
- `Ctrl+S`: Guardar configuraciones
- `Esc`: Cerrar diálogos

---

## Notas Adicionales

- Todas las funcionalidades requieren permisos de administrador
- Los procesos largos se ejecutan en segundo plano
- Se mantiene un registro completo de todas las operaciones
- El sistema es completamente conforme con el modelo OAIS (ISO 14721:2012)

