# Odoo para Vigoentrena: Adaptación Específica

## 🎯 Visión General

Este documento explica cómo Odoo se adapta a las necesidades específicas de **Vigoentrena**, un centro de fisioterapia y ejercicio personalizado que ofrece:

1. **Sesiones de fisioterapia individual**
2. **Clases de ejercicio grupal**
3. **Programas personalizados**
4. **Bonos y paquetes de sesiones**

## 🏥 El Reto de Vigoentrena

### Necesidades del Negocio

```
┌─────────────────────────────────────────────┐
│           VIGOENTRENA NECESITA              │
├─────────────────────────────────────────────┤
│ 1. Captación de clientes (Marketing/CRM)   │
│ 2. Reserva de citas online                 │
│ 3. Gestión de sesiones individuales        │
│ 4. Gestión de clases grupales              │
│ 5. Bonos y paquetes                        │
│ 6. Historia clínica del paciente           │
│ 7. Facturación y pagos                     │
│ 8. Cumplimiento normativo (VeriFactu)      │
│ 9. Comunicación automatizada                │
│ 10. Reportes y análisis                    │
└─────────────────────────────────────────────┘
```

### Problemas Sin Odoo

| Problema | Sin Sistema Integrado | Con Odoo |
|----------|----------------------|----------|
| **Gestión de citas** | Agenda papel/Google Calendar | Sistema centralizado con recordatorios automáticos |
| **Facturación** | Excel + gestor externo | Facturación automática integrada con ventas |
| **Historial paciente** | Carpetas físicas | Ficha digital completa con documentos |
| **Marketing** | Email manual | Campañas automatizadas y segmentadas |
| **Bonos** | Control manual (Excel) | Sistema automatizado con trazabilidad |
| **Reportes** | Análisis manual | Dashboards en tiempo real |
| **Pagos** | TPV independiente | TPV integrado con facturación |

## 🧩 Solución Odoo para Vigoentrena

### Flujo Completo de Cliente

```
1. CAPTACIÓN
   └─> CRM (Lead) + Marketing Email
       ↓
2. CONVERSIÓN
   └─> Oportunidad → Presupuesto → Venta
       ↓
3. RESERVA
   └─> Booking Online / Recepción → Calendario
       ↓
4. SESIÓN
   └─> Check-in → Atención → Notas clínicas
       ↓
5. PAGO
   └─> TPV / Bono / Factura recurrente
       ↓
6. FIDELIZACIÓN
   └─> Email post-sesión + Recordatorios + Ofertas
```

## 📋 Módulos Odoo para Vigoentrena

### Módulos CORE (Nativos - Imprescindibles)

#### 1. **CRM (crm)** 🎯
**Función**: Gestión de potenciales clientes

**Caso de uso Vigoentrena**:
```
Lead: "María busca fisioterapeuta para dolor lumbar"
  ├── Fuente: Formulario web
  ├── Asignado a: Fisioterapeuta Ana
  ├── Estado: Contactado
  ├── Próxima acción: Llamar mañana 10:00
  └── Notas: Prefiere tarde, cerca de su trabajo
```

**Beneficios**:
- No perder ningún contacto
- Seguimiento automático
- Historial de comunicaciones
- Conversión a cliente con 1 click

#### 2. **Ventas (sale_management)** 💰
**Función**: Presupuestos, pedidos, productos

**Productos Vigoentrena**:
- ✅ Sesión individual 60 min → 50€
- ✅ Sesión individual 30 min → 30€
- ✅ Bono 5 sesiones → 225€ (10% dto)
- ✅ Bono 10 sesiones → 400€ (20% dto)
- ✅ Mensualidad clases grupales → 60€
- ✅ Valoración inicial → 40€
- ✅ Tratamiento especializado → Variable

**Flujo de venta**:
```
Cliente nuevo
  ↓
Presupuesto → Email automático con presupuesto
  ↓
Cliente acepta (firma digital)
  ↓
Pedido de venta confirmado
  ↓
Se crea factura automáticamente
  ↓
Portal cliente: Puede ver y descargar
```

#### 3. **Facturación (account)** 📄
**Función**: Contabilidad y facturación

**Crítico para España**:
- ✅ Plan contable español (PGC)
- ✅ **VeriFactu** (obligatorio 2025)
- ✅ IVA 21% (servicios sanitarios podrían estar exentos según caso)
- ✅ AEAT (modelos 303, 390, etc.)
- ✅ Facturación recurrente (mensualidades)

**Ejemplo factura Vigoentrena**:
```
FACTURA VG-2025-001
Cliente: María López Pérez
NIF: 12345678Z

Descripción                    Cantidad  Precio  Total
─────────────────────────────────────────────────────
Bono 10 sesiones fisioterapia     1      400€   400€
IVA 21%                                           84€
─────────────────────────────────────────────────────
TOTAL                                            484€

Método de pago: Tarjeta
Estado: PAGADA
```

#### 4. **Calendario (calendar)** 📅
**Función**: Agenda compartida

**Configuración Vigoentrena**:
```
Fisioterapeuta Ana
  Lunes-Viernes: 09:00-14:00, 16:00-21:00
  Sábado: 09:00-14:00
  Domingo: Cerrado

Tipos de cita:
  ├── Valoración inicial (45 min)
  ├── Sesión individual (30 min / 60 min)
  ├── Seguimiento (20 min)
  └── [Clases grupales no aparecen aquí]

Recordatorios automáticos:
  ├── 24 horas antes → Email + SMS
  └── 2 horas antes → SMS
```

#### 5. **Reservas Online (appointment)** 🌐
**Función**: Cliente reserva desde la web

**Flujo cliente**:
```
1. Cliente entra en vigorentrena.com/reserva
2. Selecciona servicio:
   → Valoración inicial
   → Sesión fisioterapia
3. Elige profesional (o "el primero disponible")
4. Calendario muestra slots libres
5. Selecciona fecha/hora
6. Rellena datos:
   - Nombre, email, teléfono
   - Motivo consulta (opcional)
7. Confirmación inmediata:
   - Email con detalles
   - Add to Calendar (Google/Outlook)
   - Recordatorios automáticos activados
```

#### 6. **Punto de Venta (point_of_sale)** 💳
**Función**: Cobros en recepción

**Hardware Vigoentrena**:
```
├── Tablet/Ordenador táctil
├── Impresora térmica tickets (Epson TM-T20)
├── Cajón portamonedas
└── TPV contactless (Redsys/Stripe)
```

**Casos de uso**:
1. **Cliente llega a sesión**:
   - Abrir TPV
   - Buscar cliente
   - Añadir "Sesión individual 60 min"
   - Pagar (tarjeta/efectivo/bono)
   - Imprimir ticket
   
2. **Cliente compra bono**:
   - Añadir "Bono 10 sesiones"
   - Cobrar 400€
   - Bono queda registrado en ficha cliente
   - Usar en próximas sesiones

#### 7. **Website (website)** 🌐
**Función**: Página web del centro

**Contenidos**:
- Inicio
- Servicios (fisioterapia, clases)
- Equipo (fisioterapeutas)
- Blog (consejos salud)
- Contacto
- **Reserva online** (integración con appointment)
- **Portal cliente** (ver facturas, historial)

### Módulos CLÍNICOS (Terceros/Custom)

#### 8. **Gestión Clínica (módulo custom)** 🏥
**Función**: Historia clínica del paciente

**No hay módulo nativo de fisioterapia, opciones**:

**Opción A: Adaptación con nativos**
```
Cliente (res.partner) extendido con:
  ├── Anamnesis (campo texto largo)
  ├── Patologías (tags)
  ├── Alergias/precauciones (texto)
  ├── Objetivo terapéutico (texto)
  └── Documentos adjuntos:
      ├── Consentimiento informado
      ├── Informes médicos previos
      ├── Fotos evolución
      └── Protocolos ejercicios

Proyectos (project) = 1 proyecto por paciente
  └── Tareas = Sesiones
      ├── Fecha de sesión
      ├── Fisioterapeuta
      ├── Notas evolución
      ├── Técnicas aplicadas
      └── Ejercicios prescritos
```

**Opción B: Módulo de terceros**
Buscar en Odoo Apps Store:
- "healthcare"
- "clinic management"
- "physiotherapy"

Módulos españoles especializados disponibles (ejemplos):
- Medical Center Management
- Health Center
- Patient Management

**Opción C: Desarrollo custom**
Crear módulo `vigoentrena_clinic` con:
```python
Modelos:
├── Patient (extiende res.partner)
│   ├── medical_history
│   ├── pathologies
│   ├── allergies
│   └── consent_documents
├── ClinicalSession
│   ├── session_date
│   ├── therapist_id
│   ├── treatment_notes
│   ├── techniques_applied
│   └── next_session_plan
├── ExerciseProtocol
│   ├── exercises
│   ├── repetitions
│   ├── frequency
│   └── attached_videos
└── Assessment
    ├── initial_assessment
    ├── evolution_assessments
    ├── rom_tests (range of motion)
    └── strength_tests
```

#### 9. **Firma Digital (sign o terceros)** ✍️
**Función**: Consentimientos y contratos firmados

**Documentos a firmar**:
1. **Consentimiento informado** (obligatorio)
2. **LOPD/RGPD** (tratamiento datos salud)
3. **Presupuesto aceptado**
4. **Contrato mensualidad clases**
5. **Exención responsabilidad ejercicios**

**Flujo**:
```
Fisioterapeuta prepara consentimiento
  ↓
Botón "Solicitar firma"
  ↓
Cliente recibe SMS/Email con link
  ↓
Firma desde móvil (válido legalmente)
  ↓
Documento firmado almacenado en ficha paciente
  ↓
Certificado con timestamp y hash
```

### Módulos COMUNICACIÓN

#### 10. **Email Marketing (mass_mailing)** 📧
**Función**: Campañas de email

**Campañas Vigoentrena**:
- ✉️ Newsletter mensual (consejos prevención lesiones)
- ✉️ Promoción "trae un amigo"
- ✉️ Recuperación clientes inactivos (>60 días sin sesión)
- ✉️ Lanzamiento nuevas clases grupales
- ✉️ Ofertas especiales (verano, Navidad)

**Segmentación**:
```
Listas:
├── Todos los clientes activos
├── Solo fisioterapia individual
├── Solo clases grupales
├── Ambos servicios
├── Leads no convertidos
└── Clientes inactivos
```

#### 11. **WhatsApp Business (terceros)** 💬
**Función**: Mensajes automáticos WhatsApp

**Mensajes automáticos Vigoentrena**:
```
├── Confirmación cita: "✅ Hola María, tu cita está confirmada para mañana 18:00 con Ana"
├── Recordatorio 24h: "📅 Recordatorio: Mañana 18:00 tienes cita en Vigoentrena"
├── Recordatorio 2h: "⏰ Dentro de 2 horas tienes cita con Ana. ¡Te esperamos!"
├── Encuesta post-sesión: "¿Cómo fue tu sesión? Valora de 1-5 ⭐"
├── Factura lista: "💳 Tu factura VG-2025-001 está lista. Descargar: [link]"
└── Cuota mensual: "💰 Recordatorio: Cuota de marzo se cargará el día 1"
```

**Requisitos**:
- Cuenta WhatsApp Business verificada
- Módulo integración (Apps Store o API externa)
- Plantillas aprobadas por Meta

#### 12. **SMS (sms - nativo)** 📱
**Función**: Mensajes SMS cortos

**Usos Vigoentrena**:
- Confirmaciones urgentes
- Recordatorios de última hora
- Códigos de verificación
- Backups si WhatsApp falla

**Coste**: ~0.04€/SMS (según proveedor)

### Módulos FINANCIEROS

#### 13. **Facturación Recurrente (sale_subscription)** 🔄
**Función**: Mensualidades automáticas

**Caso Vigoentrena**: Clases grupales
```
Producto: Mensualidad Pilates
Precio: 60€/mes
Facturación: Día 1 de cada mes
Pago: Domiciliación bancaria SEPA
Contrato: Permanencia 3 meses, luego mensual
Cliente puede pausar: Agosto (vacaciones)

Automatizaciones:
├── Día 1: Genera factura automática
├── Día 1: Cargo SEPA automático
├── Día 3: Email con factura adjunta
└── Si falla pago: Alerta a administración
```

#### 14. **Remesas SEPA (módulo OCA)** 🏦
**Función**: Domiciliaciones bancarias

**Ventajas para clases grupales**:
- Cliente firma mandato SEPA una vez
- Cobros automáticos cada mes
- Sin gestión manual
- Ahorro tiempo administración

#### 15. **Conciliación Bancaria (account_bank_statement_import)** 💵
**Función**: Importar movimientos banco

**Workflow**:
```
1. Descargar extracto banco (CSV/OFX)
2. Importar en Odoo
3. Odoo sugiere matches automáticos:
   - Factura 001 → Pago María López 50€ ✅
   - Factura 002 → Pago Juan García 400€ ✅
4. Confirmar matches
5. Contabilidad al día
```

### Módulos OPERATIVOS

#### 16. **Gestión de Clases Grupales (event o custom)** 👥
**Función**: Clases recurrentes con inscripciones

**Configuración clase**:
```
Clase: Pilates Nivel 1
Horario: Lunes y Miércoles 18:00-19:00
Instructor: Ana
Sala: Sala Grupal
Capacidad: 12 personas
Precio: 60€/mes (8 clases aprox)
Modalidad: Mensualidad (no pago por clase)

Gestión:
├── Lista inscripciones mensuales
├── Control asistencia por clase
├── Avisos si clase se suspende
└── Lista espera si está llena
```

**Alternativa**: Usar módulo `hr_attendance` adaptado

#### 17. **Planning Profesionales (planning - Enterprise)** 📊
**Función**: Turnos fisioterapeutas

**Caso de uso**:
```
Semana del 20-26 Enero:

Lun  Mar  Mié  Jue  Vie  Sáb  Dom
Ana  09-14 09-14 09-14 09-14 09-14 09-14 LIBRE
     16-21 16-21 16-21 16-21 16-21 LIBRE
     
Luis 09-14 LIBRE 09-14 09-14 09-14 LIBRE LIBRE
     16-21       16-21 16-21 16-21

Clases grupales:
├── Lun 18:00 Pilates (Ana)
├── Mié 18:00 Pilates (Ana)
└── Vie 19:00 TRX (Luis)
```

#### 18. **Gestión de Salas (resource)** 🏠
**Función**: Reserva de espacios

**Espacios Vigoentrena**:
```
├── Sala Tratamiento 1 (individual)
├── Sala Tratamiento 2 (individual)
├── Sala Tratamiento 3 (individual)
└── Sala Grupal (clases)

Reserva automática:
  Sesión individual → Asigna sala disponible
  Clase grupal → Siempre Sala Grupal
```

## 🎨 Portal del Cliente

### ¿Qué es el Portal Cliente?

Un área privada donde cada cliente puede:

```
Portal Vigoentrena
├── 📅 Mis Citas
│   ├── Próximas citas
│   ├── Historial de sesiones
│   └── Reservar nueva cita
├── 💳 Mis Facturas
│   ├── Facturas pendientes
│   ├── Facturas pagadas
│   └── Descargar PDF
├── 📦 Mis Bonos
│   ├── Bono 10 sesiones: 7 restantes
│   └── Comprar nuevo bono
├── 📄 Mis Documentos
│   ├── Consentimientos firmados
│   ├── Informes médicos
│   └── Protocolos ejercicios
├── 💬 Mensajes
│   └── Chat con el centro
└── ⚙️ Mi Perfil
    ├── Datos personales
    ├── Método de pago
    └── Preferencias comunicación
```

### Acceso Portal
```
1. Cliente se registra (o staff le crea usuario)
2. Recibe email con link activación
3. Crea contraseña
4. Acceso a portal: vigorentrena.com/my
```

## 📊 Dashboards y Reportes

### Dashboard Dirección
```
┌──────────────────────────────────────┐
│  Ingresos Este Mes     12,450€  ↑15% │
│  Nuevos Clientes       8        ↑2   │
│  Sesiones Realizadas   247      ↑5%  │
│  Tasa Ocupación        78%      →    │
└──────────────────────────────────────┘

Gráficos:
├── Ingresos por mes (últimos 12 meses)
├── Servicios más vendidos
├── Fuentes de captación (web, referido, redes)
└── Clientes activos vs inactivos
```

### Dashboard Fisioterapeuta
```
Mi Día de Hoy:
├── 9:00  - María López (Valoración inicial)
├── 10:00 - Juan García (Sesión seguimiento)
├── 11:30 - LIBRE
├── 12:00 - Ana Rodríguez (Sesión individual)
└── ...

Mis Métricas:
├── Sesiones este mes: 78
├── Satisfacción promedio: 4.8⭐
├── Clientes activos: 24
└── Próximas tareas: 3
```

## 🔐 Seguridad y Cumplimiento

### RGPD/LOPD (Datos de Salud)
```
Medidas en Odoo:
├── ✅ Permisos granulares (solo fisios ven datos clínicos)
├── ✅ Logs de auditoría (quién accedió a qué)
├── ✅ Consentimientos firmados digitalmente
├── ✅ Encriptación datos sensibles
├── ✅ Backups cifrados
└── ✅ Derecho al olvido (anonimizar datos)
```

### VeriFactu (Crítico 2025)
```
Requisitos:
├── ✅ Software certificado
├── ✅ Numeración secuencial sin huecos
├── ✅ Firma electrónica facturas
├── ✅ Hash encadenado
├── ✅ Logs inmutables
└── ✅ Envío periódico AEAT

Implementación:
└── Módulo l10n_es + VeriFactu certificado
```

## 💰 Estimación de Costes

### Licencias Odoo
```
Opción A - Odoo Online (Recomendado inicio):
├── 3 usuarios (2 fisios + 1 admin): ~111€/mes
├── Apps necesarias: Incluidas en Custom plan
└── Total año 1: ~1.332€

Opción B - Odoo.sh (Si desarrollo custom):
├── Plan Development: ~200€/mes
├── Plan Production (cuando lances): ~400€/mes
└── Total año 1: ~4.800€
```

### Módulos de Terceros
```
├── VeriFactu certificado: 0-200€ (one-time o anual)
├── WhatsApp Business: 50-150€/mes
├── Firma digital (Signaturit): 20-80€/mes
├── Gestión clínica: 0-500€ (depende si es custom)
└── SMS créditos: ~100€/año
```

### Hardware
```
├── Tablet TPV: 300-600€
├── Impresora térmica: 150-300€
├── Cajón portamonedas: 50-100€
└── TPV contactless: 50€ + comisiones transacción
```

### Servicios (Opcional)
```
├── Partner Odoo (implementación): 3.000-8.000€
├── Desarrollo módulo custom clínica: 5.000-15.000€
├── App móvil clientes (PWA): 3.000-8.000€
├── App móvil clientes (nativa): 10.000-30.000€
└── Formación equipo: 500-1.500€
```

### Total Estimado Año 1
```
Escenario Mínimo (DIY):
├── Odoo Online Custom: 1.332€
├── Módulos básicos: 500€
├── Hardware: 1.000€
└── TOTAL: ~3.000€

Escenario Recomendado (Con partner):
├── Odoo Online Custom: 1.332€
├── Partner implementación: 5.000€
├── Módulos + integraciones: 2.000€
├── Hardware: 1.500€
└── TOTAL: ~10.000€

Escenario Premium (Todo custom):
├── Odoo.sh: 4.800€
├── Desarrollo custom: 20.000€
├── App móvil: 15.000€
├── Hardware: 2.000€
└── TOTAL: ~42.000€
```

## ✅ Checklist de Decisión

Antes de arrancar, responde:

- [ ] ¿Cuántos usuarios necesitamos? (fisioterapeutas + admin)
- [ ] ¿Necesitamos desarrollo custom o nos bastan módulos nativos?
- [ ] ¿Tenemos presupuesto para contratar un partner?
- [ ] ¿Cuánto tiempo tenemos para implementar?
- [ ] ¿Necesitamos app móvil desde el inicio o puede esperar?
- [ ] ¿Tenemos conocimientos técnicos en el equipo o necesitamos formación?
- [ ] ¿Ya tenemos proveedor TPV/banco o necesitamos buscar?
- [ ] ¿Cumplimos con RGPD actualmente? ¿Necesitamos auditoría?

## 🚀 Próximos Pasos

1. **Revisar el glosario de términos** para familiarizarte con conceptos clave
2. **Explorar casos de partners españoles** que han implementado Odoo en clínicas
3. **Ver el roadmap de implementación** por fases
4. **Decidir entre Odoo.sh y Odoo Online** según tus necesidades

📖 **Siguiente**: [Glosario de Términos](./glosario-terminos.md)

---

**Fecha de creación**: 2025-01-XX  
**Versión**: 1.0  
**Autor**: Documentación Vigoentrena  
**Última actualización**: 2025-01-XX
