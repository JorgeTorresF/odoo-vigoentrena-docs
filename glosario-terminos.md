# Glosario de Términos Odoo

## 📚 Introducción

Este glosario recoge todos los términos técnicos y conceptos que encontrarás en Odoo y en esta documentación. Está organizado alfabéticamente para fácil consulta.

---

## A

### **Action (Acción)**
Operación o comando que se ejecuta en Odoo (crear registro, enviar email, etc.). Las acciones pueden ser:
- **Manuales**: Botón que el usuario pulsa
- **Automáticas**: Triggered por eventos (crear venta → enviar email)
- **Scheduled**: Tareas programadas (cron jobs)

**Ejemplo Vigoentrena**: Acción "Enviar recordatorio 24h antes de cita"

### **Activity (Actividad)**
Tarea o to-do asociada a un registro. Aparece en el chatter y en el calendario.

**Tipos**:
- Email
- Llamada
- Meeting
- To-do
- Custom

**Ejemplo**: "Llamar a María mañana a las 10:00 para confirmar cita"

### **AEAT (Agencia Estatal de Administración Tributaria)**
Hacienda española. Odoo tiene módulos específicos para cumplimiento fiscal español.

**Módulos relacionados**:
- `l10n_es_aeat` - Modelos fiscales
- `l10n_es_aeat_sii` - Suministro Inmediato de Información

### **App (Aplicación)**
Sinónimo de **Módulo** en Odoo. Cada funcionalidad (CRM, Ventas, Inventario) es una app.

**Ubicación**: Menú principal de Odoo muestra las apps instaladas.

### **Apps Store (Tienda de Aplicaciones)**
[apps.odoo.com](https://apps.odoo.com) - Marketplace oficial donde se publican módulos de terceros.

**Tipos de apps**:
- Gratuitas (community)
- De pago (one-time o suscripción)
- Odoo Enterprise (solo con licencia Enterprise)

### **Automated Action (Acción Automatizada)**
Regla que se ejecuta automáticamente cuando se cumple una condición.

**Ejemplo Vigoentrena**:
```
Trigger: Cita creada
Condición: Fecha de cita es mañana
Acción: Enviar email recordatorio
```

---

## B

### **Backend**
Parte del sistema no visible para el cliente. Interfaz de administración de Odoo.

**Opuesto**: Frontend (website público)

### **Backup**
Copia de seguridad de la base de datos. Critical para recuperación de datos.

**Tipos en Odoo**:
- **Full**: Base de datos completa + filestore (adjuntos)
- **Parcial**: Solo base de datos
- **Automático**: Gestionado por Odoo.sh/Online
- **Manual**: Descarga desde Settings > Database Manager

**Recomendación**: Backup diario automático + backup manual antes de grandes cambios

### **BoM (Bill of Materials)**
Lista de materiales. En manufactura, define componentes de un producto final.

**No aplica directamente a Vigoentrena** (salvo si vendes kits de ejercicio)

### **Branch (Rama)**
En Odoo.sh con Git, una versión paralela del código.

**Ramas típicas**:
- `production`: Código en vivo
- `staging`: Testing antes de producción
- `development`: Desarrollo activo

### **Business Intelligence (BI)**
Análisis de datos y reportes avanzados. En Odoo incluye dashboards y pivots.

---

## C

### **Calendar (Calendario)**
Módulo que gestiona eventos, citas y meetings. Sincronizable con Google/Outlook.

### **Campaign (Campaña)**
Serie de comunicaciones automatizadas (email, SMS) hacia un segmento de clientes.

**Ejemplo Vigoentrena**: Campaña "Recuperación clientes inactivos"

### **Chatter**
Historial de comunicación de un registro. Aparece en la parte inferior de formularios.

**Contiene**:
- Mensajes/notas
- Actividades
- Emails enviados/recibidos
- Log de cambios
- Documentos adjuntos

### **Child Model (Modelo Hijo)**
Registro que depende de otro (relación padre-hijo).

**Ejemplo**: Líneas de pedido (child) de Pedido de venta (parent)

### **Community Edition (CE)**
Versión gratuita y open source de Odoo. Funcionalidades básicas pero completas.

### **Computed Field (Campo Calculado)**
Campo cuyo valor se calcula automáticamente.

**Ejemplo**: Total de factura = Suma(líneas) + IVA

### **Cron Job**
Tarea programada que se ejecuta automáticamente a intervalos.

**Ejemplo Vigoentrena**: 
- Cada noche a las 23:00: Enviar recordatorios del día siguiente
- Cada mes día 1: Generar facturas recurrentes

### **CRM (Customer Relationship Management)**
Gestión de relaciones con clientes. En Odoo es el módulo `crm`.

**Elementos**:
- Leads (contactos potenciales)
- Oportunidades (en pipeline de venta)
- Clientes (convertidos)

### **Custom Module (Módulo Custom)**
Módulo desarrollado a medida, no disponible en Apps Store.

**Ejemplo Vigoentrena**: `vigoentrena_clinic` para gestión clínica

---

## D

### **Dashboard**
Panel visual con métricas e indicadores clave (KPIs).

### **Database (Base de Datos)**
Contenedor de todos los datos de una instancia Odoo. Cada empresa suele tener 1 base de datos.

**Motor**: PostgreSQL

### **Developer Mode (Modo Desarrollador)**
Modo avanzado que muestra opciones técnicas ocultas.

**Activar**: Settings > General Settings > Developer Tools > Activate Developer Mode

**Permite**:
- Ver IDs de registros
- Ver nombres técnicos
- Editar vistas XML
- Acceder a terminal Python
- Ver SQL queries

### **Domain (Dominio)**
Filtro técnico de registros. Usa sintaxis de lista Python.

**Ejemplo**:
```python
[('customer_rank', '>', 0), ('country_id.code', '=', 'ES')]
```
Significa: Clientes de España

### **Dropdown (Desplegable)**
Campo tipo selección (Selection field) con opciones predefinidas.

**Ejemplo**: Estado de cita → Confirmada / Cancelada / Completada

---

## E

### **Enterprise Edition (EE)**
Versión de pago de Odoo con funcionalidades adicionales y soporte.

**Precio**: ~24-50€/usuario/mes

### **ERP (Enterprise Resource Planning)**
Sistema integrado de gestión empresarial. Odoo es un ERP completo.

### **Event (Evento)**
Módulo para gestionar eventos, conferencias, seminarios.

**Uso en Vigoentrena**: Gestionar clases grupales como "eventos recurrentes"

---

## F

### **Field (Campo)**
Elemento de datos en un modelo (nombre, email, fecha, etc.)

**Tipos principales**:
- `Char`: Texto corto
- `Text`: Texto largo
- `Integer`: Número entero
- `Float`: Número decimal
- `Boolean`: Verdadero/Falso
- `Date`: Fecha
- `Datetime`: Fecha y hora
- `Selection`: Opciones predefinidas
- `Many2one`: Relación a otro registro
- `One2many`: Lista de registros relacionados
- `Many2many`: Múltiples relaciones

### **Filter (Filtro)**
Criterio de búsqueda en vistas. Permite refinar resultados.

**Ejemplo**: Filtrar citas solo de hoy

### **Fiscal Position (Posición Fiscal)**
Configuración de impuestos según situación fiscal del cliente.

**Ejemplo**: 
- España peninsular: IVA 21%
- Canarias: IGIC 7%
- Intracomunitario: IVA 0% (inversión sujeto pasivo)

### **Follower (Seguidor)**
Usuario que recibe notificaciones de cambios en un registro.

**Ejemplo**: Fisioterapeuta Ana es follower de todos sus pacientes

---

## G

### **Gantt Chart (Diagrama de Gantt)**
Vista temporal de tareas/recursos. Útil para planning.

**Uso en Vigoentrena**: Planning de turnos de fisioterapeutas

### **Git**
Sistema de control de versiones. Integrado en Odoo.sh.

### **Group (Grupo)**
Conjunto de permisos. Los usuarios se asignan a grupos.

**Ejemplo grupos Vigoentrena**:
- `Fisioterapeutas`: Pueden ver agenda y pacientes
- `Recepción`: Pueden crear citas y cobrar
- `Manager`: Acceso total

---

## H

### **Hash**
Huella digital criptográfica. Usado en VeriFactu para encadenar facturas.

---

## I

### **IAP (In-App Purchase)**
Servicios de pago dentro de Odoo (SMS, firma digital, OCR, etc.)

**Compra**: Créditos prepago

### **Inherit (Herencia)**
Extender un modelo existente sin modificar el original.

**Ejemplo**: Añadir campo `allergies` al modelo `res.partner` (contacto)

### **Inventory (Inventario)**
Módulo de gestión de stock. 

**Uso limitado en Vigoentrena**: Solo consumibles (vendas, cremas)

### **Invoice (Factura)**
Documento contable de venta. Genera asientos contables.

**Estados**:
- Draft (Borrador)
- Posted (Registrada)
- Paid (Pagada)
- Cancelled (Cancelada)

---

## J

### **Journal (Diario)**
Libro contable donde se registran asientos.

**Tipos**:
- Ventas
- Compras
- Bancos
- Efectivo
- Operaciones diversas

---

## K

### **Kanban**
Vista de tarjetas organizadas en columnas (estados).

**Ejemplo CRM**: Lead → Contactado → Valoración → Propuesta → Ganado

### **KPI (Key Performance Indicator)**
Indicador clave de rendimiento. Métrica importante para el negocio.

**KPIs Vigoentrena**:
- Sesiones por mes
- Tasa de ocupación
- Ingresos mensuales
- Nuevos clientes
- Satisfacción cliente

---

## L

### **Lead (Contacto Potencial)**
Contacto que aún no es cliente. Primera etapa del CRM.

### **List View (Vista de Lista)**
Vista tabular de registros. Permite ordenar y filtrar.

### **Localization (Localización)**
Adaptación de Odoo a un país específico (contabilidad, impuestos, idioma).

**España**: Módulo `l10n_es`

### **LOPD (Ley Orgánica de Protección de Datos)**
Normativa española de protección de datos (ahora RGPD a nivel europeo).

---

## M

### **Many2many**
Relación de base de datos: muchos a muchos.

**Ejemplo**: Un paciente puede tener múltiples patologías, y una patología puede afectar a múltiples pacientes.

### **Many2one**
Relación de base de datos: muchos a uno.

**Ejemplo**: Muchas citas → Un fisioterapeuta

### **Menu**
Elemento de navegación en Odoo. Jerarquía de acceso a vistas.

### **Model (Modelo)**
Tabla de base de datos en Odoo. Define estructura de datos.

**Ejemplos**:
- `res.partner`: Contactos
- `sale.order`: Pedidos de venta
- `account.move`: Facturas

### **Module (Módulo)**
Conjunto de funcionalidades. Sinónimo de App.

**Estructura**:
```
módulo/
├── __init__.py
├── __manifest__.py
├── models/
├── views/
├── security/
└── data/
```

---

## N

### **Notification (Notificación)**
Alerta que recibe un usuario (campana en barra superior).

---

## O

### **OCA (Odoo Community Association)**
Organización que mantiene módulos open source de calidad.

**GitHub**: github.com/OCA

### **Odoo Online**
Hosting SaaS de Odoo. Sin instalación ni mantenimiento.

### **Odoo.sh**
Plataforma cloud de Odoo con Git integrado. Para desarrollo avanzado.

### **One2many**
Relación de base de datos: uno a muchos.

**Ejemplo**: Un pedido → Muchas líneas de pedido

### **Opportunity (Oportunidad)**
Lead cualificado en proceso de venta (en el pipeline).

---

## P

### **Partner (Socio/Contacto)**
Entidad genérica en Odoo. Puede ser:
- Cliente
- Proveedor
- Empleado
- Empresa

**Modelo**: `res.partner`

### **Payment (Pago)**
Registro de cobro o pago. Vinculado a facturas.

**Métodos**: Efectivo, transferencia, tarjeta, cheque, SEPA, etc.

### **Pipeline**
Embudo de venta en CRM. Visualizado en kanban.

**Etapas típicas**: Lead → Contactado → Propuesta → Negociación → Ganado/Perdido

### **Point of Sale (POS) / TPV**
Terminal de punto de venta. Interfaz táctil para cobros.

### **Portal User (Usuario Portal)**
Usuario externo con acceso limitado. Típicamente clientes.

**Acceso**: Solo sus propios datos (facturas, pedidos)

### **PostgreSQL**
Sistema de base de datos que usa Odoo.

### **Product (Producto)**
Artículo o servicio que se vende/compra.

**Tipos**:
- Consumible (consumibles fisioterapia)
- Servicio (sesión fisioterapia)
- Almacenable (productos con stock)

### **Project (Proyecto)**
Módulo de gestión de proyectos. Organiza tareas.

**Uso en Vigoentrena**: 1 proyecto por paciente con tareas = sesiones

---

## Q

### **Quotation (Presupuesto)**
Propuesta comercial. Estado previo a la venta confirmada.

---

## R

### **Record (Registro)**
Fila en una tabla de base de datos. Un dato específico.

**Ejemplo**: Cliente "María López" es un registro del modelo `res.partner`

### **Record Rule**
Regla de seguridad que limita qué registros puede ver/editar un usuario.

**Ejemplo**: Fisioterapeuta solo ve sus propios pacientes

### **Recurring (Recurrente)**
Que se repite periódicamente.

**Ejemplo**: Factura mensualidad clases grupales

### **RGPD (Reglamento General de Protección de Datos)**
Normativa europea de protección de datos. Critical para datos de salud.

### **Report (Informe)**
Documento generado desde Odoo (PDF, Excel).

**Ejemplos**: Factura PDF, Informe de ventas mensual

---

## S

### **SaaS (Software as a Service)**
Software en la nube. Odoo Online es SaaS.

### **Sale Order (Pedido de Venta)**
Confirmación de una venta. Genera factura y/o albarán.

### **Sequence (Secuencia)**
Numeración automática correlativa.

**Ejemplo**: Facturas VG-2025-001, VG-2025-002...

**Critical para VeriFactu**: Sin huecos en numeración

### **SEPA (Single Euro Payments Area)**
Área única de pagos en euros. Para domiciliaciones bancarias.

### **Server Action**
Acción Python personalizada que se ejecuta en el servidor.

### **SII (Suministro Inmediato de Información)**
Sistema de envío en tiempo real de facturas a la AEAT.

**Módulo**: `l10n_es_aeat_sii`

### **Smart Button (Botón Inteligente)**
Botón con contador en la parte superior de formularios.

**Ejemplo**: En cliente: [📄 Facturas (5)] [📅 Citas (12)]

### **SMS**
Mensajes de texto. Módulo `sms` en Odoo.

### **Snippet**
Bloque de contenido reutilizable en website builder.

### **Stages (Etapas)**
Estados en un proceso. Columnas en kanban.

**Ejemplo pipeline**: Lead → Contactado → Propuesta → Ganado

### **Studio (Odoo Studio)**
Editor visual para personalizar Odoo sin programar. Solo Enterprise.

### **Subscription (Suscripción)**
Contrato recurrente con facturación periódica.

**Ejemplo**: Mensualidad clases grupales

---

## T

### **Tags (Etiquetas)**
Clasificaciones libres para organizar registros.

**Ejemplo etiquetas pacientes**: VIP, Deportista, Dolor crónico, Postoperatorio

### **Task (Tarea)**
Elemento de proyecto. To-do asignable y temporalizado.

### **Template (Plantilla)**
Diseño reutilizable.

**Tipos**:
- Email template
- Report template (facturas, presupuestos)
- Website template

### **Ticket**
En módulo Helpdesk, solicitud de soporte.

### **Timesheet (Hoja de Horas)**
Registro de tiempo trabajado en tareas/proyectos.

### **TPV (Terminal Punto de Venta)**
Ver **Point of Sale**

### **Translation (Traducción)**
Odoo multiidioma. Permite traducir interfaz y contenidos.

---

## U

### **Unit of Measure (UoM) - Unidad de Medida**
Unidad para cuantificar productos.

**Ejemplos**: Unidad, Hora, Kilogramo, Litro

**En Vigoentrena**: Sesiones se miden en "Unidades" o "Horas"

### **User (Usuario)**
Persona con acceso a Odoo.

**Tipos**:
- Internal User (empleado): Acceso backend
- Portal User (cliente): Acceso portal
- Public User: Usuario anónimo en website

---

## V

### **VeriFactu**
Sistema español de verificación de facturas (obligatorio 2025).

**Requisitos**:
- Software certificado
- Hash encadenado de facturas
- Envío a AEAT

### **View (Vista)**
Representación visual de datos.

**Tipos principales**:
- Form: Formulario detalle
- List/Tree: Tabla
- Kanban: Tarjetas
- Calendar: Calendario
- Gantt: Línea temporal
- Graph: Gráfico
- Pivot: Tabla dinámica

---

## W

### **Website (Sitio Web)**
Módulo de creación de webs. Drag & drop builder.

### **Webhook**
Notificación HTTP automática cuando ocurre un evento.

**Ejemplo**: Odoo avisa a sistema externo cuando se crea factura

### **Widget**
Componente de interfaz para mostrar/editar un campo de forma especial.

**Ejemplos**:
- `image`: Muestra imagen
- `phone`: Link para llamar
- `email`: Link para enviar email
- `many2many_tags`: Tags visuales

### **Workflow**
Flujo de trabajo automatizado. Secuencia de estados y acciones.

**Ejemplo workflow cita**:
```
Solicitada → Confirmada → Completada → Facturada
```

---

## X

### **XML**
Lenguaje usado en Odoo para definir vistas, datos, y reportes.

### **XML-RPC**
Protocolo de comunicación API de Odoo. Permite integraciones externas.

---

## Y

*(No hay términos comunes)*

---

## Z

*(No hay términos comunes)*

---

## 🔢 Términos Adicionales

### **2FA (Two-Factor Authentication)**
Autenticación en dos pasos. Aumenta seguridad.

**Recomendado para**: Usuarios con permisos administrativos

### **API (Application Programming Interface)**
Interfaz para que aplicaciones externas se comuniquen con Odoo.

**Protocolos Odoo**:
- XML-RPC
- JSON-RPC
- REST (módulos de terceros)

### **CSV (Comma-Separated Values)**
Formato de archivo para importar/exportar datos.

### **DevOps**
Prácticas de desarrollo y operaciones. Odoo.sh facilita DevOps.

### **PoS (Point of Sale)**
Ver **TPV**

### **QR Code**
Código QR. Odoo puede generar en facturas, tickets, productos.

### **REST API**
Tipo de API. Odoo tiene REST mediante módulos de terceros.

### **SQL**
Lenguaje de base de datos. Odoo traduce acciones Python a SQL automáticamente.

### **UX (User Experience)**
Experiencia de usuario. Odoo 17 tiene UX mejorada.

### **venv (Virtual Environment)**
Entorno Python aislado. Recomendado para desarrollo Odoo local.

---

## 📖 Términos Específicos Vigoentrena

### **Bono**
Paquete prepagado de sesiones con descuento.

**Implementación**: Producto tipo "Servicio" con cantidad fija

### **Clase Grupal**
Sesión de ejercicio con múltiples participantes.

**Gestión**: Módulo Event o custom

### **Consentimiento Informado**
Documento legal firmado por paciente antes de tratamiento.

**Módulo**: Sign (firma digital)

### **Historia Clínica**
Registro médico del paciente.

**Implementación**: Extensión de `res.partner` + proyectos + documentos

### **Mensualidad**
Cuota recurrente por clases grupales.

**Módulo**: `sale_subscription`

### **Paciente**
En Odoo es un `res.partner` (contacto) con flag especial.

### **Sesión Individual**
Tratamiento fisioterapéutico 1-a-1.

**Gestión**: Cita en calendario + producto en venta

### **Valoración Inicial**
Primera consulta diagnóstica.

**Producto específico**: "Valoración Inicial (45 min)"

---

## 🎓 Cómo Usar Este Glosario

1. **Durante lectura de documentación**: Busca términos desconocidos aquí
2. **En formación**: Repasa términos antes de cursos
3. **En conversaciones con partner**: Usa terminología correcta
4. **En desarrollo**: Consulta nombres técnicos de modelos/campos

---

## 📚 Recursos Adicionales

### Para Profundizar
- **Documentación oficial**: [odoo.com/documentation](https://www.odoo.com/documentation)
- **Glosario oficial Odoo**: Disponible en docs técnicas
- **Foro Odoo**: Preguntas sobre terminología

### Siguientes Pasos
Ahora que conoces la terminología, puedes:
1. Explorar partners españoles
2. Revisar la guía técnica de instalación
3. Entender mejor los módulos específicos

📖 **Siguiente**: [Selección de Partner](./seleccion-partner.md)

---

**Fecha de creación**: 2025-01-XX  
**Versión**: 1.0  
**Autor**: Documentación Vigoentrena  
**Última actualización**: 2025-01-XX
