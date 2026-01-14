# Mendez Control de Plagas — Plataforma Operativa (Web + App)
Plataforma integral para gestionar **operaciones, clientes, servicios, evidencia, activos con QR**, documentación (PDF), facturación y analítica para **Mendez Control de Plagas**. Diseñada para crecer hacia un SaaS multi-empresa en una fase posterior, pero **arranca 100% enfocada en una sola empresa**.

---

## 1) Objetivo del producto
Centralizar y profesionalizar el ciclo completo del servicio de control de plagas:

- **Antes del servicio**: clientes, sitios, presupuestos, contratos, agenda, rutas.
- **Durante el servicio (campo)**: órdenes de trabajo, checklist, escaneo QR, evidencia (fotos), consumo de insumos, firma.
- **Después del servicio**: reportes PDF, correctivas, tickets, facturación, cobros, tendencias e indicadores.

**Resultado esperado**: reducir retrabajos, mejorar trazabilidad/auditoría, aumentar productividad del técnico, estandarizar reportes y acelerar cobros.

---

## 2) Alcance inicial (Single-company)
- Una sola razón social / empresa: **Mendez Control de Plagas**
- Multi-usuario: admin, operaciones, técnicos, calidad, ventas, cliente portal (si aplica)
- Múltiples clientes y múltiples sitios por cliente
- App móvil para técnicos + Web administrativa + (opcional) Portal de clientes

---

## 3) Principios de diseño
1. **Offline-first en campo**: la app debe funcionar sin señal; sincroniza cuando vuelva.
2. **Evidencia y trazabilidad**: todo queda auditado (quién, qué, cuándo, dónde).
3. **Configurabilidad**: formularios, plantillas y catálogos editables sin tocar código.
4. **Datos normalizados**: modelo consistente que soporte reportes y tendencias.
5. **Escalabilidad futura**: preparar multi-tenant (SaaS) sin complicar el arranque.

---

## 4) Componentes del sistema
### 4.1 Web (Backoffice)
- Administración general (empresa, usuarios, permisos)
- CRM: clientes, sitios, contactos
- Operaciones: agenda, órdenes, asignación, ruteo (manual al inicio)
- Catálogos: tipos de servicio, tipos de activos, checklists, productos/insumos
- Reportes: generación, descarga, firma, historial
- Facturación: abonos, visitas, estados de cobro, exportaciones
- Analítica: tableros y KPIs

### 4.2 App móvil (Campo)
- Mis servicios de hoy / semana
- Check-in / check-out, geolocalización opcional
- Formularios por tipo de servicio (roedores / insectos / general IPM)
- Escaneo **QR** (activos: cebaderos/trampas/UV)
- Evidencia: fotos + observaciones
- Consumo de insumos
- Firma del cliente
- Modo offline + sincronización segura

### 4.3 Portal del cliente (Opcional en primera etapa)
- Acceso a reportes PDF y certificados
- Historial de visitas y hallazgos
- Tickets / avisos (avistamientos) con fotos
- Acciones correctivas pendientes y seguimiento

---

## 5) Roles y permisos (RBAC)
> RBAC = Role-Based Access Control + permisos finos por módulo.

### Roles sugeridos
- **Admin/Owner**: todo (configuración, usuarios, facturación, reportes, métricas)
- **Operaciones/Dispatcher**: agenda, asignación, reprogramaciones, rutas, órdenes
- **Técnico**: app campo, ejecución de OT, evidencia, firma, consumos
- **Calidad/Compliance**: revisión de reportes, tendencias, CAPA/correctivas
- **Ventas**: leads, cotizaciones, renovaciones (si se implementa CRM completo)
- **Cliente (Portal)**: lectura de reportes y tickets (si se habilita portal)

### Permisos granulares (ejemplos)
- Ver/editar clientes
- Ver/editar órdenes
- Ver costos e inventario (sí/no)
- Ver facturación y cobros (sí/no)
- Aprobar reportes y bloquear edición post-firma (sí/no)

---

## 6) Módulos funcionales (Checklist “no se escapa nada”)

### 6.1 Empresa y configuración
- Datos de empresa (razón social, CUIT, dirección, logo, firma digital opcional)
- Políticas: offline, geolocalización, obligatoriedad de fotos, etc.
- Catálogos editables:
  - Tipos de servicio (mensual, emergencia, inspección, refuerzo)
  - Tipos de plaga / hallazgo
  - Tipos de activos (cebadero, trampa, UV, feromona, etc.)
  - Productos / químicos / cebos
  - Motivos de no acceso / no conformidad
- Plantillas de reporte por cliente/industria

### 6.2 CRM — Clientes, sitios y áreas
- Cliente (empresa): razón social, CUIT, rubro, SLA, horarios, condiciones de acceso
- Contactos: nombres, roles (calidad, mantenimiento, compras), teléfonos, emails
- Sitios: plantas/sucursales/depósitos
- Áreas internas: sectores (Producción, Depósito, Perímetro, Sala máquinas)
- Adjuntos por sitio: planos, fotos, instrucciones de ingreso, EPP requerido
- Historial completo: servicios, hallazgos, tickets, facturas

### 6.3 Agenda y programación
- Calendario por técnico / por cliente / por zona
- Servicios recurrentes (mensual / quincenal / semanal)
- Reprogramación con motivo (lluvia, acceso denegado, etc.)
- Ventanas horarias y duración estimada
- Planificación diaria (lista + mapa)
- Notificaciones internas (cambios de agenda)

### 6.4 Órdenes de trabajo (OT)
- OT generada desde agenda o manual
- Estados (borrador → asignada → en curso → finalizada → reportada → cerrada/facturada)
- Check-in/out (con hora real)
- Actividades y checklist
- Evidencia (fotos, notas, hallazgos)
- Firma cliente
- Bloqueo de edición post-cierre (según permisos)

### 6.5 Activos y QR (trazabilidad de campo)
- Registro de activos por sitio/área:
  - Código interno, tipo, estado, fecha instalación, coordenada (opcional)
- QR único por activo (impresión masiva)
- Flujo de campo:
  - Escanear QR → abre activo → registrar actividad (consumo/captura/limpieza)
  - Adjuntar foto, observación y condición del activo
- Reporte automático:
  - Tabla de activos intervenidos + novedades por activo
- Tendencias por activo:
  - consumo/capturas por período, activos con actividad alta

### 6.6 Hallazgos, no conformidades y correctivas (CAPA-lite)
- Hallazgo: tipo, severidad, evidencia, ubicación
- Recomendación / acción correctiva:
  - responsable (cliente / Mendez), fecha objetivo, estado
- Seguimiento:
  - vencimientos, recordatorios, historial de cambios

### 6.7 Tickets / avisos (reactivo)
- Ticket creado por operaciones o por cliente (si portal)
- Clasificación: avistamiento, reclamo, urgencia
- SLA: tiempo objetivo de respuesta
- Resolución: OT asociada + evidencia + cierre

### 6.8 Inventario e insumos (mínimo viable y luego avanzado)
- Catálogo de insumos/productos
- Stock central + stock por técnico/vehículo (futuro)
- Consumo por OT (cuánto, unidad, lote/vencimiento opcional)
- Alertas: stock bajo, vencimientos próximos
- (Fase avanzada) SDS/MSDS y registro de aplicación

### 6.9 Reportes y documentos (PDF)
- Reporte de visita (por OT):
  - encabezado (cliente/sitio/fecha/técnico)
  - resumen ejecutivo
  - actividades realizadas
  - tabla de activos revisados (QR)
  - hallazgos + fotos
  - recomendaciones/correctivas
  - firma y aclaración
- Plantillas por cliente:
  - logo cliente, textos legales, anexos (plano, certificados, etc.)
- Versionado:
  - v1 borrador / vfinal firmada
- Exportaciones:
  - PDF individual y lotes (mes/cliente)
  - Excel/CSV de tendencias y activos (para auditorías)

### 6.10 Facturación y cobros (adaptado a Argentina)
- Modelos:
  - Abono mensual (X visitas) + extras (emergencias)
  - Por visita
- Estados:
  - pendiente → facturado → cobrado → vencido
- Emisión:
  - interno (registro) + exportación para sistema contable / AFIP (según integración futura)
- Recordatorios de pago (si se integra mensajería)

### 6.11 Analítica y KPIs
- Operaciones:
  - visitas realizadas vs planificadas
  - tiempo promedio por OT
  - retrabajos (OT repetidas por ticket)
- Cliente:
  - hallazgos por área/mes, tendencia
  - activos con actividad alta
- Negocio:
  - facturación por cliente/mes
  - mora / días promedio de cobro
  - rentabilidad estimada por contrato (cuando haya costos/insumos completos)

---

## 7) Flujos principales (end-to-end)

### 7.1 Flujo “Servicio programado”
1) Operaciones agenda visita recurrente  
2) Se crea OT y se asigna técnico  
3) Técnico en app: check-in → checklist → escaneo QR activos → fotos → firma  
4) OT se finaliza → se genera PDF → queda disponible en web/portal  
5) (Opcional) se dispara facturación según contrato

### 7.2 Flujo “Ticket / emergencia”
1) Entra ticket (cliente/operaciones) con urgencia  
2) Operaciones crea OT emergencia y asigna  
3) Se ejecuta y se reporta igual que un servicio normal  
4) Ticket cierra con evidencia

### 7.3 Flujo “Correctivas”
1) Técnico registra hallazgo (no conformidad)  
2) Se crea recomendación/acción correctiva con fecha objetivo  
3) Operaciones/Calidad monitorea vencimientos  
4) Cliente confirma cierre (portal) o técnico valida en siguiente visita

---

## 8) Modelo de datos (entidades)
> Orientativo para arrancar bien desde el día 1.

### Core
- **User** (rol, permisos)
- **Customer** (cliente empresa)
- **Site** (sede/planta)
- **Area** (sector dentro del sitio)
- **Contact** (personas del cliente)
- **WorkOrder (OT)**
- **ServiceType** / **ChecklistTemplate**
- **Asset** (activo con QR)
- **AssetInspection** (evento de revisión por OT)
- **Finding** (hallazgo)
- **CorrectiveAction** (acción correctiva)
- **Ticket**
- **Attachment** (fotos/documentos)
- **Report** (PDF + metadata)
- **Contract** (abono, frecuencia, precios)
- **Invoice** / **Payment** (si se implementa completo)
- **InventoryItem** / **Consumption** (insumos)

### Relaciones clave (resumen)
- Customer 1—N Site
- Site 1—N Area
- Site/Area 1—N Asset
- WorkOrder N—1 Site, N—1 Technician(User)
- WorkOrder 1—N AssetInspection, 1—N Finding, 1—N Attachment
- Finding 1—N CorrectiveAction
- Ticket 1—N WorkOrder (o 1—1 según política)
- Contract 1—N WorkOrder (servicios programados)

---

## 9) Arquitectura recomendada (práctica y escalable)
### 9.1 Enfoque por capas
- **Frontend Web** (Admin/Operaciones/Calidad)
- **App móvil** (Técnicos)
- **Backend API** (autenticación, lógica, generación PDF, sincronización)
- **Base de datos** + **storage de archivos** (fotos/PDF)
- **Jobs/colas** (generación de PDF, notificaciones, exportaciones)

### 9.2 Stack sugerido (opción moderna, productiva)
- Web: React / Next.js
- App: React Native (Expo) o Flutter (priorizar offline)
- Backend: Node.js (NestJS) o Python (FastAPI)
- DB: PostgreSQL
- Cache/colas: Redis + BullMQ/Celery
- Storage: S3 compatible (AWS / Cloudflare R2 / MinIO)
- Auth: JWT + refresh, o proveedor (Auth0/Clerk) si se terceriza

> Nota: podés empezar simple y “endurecer” seguridad y colas en V1.

---

## 10) Offline y sincronización (requisito crítico)
### Estrategia
- App guarda local (SQLite/Realm) todas las OT asignadas, catálogos y activos relevantes del día.
- Operaciones “empuja” cambios (reprogramaciones) y app los toma al reconectar.
- Conflictos:
  - Regla: OT cerrada/finalizada no se reabre sin rol.
  - Los eventos de inspección/consumos se guardan como **append-only** (inmutable) para minimizar conflictos.

### Consideraciones
- Identificadores UUID locales
- “Last sync at” por usuario
- Reintentos robustos en subida de fotos
- Compresión de imágenes y límite por OT configurable

---

## 11) Seguridad, auditoría y cumplimiento
- MFA opcional para Admin
- Encriptación en tránsito (HTTPS) y en reposo (storage)
- Bitácora de auditoría:
  - login/logout, cambios de OT, cambios de clientes, eliminación (idealmente soft-delete)
- Políticas:
  - permisos por rol + por módulo
  - bloqueo de edición de reportes firmados
- Privacidad:
  - geolocalización opcional y con consentimiento por política de empresa

---

## 12) Generación de QR (operación real)
### Requisitos
- QR debe codificar: `asset_id` + checksum o token
- Formato de impresión:
  - plantilla A4/A5, tamaño etiqueta, opción con logo
- Flujo:
  - crear activos → generar lote de QRs → imprimir → pegar en sitio
- Reimpresión:
  - registro de reimpresión y motivo (daño, pérdida)

---

## 13) Reportes PDF (calidad “cliente industrial”)
### Contenido recomendado
- Portada (empresa, cliente, sitio, fecha, técnico)
- Resumen ejecutivo + observaciones generales
- Tabla de activos revisados con estado/novedad
- Hallazgos con fotos (antes/después si aplica)
- Recomendaciones / correctivas con vencimientos
- Firma digital o manuscrita + aclaración + DNI (si se requiere)
- Pie con trazabilidad (ID de OT, versión, timestamp)

### Plantillas
- Por industria/cliente (lácteas, alimentos, logística)
- Idioma (ES primero; EN futuro)

---

## 14) Integraciones (faseada)
### Inicial (V0/V1)
- Mapas: Google Maps / Mapbox (rutas simples)
- WhatsApp Business / Email para recordatorios (si se implementa)
- Exportaciones CSV para contabilidad

### Avanzado (V2)
- Pasarela de pagos
- Contabilidad/ERP
- API pública + webhooks (para clientes grandes)

---

## 15) Roadmap propuesto (sin humo, accionable)

### MVP (enfoque Mendez)
- Usuarios/roles
- Clientes/sitios/áreas/contactos
- Agenda básica + creación de OT
- App técnico: OT + checklist + fotos + firma
- Activos + QR + registro de inspección
- PDF de reporte (plantilla 1)
- Exportación CSV básica

### V1
- Recurrentes avanzados (abonos)
- Inventario y consumo por OT
- Tickets y correctivas con vencimientos
- Tableros básicos
- Portal cliente (descarga reportes + tickets)

### V2
- Tendencias IPM avanzadas (heatmaps, QBR)
- Ruteo optimizado automático
- Integraciones contables/pagos
- Multi-tenant para vender a otras empresas

---

## 16) Requerimientos no funcionales (NFR)
- Disponibilidad objetivo: 99.5% (MVP) → 99.9% (V2)
- Rendimiento:
  - carga de pantalla < 2s (web)
  - sync incremental (app)
- Escalabilidad:
  - miles de OT/año
  - storage de fotos/PDF por cliente
- Observabilidad:
  - logs estructurados, métricas, tracing
  - alertas por errores en generación de PDF y sync

---

## 17) QA y pruebas
- Unit tests: lógica backend (OT, reportes, permisos)
- Integration tests: API + DB
- E2E smoke: flujo OT completa con PDF
- Mobile: tests de sync offline/online (escenarios reales)
- Checklist de liberación: performance, seguridad, backups, rollback

---

## 18) Entornos y despliegue
- **Local** (dev)
- **Staging** (pruebas internas con datos simulados)
- **Production** (Mendez)

Recomendaciones:
- Migraciones de DB versionadas
- Backups automáticos diarios (DB + storage)
- Deploy con CI/CD (GitHub Actions)
- Gestión de secretos (Vault/SSM/Secrets Manager)

---

## 19) Convenciones de desarrollo
- Commits: Conventional Commits (`feat:`, `fix:`, `chore:`)
- Branching: `main` + `develop` (o trunk-based si son pocos)
- Versionado: SemVer
- API: OpenAPI/Swagger (documentación viva)
- Estándares de código: lint + formatter + pre-commit

---

## 20) Estructura de repositorio (sugerida)
- `/apps/web` (Backoffice)
- `/apps/mobile` (App técnicos)
- `/services/api` (Backend)
- `/services/pdf` (si se separa microservicio; opcional)
- `/packages/shared` (tipos, validaciones, utilidades)
- `/infra` (IaC: terraform/docker/k8s; opcional)

---

## 21) Glosario (para hablar todos igual)
- **OT**: Orden de Trabajo
- **Activo**: Cebadero, trampa, UV, etc.
- **Inspección de activo**: evento de revisión en una OT
- **Hallazgo**: evidencia/observación con posible impacto
- **Correctiva**: acción recomendada o requerida para cerrar hallazgo
- **IPM**: Manejo Integrado de Plagas
- **SLA**: acuerdo de niveles de servicio (tiempos de respuesta)

---

## 22) Criterios de aceptación (ejemplos)
- Un técnico puede cerrar una OT **offline**, adjuntar fotos y firma, y al reconectar:
  - se suben fotos,
  - se crea el reporte PDF,
  - la OT queda visible en web con estado “Reportada”.
- Un activo con QR escaneado registra:
  - estado del activo,
  - novedad (consumo/captura/limpieza),
  - foto opcional/obligatoria según política.
- Un reporte firmado queda **bloqueado** para edición salvo rol Admin.

---

## 23) Licencia y propiedad
Uso interno (Mendez Control de Plagas) hasta definir comercialización.
Si evoluciona a SaaS, definir licencia del código y Términos de Servicio.

---

## 24) Próximo paso recomendado (para empezar a construir mañana)
1) Definir **MVP exacto** en un backlog priorizado (user stories)  
2) Diseñar **pantallas mínimas**:
   - Web: clientes → sitios → activos; agenda; detalle OT; reporte
   - App: lista OT; detalle OT; escaneo QR; cámara; firma
3) Congelar **plantilla PDF v1** (un modelo)  
4) Elegir stack final y arrancar repositorio + CI/CD
