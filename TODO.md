# 📋 TODO - Plan de Implementación Vigoentrena Odoo 17

> Plan detallado paso a paso para implementar Odoo 17 en Vigoentrena

**🎯 Objetivo:** Configurar completamente Odoo 17 como sistema ERP integral para centro de fisioterapia y ejercicio personalizado.

---

## 📊 Dashboard General

| Categoría | Total | ✅ Completado | 🔄 En proceso | ⏸️ Pendiente | ⚠️ Bloqueado |
|-----------|-------|---------------|---------------|--------------|--------------|
| **Investigación** | 15 | 0 | 1 | 14 | 0 |
| **Instalación** | 8 | 0 | 0 | 8 | 0 |
| **Core Modules** | 12 | 0 | 0 | 12 | 0 |
| **Clínica** | 6 | 0 | 0 | 6 | 0 |
| **Integraciones** | 10 | 0 | 0 | 10 | 0 |
| **App Móvil** | 5 | 0 | 0 | 5 | 0 |
| **Documentación** | 20 | 1 | 1 | 18 | 0 |
| **TOTAL** | **76** | **1** | **2** | **73** | **0** |

**Progreso global:** 1.3% (1/76 tareas completadas)

---

## 🎯 FASE 0: INVESTIGACIÓN Y PLANIFICACIÓN

**Estado:** 🔄 En proceso  
**Inicio:** 2025-10-03  
**Estimación:** 1-2 semanas  
**Prioridad:** 🔴 CRÍTICA

### 📚 0.1. Recopilación de Documentación

- [x] 0.1.1 - Lanzar investigación exhaustiva sobre Odoo 17
- [ ] 0.1.2 - Recopilar documentación oficial de Odoo 17
- [ ] 0.1.3 - Documentar repositorios GitHub relevantes
- [ ] 0.1.4 - Identificar módulos nativos necesarios
- [ ] 0.1.5 - Identificar módulos de terceros (OCA)
- [ ] 0.1.6 - Investigar módulos específicos para clínica/fisioterapia
- [ ] 0.1.7 - Documentar integraciones españolas (VeriFactu, AEAT)
- [ ] 0.1.8 - Investigar soluciones de WhatsApp Business API
- [ ] 0.1.9 - Analizar sistemas de reservas online
- [ ] 0.1.10 - Investigar firma digital compatible
- [ ] 0.1.11 - Documentar opciones de app móvil

**Entregables:**
- [ ] Lista completa de recursos y enlaces
- [ ] Comparativa de módulos disponibles
- [ ] Matriz de decisión (Community vs Enterprise)
- [ ] Estimación de costos

### 🗺️ 0.2. Arquitectura y Diseño

- [ ] 0.2.1 - Definir arquitectura del sistema (cloud vs on-premise)
- [ ] 0.2.2 - Diseñar flujos de trabajo principales
- [ ] 0.2.3 - Mapear procesos actuales de Vigoentrena
- [ ] 0.2.4 - Crear diagrama de módulos e integraciones
- [ ] 0.2.5 - Definir estructura de usuarios y permisos
- [ ] 0.2.6 - Planificar estrategia de backup
- [ ] 0.2.7 - Definir política de seguridad

**Entregables:**
- [ ] Diagrama de arquitectura
- [ ] Documento de flujos de trabajo
- [ ] Matriz de roles y permisos
- [ ] Plan de backup y recuperación

### 💰 0.3. Presupuesto y Recursos

- [ ] 0.3.1 - Calcular costos de licencias (si Enterprise)
- [ ] 0.3.2 - Estimar costos de hosting
- [ ] 0.3.3 - Presupuestar módulos de pago
- [ ] 0.3.4 - Evaluar necesidad de partner certificado
- [ ] 0.3.5 - Planificar recursos humanos necesarios

**Entregables:**
- [ ] Hoja de presupuesto detallada
- [ ] Análisis ROI
- [ ] Plan de formación del equipo

---

## 🚀 FASE 1: INSTALACIÓN Y CONFIGURACIÓN BASE

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fase 0  
**Estimación:** 1-2 semanas  
**Prioridad:** 🔴 CRÍTICA

### 🖥️ 1.1. Preparación del Entorno

**Prerequisitos:**
- Decidir: Odoo.sh vs VPS propio vs On-premise
- Si VPS: Contratar servidor (recomendado: 8GB RAM, 4 cores, 80GB SSD)
- Si Odoo.sh: Crear cuenta enterprise

**Tareas:**

- [ ] 1.1.1 - Preparar servidor/entorno de producción
  - [ ] Instalar Ubuntu 22.04 LTS (si VPS propio)
  - [ ] Configurar firewall (ufw)
  - [ ] Configurar SSH con clave pública
  - [ ] Instalar y configurar fail2ban
  
- [ ] 1.1.2 - Instalar dependencias del sistema
  ```bash
  # Ver: docs/01-guia-tecnica/instalacion-odoo17.md
  ```
  - [ ] Python 3.10+
  - [ ] PostgreSQL 14+
  - [ ] Node.js 16+
  - [ ] wkhtmltopdf
  - [ ] Git
  
- [ ] 1.1.3 - Configurar PostgreSQL
  - [ ] Crear usuario odoo
  - [ ] Crear base de datos
  - [ ] Configurar permisos
  - [ ] Optimizar configuración

**Entregables:**
- [ ] Servidor configurado y seguro
- [ ] Documentación de accesos
- [ ] Script de instalación automatizado

### 📦 1.2. Instalación de Odoo 17

- [ ] 1.2.1 - Decidir versión: Community vs Enterprise
  - [ ] Analizar diferencias críticas
  - [ ] Evaluar necesidad de módulos Enterprise
  - [ ] Decisión documentada

- [ ] 1.2.2 - Descargar/clonar Odoo 17
  ```bash
  git clone https://github.com/odoo/odoo.git --depth 1 --branch 17.0
  ```

- [ ] 1.2.3 - Crear entorno virtual Python
  ```bash
  python3 -m venv odoo-venv
  source odoo-venv/bin/activate
  ```

- [ ] 1.2.4 - Instalar dependencias Python
  ```bash
  pip install -r requirements.txt
  ```

- [ ] 1.2.5 - Configurar archivo odoo.conf
  - [ ] Configurar rutas
  - [ ] Configurar base de datos
  - [ ] Configurar addons_path
  - [ ] Configurar workers (multi-processing)

- [ ] 1.2.6 - Configurar Nginx como reverse proxy
  - [ ] Instalar Nginx
  - [ ] Configurar virtual host
  - [ ] Habilitar proxy_pass a Odoo

- [ ] 1.2.7 - Configurar SSL con Let's Encrypt
  - [ ] Instalar certbot
  - [ ] Generar certificado
  - [ ] Configurar renovación automática

- [ ] 1.2.8 - Configurar Odoo como servicio systemd
  ```bash
  # Crear /etc/systemd/system/odoo.service
  ```

**Entregables:**
- [ ] Odoo 17 instalado y corriendo
- [ ] Acceso vía HTTPS
- [ ] Servicio configurado para inicio automático
- [ ] Documentación de configuración

### 🎨 1.3. Configuración Inicial de Odoo

- [ ] 1.3.1 - Acceder a Odoo por primera vez
  - URL: https://tu-dominio.com
  - Crear base de datos

- [ ] 1.3.2 - Configurar información de la empresa
  - [ ] Nombre: Vigoentrena
  - [ ] Logo
  - [ ] Dirección completa
  - [ ] CIF/NIF
  - [ ] Datos de contacto
  - [ ] Configuración regional (España)

- [ ] 1.3.3 - Configurar usuarios administradores
  - [ ] Usuario admin principal
  - [ ] Usuarios secundarios
  - [ ] Configurar autenticación de dos factores (2FA)

- [ ] 1.3.4 - Instalar localización española
  - [ ] Módulo: l10n_es (Contabilidad España)
  - [ ] Configurar plan contable español
  - [ ] Configurar impuestos (IVA 21%, 10%, 4%)
  - [ ] Configurar ejercicio fiscal

**Entregables:**
- [ ] Empresa configurada en Odoo
- [ ] Usuarios creados y documentados
- [ ] Localización española activa

---

## ⚙️ FASE 2: MÓDULOS CORE (CRÍTICO - MÁXIMA PRIORIDAD)

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fase 1  
**Estimación:** 3-4 semanas  
**Prioridad:** 🔴 CRÍTICA

> ⚠️ **IMPORTANTE:** Esta es la fase MÁS CRÍTICA. Los módulos core son la columna vertebral del sistema. Cada módulo debe quedar perfectamente configurado y probado antes de avanzar.

### 👥 2.1. CRM - Gestión de Relaciones con Clientes

**Objetivo:** Sistema completo de gestión de leads, oportunidades y clientes.

- [ ] 2.1.1 - Instalar y activar módulo CRM
  
- [ ] 2.1.2 - Configurar pipeline de ventas
  - [ ] Definir etapas del embudo:
    - [ ] Nuevo Lead
    - [ ] Contacto realizado
    - [ ] Valoración inicial
    - [ ] Propuesta enviada
    - [ ] Negociación
    - [ ] Cliente ganado/perdido
  - [ ] Configurar probabilidades por etapa
  - [ ] Definir SLA por etapa

- [ ] 2.1.3 - Configurar fuentes de leads
  - [ ] Website
  - [ ] WhatsApp
  - [ ] Redes sociales
  - [ ] Referencias
  - [ ] Campañas marketing
  - [ ] Eventos

- [ ] 2.1.4 - Configurar equipos de ventas
  - [ ] Equipo Fisioterapia
  - [ ] Equipo Entrenamiento Personal
  - [ ] Equipo Clases Grupales

- [ ] 2.1.5 - Configurar puntuación de leads (Lead Scoring)
  - [ ] Criterios de cualificación
  - [ ] Reglas automáticas

- [ ] 2.1.6 - Configurar actividades y seguimientos
  - [ ] Tipos de actividades
  - [ ] Recordatorios automáticos
  - [ ] Templates de actividades

- [ ] 2.1.7 - Configurar informes y análisis
  - [ ] Dashboard de ventas
  - [ ] Análisis de conversión
  - [ ] Forecast de ingresos

**Entregables:**
- [ ] CRM completamente configurado
- [ ] Flujos de trabajo documentados
- [ ] Manual de uso para equipo comercial
- [ ] KPIs definidos y configurados

### 💰 2.2. Ventas y Cotizaciones

**Objetivo:** Gestión completa del ciclo de ventas desde cotización hasta factura.

- [ ] 2.2.1 - Instalar y activar módulo Ventas

- [ ] 2.2.2 - Configurar productos y servicios
  - [ ] **Servicios Fisioterapia:**
    - [ ] Sesión individual (45 min)
    - [ ] Sesión individual (60 min)
    - [ ] Bono 5 sesiones
    - [ ] Bono 10 sesiones
    - [ ] Valoración inicial
    - [ ] Sesión domicilio
  
  - [ ] **Servicios Entrenamiento:**
    - [ ] Entrenamiento personal (60 min)
    - [ ] Bono 5 entrenamientos
    - [ ] Bono 10 entrenamientos
    - [ ] Valoración funcional
  
  - [ ] **Clases Grupales:**
    - [ ] Clase suelta (todas las modalidades)
    - [ ] Bono mensual ilimitado
    - [ ] Bono 10 clases
    - [ ] Bono trimestral
  
  - [ ] **Material y Productos:**
    - [ ] Vendas
    - [ ] Cremas
    - [ ] Accesorios ejercicio
    - [ ] etc.

- [ ] 2.2.3 - Configurar lista de precios
  - [ ] Precio estándar
  - [ ] Descuentos por bonos
  - [ ] Precios especiales (estudiantes, jubilados, etc.)
  - [ ] Promociones temporales

- [ ] 2.2.4 - Configurar plantillas de cotización
  - [ ] Template fisioterapia
  - [ ] Template entrenamiento
  - [ ] Template clases grupales
  - [ ] Template combinado

- [ ] 2.2.5 - Configurar proceso de aprobación
  - [ ] Descuentos automáticos
  - [ ] Descuentos que requieren aprobación
  - [ ] Workflow de aprobaciones

- [ ] 2.2.6 - Configurar términos y condiciones
  - [ ] Política de cancelación
  - [ ] Política de reembolsos
  - [ ] Términos de uso instalaciones
  - [ ] Consentimientos necesarios

- [ ] 2.2.7 - Configurar documentos de venta
  - [ ] Plantilla de cotización
  - [ ] Plantilla de confirmación de pedido
  - [ ] Diseño corporativo

- [ ] 2.2.8 - Configurar seguimiento post-venta
  - [ ] Email automático de agradecimiento
  - [ ] Encuesta de satisfacción
  - [ ] Email de renovación de bonos

**Entregables:**
- [ ] Catálogo completo de productos/servicios
- [ ] Plantillas de cotización personalizadas
- [ ] Workflow de ventas optimizado
- [ ] Manual de procedimientos de venta

### 🏪 2.3. TPV / Punto de Venta

**Objetivo:** Sistema de cobro rápido y gestión de caja.

- [ ] 2.3.1 - Instalar y activar módulo Point of Sale

- [ ] 2.3.2 - Configurar TPV físico
  - [ ] Crear sesión de TPV "Recepción Vigoentrena"
  - [ ] Configurar categorías de productos rápidas
  - [ ] Configurar interfaz de usuario
  - [ ] Configurar modo offline (si necesario)

- [ ] 2.3.3 - Configurar métodos de pago
  - [ ] Efectivo
  - [ ] Tarjeta de crédito/débito
  - [ ] Bizum
  - [ ] Transferencia bancaria
  - [ ] Bonos prepagados (consumo de sesiones)

- [ ] 2.3.4 - Integrar terminal TPV físico (si aplica)
  - [ ] Investigar compatibilidad con Odoo
  - [ ] Configurar conexión
  - [ ] Probar transacciones

- [ ] 2.3.5 - Configurar gestión de caja
  - [ ] Apertura de caja
  - [ ] Arqueo de caja
  - [ ] Cierre de caja
  - [ ] Informes de caja

- [ ] 2.3.6 - Configurar tickets de TPV
  - [ ] Diseño de ticket
  - [ ] Información legal obligatoria
  - [ ] Logo y marca

- [ ] 2.3.7 - Configurar descuentos en TPV
  - [ ] Descuentos rápidos
  - [ ] Cupones/vouchers
  - [ ] Programas de fidelización

- [ ] 2.3.8 - Integrar TPV con inventario
  - [ ] Actualización automática stock
  - [ ] Alertas de stock bajo

**Entregables:**
- [ ] TPV completamente operativo
- [ ] Manual de operación de caja
- [ ] Procedimientos de apertura/cierre
- [ ] Integración con contabilidad verificada

### 📊 2.4. Contabilidad y Finanzas (CRÍTICO)

**Objetivo:** Contabilidad completa y cumplimiento fiscal español.

- [ ] 2.4.1 - Instalar y activar módulo Contabilidad

- [ ] 2.4.2 - Configurar plan contable español
  - [ ] Verificar instalación l10n_es
  - [ ] Revisar cuentas principales
  - [ ] Añadir cuentas específicas si necesario

- [ ] 2.4.3 - Configurar impuestos españoles
  - [ ] IVA 21% (general)
  - [ ] IVA 10% (reducido)
  - [ ] IVA 4% (superreducido)
  - [ ] IRPF (si aplica)
  - [ ] Recargo de equivalencia (si aplica)

- [ ] 2.4.4 - Configurar diarios contables
  - [ ] Diario de ventas
  - [ ] Diario de compras
  - [ ] Diario de caja
  - [ ] Diario de banco
  - [ ] Diarios específicos si necesarios

- [ ] 2.4.5 - Configurar cuentas bancarias
  - [ ] Conectar cuenta(s) bancaria(s)
  - [ ] Configurar conciliación bancaria
  - [ ] Configurar importación de extractos

- [ ] 2.4.6 - Configurar formas de pago
  - [ ] Inmediato
  - [ ] 30 días
  - [ ] 60 días
  - [ ] Personalizado

- [ ] 2.4.7 - Configurar facturación
  - [ ] Secuencias de numeración
  - [ ] Plantilla de factura
  - [ ] Configurar envío automático por email
  - [ ] Factura rectificativa

- [ ] 2.4.8 - Configurar proveedores y gastos
  - [ ] Categorías de gastos
  - [ ] Workflow de aprobación de gastos
  - [ ] Gestión de facturas de proveedor

- [ ] 2.4.9 - Configurar informes financieros
  - [ ] Balance de situación
  - [ ] Cuenta de resultados
  - [ ] Libro mayor
  - [ ] Libro diario
  - [ ] Modelo 303 (IVA)
  - [ ] Modelo 347
  - [ ] Modelo 111 (IRPF)

- [ ] 2.4.10 - Configurar presupuestos
  - [ ] Por departamento
  - [ ] Por categoría de gasto
  - [ ] Alertas de desviación

**Entregables:**
- [ ] Contabilidad completamente configurada
- [ ] Integración con TPV y Ventas verificada
- [ ] Procedimientos de cierre mensual
- [ ] Checklist de obligaciones fiscales
- [ ] Manual de contabilidad

### 📦 2.5. Inventario y Almacén

**Objetivo:** Control de stock de material clínico, deportivo y productos de venta.

- [ ] 2.5.1 - Instalar y activar módulo Inventario

- [ ] 2.5.2 - Configurar almacenes y ubicaciones
  - [ ] Almacén principal
  - [ ] Ubicaciones:
    - [ ] Recepción
    - [ ] Stock
    - [ ] Sala fisioterapia
    - [ ] Sala entrenamiento
    - [ ] Exposición/venta
    - [ ] Trastero

- [ ] 2.5.3 - Configurar categorías de productos
  - [ ] Material clínico
  - [ ] Material deportivo/fitness
  - [ ] Productos de venta
  - [ ] Productos de higiene/limpieza
  - [ ] Material de oficina

- [ ] 2.5.4 - Dar de alta productos en inventario
  - [ ] Nombre y descripción
  - [ ] Código de barras (si aplica)
  - [ ] Categoría
  - [ ] Precio de compra
  - [ ] Precio de venta
  - [ ] Proveedor habitual
  - [ ] Stock mínimo
  - [ ] Stock máximo
  - [ ] Unidad de medida

- [ ] 2.5.5 - Configurar rutas de reabastecimiento
  - [ ] Reglas de reabastecimiento automático
  - [ ] Punto de reorden
  - [ ] Cantidad de reorden

- [ ] 2.5.6 - Configurar recepciones y entregas
  - [ ] Workflow de recepción de mercancía
  - [ ] Control de calidad
  - [ ] Workflow de entrega

- [ ] 2.5.7 - Configurar ajustes de inventario
  - [ ] Proceso de inventario físico
  - [ ] Valoración de stock (FIFO, promedio, etc.)
  - [ ] Cuentas contables vinculadas

- [ ] 2.5.8 - Configurar trazabilidad (si necesario)
  - [ ] Números de serie
  - [ ] Lotes
  - [ ] Fechas de caducidad

**Entregables:**
- [ ] Inventario inicial cargado
- [ ] Procedimientos de gestión de stock
- [ ] Integración con ventas y compras
- [ ] Sistema de alertas de stock bajo

### 📅 2.6. Calendario y Citas (CRÍTICO)

**Objetivo:** Sistema de gestión de agenda para fisioterapeutas, entrenadores y clases.

- [ ] 2.6.1 - Instalar y activar módulo Calendario

- [ ] 2.6.2 - Configurar calendarios
  - [ ] Calendario por profesional (fisios)
  - [ ] Calendario por entrenador
  - [ ] Calendario de clases grupales
  - [ ] Calendario de instalaciones

- [ ] 2.6.3 - Configurar tipos de citas
  - [ ] Fisioterapia - Primera consulta (60 min)
  - [ ] Fisioterapia - Sesión seguimiento (45 min)
  - [ ] Entrenamiento personal (60 min)
  - [ ] Valoración funcional (45 min)
  - [ ] Clase grupal (según tipo)

- [ ] 2.6.4 - Configurar horarios laborables
  - [ ] Horarios por profesional
  - [ ] Días festivos
  - [ ] Vacaciones
  - [ ] Huecos bloqueados

- [ ] 2.6.5 - Configurar duración de citas
  - [ ] Duración estándar por tipo
  - [ ] Tiempo de buffer entre citas
  - [ ] Tiempo de limpieza/desinfección

- [ ] 2.6.6 - Configurar recordatorios automáticos
  - [ ] Email 24h antes
  - [ ] WhatsApp 24h antes (cuando esté integrado)
  - [ ] SMS 2h antes (opcional)

- [ ] 2.6.7 - Configurar política de cancelaciones
  - [ ] Plazo mínimo de cancelación
  - [ ] Penalizaciones por no asistencia
  - [ ] Reprogramación automática

- [ ] 2.6.8 - Configurar sincronización de calendarios
  - [ ] Google Calendar (si aplica)
  - [ ] Outlook Calendar (si aplica)
  - [ ] CalDAV

**Entregables:**
- [ ] Sistema de citas completamente funcional
- [ ] Calendarios sincronizados
- [ ] Política de citas documentada
- [ ] Manual de gestión de agenda

### 📧 2.7. Marketing y Automatización

**Objetivo:** Campañas de marketing y comunicación automatizada.

- [ ] 2.7.1 - Instalar y activar módulo Marketing Automation

- [ ] 2.7.2 - Configurar email marketing
  - [ ] Servidor SMTP
  - [ ] Templates de emails
  - [ ] Listas de distribución
  - [ ] Gestión de bajas (RGPD)

- [ ] 2.7.3 - Crear segmentos de clientes
  - [ ] Clientes activos fisioterapia
  - [ ] Clientes activos entrenamiento
  - [ ] Clientes activos clases grupales
  - [ ] Clientes inactivos (para reactivación)
  - [ ] Leads no convertidos

- [ ] 2.7.4 - Configurar campañas automáticas
  - [ ] Bienvenida nuevo cliente
  - [ ] Recordatorio renovación bono
  - [ ] Cumpleaños
  - [ ] Reactivación clientes inactivos
  - [ ] Solicitud de opinión/review

- [ ] 2.7.5 - Configurar SMS marketing (opcional)
  - [ ] Proveedor de SMS
  - [ ] Templates de mensajes
  - [ ] Campañas SMS

- [ ] 2.7.6 - Configurar landing pages
  - [ ] Página de captura leads
  - [ ] Página de ofertas especiales
  - [ ] Formularios integrados

- [ ] 2.7.7 - Configurar análisis y métricas
  - [ ] Tasa de apertura emails
  - [ ] Click-through rate
  - [ ] Conversiones
  - [ ] ROI por campaña

**Entregables:**
- [ ] Sistema de marketing automatizado
- [ ] Campañas básicas creadas
- [ ] Templates de comunicación
- [ ] Dashboard de métricas

### 🌐 2.8. Sitio Web

**Objetivo:** Presencia web corporativa básica (el booking avanzado va en Fase 3).

- [ ] 2.8.1 - Instalar y activar módulo Website

- [ ] 2.8.2 - Configurar diseño del sitio
  - [ ] Seleccionar tema
  - [ ] Aplicar branding (colores, logo)
  - [ ] Configurar menú de navegación

- [ ] 2.8.3 - Crear páginas principales
  - [ ] Inicio
  - [ ] Servicios
    - [ ] Fisioterapia
    - [ ] Entrenamiento personal
    - [ ] Clases grupales
  - [ ] Equipo
  - [ ] Instalaciones
  - [ ] Blog/Noticias
  - [ ] Contacto

- [ ] 2.8.4 - Configurar formularios de contacto
  - [ ] Formulario general
  - [ ] Formulario solicitud cita
  - [ ] Integración con CRM

- [ ] 2.8.5 - Configurar SEO básico
  - [ ] Meta tags
  - [ ] URLs amigables
  - [ ] Sitemap XML
  - [ ] robots.txt

- [ ] 2.8.6 - Configurar blog
  - [ ] Categorías
  - [ ] Plantilla de posts
  - [ ] Comentarios (si se desea)

- [ ] 2.8.7 - Integrar con redes sociales
  - [ ] Enlaces a perfiles sociales
  - [ ] Botones de compartir
  - [ ] Feed de Instagram (si aplica)

**Entregables:**
- [ ] Sitio web corporativo funcional
- [ ] Contenido básico publicado
- [ ] Formularios integrados con CRM
- [ ] SEO básico configurado

### 👥 2.9. Recursos Humanos (Básico)

**Objetivo:** Gestión básica de empleados y horarios.

- [ ] 2.9.1 - Instalar y activar módulo Employees

- [ ] 2.9.2 - Dar de alta empleados
  - [ ] Datos personales
  - [ ] Datos de contacto
  - [ ] Foto
  - [ ] Puesto de trabajo
  - [ ] Departamento
  - [ ] Manager/supervisor

- [ ] 2.9.3 - Configurar departamentos
  - [ ] Dirección
  - [ ] Fisioterapia
  - [ ] Entrenamiento
  - [ ] Recepción/Administración

- [ ] 2.9.4 - Configurar contratos (básico)
  - [ ] Tipos de contrato
  - [ ] Fechas de contrato
  - [ ] Jornada

- [ ] 2.9.5 - Configurar ausencias (opcional en esta fase)
  - [ ] Tipos de ausencias
  - [ ] Solicitud de vacaciones
  - [ ] Aprobación de ausencias

**Entregables:**
- [ ] Empleados dados de alta
- [ ] Organigrama básico
- [ ] Sistema de gestión de ausencias (si implementado)

### 📄 2.10. Documentos y Firma Digital

**Objetivo:** Gestión documental y firma electrónica de consentimientos.

- [ ] 2.10.1 - Instalar y activar módulo Documents

- [ ] 2.10.2 - Configurar estructura de carpetas
  - [ ] Documentos corporativos
  - [ ] Contratos
  - [ ] Facturas
  - [ ] Documentos clientes
    - [ ] Consentimientos informados
    - [ ] Informes médicos
    - [ ] Historiales
  - [ ] Recursos humanos
  - [ ] Proveedores

- [ ] 2.10.3 - Configurar permisos de acceso
  - [ ] Por rol
  - [ ] Por departamento
  - [ ] Documentos privados vs compartidos

- [ ] 2.10.4 - Instalar módulo de firma electrónica
  - [ ] Evaluar Sign vs DocuSign vs alternativas
  - [ ] Instalar módulo elegido
  - [ ] Configurar integración

- [ ] 2.10.5 - Crear plantillas de documentos firmables
  - [ ] Consentimiento informado fisioterapia
  - [ ] Consentimiento informado ejercicio
  - [ ] Contrato servicios
  - [ ] Política de privacidad (RGPD)
  - [ ] Cesión de imagen

- [ ] 2.10.6 - Configurar workflow de firma
  - [ ] Envío automático al cliente
  - [ ] Recordatorios si no firma
  - [ ] Almacenamiento documento firmado
  - [ ] Notificación a staff cuando firmado

**Entregables:**
- [ ] Sistema documental organizado
- [ ] Firma electrónica funcional
- [ ] Plantillas de consentimientos creadas
- [ ] Workflow de firma automatizado

### 🔗 2.11. Integraciones Internas

**Objetivo:** Asegurar que todos los módulos core están perfectamente integrados.

- [ ] 2.11.1 - Verificar integración CRM → Ventas
  - [ ] Lead convertido crea oportunidad de venta
  - [ ] Cliente ganado sincroniza con contactos

- [ ] 2.11.2 - Verificar integración Ventas → Inventario
  - [ ] Pedido confirmado actualiza stock
  - [ ] Stock insuficiente bloquea venta

- [ ] 2.11.3 - Verificar integración Ventas → Contabilidad
  - [ ] Factura de venta genera asiento contable
  - [ ] Cobro registrado actualiza contabilidad

- [ ] 2.11.4 - Verificar integración TPV → Contabilidad
  - [ ] Ventas TPV se registran contablemente
  - [ ] Cierre de caja cuadra con contabilidad

- [ ] 2.11.5 - Verificar integración TPV → Inventario
  - [ ] Venta en TPV descuenta stock

- [ ] 2.11.6 - Verificar integración Calendario → Ventas
  - [ ] Cita agendada desde venta
  - [ ] Cita completada puede facturarse

- [ ] 2.11.7 - Verificar integración Marketing → CRM
  - [ ] Leads de campañas llegan a CRM
  - [ ] Actividades de marketing se reflejan

- [ ] 2.11.8 - Verificar integración Documentos → CRM
  - [ ] Documentos vinculados a cliente
  - [ ] Firma completada registrada en cliente

**Entregables:**
- [ ] Matriz de integraciones verificada
- [ ] Todos los flujos principales testeados
- [ ] Documentación de integraciones

### 🧪 2.12. Testing Completo de Módulos Core

**Objetivo:** Asegurar que todo funciona correctamente antes de avanzar.

- [ ] 2.12.1 - Test: Flujo completo de venta
  - [ ] Lead → Oportunidad → Cotización → Pedido → Factura → Cobro
  - [ ] Verificar en cada paso que todo se registra correctamente

- [ ] 2.12.2 - Test: Gestión de citas
  - [ ] Crear cita → Confirmar → Recordatorio → Completar
  - [ ] Cancelar cita
  - [ ] Reprogramar cita

- [ ] 2.12.3 - Test: TPV completo
  - [ ] Abrir caja → Vender productos → Diferentes métodos de pago → Cerrar caja
  - [ ] Verificar cuadre contable

- [ ] 2.12.4 - Test: Contabilidad
  - [ ] Registrar factura de gasto
  - [ ] Registrar pago
  - [ ] Generar informes básicos

- [ ] 2.12.5 - Test: Inventario
  - [ ] Recepción de mercancía
  - [ ] Venta que descuenta stock
  - [ ] Ajuste de inventario

- [ ] 2.12.6 - Test: Documentos y firma
  - [ ] Subir documento
  - [ ] Enviar para firma
  - [ ] Firmar
  - [ ] Verificar almacenamiento

- [ ] 2.12.7 - Test: Marketing
  - [ ] Crear campaña email
  - [ ] Enviar a segmento
  - [ ] Verificar métricas

**Entregables:**
- [ ] Checklist de tests completado
- [ ] Issues encontrados y resueltos
- [ ] Módulos core certificados como funcionales

---

## 🏥 FASE 3: MÓDULOS CLÍNICOS Y OPERATIVOS

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fase 2 (Core 100% funcional)  
**Estimación:** 2-3 semanas  
**Prioridad:** 🟠 ALTA

### 🩺 3.1. Gestión de Pacientes

- [ ] 3.1.1 - Investigar módulos disponibles
  - [ ] healthcare (OCA)
  - [ ] medical (terceros)
  - [ ] Otros módulos clínicos

- [ ] 3.1.2 - Instalar módulo elegido

- [ ] 3.1.3 - Configurar ficha de paciente
  - [ ] Datos personales extendidos
  - [ ] Antecedentes médicos
  - [ ] Alergias
  - [ ] Medicación actual
  - [ ] Cirugías previas
  - [ ] Patologías crónicas
  - [ ] Contacto de emergencia

- [ ] 3.1.4 - Configurar historial clínico
  - [ ] Registro de consultas
  - [ ] Diagnósticos
  - [ ] Tratamientos aplicados
  - [ ] Evolución
  - [ ] Notas del profesional

- [ ] 3.1.5 - Configurar valoraciones
  - [ ] Plantillas de valoración inicial
  - [ ] Tests funcionales
  - [ ] Rangos de movimiento
  - [ ] Escalas de dolor
  - [ ] Objetivos de tratamiento

- [ ] 3.1.6 - Integrar con CRM y Ventas
  - [ ] Cliente → Paciente
  - [ ] Sesiones vendidas → Sesiones programables

**Entregables:**
- [ ] Módulo de pacientes funcional
- [ ] Plantillas de valoración creadas
- [ ] Manual de uso para fisioterapeutas

### 📋 3.2. Sesiones y Tratamientos

- [ ] 3.2.1 - Configurar tipos de sesiones
  - [ ] Fisioterapia manual
  - [ ] Electroterapia
  - [ ] Punción seca
  - [ ] Vendaje neuromuscular
  - [ ] Ejercicio terapéutico
  - [ ] etc.

- [ ] 3.2.2 - Configurar plantillas de tratamiento
  - [ ] Protocolos por patología
  - [ ] Secuencias de sesiones
  - [ ] Ejercicios recomendados

- [ ] 3.2.3 - Configurar registro de sesión
  - [ ] Técnicas aplicadas
  - [ ] Duración
  - [ ] Zonas tratadas
  - [ ] Evolución
  - [ ] Recomendaciones
  - [ ] Próxima cita

- [ ] 3.2.4 - Configurar planes de tratamiento
  - [ ] Objetivo del tratamiento
  - [ ] Número de sesiones estimadas
  - [ ] Frecuencia recomendada
  - [ ] Seguimiento de progreso

- [ ] 3.2.5 - Integrar con calendario
  - [ ] Cita de calendario → Registro de sesión
  - [ ] Completar sesión actualiza historial

**Entregables:**
- [ ] Sistema de sesiones funcional
- [ ] Plantillas de tratamiento creadas
- [ ] Historial clínico completo

### 💪 3.3. Gestión de Clases Grupales

- [ ] 3.3.1 - Configurar tipos de clases
  - [ ] Pilates
  - [ ] Yoga
  - [ ] GAP
  - [ ] Espalda sana
  - [ ] Funcional
  - [ ] etc.

- [ ] 3.3.2 - Configurar horario de clases
  - [ ] Parrilla semanal
  - [ ] Horarios por clase
  - [ ] Instructor asignado
  - [ ] Sala asignada

- [ ] 3.3.3 - Configurar capacidad y aforo
  - [ ] Aforo máximo por clase
  - [ ] Aforo mínimo para realizar clase
  - [ ] Lista de espera

- [ ] 3.3.4 - Configurar reservas de clases
  - [ ] Sistema de reserva
  - [ ] Confirmación automática
  - [ ] Check-in en recepción
  - [ ] Cancelación de reserva

- [ ] 3.3.5 - Configurar bonos de clases
  - [ ] Bono 10 clases
  - [ ] Bono mensual ilimitado
  - [ ] Bono trimestral
  - [ ] Consumo de bonos

- [ ] 3.3.6 - Configurar informes de asistencia
  - [ ] Asistencia por clase
  - [ ] Asistencia por alumno
  - [ ] Ocupación media
  - [ ] Clases más demandadas

**Entregables:**
- [ ] Sistema de clases grupales funcional
- [ ] Calendario de clases publicado
- [ ] Sistema de reservas operativo
- [ ] Informes de ocupación

### 📝 3.4. Consentimientos y Documentación Clínica

- [ ] 3.4.1 - Crear consentimiento informado fisioterapia
- [ ] 3.4.2 - Crear consentimiento informado ejercicio
- [ ] 3.4.3 - Crear ficha de anamnesis
- [ ] 3.4.4 - Crear plantilla informe de alta
- [ ] 3.4.5 - Configurar workflow de consentimientos
  - [ ] Envío automático en primera cita
  - [ ] Firma digital
  - [ ] Almacenamiento en historial
- [ ] 3.4.6 - Configurar cumplimiento RGPD/LOPD
  - [ ] Información al paciente
  - [ ] Consentimiento datos personales
  - [ ] Derecho de acceso
  - [ ] Derecho de rectificación
  - [ ] Derecho al olvido

**Entregables:**
- [ ] Documentación clínica completa
- [ ] Consentimientos digitalizados
- [ ] Cumplimiento legal verificado

---

## ⚖️ FASE 4: INTEGRACIONES CRÍTICAS (LEGAL Y FISCAL)

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fase 2  
**Estimación:** 2-3 semanas  
**Prioridad:** 🔴 CRÍTICA (Legal obligatorio)

### 📊 4.1. VeriFactu - Sistema de Facturación Verificable

> ⚠️ **OBLIGATORIO POR LEY EN ESPAÑA**

- [ ] 4.1.1 - Investigar módulos VeriFactu disponibles
  - [ ] Módulo oficial (si existe)
  - [ ] Módulos OCA
  - [ ] Módulos de partners certificados
  - [ ] Soluciones propietarias

- [ ] 4.1.2 - Seleccionar e instalar módulo VeriFactu
  - [ ] Evaluar opciones
  - [ ] Decisión documentada
  - [ ] Instalación

- [ ] 4.1.3 - Configurar VeriFactu
  - [ ] Certificado digital empresa
  - [ ] Configuración parámetros técnicos
  - [ ] Hash de facturas
  - [ ] Cadena de bloques

- [ ] 4.1.4 - Integrar con módulo de Ventas/Facturación
  - [ ] Todas las facturas pasan por VeriFactu
  - [ ] Validación antes de emisión

- [ ] 4.1.5 - Integrar con TPV
  - [ ] Tickets TPV cumplen VeriFactu
  - [ ] Verificación en tiempo real

- [ ] 4.1.6 - Configurar registro de facturas
  - [ ] Libro registro de facturas emitidas
  - [ ] Libro registro de facturas recibidas
  - [ ] Firma digital de libros

- [ ] 4.1.7 - Configurar comunicación con AEAT
  - [ ] Envío automático/manual
  - [ ] Verificación de recepción
  - [ ] Gestión de errores

- [ ] 4.1.8 - Testing exhaustivo
  - [ ] Factura de prueba
  - [ ] Verificación hash
  - [ ] Envío AEAT en entorno de pruebas
  - [ ] Validación con asesor fiscal

- [ ] 4.1.9 - Formación al equipo
  - [ ] Qué es VeriFactu
  - [ ] Importancia del cumplimiento
  - [ ] Procedimientos operativos

**Entregables:**
- [ ] VeriFactu completamente funcional
- [ ] Cumplimiento legal verificado
- [ ] Documentación de configuración
- [ ] Validación de asesor fiscal

### 🏛️ 4.2. Integración AEAT (Agencia Tributaria)

- [ ] 4.2.1 - Configurar certificado digital
  - [ ] Instalar certificado empresa
  - [ ] Configurar en Odoo

- [ ] 4.2.2 - Configurar SII (Suministro Inmediato de Información)
  - [ ] Si facturación > umbral
  - [ ] Configurar envío automático

- [ ] 4.2.3 - Configurar modelos tributarios
  - [ ] Modelo 303 (IVA trimestral)
  - [ ] Modelo 130 (IRPF trimestral) - si aplica
  - [ ] Modelo 111 (Retenciones trimestrales)
  - [ ] Modelo 347 (Operaciones con terceros anual)
  - [ ] Modelo 390 (Resumen anual IVA)

- [ ] 4.2.4 - Configurar generación automática de modelos
  - [ ] Extracción de datos de Odoo
  - [ ] Formato oficial
  - [ ] Exportación

- [ ] 4.2.5 - Configurar presentación telemática (si posible)
  - [ ] Conexión con AEAT
  - [ ] Firma digital
  - [ ] Envío

**Entregables:**
- [ ] Integración AEAT funcional
- [ ] Modelos tributarios automatizados
- [ ] Calendario fiscal configurado

### 📄 4.3. Facturación Electrónica (FACe/FACeB2B)

- [ ] 4.3.1 - Evaluar necesidad de factura electrónica
  - [ ] ¿Clientes administración pública?
  - [ ] ¿Grandes empresas que lo requieren?

- [ ] 4.3.2 - Si necesario: Instalar módulo factura-e
- [ ] 4.3.3 - Configurar formato Facturae
- [ ] 4.3.4 - Configurar envío a FACe/FACeB2B
- [ ] 4.3.5 - Integrar con proceso normal de facturación

**Entregables:**
- [ ] Facturación electrónica (si necesaria)
- [ ] Proceso de envío automatizado

---

## 📱 FASE 5: COMUNICACIONES Y ENGAGEMENT

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fase 2  
**Estimación:** 2-3 semanas  
**Prioridad:** 🔴 CRÍTICA (WhatsApp es canal principal)

### 💬 5.1. WhatsApp Business API

> 🔥 **PRIORITARIO:** Canal principal de comunicación con clientes

- [ ] 5.1.1 - Investigar soluciones de integración
  - [ ] WhatsApp Business API oficial
  - [ ] Proveedores intermediarios (Twilio, 360dialog, etc.)
  - [ ] Módulos Odoo disponibles
  - [ ] Comparativa de costos

- [ ] 5.1.2 - Contratar y configurar proveedor WhatsApp
  - [ ] Seleccionar proveedor
  - [ ] Verificar cuenta business
  - [ ] Obtener API key
  - [ ] Configurar número de teléfono
  - [ ] Verificar empresa con Meta

- [ ] 5.1.3 - Instalar módulo integración Odoo-WhatsApp
  - [ ] Módulo OCA (si existe)
  - [ ] Módulo de partner certificado
  - [ ] Módulo personalizado vía N8N (Fase 6)

- [ ] 5.1.4 - Configurar perfiles y permisos
  - [ ] Nombre del negocio
  - [ ] Descripción
  - [ ] Foto de perfil
  - [ ] Horario de atención
  - [ ] Enlace web

- [ ] 5.1.5 - Configurar plantillas de mensajes
  - [ ] Bienvenida
  - [ ] Confirmación de cita
  - [ ] Recordatorio de cita (24h antes)
  - [ ] Recordatorio de cita (2h antes)
  - [ ] Cancelación de cita
  - [ ] Reprogramación de cita
  - [ ] Confirmación de pago
  - [ ] Recordatorio renovación bono
  - [ ] Información sesiones restantes
  - [ ] Solicitud de feedback
  - [ ] Promociones especiales

- [ ] 5.1.6 - Obtener aprobación plantillas por Meta
  - [ ] Enviar para revisión
  - [ ] Ajustar según feedback
  - [ ] Aprobación final

- [ ] 5.1.7 - Configurar automatizaciones
  - [ ] Cita creada → Confirmación automática
  - [ ] 24h antes de cita → Recordatorio
  - [ ] Cita cancelada → Mensaje cancelación
  - [ ] Bono < 2 sesiones → Recordatorio renovación
  - [ ] Post-sesión → Solicitud feedback

- [ ] 5.1.8 - Configurar chatbot básico (opcional)
  - [ ] Menú de opciones
  - [ ] Respuestas automáticas FAQ
  - [ ] Derivación a humano

- [ ] 5.1.9 - Integrar con CRM
  - [ ] Conversaciones WhatsApp → CRM
  - [ ] Historial de conversaciones en cliente
  - [ ] Crear actividad desde WhatsApp

- [ ] 5.1.10 - Configurar analíticas
  - [ ] Mensajes enviados
  - [ ] Tasa de entrega
  - [ ] Tasa de lectura
  - [ ] Tasa de respuesta
  - [ ] Conversiones

- [ ] 5.1.11 - Formación al equipo
  - [ ] Cómo responder mensajes
  - [ ] Tiempos de respuesta objetivo
  - [ ] Plantillas disponibles
  - [ ] Tono de comunicación

**Entregables:**
- [ ] WhatsApp Business API integrado
- [ ] Plantillas aprobadas y funcionando
- [ ] Automatizaciones básicas activas
- [ ] Manual de uso para equipo

### 📧 5.2. Otros Canales de Comunicación

- [ ] 5.2.1 - Optimizar email marketing (ya configurado en Fase 2)
  - [ ] Verificar dominio para mejor entregabilidad
  - [ ] Configurar DKIM, SPF, DMARC
  - [ ] Diseñar templates adicionales

- [ ] 5.2.2 - Configurar SMS (opcional)
  - [ ] Proveedor SMS España
  - [ ] Integración con Odoo
  - [ ] Templates de emergencia

- [ ] 5.2.3 - Configurar notificaciones push (para app - Fase 6)
  - [ ] Proveedor (Firebase, OneSignal)
  - [ ] Integración

**Entregables:**
- [ ] Canales de comunicación multicanal
- [ ] Estrategia de comunicación documentada

---

## 🌐 FASE 6: RESERVAS ONLINE Y PAGOS

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fases 2 y 3  
**Estimación:** 2-3 semanas  
**Prioridad:** 🟠 ALTA

### 📅 6.1. Sistema de Reservas Online

- [ ] 6.1.1 - Investigar módulos de booking
  - [ ] Módulo Website Appointment (nativo Odoo)
  - [ ] Módulos OCA
  - [ ] Soluciones de terceros (Calendly + integración, etc.)

- [ ] 6.1.2 - Instalar y configurar módulo elegido

- [ ] 6.1.3 - Configurar disponibilidad online
  - [ ] Sincronizar con calendarios internos
  - [ ] Definir huecos reservables online
  - [ ] Bloquear huecos no disponibles

- [ ] 6.1.4 - Configurar tipos de citas reservables
  - [ ] Primera consulta fisioterapia
  - [ ] Sesión seguimiento (solo clientes existentes)
  - [ ] Valoración funcional
  - [ ] Entrenamiento personal
  - [ ] Clases grupales

- [ ] 6.1.5 - Configurar formulario de reserva
  - [ ] Datos cliente
  - [ ] Motivo de consulta
  - [ ] Preferencias horarias
  - [ ] Términos y condiciones

- [ ] 6.1.6 - Configurar calendario público
  - [ ] Visualización de disponibilidad
  - [ ] Selección de fecha/hora
  - [ ] Selección de profesional (opcional)

- [ ] 6.1.7 - Configurar confirmación de reserva
  - [ ] Email confirmación
  - [ ] WhatsApp confirmación
  - [ ] Añadir a calendario (ics)

- [ ] 6.1.8 - Configurar gestión de cancelaciones online
  - [ ] Plazo de cancelación
  - [ ] Proceso de cancelación
  - [ ] Notificaciones

- [ ] 6.1.9 - Configurar lista de espera
  - [ ] Notificación si hueco disponible
  - [ ] Gestión automática

**Entregables:**
- [ ] Sistema de reservas online funcional
- [ ] Integrado con calendarios internos
- [ ] Proceso de reserva optimizado

### 💳 6.2. Pasarelas de Pago Online

- [ ] 6.2.1 - Investigar pasarelas compatibles con Odoo
  - [ ] Redsys (TPV virtual bancos españoles)
  - [ ] Stripe
  - [ ] PayPal
  - [ ] Bizum (a través de Redsys)

- [ ] 6.2.2 - Contratar cuenta en pasarela(s) elegida(s)

- [ ] 6.2.3 - Instalar módulos de pago en Odoo
  - [ ] Payment Provider: Redsys
  - [ ] Payment Provider: Stripe
  - [ ] Payment Provider: PayPal

- [ ] 6.2.4 - Configurar pasarelas
  - [ ] API keys
  - [ ] Modo pruebas
  - [ ] Modo producción

- [ ] 6.2.5 - Integrar con e-commerce (si aplica)
  - [ ] Compra de bonos online
  - [ ] Pago de sesiones online
  - [ ] Productos de venta online

- [ ] 6.2.6 - Configurar pago en reserva (opcional)
  - [ ] Señal al reservar
  - [ ] Pago completo al reservar
  - [ ] Gestión de reembolsos

- [ ] 6.2.7 - Configurar seguridad
  - [ ] PCI compliance
  - [ ] 3D Secure
  - [ ] Cifrado

- [ ] 6.2.8 - Testing exhaustivo
  - [ ] Transacciones de prueba
  - [ ] Diferentes métodos de pago
  - [ ] Reembolsos
  - [ ] Integración contable

**Entregables:**
- [ ] Pasarelas de pago funcionando
- [ ] Proceso de pago seguro
- [ ] Integrado con contabilidad

### 🎫 6.3. Gestión de Bonos y Packs

- [ ] 6.3.1 - Configurar venta de bonos online
- [ ] 6.3.2 - Configurar consumo de bonos
- [ ] 6.3.3 - Configurar alertas de bonos próximos a vencer
- [ ] 6.3.4 - Configurar renovación automática (opcional)

**Entregables:**
- [ ] Sistema de bonos online funcional
- [ ] Portal cliente para ver bonos

---

## 📱 FASE 7: APP MÓVIL CLIENTE-PROFESIONAL

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fases 2, 3, 5, 6  
**Estimación:** 4-8 semanas (desarrollo custom)  
**Prioridad:** 🟡 MEDIA-ALTA

### 📋 7.1. Análisis y Diseño

- [ ] 7.1.1 - Definir funcionalidades app cliente
  - [ ] Ver citas programadas
  - [ ] Reservar nuevas citas
  - [ ] Cancelar/reprogramar citas
  - [ ] Ver bonos y sesiones restantes
  - [ ] Ver historial de sesiones
  - [ ] Acceder a documentación (informes, ejercicios)
  - [ ] Chat con profesional
  - [ ] Notificaciones push
  - [ ] Perfil y datos personales
  - [ ] Facturas y pagos

- [ ] 7.1.2 - Definir funcionalidades app profesional
  - [ ] Ver agenda del día
  - [ ] Acceder a ficha de paciente
  - [ ] Registrar sesión realizada
  - [ ] Añadir notas al historial
  - [ ] Ver próximas citas
  - [ ] Comunicación con pacientes
  - [ ] Acceso a plantillas y protocolos

- [ ] 7.1.3 - Diseñar arquitectura técnica
  - [ ] App nativa vs híbrida
  - [ ] Framework (Flutter, React Native, etc.)
  - [ ] Backend: API de Odoo
  - [ ] Autenticación
  - [ ] Sincronización offline

- [ ] 7.1.4 - Diseñar UX/UI
  - [ ] Wireframes
  - [ ] Mockups
  - [ ] Flujos de usuario
  - [ ] Branding

**Entregables:**
- [ ] Documento de requisitos funcionales
- [ ] Arquitectura técnica
- [ ] Diseños UI/UX
- [ ] Presupuesto de desarrollo

### 🔧 7.2. Desarrollo Backend (API)

- [ ] 7.2.1 - Configurar API REST de Odoo
  - [ ] Endpoints necesarios
  - [ ] Autenticación OAuth2
  - [ ] Documentación API

- [ ] 7.2.2 - Desarrollar endpoints custom (si necesario)
  - [ ] API de citas
  - [ ] API de pacientes
  - [ ] API de sesiones
  - [ ] API de documentos
  - [ ] API de chat

- [ ] 7.2.3 - Configurar seguridad API
  - [ ] Tokens de acceso
  - [ ] Rate limiting
  - [ ] Validación de permisos

- [ ] 7.2.4 - Testing de API
  - [ ] Tests unitarios
  - [ ] Tests de integración
  - [ ] Documentación con Postman/Swagger

**Entregables:**
- [ ] API REST funcional
- [ ] Documentación de API
- [ ] Tests pasando

### 📱 7.3. Desarrollo App Móvil

- [ ] 7.3.1 - Setup proyecto
  - [ ] Crear proyecto Flutter/React Native
  - [ ] Configurar dependencias
  - [ ] Estructura de carpetas

- [ ] 7.3.2 - Desarrollar autenticación
  - [ ] Login
  - [ ] Registro (si aplica)
  - [ ] Recuperar contraseña
  - [ ] Biométrica (huella/FaceID)

- [ ] 7.3.3 - Desarrollar módulo de citas
  - [ ] Lista de citas
  - [ ] Detalle de cita
  - [ ] Reservar cita
  - [ ] Cancelar cita

- [ ] 7.3.4 - Desarrollar módulo de perfil
  - [ ] Ver datos personales
  - [ ] Editar datos
  - [ ] Ver bonos
  - [ ] Ver historial

- [ ] 7.3.5 - Desarrollar módulo de documentos
  - [ ] Lista de documentos
  - [ ] Visualizar documento
  - [ ] Descargar documento

- [ ] 7.3.6 - Desarrollar módulo de comunicación
  - [ ] Chat con profesional
  - [ ] Notificaciones push

- [ ] 7.3.7 - Desarrollar para profesionales (si aplica)
  - [ ] Vista de agenda
  - [ ] Ficha de paciente
  - [ ] Registro de sesión

- [ ] 7.3.8 - Testing
  - [ ] Testing manual
  - [ ] Testing automatizado
  - [ ] Beta testing con usuarios

**Entregables:**
- [ ] App funcional en Android
- [ ] App funcional en iOS
- [ ] Beta disponible para testing

### 🚀 7.4. Publicación y Lanzamiento

- [ ] 7.4.1 - Preparar para stores
  - [ ] Capturas de pantalla
  - [ ] Descripción de app
  - [ ] Icono de app
  - [ ] Video promocional (opcional)

- [ ] 7.4.2 - Publicar en Google Play Store
  - [ ] Crear cuenta developer
  - [ ] Subir APK/AAB
  - [ ] Completar información
  - [ ] Enviar para revisión

- [ ] 7.4.3 - Publicar en Apple App Store
  - [ ] Crear cuenta Apple Developer
  - [ ] Subir IPA
  - [ ] Completar información
  - [ ] Enviar para revisión

- [ ] 7.4.4 - Campaña de lanzamiento
  - [ ] Comunicar a clientes existentes
  - [ ] Incentivos para descargar
  - [ ] Tutorial de uso

**Entregables:**
- [ ] App publicada en Google Play
- [ ] App publicada en App Store
- [ ] Material de marketing

---

## 🤖 FASE 8: AUTOMATIZACIÓN AVANZADA (FUTURO)

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fases anteriores  
**Estimación:** TBD  
**Prioridad:** 🟢 BAJA (Futuro)

> 📝 **Nota:** Esta fase se desarrollará en detalle en el futuro. Incluirá integraciones avanzadas.

### 🔄 8.1. N8N - Workflow Automation

- [ ] 8.1.1 - Instalar y configurar N8N
- [ ] 8.1.2 - Crear workflows de automatización
- [ ] 8.1.3 - Integrar con Odoo
- [ ] 8.1.4 - Integrar con WhatsApp
- [ ] 8.1.5 - Integrar con otras herramientas

### 🤖 8.2. Archon - Agentes AI

- [ ] 8.2.1 - Investigar Archon
- [ ] 8.2.2 - Casos de uso para Vigoentrena
- [ ] 8.2.3 - Implementación

### 🔗 8.3. MCP (Model Context Protocol)

- [ ] 8.3.1 - Investigar MCP
- [ ] 8.3.2 - Implementación

### 🤝 8.4. A2A (Agent-to-Agent)

- [ ] 8.4.1 - Investigar A2A
- [ ] 8.4.2 - Implementación

---

## 📚 FASE 9: DOCUMENTACIÓN COMPLETA

**Estado:** 🔄 En proceso  
**Prioridad:** 🔴 CRÍTICA (Transversal a todas las fases)

### 📖 9.1. Documentación Técnica

- [x] 9.1.1 - Crear README.md principal
- [ ] 9.1.2 - Crear TODO.md (este archivo)
- [ ] 9.1.3 - Documentar instalación de Odoo 17
- [ ] 9.1.4 - Documentar configuración de servidor
- [ ] 9.1.5 - Documentar arquitectura del sistema
- [ ] 9.1.6 - Documentar seguridad y permisos
- [ ] 9.1.7 - Documentar backup y recuperación
- [ ] 9.1.8 - Documentar procedimientos de mantenimiento
- [ ] 9.1.9 - Documentar actualización de Odoo
- [ ] 9.1.10 - Documentar troubleshooting común

### 📝 9.2. Documentación Funcional

- [ ] 9.2.1 - Documentar configuración inicial
- [ ] 9.2.2 - Documentar gestión de usuarios
- [ ] 9.2.3 - Documentar flujos de trabajo principales
- [ ] 9.2.4 - Crear manual de usuario final
- [ ] 9.2.5 - Crear guías rápidas por módulo
- [ ] 9.2.6 - Crear FAQs

### 📋 9.3. Documentación por Módulo

- [ ] 9.3.1 - Documentar CRM
- [ ] 9.3.2 - Documentar Ventas
- [ ] 9.3.3 - Documentar TPV
- [ ] 9.3.4 - Documentar Contabilidad
- [ ] 9.3.5 - Documentar Inventario
- [ ] 9.3.6 - Documentar Calendario
- [ ] 9.3.7 - Documentar Marketing
- [ ] 9.3.8 - Documentar Sitio Web
- [ ] 9.3.9 - Documentar RR.HH.
- [ ] 9.3.10 - Documentar Documentos y Firma
- [ ] 9.3.11 - Documentar Gestión Clínica
- [ ] 9.3.12 - Documentar Clases Grupales
- [ ] 9.3.13 - Documentar VeriFactu
- [ ] 9.3.14 - Documentar WhatsApp
- [ ] 9.3.15 - Documentar Reservas Online
- [ ] 9.3.16 - Documentar App Móvil

### 🎓 9.4. Materiales de Formación

- [ ] 9.4.1 - Crear plan de formación para equipo
- [ ] 9.4.2 - Crear videos tutoriales (opcional)
- [ ] 9.4.3 - Crear presentaciones de formación
- [ ] 9.4.4 - Crear ejercicios prácticos

---

## ✅ FASE 10: TESTING Y VALIDACIÓN FINAL

**Estado:** ⏸️ Pendiente  
**Dependencias:** Completar Fases 1-7  
**Estimación:** 2 semanas  
**Prioridad:** 🔴 CRÍTICA

### 🧪 10.1. Testing Integral del Sistema

- [ ] 10.1.1 - Test de flujos end-to-end
  - [ ] Cliente nuevo → Venta → Cita → Sesión → Factura → Cobro
  - [ ] Reserva online → Confirmación → Asistencia → Pago
  - [ ] Compra de bono → Consumo → Renovación

- [ ] 10.1.2 - Test de integraciones
  - [ ] Verificar todas las integraciones entre módulos
  - [ ] Verificar sincronización de datos

- [ ] 10.1.3 - Test de rendimiento
  - [ ] Carga de sistema
  - [ ] Tiempos de respuesta
  - [ ] Concurrencia

- [ ] 10.1.4 - Test de seguridad
  - [ ] Permisos de usuario
  - [ ] Acceso a datos sensibles
  - [ ] Vulnerabilidades

- [ ] 10.1.5 - Test de backup y recuperación
  - [ ] Realizar backup
  - [ ] Simular fallo
  - [ ] Restaurar backup

### 📊 10.2. Validación de Negocio

- [ ] 10.2.1 - Validar flujos operativos con equipo
- [ ] 10.2.2 - Validar flujos clínicos con fisioterapeutas
- [ ] 10.2.3 - Validar flujos comerciales con recepción
- [ ] 10.2.4 - Validar flujos financieros con administración
- [ ] 10.2.5 - Ajustes según feedback

### 🚀 10.3. Preparación para Go-Live

- [ ] 10.3.1 - Migración de datos (si hay sistema anterior)
  - [ ] Clientes
  - [ ] Proveedores
  - [ ] Productos
  - [ ] Histórico (si aplica)

- [ ] 10.3.2 - Formación final al equipo
- [ ] 10.3.3 - Documentación de procedimientos actualizada
- [ ] 10.3.4 - Plan de contingencia
- [ ] 10.3.5 - Comunicación a clientes (si aplica)

### ✅ 10.4. Go-Live y Soporte Post-Lanzamiento

- [ ] 10.4.1 - Go-Live del sistema
- [ ] 10.4.2 - Soporte intensivo primera semana
- [ ] 10.4.3 - Ajustes post-lanzamiento
- [ ] 10.4.4 - Recopilación de feedback
- [ ] 10.4.5 - Optimizaciones

---

## 📈 MÉTRICAS Y KPIs

### Métricas de Proyecto

- **Progreso global:** 1.3% (1/76 tareas)
- **Fases completadas:** 0/10
- **Documentos generados:** 2 (README.md, TODO.md)
- **Módulos instalados:** 0
- **Integraciones activas:** 0

### KPIs Post-Implementación (para definir)

- [ ] Tiempo medio de gestión de cita
- [ ] Tasa de ocupación de agenda
- [ ] Satisfacción de cliente (NPS)
- [ ] Tiempo de respuesta WhatsApp
- [ ] Tasa de renovación de bonos
- [ ] Facturación mensual
- [ ] Costos operativos
- [ ] ROI del sistema

---

## 🚨 RIESGOS Y MITIGACIÓN

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|---------|------------|
| VeriFactu no cumple normativa | Baja | Crítico | Validar con asesor fiscal antes de Go-Live |
| Integración WhatsApp falla | Media | Alto | Tener plan B (email + SMS) |
| App móvil se retrasa | Media | Medio | Fase 7 es opcional inicialmente |
| Problemas de rendimiento | Media | Alto | Testing exhaustivo de carga |
| Resistencia al cambio equipo | Alta | Medio | Formación y acompañamiento |
| Pérdida de datos | Baja | Crítico | Backups automáticos diarios |
| Costos superan presupuesto | Media | Alto | Revisión presupuestaria por fase |

---

## 📅 CALENDARIO ESTIMADO

```
FASE 0: Semanas 1-2    [🔄 En curso]
FASE 1: Semanas 3-4    [⏸️ Pendiente]
FASE 2: Semanas 5-8    [⏸️ Pendiente] ← CRÍTICO
FASE 3: Semanas 9-11   [⏸️ Pendiente]
FASE 4: Semanas 12-14  [⏸️ Pendiente] ← CRÍTICO (Legal)
FASE 5: Semanas 15-17  [⏸️ Pendiente] ← CRÍTICO (WhatsApp)
FASE 6: Semanas 18-20  [⏸️ Pendiente]
FASE 7: Semanas 21-28  [⏸️ Pendiente] (Opcional inicialmente)
FASE 8: TBD            [⏸️ Futuro]
FASE 9: Transversal    [🔄 En proceso]
FASE 10: Semanas 29-30 [⏸️ Pendiente]

GO-LIVE ESTIMADO: Semana 30 (sin app móvil)
GO-LIVE CON APP: Semana 35
```

---

## 💡 NOTAS IMPORTANTES

### Para Usuarios Sin Experiencia

Este TODO puede parecer abrumador, pero recuerda:

1. **Paso a paso:** No intentarás hacer todo a la vez. Cada fase se completa antes de pasar a la siguiente.

2. **Documentación didáctica:** Para cada tarea, habrá documentación explicativa en `/docs/` que te guiará.

3. **Apoyo disponible:** Puedes consultar:
   - Documentación oficial de Odoo
   - Comunidad OCA
   - Partners certificados en España
   - Esta documentación interna

4. **Prioridades claras:** Las tareas marcadas como 🔴 CRÍTICAS son las más importantes.

5. **Flexibilidad:** Este plan puede ajustarse según avances y necesidades.

### Decisiones Clave Pendientes

1. **Odoo Community vs Enterprise** → Decidir en Fase 0
2. **Hosting: Odoo.sh vs VPS vs On-premise** → Decidir en Fase 0
3. **Módulos clínicos: ¿cuál usar?** → Decidir en Fase 0
4. **Proveedor WhatsApp API** → Decidir en Fase 0
5. **Framework para app móvil** → Decidir en Fase 7
6. **¿Contratar partner certificado?** → Decidir en Fase 0

---

## 🔄 CONTROL DE VERSIONES

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0 | 2025-10-03 | Creación inicial del TODO |

---

## 👤 RESPONSABLES

- **Project Owner:** [Nombre]
- **Technical Lead:** [Nombre]
- **Functional Lead:** [Nombre]
- **Fiscal/Legal Advisor:** [Nombre/Empresa]

---

## 📞 CONTACTOS CLAVE

- **Soporte Odoo:** https://www.odoo.com/help
- **Comunidad OCA:** https://odoo-community.org/
- **Partners Odoo España:** [Lista en docs/]
- **Asesor Fiscal:** [Contacto]

---

**Última actualización:** 2025-10-03  
**Próxima revisión:** Al completar Fase 0

---

