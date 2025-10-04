# RGPD y LOPD en Odoo 17 para Vigoentrena

## 📋 Índice

1. [Introducción](#introducción)
2. [Marco Legal](#marco-legal)
3. [Datos Personales en Vigoentrena](#datos-personales-en-vigoentrena)
4. [Configuración Base de RGPD en Odoo](#configuración-base-de-rgpd-en-odoo)
5. [Gestión de Consentimientos](#gestión-de-consentimientos)
6. [Derechos de los Interesados](#derechos-de-los-interesados)
7. [Seguridad y Medidas Técnicas](#seguridad-y-medidas-técnicas)
8. [Registro de Actividades de Tratamiento](#registro-de-actividades-de-tratamiento)
9. [Auditorías y Logs](#auditorías-y-logs)
10. [Breach Notifications (Brechas de Seguridad)](#breach-notifications)
11. [Políticas y Documentación](#políticas-y-documentación)
12. [Módulos y Herramientas](#módulos-y-herramientas)
13. [Checklist de Cumplimiento](#checklist-de-cumplimiento)
14. [FAQs](#faqs)

---

## Introducción

### ¿Por qué es Crítico para Vigoentrena?

Vigoentrena maneja **datos sensibles de salud** de sus pacientes:
- Historial clínico y lesiones
- Datos médicos y tratamientos
- Información física (peso, altura, capacidades)
- Datos de contacto y facturación
- Consentimientos informados

> ⚠️ **IMPORTANTE**: Los datos de salud son considerados **categoría especial** bajo RGPD y requieren protección reforzada.

### Sanciones por Incumplimiento

**RGPD** (Reglamento UE 2016/679):
- Infracciones graves: Hasta **20 millones de euros** o **4% de facturación global anual**
- Infracciones leves: Hasta **10 millones de euros** o **2% de facturación global anual**

**LOPDGDD** (Ley Orgánica 3/2018):
- Infracciones muy graves: 300.001€ a 20.000.000€
- Infracciones graves: 40.001€ a 300.000€
- Infracciones leves: 900€ a 40.000€

### Alcance de esta Guía

Esta guía cubre:
✅ Configuración de Odoo 17 para cumplimiento RGPD/LOPD  
✅ Gestión de consentimientos de pacientes  
✅ Implementación de derechos de los interesados  
✅ Medidas de seguridad técnicas y organizativas  
✅ Documentación y auditorías  
✅ Procedimientos ante brechas de seguridad  

---

## Marco Legal

### RGPD - Reglamento General de Protección de Datos

**Texto completo**: [Reglamento (UE) 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj)

**Ámbito de aplicación**:
- Todos los países de la UE (incluida España)
- Empresas que tratan datos de residentes UE
- Aplicable desde el 25 de mayo de 2018

**Principios clave**:
1. **Licitud, lealtad y transparencia**: Informar claramente sobre el uso de datos
2. **Limitación de la finalidad**: Usar datos solo para fines específicos
3. **Minimización de datos**: Recopilar solo lo necesario
4. **Exactitud**: Mantener datos actualizados
5. **Limitación del plazo de conservación**: No guardar datos indefinidamente
6. **Integridad y confidencialidad**: Proteger los datos adecuadamente
7. **Responsabilidad proactiva**: Demostrar cumplimiento

### LOPDGDD - Ley Orgánica de Protección de Datos

**Texto completo**: [Ley Orgánica 3/2018](https://www.boe.es/eli/es/lo/2018/12/05/3)

**Complementa RGPD con**:
- Adaptaciones específicas para España
- Regulación de video vigilancia
- Edad de consentimiento digital (14 años en España)
- Derechos digitales
- Procedimientos sancionadores AEPD

### Normativa Sanitaria Específica

**Ley 41/2002** - Autonomía del Paciente:
- Historia clínica
- Consentimiento informado
- Confidencialidad médica

**Real Decreto 1720/2007** - Desarrollo LOPD sanitaria:
- Medidas de seguridad datos de salud
- Niveles de seguridad alto para datos clínicos

---

## Datos Personales en Vigoentrena

### Categorías de Datos Tratados

#### 1. Datos Identificativos (Nivel Básico)
- Nombre y apellidos
- DNI/NIE
- Fecha de nacimiento
- Dirección postal
- Teléfono
- Email

#### 2. Datos Económicos (Nivel Básico)
- Datos bancarios (IBAN)
- Historial de pagos
- Facturas emitidas
- Bonos y saldo

#### 3. Datos de Salud (Nivel Alto - Categoría Especial)
- **Anamnesis**: Historial médico previo
- **Lesiones y patologías**: Actuales y pasadas
- **Tratamientos**: Fisioterapia aplicada
- **Evolución clínica**: Notas de sesiones
- **Capacidades físicas**: Movilidad, fuerza, equilibrio
- **Consentimientos informados**: Tratamientos específicos
- **Fotografías clínicas**: Evolución lesiones (si aplica)
- **Informes médicos**: De otros profesionales
- **Alergias y precauciones**: Medicamentos, látex, etc.

#### 4. Datos Biométricos (Nivel Alto - si aplica)
- Fotografías faciales (reconocimiento)
- Huella dactilar (acceso instalaciones)

### Finalidades del Tratamiento

| Finalidad | Base Legal | Datos Tratados |
|-----------|------------|----------------|
| Gestión clínica (diagnóstico, tratamiento) | Ejecución contrato + Interés vital + Consentimiento específico | Todos los datos de salud |
| Facturación y cobros | Ejecución contrato + Obligación legal | Identificativos, económicos |
| Comunicaciones comerciales | Consentimiento | Identificativos, email, teléfono |
| Reservas y citas online | Ejecución contrato | Identificativos, teléfono |
| Cumplimiento normativo (VeriFactu, AEAT) | Obligación legal | Identificativos, económicos |
| Videovigilancia instalaciones | Interés legítimo (seguridad) | Imágenes |

### Plazos de Conservación

```
📅 Datos de Salud (Historia Clínica):
   Mínimo: 5 años desde última asistencia
   Recomendado: 15 años (prescripción responsabilidad civil)
   
📅 Datos Económicos (Facturas):
   6 años (Ley General Tributaria)
   
📅 Datos Comerciales (Newsletter):
   3 años desde última interacción (inactividad)
   O hasta revocación de consentimiento
   
📅 Datos Laborales (Empleados):
   4 años desde fin relación laboral
   
📅 Videovigilancia:
   Máximo 1 mes (salvo investigación delito)
```

---

## Configuración Base de RGPD en Odoo

### Paso 1: Activar Módulo de Privacidad

Odoo 17 incluye módulos nativos para RGPD:

```bash
# Módulos recomendados
- privacy (Enterprise)
- privacy_lookup (Enterprise)
- website_privacy (Enterprise)
```

**Instalación**:
1. Ir a `Aplicaciones` en Odoo
2. Buscar "Privacy"
3. Instalar:
   - ☑️ **Privacy**: Gestión general RGPD
   - ☑️ **Privacy Lookup**: Búsqueda de datos personales
   - ☑️ **Website Privacy**: Cookies y consentimientos web

### Paso 2: Configurar Política de Privacidad

**Ruta**: `Ajustes` > `Sitio Web` > `Privacidad`

```markdown
# Plantilla Política de Privacidad Vigoentrena

## 1. Responsable del Tratamiento
VIGOENTRENA S.L.
CIF: B-XXXXXXXX
Domicilio: [Dirección completa]
Email: privacidad@vigoentrena.com
Teléfono: [Teléfono]

Delegado de Protección de Datos (DPD): [Si aplica]
Email DPD: dpd@vigoentrena.com

## 2. Finalidades del Tratamiento
Sus datos personales serán tratados para:
- Prestación de servicios de fisioterapia y ejercicio
- Gestión de citas y reservas
- Facturación y cobros
- Comunicaciones comerciales (con su consentimiento)
- Cumplimiento de obligaciones legales

## 3. Base Legal
- Ejecución del contrato de prestación de servicios
- Consentimiento expreso para datos de salud
- Obligación legal (facturación, AEAT)
- Interés legítimo (seguridad instalaciones)

## 4. Destinatarios
Sus datos podrán ser comunicados a:
- Entidades bancarias (cobros/pagos)
- Administraciones Públicas (AEAT, Seguridad Social)
- Proveedores de servicios tecnológicos (hosting, email)

No realizamos transferencias internacionales de datos.

## 5. Derechos
Puede ejercer sus derechos de:
- Acceso, rectificación, supresión
- Limitación del tratamiento
- Portabilidad de datos
- Oposición
- Revocación del consentimiento

Envíe solicitud a: privacidad@vigoentrena.com

## 6. Plazo de Conservación
- Datos clínicos: 15 años desde última asistencia
- Datos fiscales: 6 años
- Datos comerciales: 3 años o hasta revocación

## 7. Medidas de Seguridad
Aplicamos medidas técnicas y organizativas apropiadas:
- Cifrado de comunicaciones (SSL/TLS)
- Control de acceso por roles
- Copias de seguridad cifradas
- Auditorías periódicas

## 8. Reclamación
Puede reclamar ante la Agencia Española de Protección de Datos:
www.aepd.es
```

### Paso 3: Configurar Cookie Consent (Website)

**Ruta**: `Sitio Web` > `Configuración` > `Cookies`

**Configuración recomendada**:

```python
# Categorías de cookies
1. Cookies Técnicas (Obligatorias):
   - Sesión de usuario
   - Carrito de compra
   - Preferencias idioma
   
2. Cookies Analíticas (Opcional - requiere consentimiento):
   - Google Analytics
   - Odoo Analytics
   
3. Cookies Marketing (Opcional - requiere consentimiento):
   - Google Ads
   - Facebook Pixel
   - LinkedIn Insight Tag
```

**Texto banner cookies**:

```
🍪 Este sitio web utiliza cookies

Utilizamos cookies propias y de terceros para mejorar su experiencia 
de navegación y ofrecer contenido de interés.

Cookies técnicas: Imprescindibles para el funcionamiento.
Cookies analíticas: Nos ayudan a mejorar el sitio.
Cookies de marketing: Para mostrar anuncios relevantes.

[Aceptar todas] [Solo necesarias] [Configurar]
```

### Paso 4: Campos Personalizados para Consentimientos

Crear campos en el modelo `res.partner` (Contacto):

```python
# Módulo custom: vigoentrena_gdpr

from odoo import models, fields

class Partner(models.Model):
    _inherit = 'res.partner'
    
    # Consentimientos
    consent_data_treatment = fields.Boolean(
        string='Consentimiento Tratamiento Datos Salud',
        help='Acepta el tratamiento de datos de salud para diagnóstico y tratamiento'
    )
    consent_data_treatment_date = fields.Date(
        string='Fecha Consentimiento Salud'
    )
    
    consent_commercial = fields.Boolean(
        string='Consentimiento Comunicaciones Comerciales',
        help='Acepta recibir información comercial y promociones'
    )
    consent_commercial_date = fields.Date(
        string='Fecha Consentimiento Comercial'
    )
    
    consent_whatsapp = fields.Boolean(
        string='Consentimiento WhatsApp',
        help='Acepta recibir notificaciones por WhatsApp'
    )
    consent_whatsapp_date = fields.Date(
        string='Fecha Consentimiento WhatsApp'
    )
    
    # Trazabilidad
    gdpr_consent_history = fields.One2many(
        'gdpr.consent.log', 
        'partner_id', 
        string='Historial Consentimientos'
    )
    
    data_retention_until = fields.Date(
        string='Conservar Datos Hasta',
        help='Fecha límite conservación datos (cálculo automático)'
    )
    
    anonymization_requested = fields.Boolean(
        string='Anonimización Solicitada',
        help='Cliente ha solicitado derecho al olvido'
    )
    anonymization_date = fields.Date(
        string='Fecha Anonimización'
    )

class GDPRConsentLog(models.Model):
    _name = 'gdpr.consent.log'
    _description = 'Log de Consentimientos RGPD'
    _order = 'create_date desc'
    
    partner_id = fields.Many2one('res.partner', required=True)
    consent_type = fields.Selection([
        ('health_data', 'Datos Salud'),
        ('commercial', 'Comercial'),
        ('whatsapp', 'WhatsApp'),
        ('cookies', 'Cookies Web'),
    ], required=True)
    
    action = fields.Selection([
        ('granted', 'Otorgado'),
        ('revoked', 'Revocado'),
        ('modified', 'Modificado'),
    ], required=True)
    
    consent_text = fields.Text('Texto Consentimiento')
    ip_address = fields.Char('Dirección IP')
    user_agent = fields.Char('Navegador')
    obtained_via = fields.Selection([
        ('web', 'Formulario Web'),
        ('paper', 'Documento Físico'),
        ('verbal', 'Verbal con Testigo'),
        ('backoffice', 'Registro Manual Staff'),
    ])
```

---

## Gestión de Consentimientos

### Tipos de Consentimientos Necesarios

#### 1. Consentimiento Tratamiento Datos de Salud

**Base legal**: Artículo 9.2.h RGPD + Artículo 9 LOPDGDD

**Texto modelo**:

```markdown
CONSENTIMIENTO INFORMADO PARA TRATAMIENTO DE DATOS DE SALUD

Yo, [Nombre Apellidos], con DNI [DNI], AUTORIZO expresamente a VIGOENTRENA S.L. 
al tratamiento de mis datos de salud con las siguientes finalidades:

✓ Elaboración y conservación de historia clínica
✓ Diagnóstico, tratamiento y seguimiento de mi condición física
✓ Prescripción de ejercicios terapéuticos personalizados
✓ Evaluación de la evolución y resultados del tratamiento

Estos datos incluyen:
- Historial médico previo
- Lesiones, patologías y limitaciones actuales
- Tratamientos aplicados y su evolución
- Capacidades físicas y movilidad
- Cualquier información relevante para mi tratamiento

He sido informado/a de:
→ El responsable del tratamiento es VIGOENTRENA S.L.
→ Mis datos se conservarán durante 15 años desde mi última asistencia
→ Puedo ejercer mis derechos de acceso, rectificación, supresión, 
  limitación, portabilidad y oposición
→ Puedo revocar este consentimiento en cualquier momento
→ Puedo reclamar ante la Agencia Española de Protección de Datos

Fecha: _______________

Firma: _______________
```

**Implementación en Odoo**:

```python
# Acción automatizada: Al crear nuevo paciente
def action_request_health_consent(self):
    """Enviar formulario de consentimiento de datos de salud"""
    template = self.env.ref('vigoentrena_gdpr.email_health_consent')
    template.send_mail(self.id, force_send=True)
    
# Vista formulario web
@http.route('/gdpr/health-consent/<int:partner_id>/<string:token>', 
            type='http', auth='public', website=True)
def health_consent_form(self, partner_id, token, **kwargs):
    partner = request.env['res.partner'].sudo().browse(partner_id)
    
    # Verificar token de seguridad
    if not self._verify_token(partner, token):
        return request.render('website.404')
    
    return request.render('vigoentrena_gdpr.health_consent_form', {
        'partner': partner
    })

@http.route('/gdpr/health-consent/submit', type='http', auth='public', 
            website=True, methods=['POST'])
def submit_health_consent(self, **post):
    partner = request.env['res.partner'].sudo().browse(int(post.get('partner_id')))
    
    # Guardar consentimiento
    partner.write({
        'consent_data_treatment': True,
        'consent_data_treatment_date': fields.Date.today(),
    })
    
    # Log de auditoría
    request.env['gdpr.consent.log'].sudo().create({
        'partner_id': partner.id,
        'consent_type': 'health_data',
        'action': 'granted',
        'consent_text': post.get('consent_text'),
        'ip_address': request.httprequest.remote_addr,
        'user_agent': request.httprequest.user_agent.string,
        'obtained_via': 'web',
    })
    
    # Generar PDF firmado
    consent_pdf = self._generate_consent_pdf(partner, post)
    
    # Adjuntar a ficha paciente
    attachment = request.env['ir.attachment'].sudo().create({
        'name': f'Consentimiento_Salud_{partner.name}_{fields.Date.today()}.pdf',
        'datas': consent_pdf,
        'res_model': 'res.partner',
        'res_id': partner.id,
    })
    
    return request.render('vigoentrena_gdpr.consent_confirmation')
```

#### 2. Consentimiento Comunicaciones Comerciales

**Base legal**: Artículo 6.1.a RGPD (Consentimiento)

**Texto modelo**:

```markdown
CONSENTIMIENTO PARA COMUNICACIONES COMERCIALES

Acepto recibir comunicaciones comerciales de VIGOENTRENA S.L. a través de:

☐ Email
☐ SMS
☐ WhatsApp
☐ Teléfono

Sobre:
☐ Nuevos servicios y tratamientos
☐ Promociones y descuentos
☐ Eventos y talleres
☐ Newsletter con consejos de salud

Puede revocar este consentimiento en cualquier momento enviando 
un email a: baja@vigoentrena.com

Fecha: _______________  Firma: _______________
```

**Implementación**:

```python
# Al crear campaña de email marketing
def action_send_campaign(self):
    # Filtrar solo contactos con consentimiento
    recipients = self.mailing_list_ids.contact_ids.filtered(
        lambda c: c.partner_id.consent_commercial
    )
    
    # Incluir enlace de baja
    for contact in recipients:
        unsubscribe_token = self._generate_unsubscribe_token(contact)
        # ...enviar email con token
```

#### 3. Consentimiento Cookies (Website)

**Implementación en website**:

```html
<!-- Cookie Banner -->
<div id="cookie-consent-banner" class="cookie-banner">
    <div class="container">
        <p>
            🍪 Utilizamos cookies propias y de terceros para mejorar 
            su experiencia. 
            <a href="/privacy-policy">Más información</a>
        </p>
        <div class="cookie-actions">
            <button onclick="acceptAllCookies()">Aceptar todas</button>
            <button onclick="acceptNecessaryCookies()">Solo necesarias</button>
            <button onclick="showCookieSettings()">Configurar</button>
        </div>
    </div>
</div>

<script>
function acceptAllCookies() {
    // Guardar consentimiento
    localStorage.setItem('cookie_consent', 'all');
    document.getElementById('cookie-consent-banner').style.display = 'none';
    
    // Activar cookies analíticas y marketing
    enableAnalytics();
    enableMarketing();
    
    // Registrar en backend
    fetch('/gdpr/cookie-consent', {
        method: 'POST',
        body: JSON.stringify({
            consent_level: 'all',
            timestamp: new Date().toISOString()
        })
    });
}

function acceptNecessaryCookies() {
    localStorage.setItem('cookie_consent', 'necessary');
    document.getElementById('cookie-consent-banner').style.display = 'none';
    
    // Solo cookies técnicas (ya activas)
}

function showCookieSettings() {
    // Mostrar modal con configuración detallada
    $('#cookie-settings-modal').modal('show');
}
</script>
```

### Gestión de Revocaciones

**Flujo de revocación de consentimientos**:

```python
def action_revoke_consent(self, consent_type):
    """Revocar un consentimiento específico"""
    
    consent_fields = {
        'health_data': 'consent_data_treatment',
        'commercial': 'consent_commercial',
        'whatsapp': 'consent_whatsapp',
    }
    
    field_name = consent_fields.get(consent_type)
    
    if not field_name:
        raise UserError("Tipo de consentimiento no válido")
    
    # Marcar como revocado
    self.write({
        field_name: False,
        f'{field_name}_date': False,
    })
    
    # Log de auditoría
    self.env['gdpr.consent.log'].create({
        'partner_id': self.id,
        'consent_type': consent_type,
        'action': 'revoked',
        'ip_address': request.httprequest.remote_addr if request else None,
    })
    
    # Acciones específicas según tipo
    if consent_type == 'commercial':
        # Dar de baja de listas de email marketing
        self.env['mailing.contact'].search([
            ('partner_id', '=', self.id)
        ]).write({'opt_out': True})
        
    elif consent_type == 'whatsapp':
        # Desactivar notificaciones WhatsApp
        # ...lógica específica
        pass
    
    # Notificar al paciente
    template = self.env.ref('vigoentrena_gdpr.email_consent_revoked')
    template.send_mail(self.id)
    
    return True
```

---

## Derechos de los Interesados

### 1. Derecho de Acceso

**Artículo 15 RGPD**: El paciente puede solicitar:
- Qué datos personales se tratan
- Finalidades del tratamiento
- Destinatarios de los datos
- Plazo de conservación
- Origen de los datos (si no se obtuvieron directamente)

**Implementación**:

```python
def action_data_access_request(self):
    """Generar informe completo de datos del paciente"""
    
    # Recopilar todos los datos
    data = {
        'personal_info': {
            'name': self.name,
            'email': self.email,
            'phone': self.phone,
            'address': self._format_address(),
            'birthdate': self.birthdate,
            'dni': self.vat,
        },
        'clinical_data': {
            'medical_history': self._get_medical_history(),
            'sessions': self._get_session_notes(),
            'protocols': self._get_exercise_protocols(),
        },
        'financial_data': {
            'invoices': self._get_invoice_data(),
            'payments': self._get_payment_data(),
            'outstanding_balance': self.credit,
        },
        'consents': {
            'health_data': self.consent_data_treatment,
            'commercial': self.consent_commercial,
            'whatsapp': self.consent_whatsapp,
        },
        'activity_log': self._get_activity_log(),
    }
    
    # Generar PDF
    pdf = self.env.ref('vigoentrena_gdpr.report_data_access').render_qweb_pdf([self.id])[0]
    
    # Enviar por email con cifrado
    attachment = self.env['ir.attachment'].create({
        'name': f'Datos_Personales_{self.name}_{fields.Date.today()}.pdf',
        'datas': base64.b64encode(pdf),
        'res_model': 'res.partner',
        'res_id': self.id,
    })
    
    # Email con link de descarga temporal (48h)
    download_token = self._generate_secure_token()
    template = self.env.ref('vigoentrena_gdpr.email_data_access')
    template.with_context(
        download_token=download_token
    ).send_mail(self.id)
    
    # Log de auditoría
    self._log_gdpr_action('data_access', 'Solicitud de acceso a datos personales')
```

### 2. Derecho de Rectificación

**Artículo 16 RGPD**: Corregir datos inexactos o incompletos

**Implementación**:

```python
# Portal de paciente - Editar datos personales
@http.route('/my/profile/edit', type='http', auth='user', website=True)
def edit_profile(self, **kwargs):
    partner = request.env.user.partner_id
    
    # Campos editables por el paciente
    editable_fields = ['email', 'phone', 'mobile', 'street', 'city', 'zip']
    
    # Campos que requieren validación del staff
    staff_validation_fields = ['name', 'vat', 'birthdate']
    
    return request.render('vigoentrena_gdpr.edit_profile', {
        'partner': partner,
        'editable_fields': editable_fields,
    })

# Acción desde backend (staff)
def action_rectify_data(self, changes):
    """Rectificar datos - con log de auditoría"""
    
    old_values = {field: self[field] for field in changes.keys()}
    
    # Aplicar cambios
    self.write(changes)
    
    # Log de auditoría
    self.env['gdpr.audit.log'].create({
        'partner_id': self.id,
        'action': 'data_rectification',
        'user_id': self.env.user.id,
        'old_values': json.dumps(old_values),
        'new_values': json.dumps(changes),
        'reason': 'Rectificación solicitada por el paciente',
    })
```

### 3. Derecho de Supresión (Derecho al Olvido)

**Artículo 17 RGPD**: Borrar datos cuando:
- Ya no son necesarios
- Se retira el consentimiento
- Oposición legítima al tratamiento
- Datos tratados ilícitamente

**⚠️ IMPORTANTE**: En el sector salud, NO se puede suprimir la historia clínica durante el plazo legal de conservación (15 años).

**Implementación**:

```python
def action_right_to_erasure(self, reason):
    """
    Derecho al olvido - con restricciones legales sanitarias
    """
    
    # Verificar si es legalmente posible
    last_visit = self._get_last_visit_date()
    years_since_last_visit = (fields.Date.today() - last_visit).days / 365
    
    if years_since_last_visit < 15:
        raise UserError(
            "No es posible eliminar los datos de salud. "
            "La legislación sanitaria obliga a conservar la historia clínica "
            f"durante 15 años. Última visita: {last_visit}. "
            f"Puede solicitar la eliminación a partir del {last_visit + relativedelta(years=15)}."
        )
    
    # Anonimización en lugar de borrado total
    anonymized_name = f"Paciente-{self.id}-ANONIMIZADO"
    
    self.write({
        'name': anonymized_name,
        'email': f'anonimizado-{self.id}@vigoentrena.local',
        'phone': False,
        'mobile': False,
        'street': 'ANONIMIZADO',
        'vat': False,
        'birthdate': False,
        
        # Mantener datos de salud pero marcar como anonimizado
        'anonymization_requested': True,
        'anonymization_date': fields.Date.today(),
        'anonymization_reason': reason,
        
        # Revocar todos los consentimientos
        'consent_data_treatment': False,
        'consent_commercial': False,
        'consent_whatsapp': False,
    })
    
    # Marcar facturas como "anonimizadas" pero conservar por ley fiscal
    self.invoice_ids.write({
        'partner_name': anonymized_name
    })
    
    # Log de auditoría
    self._log_gdpr_action('erasure_request', f'Anonimización: {reason}')
    
    # Notificar al DPO
    self._notify_dpo('Solicitud derecho al olvido procesada', {
        'partner_id': self.id,
        'original_name': self.name,
        'reason': reason,
    })
```

### 4. Derecho a la Limitación del Tratamiento

**Artículo 18 RGPD**: "Congelar" datos temporalmente

**Implementación**:

```python
# Campo en res.partner
data_processing_limited = fields.Boolean(
    string='Tratamiento Limitado',
    help='El paciente ha solicitado limitar el tratamiento de sus datos'
)
limitation_reason = fields.Selection([
    ('accuracy_contest', 'Exactitud Cuestionada'),
    ('unlawful_processing', 'Tratamiento Ilícito'),
    ('no_longer_needed', 'Ya No Necesario'),
    ('pending_objection', 'Oposición Pendiente Verificación'),
], string='Motivo Limitación')

# Acción
def action_limit_processing(self, reason):
    """Limitar el tratamiento de datos"""
    
    self.write({
        'data_processing_limited': True,
        'limitation_reason': reason,
    })
    
    # Bloquear uso de datos en campañas
    self.env['mailing.contact'].search([
        ('partner_id', '=', self.id)
    ]).write({'opt_out': True})
    
    # Notificar al equipo
    self.message_post(
        body=f"⚠️ LIMITACIÓN TRATAMIENTO DATOS - Motivo: {reason}. "
             "Solo se pueden usar estos datos para cumplimiento legal o "
             "con consentimiento expreso del paciente.",
        message_type='notification',
        subtype_id=self.env.ref('mail.mt_note').id,
    )
```

### 5. Derecho a la Portabilidad

**Artículo 20 RGPD**: Recibir datos en formato estructurado (JSON, CSV, XML)

**Implementación**:

```python
def action_data_portability(self, export_format='json'):
    """Exportar datos en formato portable"""
    
    data = {
        'personal_data': {
            'name': self.name,
            'email': self.email,
            'phone': self.phone,
            'birthdate': str(self.birthdate) if self.birthdate else None,
        },
        'clinical_records': [
            {
                'date': str(session.date),
                'notes': session.notes,
                'treatment': session.treatment_type,
                'therapist': session.therapist_id.name,
            }
            for session in self.session_ids
        ],
        'appointments': [
            {
                'date': str(appt.start_datetime),
                'service': appt.appointment_type_id.name,
                'duration': appt.duration,
            }
            for appt in self.calendar_event_ids
        ],
        'invoices': [
            {
                'number': inv.name,
                'date': str(inv.invoice_date),
                'amount': inv.amount_total,
                'status': inv.state,
            }
            for inv in self.invoice_ids
        ],
    }
    
    if export_format == 'json':
        file_content = json.dumps(data, indent=2, ensure_ascii=False)
        mimetype = 'application/json'
        extension = 'json'
    elif export_format == 'csv':
        # Convertir a CSV (simplificado, cada sección en archivo separado)
        file_content = self._convert_to_csv(data)
        mimetype = 'text/csv'
        extension = 'csv'
    elif export_format == 'xml':
        file_content = self._convert_to_xml(data)
        mimetype = 'application/xml'
        extension = 'xml'
    
    # Crear archivo descargable
    attachment = self.env['ir.attachment'].create({
        'name': f'Datos_{self.name}_{fields.Date.today()}.{extension}',
        'datas': base64.b64encode(file_content.encode('utf-8')),
        'mimetype': mimetype,
        'res_model': 'res.partner',
        'res_id': self.id,
    })
    
    # Enviar link de descarga
    template = self.env.ref('vigoentrena_gdpr.email_data_portability')
    template.send_mail(self.id)
    
    return attachment
```

### 6. Derecho de Oposición

**Artículo 21 RGPD**: Oponerse al tratamiento (marketing directo, interés legítimo)

**Implementación**:

```python
def action_object_to_processing(self, processing_type, reason=None):
    """Oposición al tratamiento"""
    
    if processing_type == 'marketing':
        # Oposición a marketing directo - DEBE aceptarse
        self.write({
            'consent_commercial': False,
            'consent_whatsapp': False,
        })
        self.env['mailing.contact'].search([
            ('partner_id', '=', self.id)
        ]).write({'opt_out': True})
        
        message = "Oposición a marketing directo procesada. "\
                  "No recibirá más comunicaciones comerciales."
    
    elif processing_type == 'profiling':
        # Oposición a decisiones automatizadas
        self.write({
            'disable_automated_decisions': True
        })
        message = "Oposición a decisiones automatizadas procesada."
    
    elif processing_type == 'legitimate_interest':
        # Oposición a tratamiento por interés legítimo
        # Requiere evaluación caso por caso
        self._create_objection_case(reason)
        message = "Su oposición está siendo evaluada. "\
                  "Le responderemos en 1 mes."
    
    # Log
    self._log_gdpr_action('objection', f'{processing_type}: {reason}')
    
    # Notificar al paciente
    self.message_post(body=message)
```

### Plazos de Respuesta

**RGPD Artículo 12.3**:

```
📅 Plazo general: 1 MES desde recepción solicitud

📅 Prórroga: +2 MESES si es compleja
   (con notificación al interesado en el 1er mes)

📅 Gratuita la primera solicitud
   Puede cobrarse si es:
   - Manifiestamente infundada
   - Excesiva (repetitiva)
```

---

## Seguridad y Medidas Técnicas

### Medidas de Seguridad por Nivel

#### Nivel Alto (Datos de Salud)

**Obligatorio por Real Decreto 1720/2007**:

✅ **Control de acceso**:
```python
# Grupos de seguridad en Odoo
1. Administrador Sistema (todos los datos)
2. Fisioterapeuta (solo sus pacientes + datos clínicos)
3. Recepción (datos contacto + facturación, NO clínicos)
4. Contabilidad (solo datos económicos)
5. Marketing (solo con consentimiento comercial)

# Regla de registro (ir.rule)
<record id="rule_partner_clinical_therapist" model="ir.rule">
    <field name="name">Fisioterapeuta: Solo sus pacientes</field>
    <field name="model_id" ref="base.model_res_partner"/>
    <field name="domain_force">[
        '|',
        ('assigned_therapist_ids', 'in', [user.id]),
        ('create_uid', '=', user.id)
    ]</field>
    <field name="groups" eval="[(4, ref('vigoentrena.group_therapist'))]"/>
</record>
```

✅ **Cifrado**:
```bash
# Cifrado en tránsito
- SSL/TLS en todas las comunicaciones
- HTTPS obligatorio (no HTTP)
- Certificado válido (Let's Encrypt o comercial)

# Cifrado en reposo
- Base de datos: Cifrado a nivel filesystem (LUKS, dm-crypt)
- Backups: Cifrados con GPG
- Archivos adjuntos: Almacenamiento cifrado
```

✅ **Trazabilidad (logs de auditoría)**:
```python
# Registrar TODAS las acciones sobre datos de salud

class AuditLog(models.Model):
    _name = 'gdpr.audit.log'
    _order = 'create_date desc'
    
    partner_id = fields.Many2one('res.partner', 'Paciente', required=True)
    user_id = fields.Many2one('res.users', 'Usuario', required=True)
    action = fields.Selection([
        ('read', 'Lectura'),
        ('create', 'Creación'),
        ('write', 'Modificación'),
        ('delete', 'Eliminación'),
        ('export', 'Exportación'),
        ('print', 'Impresión'),
    ], required=True)
    
    model_name = fields.Char('Modelo')
    record_id = fields.Integer('ID Registro')
    field_name = fields.Char('Campo Modificado')
    old_value = fields.Text('Valor Anterior')
    new_value = fields.Text('Valor Nuevo')
    
    ip_address = fields.Char('IP')
    user_agent = fields.Char('Navegador')
    
# Interceptar todas las operaciones en res.partner
class Partner(models.Model):
    _inherit = 'res.partner'
    
    @api.model
    def create(self, vals):
        record = super().create(vals)
        self._log_audit('create', record, vals)
        return record
    
    def write(self, vals):
        old_vals = {field: self[field] for field in vals.keys()}
        result = super().write(vals)
        self._log_audit('write', self, vals, old_vals)
        return result
    
    def _log_audit(self, action, record, new_vals, old_vals=None):
        if not record.is_patient:  # Solo pacientes (datos de salud)
            return
        
        self.env['gdpr.audit.log'].sudo().create({
            'partner_id': record.id,
            'user_id': self.env.user.id,
            'action': action,
            'model_name': 'res.partner',
            'record_id': record.id,
            'old_value': json.dumps(old_vals) if old_vals else None,
            'new_value': json.dumps(new_vals),
            'ip_address': request.httprequest.remote_addr if request else None,
        })
```

✅ **Copias de seguridad**:
```bash
# Frecuencia
- Diarias: Base de datos completa
- Horarias: Logs y archivos modificados
- Semanal: Backup completo offsite

# Cifrado
gpg --encrypt --recipient vigoentrena@vigoentrena.com backup_YYYYMMDD.sql

# Retención
- 30 días: Backups diarios
- 12 meses: Backups semanales
- 7 años: Backups anuales (cumplimiento fiscal)

# Pruebas de restauración
- Trimestral: Simulacro completo
```

✅ **Formación del personal**:
```markdown
PLAN DE FORMACIÓN ANUAL RGPD

Módulo 1: Introducción RGPD (2h) - TODO EL PERSONAL
- Qué es RGPD
- Sanciones
- Responsabilidades

Módulo 2: Manejo de datos de salud (4h) - FISIOTERAPEUTAS
- Confidencialidad médica
- Consentimientos
- Derechos de pacientes
- Uso correcto de Odoo

Módulo 3: Seguridad y cifrado (3h) - IT
- Backups
- Control de acceso
- Brechas de seguridad

Módulo 4: Gestión de incidencias (2h) - RESPONSABLES
- Breach notifications
- Plan de respuesta
- Comunicación con AEPD

Frecuencia: Anual + Actualización cuando cambien normativas
```

#### Medidas Organizativas

✅ **Análisis de Riesgos**:
```markdown
MATRIZ DE RIESGOS VIGOENTRENA

| Riesgo | Probabilidad | Impacto | Medidas Mitigación |
|--------|--------------|---------|-------------------|
| Acceso no autorizado a historias clínicas | Media | Muy Alto | Control acceso por roles + 2FA |
| Pérdida de datos (fallo servidor) | Baja | Alto | Backups diarios cifrados offsite |
| Robo de dispositivos (portátiles) | Media | Alto | Cifrado de disco completo + VPN |
| Email con datos enviado a destinatario incorrecto | Media | Alto | Formación + Revisión doble |
| Brecha de seguridad proveedor cloud | Baja | Muy Alto | Cláusulas contractuales + Auditoría |
```

✅ **Política de escritorios limpios**:
```
- No dejar documentos impresos con datos de salud
- Bloqueo automático de pantalla (3 minutos inactividad)
- Destrucción segura documentos (trituradora)
- Prohibido llevar historias clínicas a casa
```

✅ **Gestión de proveedores (Encargados del Tratamiento)**:
```markdown
PROVEEDORES CLAVE + CONTRATOS REQUERIDOS

1. Odoo S.A. / Odoo.sh
   Contrato: Data Processing Agreement (DPA)
   Certificación: ISO 27001
   
2. Proveedor Hosting (si on-premise)
   Contrato: DPA personalizado
   Auditoría: Anual
   
3. Pasarela de pago (Stripe, Redsys)
   Contrato: DPA incluido en TOS
   PCI-DSS: Certificado
   
4. Email Marketing (si externo)
   Contrato: DPA
   Verificar: Transferencias internacionales
   
5. WhatsApp Business API
   Contrato: DPA Meta/Proveedor
   Cifrado: End-to-end verificado
```

### Evaluación de Impacto (EIPD)

**Cuándo es obligatorio** (Artículo 35 RGPD):
- Tratamiento a gran escala de categorías especiales (datos de salud) ✅ APLICA
- Decisiones automatizadas con efectos jurídicos
- Videovigilancia a gran escala de zonas públicas

**Proceso EIPD para Vigoentrena**:

```markdown
EVALUACIÓN DE IMPACTO EN PROTECCIÓN DE DATOS
VIGOENTRENA S.L. - Sistema Odoo 17

1. DESCRIPCIÓN DEL TRATAMIENTO
   - Finalidad: Gestión clínica, administrativa y comercial
   - Datos: Salud (categoría especial) + identificativos + económicos
   - Volumen: ~500 pacientes/año (proyección)
   - Responsable: VIGOENTRENA S.L.
   - Encargados: Odoo S.A., [Hosting Provider], [Payment Gateway]

2. NECESIDAD Y PROPORCIONALIDAD
   ✓ Tratamiento necesario para prestación servicio sanitario
   ✓ Datos recogidos: mínimos necesarios
   ✓ Conservación: limitada a plazos legales (15 años)

3. RIESGOS PARA LOS INTERESADOS
   
   Riesgo 1: Acceso no autorizado a historias clínicas
   - Probabilidad: Media
   - Gravedad: Crítica (datos sensibles salud)
   - Controles: Roles, 2FA, cifrado, logs
   
   Riesgo 2: Pérdida de datos por fallo técnico
   - Probabilidad: Baja
   - Gravedad: Alta
   - Controles: Backups diarios, redundancia
   
   Riesgo 3: Uso indebido para marketing sin consentimiento
   - Probabilidad: Baja
   - Gravedad: Media
   - Controles: Separación listas, doble opt-in
   
   Riesgo 4: Brecha de seguridad proveedor cloud
   - Probabilidad: Muy Baja
   - Gravedad: Crítica
   - Controles: DPA, cláusulas contractuales, ISO 27001

4. MEDIDAS DE MITIGACIÓN
   ✓ Control de acceso basado en roles (RBAC)
   ✓ Cifrado TLS/SSL + cifrado en reposo
   ✓ Backups cifrados diarios con retención 30d
   ✓ Logs de auditoría completos (quién, qué, cuándo)
   ✓ Formación anual del personal
   ✓ DPA con todos los proveedores
   ✓ Política de escritorios limpios
   ✓ Plan de respuesta ante brechas

5. RIESGOS RESIDUALES
   Tras aplicar medidas, los riesgos residuales son ACEPTABLES.

6. CONCLUSIÓN
   El tratamiento cumple con RGPD. Se implementarán todas las medidas.
   Revisión EIPD: Anual o ante cambios significativos.

Fecha: [Fecha]
Responsable: [Nombre + Cargo]
DPD: [Si aplica]
```

---

## Registro de Actividades de Tratamiento

**Artículo 30 RGPD**: Obligatorio para empresas con >250 empleados O que traten datos sensibles.

> ✅ **VIGOENTRENA DEBE TENERLO** (trata datos de salud)

**Plantilla Registro de Actividades**:

```markdown
REGISTRO DE ACTIVIDADES DE TRATAMIENTO
VIGOENTRENA S.L.

---

ACTIVIDAD 1: GESTIÓN DE PACIENTES Y TRATAMIENTOS

Responsable del tratamiento:
- Nombre: VIGOENTRENA S.L.
- CIF: B-XXXXXXXX
- Contacto: privacidad@vigoentrena.com

Delegado de Protección de Datos:
- [Si aplica]: Nombre, contacto

Finalidades del tratamiento:
- Gestión de historia clínica del paciente
- Diagnóstico, tratamiento y seguimiento
- Elaboración de protocolos de ejercicios personalizados
- Seguimiento de evolución y resultados

Categorías de interesados:
- Pacientes actuales
- Pacientes históricos (últimos 15 años)

Categorías de datos personales:
- Identificativos: Nombre, DNI, fecha nacimiento, dirección
- Contacto: Email, teléfono, móvil
- Salud (categoría especial):
  * Historial médico previo
  * Lesiones y patologías
  * Tratamientos aplicados
  * Notas de evolución clínica
  * Capacidades físicas
  * Alergias y precauciones
  * Fotografías clínicas (si aplica)

Categorías de destinatarios:
- Personal sanitario (fisioterapeutas)
- Personal administrativo (limitado: solo contacto/pago)
- Otros profesionales sanitarios (con consentimiento paciente)
- Administraciones públicas (obligación legal)

Transferencias internacionales:
- NO se realizan transferencias fuera del EEE
[O SI Odoo.sh en servidores UE: Odoo S.A., servidores en Bélgica/Alemania]

Plazos de supresión:
- Datos clínicos: 15 años desde última asistencia
- Datos contacto/pago: Hasta supresión datos clínicos

Medidas de seguridad:
- Nivel ALTO (datos de salud)
- Control de acceso por roles
- Cifrado TLS/SSL
- Backups diarios cifrados
- Logs de auditoría
- Formación anual del personal
- DPA con encargados del tratamiento

---

ACTIVIDAD 2: FACTURACIÓN Y COBROS

Responsable: VIGOENTRENA S.L.

Finalidades:
- Emisión de facturas
- Gestión de cobros y pagos
- Contabilidad
- Cumplimiento fiscal (VeriFactu, AEAT)

Categorías de interesados:
- Clientes/Pacientes
- Proveedores

Categorías de datos:
- Identificativos: Nombre, DNI/CIF, dirección fiscal
- Económicos: IBAN, datos facturación, historial pagos

Destinatarios:
- Entidades bancarias (domiciliaciones)
- AEAT (obligación legal)
- Gestoría/Asesoría fiscal
- Plataforma de pagos (Stripe, Redsys)

Transferencias internacionales:
- Stripe Inc. (USA) - Cláusulas contractuales tipo UE

Plazos de supresión:
- 6 años (Ley General Tributaria)

Medidas de seguridad:
- Nivel BÁSICO (datos económicos)
- Control de acceso
- Cifrado
- Backups diarios

---

ACTIVIDAD 3: COMUNICACIONES COMERCIALES

Responsable: VIGOENTRENA S.L.

Finalidades:
- Envío de newsletter
- Promociones y ofertas
- Información sobre nuevos servicios
- Encuestas de satisfacción

Categorías de interesados:
- Clientes actuales
- Clientes potenciales (leads)

Categorías de datos:
- Identificativos: Nombre, email
- Contacto: Teléfono (si consentimiento WhatsApp)
- Comerciales: Preferencias, intereses

Destinatarios:
- Plataforma email marketing (Odoo Mass Mailing)
- Proveedor WhatsApp Business API (si aplica)

Transferencias internacionales:
- Según proveedor email/WhatsApp

Plazos de supresión:
- 3 años desde última interacción
- O inmediatamente tras revocación de consentimiento

Medidas de seguridad:
- Nivel BÁSICO
- Doble opt-in (confirmación)
- Enlace de baja en cada comunicación
- Separación de listas (con/sin consentimiento)

---

ACTIVIDAD 4: VIDEOVIGILANCIA

Responsable: VIGOENTRENA S.L.

Finalidades:
- Seguridad de las instalaciones
- Prevención de actos delictivos

Categorías de interesados:
- Pacientes
- Empleados
- Visitantes

Categorías de datos:
- Imágenes de personas (dato personal)

Destinatarios:
- Fuerzas y Cuerpos de Seguridad (solo si delito)

Transferencias internacionales:
- NO

Plazos de supresión:
- Máximo 1 mes (salvo investigación delito)

Medidas de seguridad:
- Cartel informativo visible
- Acceso limitado a grabaciones
- Cifrado de almacenamiento
- Borrado automático >30 días

---

Fecha elaboración: [Fecha]
Última revisión: [Fecha]
Próxima revisión: [Fecha + 1 año]
```

---

## Auditorías y Logs

### Qué Registrar en Logs

**Acciones críticas sobre datos de salud**:

```python
EVENTOS A REGISTRAR (24/7):

✓ Accesos a fichas de pacientes
  - Quién: user_id
  - Qué: partner_id
  - Cuándo: timestamp
  - Cómo: lectura/escritura
  - Desde dónde: IP, navegador

✓ Modificaciones de datos
  - Campo modificado
  - Valor anterior → valor nuevo
  - Motivo (si aplica)

✓ Exportaciones de datos
  - Formato (PDF, CSV, JSON)
  - Registros incluidos
  - Destino (email, descarga)

✓ Impresiones
  - Documento impreso
  - Impresora utilizada

✓ Intentos de acceso fallidos
  - Usuario
  - Recurso solicitado
  - Motivo de denegación

✓ Cambios en permisos
  - Usuario afectado
  - Grupo añadido/eliminado
  - Quién realizó el cambio

✓ Backups y restauraciones
  - Tipo de backup
  - Éxito/Fallo
  - Ubicación destino
```

### Implementación de Logging Avanzado

```python
# Módulo: vigoentrena_audit

class AdvancedAuditLog(models.Model):
    _name = 'gdpr.advanced.audit'
    _order = 'create_date desc'
    _rec_name = 'action_type'
    
    # Quién
    user_id = fields.Many2one('res.users', 'Usuario', required=True)
    user_login = fields.Char('Login Usuario', required=True)
    user_role = fields.Char('Rol Usuario')
    
    # Qué
    action_type = fields.Selection([
        ('read', 'Lectura'),
        ('create', 'Creación'),
        ('update', 'Modificación'),
        ('delete', 'Eliminación'),
        ('export', 'Exportación'),
        ('print', 'Impresión'),
        ('login', 'Inicio Sesión'),
        ('logout', 'Cierre Sesión'),
        ('failed_login', 'Login Fallido'),
        ('permission_denied', 'Acceso Denegado'),
    ], required=True)
    
    model_name = fields.Char('Modelo', required=True)
    record_id = fields.Integer('ID Registro')
    record_name = fields.Char('Nombre Registro')
    
    # Si es paciente
    patient_id = fields.Many2one('res.partner', 'Paciente')
    
    # Detalles
    field_changed = fields.Char('Campo Modificado')
    old_value = fields.Text('Valor Anterior')
    new_value = fields.Text('Valor Nuevo')
    
    # Cuándo
    create_date = fields.Datetime('Fecha/Hora', readonly=True, required=True)
    
    # Dónde
    ip_address = fields.Char('Dirección IP')
    user_agent = fields.Text('Navegador/Dispositivo')
    session_id = fields.Char('ID Sesión')
    
    # Contexto
    http_method = fields.Char('Método HTTP')
    http_path = fields.Char('Ruta URL')
    http_referer = fields.Char('Referer')
    
    # Resultado
    success = fields.Boolean('Éxito', default=True)
    error_message = fields.Text('Mensaje Error')

# Interceptor global de todas las operaciones
@api.model
def _register_hook(self):
    """Monkey patch para auditar TODAS las operaciones en res.partner"""
    
    original_read = models.BaseModel.read
    original_create = models.BaseModel.create
    original_write = models.BaseModel.write
    original_unlink = models.BaseModel.unlink
    
    @api.model
    def audited_read(self, fields=None, load='_classic_read'):
        result = original_read(self, fields=fields, load=load)
        
        # Solo auditar modelos sensibles
        if self._name in ['res.partner', 'clinic.session', 'medical.history']:
            self.env['gdpr.advanced.audit'].sudo()._log_action(
                action_type='read',
                model_name=self._name,
                record_ids=self.ids,
                fields_accessed=fields,
            )
        
        return result
    
    @api.model
    def audited_create(self, vals_list):
        result = original_create(self, vals_list)
        
        if self._name in ['res.partner', 'clinic.session']:
            self.env['gdpr.advanced.audit'].sudo()._log_action(
                action_type='create',
                model_name=self._name,
                record_ids=result.ids,
                values=vals_list,
            )
        
        return result
    
    def audited_write(self, vals):
        old_values = {rec.id: {k: rec[k] for k in vals.keys()} for rec in self}
        result = original_write(self, vals)
        
        if self._name in ['res.partner', 'clinic.session']:
            self.env['gdpr.advanced.audit'].sudo()._log_action(
                action_type='update',
                model_name=self._name,
                record_ids=self.ids,
                old_values=old_values,
                new_values=vals,
            )
        
        return result
    
    # Aplicar monkey patches
    models.BaseModel.read = audited_read
    models.BaseModel.create = audited_create
    models.BaseModel.write = audited_write
```

### Retención de Logs

```python
# Política de retención de logs

RETENTION_POLICY = {
    'gdpr.advanced.audit': {
        'hot_storage': 90,  # días en BD principal (búsquedas rápidas)
        'cold_storage': 2555,  # 7 años en archivo comprimido
        'compression': True,
        'encryption': True,
    }
}

# Cron job: Archivar logs antiguos
@api.model
def _cron_archive_old_logs(self):
    """Ejecutar diariamente a las 02:00"""
    
    cutoff_date = fields.Datetime.now() - relativedelta(days=90)
    
    old_logs = self.env['gdpr.advanced.audit'].search([
        ('create_date', '<', cutoff_date),
        ('archived', '=', False),
    ])
    
    if old_logs:
        # Exportar a archivo comprimido cifrado
        export_data = old_logs.export_data(['user_id', 'action_type', ...])
        
        compressed = gzip.compress(json.dumps(export_data).encode())
        encrypted = gpg.encrypt(compressed, recipients=['dpo@vigoentrena.com'])
        
        filename = f'audit_logs_{cutoff_date.strftime("%Y%m")}.gz.gpg'
        
        # Guardar en almacenamiento frío (S3, NAS...)
        self._save_to_cold_storage(filename, encrypted)
        
        # Marcar como archivados (no eliminar de BD aún, por si acaso)
        old_logs.write({'archived': True})
    
    # Eliminar definitivamente logs >7 años
    very_old_date = fields.Datetime.now() - relativedelta(years=7)
    self.env['gdpr.advanced.audit'].search([
        ('create_date', '<', very_old_date)
    ]).unlink()
```

### Dashboard de Auditoría

```python
# Vista de auditoría para DPO/Responsables

class AuditDashboard(models.TransientModel):
    _name = 'gdpr.audit.dashboard'
    
    @api.model
    def get_stats(self):
        """Estadísticas de auditoría últimos 30 días"""
        
        start_date = fields.Datetime.now() - relativedelta(days=30)
        
        AuditLog = self.env['gdpr.advanced.audit']
        
        return {
            'total_accesses': AuditLog.search_count([
                ('create_date', '>=', start_date),
                ('action_type', '=', 'read'),
            ]),
            
            'unique_users': AuditLog.read_group(
                [('create_date', '>=', start_date)],
                ['user_id'],
                ['user_id']
            ),
            
            'top_accessed_patients': AuditLog.read_group(
                [
                    ('create_date', '>=', start_date),
                    ('patient_id', '!=', False),
                ],
                ['patient_id'],
                ['patient_id'],
                limit=10,
                orderby='patient_id_count desc'
            ),
            
            'failed_access_attempts': AuditLog.search_count([
                ('create_date', '>=', start_date),
                ('action_type', 'in', ['failed_login', 'permission_denied']),
            ]),
            
            'exports_count': AuditLog.search_count([
                ('create_date', '>=', start_date),
                ('action_type', '=', 'export'),
            ]),
            
            'unusual_activity': self._detect_unusual_activity(start_date),
        }
    
    def _detect_unusual_activity(self, since_date):
        """Detectar actividad sospechosa"""
        
        alerts = []
        
        # Alerta 1: Múltiples accesos al mismo paciente en poco tiempo
        suspicious_reads = self.env.cr.execute("""
            SELECT user_id, patient_id, COUNT(*) as access_count
            FROM gdpr_advanced_audit
            WHERE create_date >= %s
            AND action_type = 'read'
            AND patient_id IS NOT NULL
            GROUP BY user_id, patient_id, DATE(create_date)
            HAVING COUNT(*) > 20
        """, [since_date])
        
        if suspicious_reads:
            alerts.append({
                'type': 'excessive_access',
                'message': 'Usuario accedió >20 veces al mismo paciente en un día',
                'data': suspicious_reads,
            })
        
        # Alerta 2: Exportaciones masivas
        mass_exports = self.env['gdpr.advanced.audit'].search([
            ('create_date', '>=', since_date),
            ('action_type', '=', 'export'),
        ])
        
        if len(mass_exports) > 10:
            alerts.append({
                'type': 'mass_export',
                'message': f'{len(mass_exports)} exportaciones en 30 días',
                'data': mass_exports.ids,
            })
        
        # Alerta 3: Accesos fuera de horario (21:00 - 07:00)
        night_access = self.env['gdpr.advanced.audit'].search([
            ('create_date', '>=', since_date),
            '|',
            ('create_date', '<=', since_date.replace(hour=7)),
            ('create_date', '>=', since_date.replace(hour=21)),
        ])
        
        if night_access:
            alerts.append({
                'type': 'after_hours',
                'message': f'{len(night_access)} accesos fuera de horario',
                'data': night_access.ids,
            })
        
        return alerts
```

---

## Breach Notifications

### Definición de Brecha de Seguridad

**RGPD Artículo 4.12**:
> "Violación de la seguridad de los datos personales: violación de la seguridad que ocasione 
> la destrucción, pérdida o alteración accidental o ilícita de datos personales transmitidos, 
> conservados o tratados de otra forma, o la comunicación o acceso no autorizados a dichos datos."

**Ejemplos en Vigoentrena**:
- 💥 Ransomware cifra base de datos Odoo
- 💥 Empleado envía email con historias clínicas a destinatario equivocado
- 💥 Robo de portátil con datos de pacientes no cifrados
- 💥 Acceso no autorizado a cuenta Odoo por credenciales débiles
- 💥 Brecha de seguridad en proveedor cloud (Odoo.sh)
- 💥 Publicación accidental de fichero con datos en web pública

### Plazos Legales

```
⏰ 72 HORAS para notificar a AEPD desde que se CONOCE la brecha
   (no desde que ocurrió, sino desde que te enteras)

⏰ SIN DEMORA INDEBIDA para notificar a los interesados
   (si hay alto riesgo para sus derechos y libertades)

❌ Multas por no notificar:
   Hasta 10 millones € o 2% facturación global anual
```

### Protocolo de Respuesta ante Brechas

**PASO 1: Detección y Contención (0-2 horas)**

```markdown
EQUIPO DE RESPUESTA A INCIDENTES:
- Coordinador: [Responsable de Tratamiento / DPO]
- Técnico: [Administrador Sistemas]
- Legal: [Asesor jurídico si aplica]
- Comunicación: [Responsable Comunicación si aplica]

ACCIONES INMEDIATAS:

1.1. Identificar el tipo de brecha:
   [ ] Confidencialidad (acceso no autorizado)
   [ ] Integridad (alteración/destrucción datos)
   [ ] Disponibilidad (pérdida acceso a datos)

1.2. Contener la brecha:
   - Si es ransomware: Aislar sistemas afectados de red
   - Si es acceso no autorizado: Cambiar credenciales, cerrar sesiones
   - Si es email enviado por error: Solicitar devolución/eliminación
   - Si es robo físico: Cambio forzado de contraseñas

1.3. Preservar evidencias:
   - NO borrar logs
   - Capturar pantallas
   - Documentar cronología eventos
```

**PASO 2: Evaluación del Riesgo (2-12 horas)**

```markdown
EVALUAR IMPACTO:

2.1. ¿Qué datos se han visto afectados?
   [ ] Identificativos básicos (nombre, email, teléfono)
   [ ] Datos de salud (historias clínicas, diagnósticos)
   [ ] Datos económicos (IBAN, datos pago)
   [ ] Datos sensibles agravados (fotografías clínicas, etc.)

2.2. ¿Cuántos interesados afectados?
   Número aproximado: _______

2.3. ¿Qué consecuencias negativas pueden sufrir?
   [ ] Daños reputacionales
   [ ] Discriminación
   [ ] Suplantación de identidad
   [ ] Pérdidas financieras
   [ ] Daños físicos/psicológicos
   [ ] Otros: _______

2.4. Nivel de riesgo:
   [ ] BAJO: Sin riesgo significativo (ej: solo nombres sin más datos)
   [ ] MEDIO: Riesgo moderado (ej: datos contacto + datos económicos)
   [ ] ALTO: Riesgo elevado (ej: datos de salud sensibles)

DECISIÓN: ¿Requiere notificación a AEPD?
   [ ] SÍ (cualquier brecha que afecte datos personales)
   [ ] NO (solo si es irrelevante - MUY RARO)

DECISIÓN: ¿Requiere notificación a interesados?
   [ ] SÍ (si riesgo ALTO para derechos y libertades)
   [ ] NO (si riesgo BAJO/MEDIO y medidas mitigadoras efectivas)
```

**PASO 3: Notificación a AEPD (0-72 horas)**

```markdown
VÍA DE NOTIFICACIÓN:
Sede electrónica AEPD: https://sedeagpd.gob.es

FORMULARIO: "Notificación de violación de seguridad de los datos"

INFORMACIÓN A INCLUIR (Artículo 33.3 RGPD):

1. Naturaleza de la violación:
   - Descripción detallada de qué ocurrió
   - Cuándo ocurrió (fecha y hora estimada)
   - Cuándo se detectó
   - Cómo se detectó

2. Contacto:
   - Nombre y datos de contacto del DPD (o responsable)
   - Teléfono, email

3. Consecuencias probables:
   - Riesgos para los interesados
   - Impacto estimado

4. Medidas adoptadas:
   - Medidas de mitigación ya tomadas
   - Medidas propuestas para evitar repetición

5. Datos afectados:
   - Categorías de datos
   - Número aproximado de interesados
   - Número aproximado de registros

PLANTILLA EMAIL NOTIFICACIÓN AEPD:

---
Asunto: NOTIFICACIÓN BRECHA SEGURIDAD - VIGOENTRENA S.L.

Estimados Sres.:

Por la presente, VIGOENTRENA S.L. (CIF: B-XXXXXXXX) notifica una violación 
de seguridad de datos personales de conformidad con el artículo 33 RGPD.

1. DESCRIPCIÓN DEL INCIDENTE:
   Fecha/Hora ocurrencia: [DD/MM/YYYY HH:MM]
   Fecha/Hora detección: [DD/MM/YYYY HH:MM]
   
   Descripción: [Explicación detallada]
   
   Tipo de brecha: [ ] Confidencialidad [ ] Integridad [ ] Disponibilidad

2. DATOS AFECTADOS:
   - Categorías: Datos de salud, datos identificativos, datos de contacto
   - Nº aproximado interesados: [Número]
   - Nº aproximado registros: [Número]

3. CONSECUENCIAS PROBABLES:
   [Evaluación del impacto para los interesados]

4. MEDIDAS ADOPTADAS:
   Inmediatas:
   - [Lista de medidas de contención]
   
   Preventivas futuras:
   - [Medidas para evitar recurrencia]

5. CONTACTO:
   Delegado Protección Datos: [Nombre]
   Email: [Email]
   Teléfono: [Teléfono]

Quedamos a su disposición para cualquier aclaración.

Atentamente,
[Firma Responsable Tratamiento / DPD]
---
```

**PASO 4: Notificación a Interesados (Si aplica)**

```markdown
CUÁNDO NOTIFICAR:
✓ Riesgo ALTO para derechos y libertades
✓ Ejemplo: Datos de salud expuestos públicamente

EXCEPCIONES (no notificar si):
- Datos estaban cifrados y clave no comprometida
- Medidas posteriores garantizan que riesgo alto ya no se materializa
- Supondría esfuerzo desproporcionado (en ese caso: comunicación pública)

VÍA DE NOTIFICACIÓN:
- Email personal (preferible)
- Carta certificada (si no hay email)
- Comunicación pública (si >1000 afectados o esfuerzo desproporcionado)

PLANTILLA EMAIL A INTERESADOS:

---
Asunto: IMPORTANTE: Información sobre incidente de seguridad - Vigoentrena

Estimado/a [Nombre],

Le contactamos para informarle sobre un incidente de seguridad que ha afectado 
a algunos de sus datos personales en nuestra base de datos.

¿QUÉ HA OCURRIDO?
El [Fecha], hemos detectado [breve descripción del incidente].

¿QUÉ DATOS SE HAN VISTO AFECTADOS?
Los siguientes datos suyos pueden haber sido afectados:
- [Lista de categorías de datos]

¿QUÉ RIESGOS PUEDE SUPONER PARA USTED?
[Explicación clara y sencilla de los riesgos]

¿QUÉ HEMOS HECHO?
Inmediatamente hemos:
- [Medidas de contención]
- Notificado a la Agencia Española de Protección de Datos
- [Otras medidas]

¿QUÉ PUEDE HACER USTED?
Le recomendamos:
- [Acciones recomendadas: cambio contraseña, vigilar movimientos bancarios, etc.]
- Estar alerta ante posibles intentos de phishing

¿DÓNDE OBTENER MÁS INFORMACIÓN?
- Email: incidentes@vigoentrena.com
- Teléfono: [Teléfono]
- Horario: Lunes a Viernes, 9:00-18:00

Lamentamos sinceramente este incidente y le aseguramos que hemos tomado 
todas las medidas necesarias para evitar que vuelva a ocurrir.

Atentamente,
Equipo Vigoentrena
---
```

**PASO 5: Análisis Post-Mortem y Mejoras (1-4 semanas)**

```markdown
REUNIÓN POST-MORTEM:
Asistentes: Todo el equipo de respuesta + dirección

ANÁLISIS:

1. ¿Qué ocurrió exactamente?
   [Cronología detallada]

2. ¿Por qué ocurrió?
   Causa raíz: [Análisis de los 5 porqués]

3. ¿Qué funcionó bien en la respuesta?
   [Aspectos positivos]

4. ¿Qué NO funcionó?
   [Fallos en el proceso de respuesta]

5. Lecciones aprendidas:
   [Lista de aprendizajes]

PLAN DE ACCIÓN:

| Acción | Responsable | Plazo | Prioridad | Estado |
|--------|-------------|-------|-----------|--------|
| [Medida técnica 1] | [Nombre] | [Fecha] | Alta | Pendiente |
| [Medida organizativa 1] | [Nombre] | [Fecha] | Media | En curso |
| [Formación adicional] | [Nombre] | [Fecha] | Alta | Completado |

ACTUALIZACIÓN DOCUMENTACIÓN:
☐ Actualizar análisis de riesgos
☐ Actualizar EIPD
☐ Actualizar procedimientos de respuesta
☐ Actualizar formación del personal
```

### Registro de Brechas

```python
class DataBreachLog(models.Model):
    _name = 'gdpr.data.breach'
    _order = 'detection_date desc'
    
    name = fields.Char('Referencia', required=True, default='NEW')
    
    # Fechas
    occurrence_date = fields.Datetime('Fecha Ocurrencia (estimada)')
    detection_date = fields.Datetime('Fecha Detección', required=True, 
                                     default=fields.Datetime.now)
    notification_aepd_date = fields.Datetime('Fecha Notificación AEPD')
    notification_subjects_date = fields.Datetime('Fecha Notificación Interesados')
    
    # Descripción
    breach_type = fields.Selection([
        ('confidentiality', 'Confidencialidad (acceso no autorizado)'),
        ('integrity', 'Integridad (alteración/destrucción)'),
        ('availability', 'Disponibilidad (pérdida de acceso)'),
    ], required=True)
    
    description = fields.Text('Descripción Detallada', required=True)
    root_cause = fields.Text('Causa Raíz')
    
    # Impacto
    affected_data_types = fields.Many2many('gdpr.data.type', string='Tipos de Datos Afectados')
    affected_subjects_count = fields.Integer('Nº Interesados Afectados')
    affected_records_count = fields.Integer('Nº Registros Afectados')
    
    # Evaluación de riesgo
    risk_level = fields.Selection([
        ('low', 'Bajo'),
        ('medium', 'Medio'),
        ('high', 'Alto'),
    ], required=True)
    
    consequences = fields.Text('Consecuencias Probables')
    
    # Notificaciones
    notified_aepd = fields.Boolean('Notificado a AEPD')
    aepd_reference = fields.Char('Referencia AEPD')
    notified_subjects = fields.Boolean('Notificado a Interesados')
    
    # Medidas
    containment_measures = fields.Text('Medidas de Contención')
    preventive_measures = fields.Text('Medidas Preventivas Futuras')
    
    # Seguimiento
    state = fields.Selection([
        ('detected', 'Detectada'),
        ('contained', 'Contenida'),
        ('notified', 'Notificada'),
        ('resolved', 'Resuelta'),
        ('closed', 'Cerrada'),
    ], default='detected', required=True)
    
    responsible_id = fields.Many2one('res.users', 'Responsable Gestión')
    
    # Documentación
    attachment_ids = fields.Many2many('ir.attachment', string='Evidencias')
    
    @api.model
    def create(self, vals):
        if vals.get('name', 'NEW') == 'NEW':
            vals['name'] = self.env['ir.sequence'].next_by_code('gdpr.data.breach') or 'BREACH-001'
        return super().create(vals)
```

---

## Políticas y Documentación

### Documentos Obligatorios

#### 1. Política de Privacidad (Clientes/Pacientes)

**Ya cubierto anteriormente** - Ver sección "Configuración Base de RGPD"

#### 2. Política Interna de Protección de Datos (Empleados)

```markdown
POLÍTICA INTERNA DE PROTECCIÓN DE DATOS
VIGOENTRENA S.L.

OBJETIVO:
Establecer las normas internas para el correcto tratamiento de datos personales 
y garantizar el cumplimiento del RGPD y LOPDGDD.

ÁMBITO DE APLICACIÓN:
Todo el personal de Vigoentrena: fisioterapeutas, recepción, administración, limpieza.

PRINCIPIOS BÁSICOS:

1. CONFIDENCIALIDAD:
   - Los datos de los pacientes son CONFIDENCIALES
   - Solo pueden acceder las personas autorizadas
   - Prohibido compartir fuera del entorno profesional
   - Prohibido comentar casos con personas ajenas

2. NECESIDAD DE SABER:
   - Acceder solo a los datos necesarios para tu trabajo
   - Si no los necesitas, no los consultes

3. SEGURIDAD:
   - Contraseñas robustas (mínimo 12 caracteres, mayúsculas, números, símbolos)
   - Cambio de contraseña cada 6 meses
   - No compartir credenciales
   - Bloqueo de pantalla al ausentarse (3 minutos automático)
   - No usar ordenadores/dispositivos personales para acceder a datos

4. ESCRITORIOS LIMPIOS:
   - No dejar documentos impresos con datos
   - Guardar en cajones con llave al finalizar jornada
   - Destrucción segura (trituradora) de documentos

5. COMUNICACIONES:
   - Email: Verificar destinatario antes de enviar
   - No enviar datos de salud por email sin cifrado
   - WhatsApp: Solo con consentimiento paciente y datos mínimos

PROHIBICIONES:

❌ Acceder a datos de familiares o conocidos (salvo relación profesional)
❌ Compartir información de pacientes en redes sociales
❌ Fotografiar pantallas con datos de pacientes
❌ Copiar bases de datos a dispositivos personales
❌ Usar USB/discos externos sin cifrado
❌ Imprimir innecesariamente

CONSECUENCIAS INCUMPLIMIENTO:

El incumplimiento de esta política puede constituir:
- Falta laboral (amonestación, suspensión, despido)
- Infracción RGPD (sanciones AEPD)
- Delito penal (revelación de secretos - art. 197 Código Penal)

FORMACIÓN:

- Formación inicial: 4 horas (RGPD básico)
- Formación anual: 2 horas (actualización)
- Formación específica: Según cambios normativos

CONTACTO:

Dudas o incidentes:
- Email: privacidad@vigoentrena.com
- DPD: [Si aplica]

FIRMA DE ACEPTACIÓN:

He leído y comprendo esta política. Me comprometo a cumplirla.

Nombre: _____________________
Puesto: _____________________
Fecha: _____________________
Firma: _____________________
```

#### 3. Cláusulas Informativas (Formularios, Contratos)

```html
<!-- Formulario Web de Contacto -->

<form id="contact-form">
    <!-- Campos del formulario -->
    
    <div class="gdpr-notice">
        <p class="small">
            <strong>INFORMACIÓN BÁSICA SOBRE PROTECCIÓN DE DATOS</strong><br>
            
            <strong>Responsable:</strong> VIGOENTRENA S.L. - CIF B-XXXXXXXX<br>
            
            <strong>Finalidad:</strong> Gestionar su solicitud de información y 
            enviarle comunicaciones comerciales de nuestros servicios (con su consentimiento).<br>
            
            <strong>Legitimación:</strong> Consentimiento del interesado.<br>
            
            <strong>Destinatarios:</strong> No se cederán datos a terceros, salvo 
            obligación legal.<br>
            
            <strong>Derechos:</strong> Acceder, rectificar y suprimir los datos, así 
            como otros derechos, como se explica en la 
            <a href="/privacy-policy">Política de Privacidad</a>.<br>
            
            <strong>Información adicional:</strong> Puede consultar información adicional 
            y detallada en nuestra <a href="/privacy-policy">Política de Privacidad</a>.
        </p>
    </div>
    
    <div class="form-check">
        <input type="checkbox" id="accept-privacy" required>
        <label for="accept-privacy">
            He leído y acepto la 
            <a href="/privacy-policy" target="_blank">Política de Privacidad</a>*
        </label>
    </div>
    
    <div class="form-check">
        <input type="checkbox" id="accept-commercial">
        <label for="accept-commercial">
            Acepto recibir comunicaciones comerciales sobre servicios de Vigoentrena
        </label>
    </div>
    
    <button type="submit">Enviar</button>
</form>
```

```markdown
<!-- Contrato de Prestación de Servicios -->

CLÁUSULA DE PROTECCIÓN DE DATOS

De conformidad con el Reglamento (UE) 2016/679 (RGPD) y la Ley Orgánica 3/2018 (LOPDGDD), 
le informamos:

RESPONSABLE: VIGOENTRENA S.L. - CIF: B-XXXXXXXX
Dirección: [Dirección]
Email: privacidad@vigoentrena.com

FINALIDAD: Sus datos serán tratados para:
- Gestión de la relación contractual (prestación de servicios de fisioterapia)
- Elaboración y conservación de su historia clínica
- Facturación y cobros
- Cumplimiento de obligaciones legales

BASE LEGAL:
- Ejecución del presente contrato
- Consentimiento expreso para datos de salud (artículo 9.2.h RGPD)
- Obligación legal (facturación, normativa sanitaria)

CONSERVACIÓN: Sus datos se conservarán durante:
- Datos clínicos: 15 años desde la última asistencia
- Datos económicos: 6 años (Ley General Tributaria)

DESTINATARIOS: Podrán comunicarse a:
- Administraciones Públicas (obligación legal)
- Entidades bancarias (cobros/pagos)
- Proveedores tecnológicos (con Contrato de Encargado del Tratamiento)

DERECHOS: Puede ejercitar sus derechos de acceso, rectificación, supresión, 
limitación, portabilidad y oposición dirigiéndose a privacidad@vigoentrena.com.

También puede reclamar ante la Agencia Española de Protección de Datos (www.aepd.es).

CONSENTIMIENTO EXPRESO DATOS DE SALUD:

Mediante la firma de este contrato, AUTORIZO expresamente a Vigoentrena al 
tratamiento de mis datos de salud para las finalidades indicadas.

Este consentimiento puede ser revocado en cualquier momento, sin que ello afecte 
a la licitud del tratamiento anterior.


Firmado en [Ciudad], a [Fecha]

El Cliente                      Vigoentrena S.L.


_________________              _________________
```

#### 4. Contratos con Encargados del Tratamiento (DPA)

```markdown
CONTRATO DE ENCARGADO DEL TRATAMIENTO

Entre:

A) VIGOENTRENA S.L., con CIF B-XXXXXXXX, en calidad de RESPONSABLE DEL TRATAMIENTO

y

B) [NOMBRE PROVEEDOR], con CIF [CIF], en calidad de ENCARGADO DEL TRATAMIENTO

Se acuerda:

PRIMERA. OBJETO
El Encargado tratará por cuenta del Responsable los siguientes datos personales:

- Categorías de datos: [Identificativos, Salud, Económicos, etc.]
- Finalidad: [Hosting de aplicación, Email marketing, etc.]
- Interesados: Pacientes/clientes de Vigoentrena
- Duración: [Duración del contrato principal]

SEGUNDA. OBLIGACIONES DEL ENCARGADO

El Encargado se compromete a:

1. Tratar los datos únicamente conforme a instrucciones documentadas del Responsable
2. NO aplicar datos a otra finalidad
3. Garantizar la confidencialidad (obligación de secreto del personal)
4. Implementar medidas de seguridad técnicas y organizativas apropiadas
5. Notificar al Responsable cualquier brecha de seguridad sin demora indebida 
   (máximo 24 horas)
6. Asistir al Responsable en el ejercicio de derechos de los interesados
7. Asistir en evaluaciones de impacto y consultas previas
8. Al finalizar el servicio: Devolver o destruir todos los datos (según elección 
   del Responsable)
9. Poner a disposición del Responsable toda la información necesaria para demostrar 
   el cumplimiento
10. Permitir auditorías por parte del Responsable

TERCERA. SUBCONTRATACIÓN

El Encargado NO podrá subcontratar sin autorización previa, específica, por escrito 
del Responsable.

Subcontratistas autorizados:
- [Lista si los hay]

Cualquier subcontratista deberá firmar un contrato con las mismas obligaciones que 
este documento.

CUARTA. TRANSFERENCIAS INTERNACIONALES

[ ] NO se realizarán transferencias fuera del EEE

[ ] SI se realizarán transferencias a: [País]
    Base legal: [ ] Decisión de adecuación
                [ ] Cláusulas contractuales tipo UE
                [ ] Normas corporativas vinculantes
                [ ] Otra: _______

QUINTA. MEDIDAS DE SEGURIDAD

El Encargado garantiza implementar al menos:

- Control de acceso basado en roles
- Cifrado de comunicaciones (TLS 1.2+)
- Cifrado de datos en reposo (AES-256)
- Copias de seguridad diarias, conservadas 30 días
- Logs de auditoría durante [X] meses
- Plan de continuidad de negocio
- Formación anual del personal en protección de datos

Certificaciones acreditadas:
[ ] ISO 27001
[ ] ISO 27018
[ ] SOC 2 Type II
[ ] Otra: _______

SEXTA. DURACIÓN Y EXTINCIÓN

Duración: Vinculado al contrato principal de [Servicio]

Al finalizar:
[ ] Devolver todos los datos al Responsable
[ ] Destruir todos los datos (certificado de destrucción)

Plazo: 30 días desde finalización

SÉPTIMA. RESPONSABILIDAD

El Encargado responderá de los daños causados por incumplimiento de este contrato.

En caso de sanción de la autoridad de control, cada parte asumirá la parte 
proporcional a su responsabilidad.

OCTAVA. LEGISLACIÓN Y JURISDICCIÓN

Legislación aplicable: Española
Jurisdicción: Tribunales de [Ciudad]


Firmado en [Ciudad], a [Fecha]

El Responsable                  El Encargado


_________________              _________________
VIGOENTRENA S.L.               [PROVEEDOR]
```

---

## Módulos y Herramientas

### Módulos Odoo Nativos

**Odoo Enterprise 17**:

```python
# Módulos de privacidad incluidos
1. privacy
   - Gestión de peticiones de datos (acceso, rectificación, supresión)
   - Dashboard de privacidad
   - Flujos de trabajo para ejercicio de derechos

2. privacy_lookup
   - Búsqueda rápida de todos los datos de un contacto
   - Vista unificada de datos en todos los módulos
   
3. website_privacy
   - Banner de cookies configurable
   - Gestión de consentimientos web
   - Políticas de privacidad editables
```

**Configuración**:

```bash
# Activar módulos
Apps > Buscar "Privacy" > Instalar todos

# Configurar privacidad
Ajustes > General > Privacy

☑️ Enable GDPR Cookie Consent
☑️ Show Cookie Policy
☑️ Show Privacy Policy
```

### Módulos de Terceros (OCA / Apps Store)

**Recomendados**:

```
1. GDPR Compliance (Apps Store)
   https://apps.odoo.com/apps/modules/17.0/gdpr_compliance/
   - Gestión automatizada de derechos
   - Plantillas de emails conformes
   - Dashboard de cumplimiento
   
2. Data Anonymization (OCA)
   https://github.com/OCA/data-protection
   - Anonimización automática tras plazo conservación
   - Scripts de anonimización personalizables
   
3. Audit Trail (OCA)
   https://github.com/OCA/server-tools
   - Logs detallados de cambios en modelos
   - Trazabilidad completa
```

### Herramientas Externas

**DPO Tools** (Software gestión cumplimiento):

```
1. OneTrust
   - Suite completa de privacidad
   - Gestión de consentimientos
   - Evaluaciones de impacto
   - Integración API con Odoo

2. TrustArc
   - Mapeo de datos
   - Gestión de riesgos
   - Cookie consent management

3. Securiti.ai
   - Automatización de derechos
   - DSR (Data Subject Requests) automation
```

**Generadores de Políticas**:

```
1. iubenda.com
   - Generador de políticas de privacidad
   - Generador de cookie policy
   - Multilenguas
   - Integración con website

2. TermsFeed
   - Plantillas RGPD
   - Personalizables por sector
```

---

## Checklist de Cumplimiento

### Pre-Launch (Antes de Producción)

```markdown
CHECKLIST RGPD - VIGOENTRENA

FASE 0: DOCUMENTACIÓN BASE
☐ Política de Privacidad redactada y publicada
☐ Política Interna de Protección de Datos firmada por empleados
☐ Registro de Actividades de Tratamiento completado
☐ Evaluación de Impacto (EIPD) realizada y firmada
☐ Contratos DPA con todos los proveedores (Odoo, hosting, email, pagos)
☐ Procedimiento de respuesta ante brechas documentado
☐ Formularios de consentimiento creados (salud, comercial, cookies)

FASE 1: CONFIGURACIÓN TÉCNICA ODOO
☐ Módulos privacy instalados y configurados
☐ Grupos de seguridad definidos (fisio, recepción, admin, marketing)
☐ Reglas de registro (ir.rule) configuradas
☐ Campos de consentimientos añadidos a res.partner
☐ Modelo de logs de auditoría creado
☐ Cron de archivo de logs antiguo configurado
☐ Banner de cookies activo en website
☐ Política de privacidad enlazada en formularios

FASE 2: SEGURIDAD
☐ HTTPS obligatorio (certificado SSL válido)
☐ Cifrado en tránsito (TLS 1.2+)
☐ Cifrado en reposo (base de datos, backups)
☐ Contraseñas robustas obligatorias (min. 12 caracteres)
☐ 2FA activado para usuarios administradores
☐ Bloqueo automático de pantalla (3 minutos)
☐ Backups diarios automáticos cifrados
☐ Backup offsite configurado (cloud remoto)
☐ Prueba de restauración realizada
☐ Firewall configurado (solo puertos necesarios)
☐ Logs de acceso activados y monitorizados
☐ Plan de Recuperación ante Desastres documentado

FASE 3: FORMACIÓN
☐ Formación RGPD básica a TODO el personal (2-4h)
☐ Formación uso seguro de Odoo
☐ Política Interna firmada por cada empleado
☐ Material de formación disponible para nuevas incorporaciones

FASE 4: PROCESOS
☐ Procedimiento de alta de pacientes (con consentimientos)
☐ Procedimiento de ejercicio de derechos (acceso, rectificación, supresión, etc.)
☐ Procedimiento de gestión de brechas
☐ Procedimiento de revisión de consentimientos (anual)
☐ Asignado responsable de privacidad/DPD

FASE 5: TESTING
☐ Simulacro de brecha de seguridad
☐ Test de ejercicio de derechos (solicitar acceso a datos de prueba)
☐ Test de formularios web (consentimientos, cookies)
☐ Test de emails automáticos (confirmación consentimiento, etc.)
☐ Test de backup y restauración

FASE 6: LEGAL
☐ Verificar con asesor jurídico que todo está correcto
☐ (Opcional) Inscripción ante AEPD como fichero [Ya no obligatorio tras RGPD]
☐ Seguro de responsabilidad civil profesional (incluye ciberriesgos)
```

### Post-Launch (Operación Continua)

```markdown
TAREAS RECURRENTES RGPD

DIARIAS:
☐ Verificar backups automáticos ejecutados correctamente
☐ Monitorizar alertas de seguridad (accesos fallidos, actividad sospechosa)

SEMANALES:
☐ Revisar peticiones de ejercicio de derechos (si las hay)
☐ Revisar logs de auditoría (actividad inusual)

MENSUALES:
☐ Revisar estado de consentimientos (revocaciones)
☐ Verificar que listas de email marketing solo incluyen contactos con consentimiento
☐ Comprobar actualizaciones de seguridad de Odoo

TRIMESTRALES:
☐ Simulacro de restauración de backup
☐ Revisar Registro de Actividades de Tratamiento (cambios)
☐ Revisar contratos con proveedores (cambios en servicios)
☐ Formación de reciclaje al personal (breve)

SEMESTRALES:
☐ Cambio de contraseñas de usuarios con acceso a datos sensibles
☐ Revisar y actualizar EIPD si hay cambios significativos
☐ Auditoría interna de cumplimiento RGPD

ANUALES:
☐ Formación completa RGPD a todo el personal
☐ Revisar y actualizar todas las políticas de privacidad
☐ Revisar plazos de conservación (eliminar/anonimizar datos antiguos)
☐ Auditoría externa (recomendado, no obligatorio)
☐ Revisar certificaciones de proveedores (ISO 27001, etc.)

AL CAMBIO:
☐ Nuevo proveedor/encargado: Firmar DPA antes de compartir datos
☐ Nuevo tipo de dato: Actualizar Registro de Actividades + EIPD
☐ Nueva finalidad: Solicitar nuevo consentimiento
☐ Cambio normativo: Actualizar políticas y procedimientos
```

---

## FAQs

### 1. ¿Necesito un Delegado de Protección de Datos (DPD)?

**Artículo 37 RGPD**: Es obligatorio si:
- Autoridad u organismo público
- Actividades principales requieren seguimiento regular y sistemático a gran escala
- **Tratamiento a gran escala de categorías especiales (datos de salud)** ✅

> **VIGOENTRENA**: Depende del volumen.
> - Si >500 pacientes activos simultáneamente: **SÍ, recomendable**
> - Si <500: No obligatorio, pero recomendable tener asesor RGPD externo

**Costes DPD**:
- Interno: Formación empleado (3.000-5.000€) + Tiempo dedicado
- Externo: 200-800€/mes según proveedor

### 2. ¿Puedo usar Google Drive para backups de Odoo?

**SÍ**, si:
- ✅ Cifras los backups antes de subirlos
- ✅ Tienes DPA firmado con Google (Google Workspace incluye DPA)
- ✅ Usas cuenta de empresa (no personal)

**Mejor opción**: rclone con cifrado automático

```bash
rclone sync /backups/ gdrive:backups/ --crypt-mode=encrypt
```

### 3. ¿Cuánto tiempo conservo los datos de un paciente que no vuelve?

**Datos de salud**: 15 años desde última asistencia  
**Datos económicos**: 6 años (obligación fiscal)  
**Datos comerciales**: 3 años o hasta revocación consentimiento

Pasado el plazo: Anonimizar (no eliminar historial clínico, pero sí datos identificativos)

### 4. ¿Puedo enviar recordatorios de citas por WhatsApp?

**SÍ**, si:
- ✅ Tienes consentimiento específico del paciente
- ✅ Usas WhatsApp Business (no personal)
- ✅ Tienes DPA con proveedor de API (Meta / 360dialog / Twilio)
- ✅ Envías solo datos mínimos (nombre, fecha/hora cita - NO diagnóstico)

**Texto recomendado**:
```
Hola [Nombre], te recordamos tu cita en Vigoentrena el [Fecha] a las [Hora]. 
Confirma tu asistencia respondiendo SÍ. Gracias!
```

❌ **NO envíes**: "Recordatorio fisioterapia para tu lesión de rodilla..."

### 5. ¿Qué hago si un paciente solicita eliminar sus datos pero aún está en plazo de conservación?

**Respuesta**:
```
"Lamentamos informarle que la legislación sanitaria española nos obliga 
a conservar su historia clínica durante 15 años desde la última asistencia.

Su última visita fue el [Fecha]. Podremos proceder a la anonimización de 
sus datos a partir del [Fecha + 15 años].

Mientras tanto, podemos:
- Limitar el tratamiento de sus datos (solo conservación, no uso activo)
- Revocar su consentimiento para comunicaciones comerciales
- Bloquear su acceso al portal de pacientes

¿Desea que procedamos con alguna de estas opciones?"
```

### 6. ¿Puedo tomar fotografías de las lesiones de los pacientes?

**SÍ**, si:
- ✅ Consentimiento informado específico y por escrito
- ✅ Finalidad clara: Seguimiento evolución clínica
- ✅ Almacenamiento seguro (dentro de Odoo, no en móviles personales)
- ✅ Acceso limitado a fisioterapeuta tratante

**Texto consentimiento**:
```
CONSENTIMIENTO PARA FOTOGRAFÍAS CLÍNICAS

Autorizo a Vigoentrena a tomar fotografías de mi [zona corporal] con 
finalidad exclusiva de seguimiento de la evolución de mi tratamiento.

Estas imágenes:
- Se almacenarán en mi historia clínica digital (Odoo)
- Solo serán visibles por mi fisioterapeuta y personal autorizado
- Se conservarán durante 15 años (plazo legal)
- NO se utilizarán para fines publicitarios o docentes
- Puedo solicitar su eliminación al finalizar mi tratamiento

Fecha: _______________  Firma: _______________
```

### 7. ¿Cómo gestiono el derecho de portabilidad si el paciente quiere cambiar de fisioterapeuta?

**Proceso**:
1. Paciente solicita portabilidad (email a privacidad@vigoentrena.com)
2. Verificar identidad (DNI)
3. Exportar datos en formato estructurado:
   ```python
   partner.action_data_portability(export_format='json')
   # o 'xml', 'csv'
   ```
4. Entregar al paciente en 1 mes (por email seguro o descarga temporal)
5. El paciente puede:
   - Entregar a nuevo profesional
   - Conservar para sí mismo

**NO incluir** en exportación:
- Opiniones/anotaciones internas del fisio (no son datos del paciente)
- Datos de otros pacientes (si hay menciones)

### 8. ¿Qué pasa si Odoo.sh tiene una brecha de seguridad?

**Responsabilidades**:
- **Odoo S.A.**: Notificar a Vigoentrena (encargado → responsable)
- **Vigoentrena**: Evaluar impacto y notificar a AEPD y pacientes si aplica

**Proceso**:
1. Odoo.sh te notifica la brecha (debe hacerlo en <24h según DPA)
2. Evaluación conjunta del impacto
3. Si afecta a datos de salud → Notificar AEPD en 72h
4. Si alto riesgo → Notificar a pacientes afectados

**Cláusula DPA con Odoo**:
> "El Encargado notificará al Responsable cualquier brecha de seguridad 
> sin demora indebida y, en cualquier caso, en un plazo máximo de 24 horas."

### 9. ¿Puedo compartir la historia clínica con otro profesional (médico, otro fisio)?

**SÍ**, si:
- ✅ Consentimiento explícito del paciente (verbal está bien, pero mejor escrito)
- ✅ Finalidad: Continuidad asistencial / Segunda opinión
- ✅ Método seguro: Email cifrado, plataforma sanitaria, entrega en mano cifrada

**NO**: 
- ❌ Sin consentimiento del paciente
- ❌ Por email normal (sin cifrado)
- ❌ Con fines ajenos al tratamiento

### 10. ¿Cómo demuestro cumplimiento si me audita la AEPD?

**Documentos a tener listos**:

```
📁 CARPETA RGPD VIGOENTRENA/

├── 01-DOCUMENTACION-BASE/
│   ├── Politica_Privacidad_Web.pdf
│   ├── Politica_Interna_Proteccion_Datos.pdf (firmada por empleados)
│   ├── Registro_Actividades_Tratamiento.pdf
│   ├── EIPD_Evaluacion_Impacto.pdf
│   
├── 02-CONSENTIMIENTOS/
│   ├── Formulario_Consentimiento_Salud.pdf
│   ├── Formulario_Consentimiento_Comercial.pdf
│   ├── Formulario_Cookies.pdf
│   └── LOGS/ (registros consentimientos otorgados/revocados)
│   
├── 03-CONTRATOS-DPA/
│   ├── DPA_Odoo.pdf
│   ├── DPA_Hosting.pdf (si aplica)
│   ├── DPA_Pasarela_Pago.pdf
│   ├── DPA_Email_Marketing.pdf
│   └── DPA_WhatsApp.pdf
│   
├── 04-MEDIDAS-SEGURIDAD/
│   ├── Analisis_Riesgos.pdf
│   ├── Configuracion_Grupos_Seguridad_Odoo.pdf
│   ├── Politica_Contraseñas.pdf
│   ├── Politica_Backups.pdf
│   ├── Logs_Auditoría/ (últimos 6 meses accesibles)
│   └── Certificados_Formacion_Personal.pdf
│   
├── 05-PROCEDIMIENTOS/
│   ├── Procedimiento_Ejercicio_Derechos.pdf
│   ├── Procedimiento_Brechas_Seguridad.pdf
│   └── Checklist_Cumplimiento.pdf
│   
├── 06-EVIDENCIAS/
│   ├── Capturas_Banner_Cookies.pdf
│   ├── Captura_Formulario_Consentimiento_Web.pdf
│   ├── Logs_Backups_Ultimo_Mes.pdf
│   └── Certificado_SSL.pdf
│   
└── 07-REVISIONES/
    ├── Acta_Revision_RGPD_2024.pdf
    ├── Informe_Simulacro_Brecha_2024.pdf
    └── Plan_Mejora_Continua.pdf
```

---

## Conclusión

El cumplimiento de RGPD y LOPD en Vigoentrena no es solo una obligación legal, sino una **ventaja competitiva** que genera confianza en tus pacientes.

### Inversión Estimada

```
COSTES INICIALES:
- Formación RGPD personal: 500-1.000€
- Asesoría jurídica (revisión documentos): 1.000-2.000€
- Módulos Odoo GDPR: 0€ (nativos Enterprise) o 200-500€ (terceros)
- DPD externo (opcional): 0€ o 200-800€/mes

TOTAL INICIAL: 1.500-3.500€

COSTES RECURRENTES:
- DPD externo: 0€ o 200-800€/mes (2.400-9.600€/año)
- Formación anual: 300-500€
- Auditorías externas (opcional): 1.000-3.000€/año
- Actualizaciones legales: 200-500€/año

TOTAL ANUAL: 2.000-14.000€/año (según si DPD externo o no)
```

### ROI No Monetario

- 🛡️ **Protección ante sanciones** (hasta 20M€)
- 💚 **Confianza de pacientes**
- 🏅 **Diferenciación competitiva**
- 📈 **Mejor reputación online**
- ⚖️ **Tranquilidad jurídica**

### Próximos Pasos

1. **Revisión**: Usar el checklist para identificar gaps
2. **Priorización**: Empezar por lo crítico (datos de salud)
3. **Implementación**: Configurar Odoo según esta guía
4. **Formación**: Capacitar al equipo
5. **Monitorización**: Mantener cumplimiento continuo

---

**Última actualización**: Octubre 2025  
**Próxima revisión**: Octubre 2026  
**Contacto**: Para dudas sobre esta guía, consulte con su asesor RGPD o DPD.

---

## Recursos Adicionales

**Enlaces oficiales**:
- [Agencia Española de Protección de Datos (AEPD)](https://www.aepd.es)
- [Reglamento RGPD (texto completo)](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [LOPDGDD (texto completo)](https://www.boe.es/eli/es/lo/2018/12/05/3)
- [Guías sectoriales AEPD](https://www.aepd.es/es/guias-y-herramientas)

**Herramientas AEPD**:
- [Facilita RGPD](https://www.aepd.es/es/herramientas/facilita-rgpd): Asistente online
- [Evalúa RGPD](https://www.aepd.es/es/herramientas/evalua-rgpd): Autoevaluación

**Formación**:
- [Cursos AEPD gratuitos](https://sedeagpd.gob.es/formacion)
- Udemy: "RGPD para empresas"
- LinkedIn Learning: "GDPR Compliance"

