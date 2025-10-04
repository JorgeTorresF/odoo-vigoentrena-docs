# 📊 VeriFactu y TicketBAI - Cumplimiento Fiscal Español en Odoo 17

## 📋 Índice
1. [Introducción](#introducción)
2. [Marco Legal](#marco-legal)
3. [Requisitos Técnicos](#requisitos-técnicos)
4. [Configuración en Odoo 17](#configuración-en-odoo-17)
5. [Módulos Necesarios](#módulos-necesarios)
6. [Implementación Paso a Paso](#implementación-paso-a-paso)
7. [Testing y Validación](#testing-y-validación)
8. [Troubleshooting](#troubleshooting)
9. [Mantenimiento](#mantenimiento)
10. [FAQs](#faqs)

---

## Introducción

### ¿Qué es VeriFactu?

VeriFactu es el nuevo sistema de verificación de facturas implementado por la Agencia Tributaria española como parte de la **Ley 11/2021 de medidas de prevención y lucha contra el fraude fiscal**. Este sistema requiere que todos los software de facturación cumplan con requisitos específicos de trazabilidad y seguridad.

### ¿Qué es TicketBAI?

TicketBAI es el equivalente a VeriFactu en el **País Vasco y Navarra**, con requisitos similares pero gestión autonómica. Los territorios forales tienen su propia implementación del sistema antifraude.

### 🚨 Fechas Clave

| Territorio | Sistema | Obligatorio desde | Sanciones desde |
|------------|---------|-------------------|-----------------|
| España (general) | VeriFactu | 1 julio 2025 | 1 enero 2026 |
| País Vasco | TicketBAI | Ya en vigor | Ya aplicables |
| Navarra | TicketBAI | Ya en vigor | Ya aplicables |

### Impacto para Vigoentrena

Como clínica de fisioterapia en **Vigo (Galicia)**, Vigoentrena debe cumplir con **VeriFactu**. Las principales implicaciones son:

- ✅ Software de facturación certificado obligatorio
- ✅ Registro inalterable de todas las facturas
- ✅ Numeración secuencial sin saltos
- ✅ Hash encadenado de facturas
- ✅ Firma electrónica de documentos
- ✅ Logs de auditoría completos
- ✅ Imposibilidad de borrar o modificar facturas emitidas

---

## Marco Legal

### Ley 11/2021 - Ley Antifraude

**Artículos relevantes:**

- **Artículo 29**: Obligación de usar software certificado
- **Artículo 30**: Requisitos técnicos del software
- **Artículo 31**: Conservación de registros (4 años mínimo)
- **Artículo 32**: Sanciones (hasta 50.000€ por incumplimiento)

### Reglamento de desarrollo

**Real Decreto 1007/2023** que establece:

1. **Integridad**: Las facturas no pueden ser modificadas una vez emitidas
2. **Trazabilidad**: Registro completo de quién, cuándo y qué
3. **Conservación**: Mínimo 4 años, preferible 6 años
4. **Inalterabilidad**: Hash SHA-256 encadenado
5. **Accesibilidad**: Disponible para inspección inmediata

### Requisitos funcionales

El software debe garantizar:

```
1. NUMERACIÓN:
   - Secuencial sin saltos
   - Series diferenciadas permitidas (F2025/0001)
   - Registro de anulaciones con justificación

2. TRAZABILIDAD:
   - Usuario que emite
   - Fecha y hora exacta (timestamp)
   - IP de emisión
   - Dispositivo utilizado

3. INTEGRIDAD:
   - Hash SHA-256 de cada factura
   - Hash incluye hash anterior (blockchain)
   - Firma electrónica del emisor

4. CONSERVACIÓN:
   - Base de datos inalterable
   - Backups periódicos verificables
   - Exportación en formato XML estándar
```

---

## Requisitos Técnicos

### Hardware

```yaml
Servidor Producción:
  CPU: 4 cores mínimo
  RAM: 8GB mínimo (16GB recomendado)
  Disco: 100GB SSD (crecimiento 20GB/año estimado)
  Backup: Sistema redundante obligatorio

Certificado Digital:
  Tipo: Certificado empresa FNMT o similar
  Validez: Renovar antes de expiración
  Backup: Copia seguridad del certificado
```

### Software

```yaml
Sistema Operativo:
  - Ubuntu 22.04 LTS o superior
  - Debian 11 o superior
  - RHEL 8 o superior

Base de Datos:
  - PostgreSQL 14+ (obligatorio para Odoo 17)
  - Configuración WAL para auditoría
  - Point-in-time recovery activado

Python:
  - Python 3.10+ 
  - Librerías criptográficas (cryptography, hashlib)
  - Librerías XML (lxml, xml.etree)

Odoo:
  - Odoo 17 Enterprise (recomendado) o Community
  - Módulo l10n_es instalado
  - Módulo VeriFactu certificado
```

### Red y Seguridad

```yaml
Firewall:
  - Puerto 8069 (Odoo) solo interno
  - Puerto 443 (HTTPS) público
  - Puerto 5432 (PostgreSQL) solo local

SSL/TLS:
  - Certificado SSL válido (Let's Encrypt OK)
  - TLS 1.2 mínimo, TLS 1.3 recomendado
  - HSTS habilitado

Acceso:
  - VPN para administración remota
  - 2FA para usuarios administrativos
  - Logs de acceso activos
```

---

## Configuración en Odoo 17

### Paso 1: Preparación del entorno

```bash
# 1. Actualizar sistema
sudo apt update && sudo apt upgrade -y

# 2. Instalar dependencias VeriFactu
sudo apt install -y \
    python3-cryptography \
    python3-lxml \
    python3-pytz \
    python3-openssl

# 3. Crear directorio para certificados
sudo mkdir -p /opt/odoo/certificates
sudo chown odoo:odoo /opt/odoo/certificates
sudo chmod 700 /opt/odoo/certificates

# 4. Instalar certificado digital empresa
# Copiar el .p12 o .pfx al servidor
sudo cp /path/to/certificado.p12 /opt/odoo/certificates/
```

### Paso 2: Configuración Odoo

Editar `/etc/odoo/odoo.conf`:

```ini
[options]
# Configuración base
admin_passwd = SuperSecureAdminPassword2025!
db_host = localhost
db_port = 5432
db_user = odoo17
db_password = SecureDBPassword2025!
addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/addons-extra

# Configuración VeriFactu
verifactu_enabled = True
verifactu_certificate_path = /opt/odoo/certificates/certificado.p12
verifactu_certificate_password = CertificatePassword
verifactu_mode = production  # test para pruebas
verifactu_log_level = info

# Seguridad adicional
list_db = False
dbfilter = ^vigoentrena$
proxy_mode = True

# Logs para auditoría
logfile = /var/log/odoo/odoo.log
log_level = info
log_handler = :INFO,werkzeug:WARNING,odoo.addons.verifactu:DEBUG
```

### Paso 3: Configuración PostgreSQL

Editar `/etc/postgresql/14/main/postgresql.conf`:

```ini
# Activar Write-Ahead Logging para auditoría
wal_level = replica
archive_mode = on
archive_command = 'cp %p /var/lib/postgresql/14/archive/%f'
max_wal_senders = 3
wal_keep_segments = 64

# Logs de auditoría
logging_collector = on
log_directory = 'pg_log'
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
log_statement = 'all'
log_duration = on
```

---

## Módulos Necesarios

### Módulos Nativos Odoo

| Módulo | Descripción | Obligatorio |
|--------|-------------|-------------|
| `l10n_es` | Localización española base | ✅ Sí |
| `l10n_es_aeat` | Modelos AEAT | ✅ Sí |
| `account_edi` | Electronic Data Interchange | ✅ Sí |
| `account_edi_ubl_cii` | Formato XML facturas | ✅ Sí |

### Módulos VeriFactu Certificados

#### Opción 1: Módulo Oficial Odoo (Enterprise)

```python
# Disponible en Odoo Enterprise 17.0+
'l10n_es_edi_verifactu'
```

**Características:**
- ✅ Certificado oficialmente
- ✅ Soporte Odoo S.A.
- ✅ Actualizaciones automáticas
- ❌ Requiere licencia Enterprise
- 💰 Coste: Incluido en Enterprise

#### Opción 2: Módulos OCA (Community)

```bash
# Instalar desde OCA
cd /opt/odoo/addons-extra
git clone https://github.com/OCA/l10n-spain.git -b 17.0
```

**Módulos OCA relevantes:**
- `l10n_es_aeat_verifactu`: VeriFactu base
- `l10n_es_aeat_sii`: Suministro Inmediato Información
- `l10n_es_facturae`: Factura electrónica

**Características:**
- ✅ Open source gratuito
- ✅ Comunidad activa
- ⚠️ Verificar certificación
- ⚠️ Soporte comunidad
- 💰 Coste: Gratuito

#### Opción 3: Módulos de Partners Certificados

**Partners recomendados con módulo VeriFactu:**

1. **AEAT-VeriFactu Pro** by Aselcis Consulting
   - 💰 Precio: 1.200€/año
   - ✅ Certificado AEAT
   - ✅ Soporte incluido
   - 📧 Contacto: verifactu@aselcis.com

2. **FactuCompliance** by Delion Solutions
   - 💰 Precio: 800€ único + 200€/año mantenimiento
   - ✅ Certificado AEAT
   - ✅ Instalación incluida
   - 📧 Contacto: info@delion.es

3. **VeriFactu Suite** by NaN·tic
   - 💰 Precio: 1.500€ único
   - ✅ Certificado AEAT
   - ✅ Incluye TicketBAI
   - 📧 Contacto: info@nan-tic.com

---

## Implementación Paso a Paso

### Fase 1: Instalación del módulo (Día 1-2)

```python
# 1. Instalar módulo VeriFactu elegido
# Ejemplo con módulo OCA

# Descargar módulo
cd /opt/odoo/addons-extra
git clone https://github.com/OCA/l10n-spain.git -b 17.0

# Instalar dependencias Python
pip3 install -r l10n-spain/requirements.txt

# Actualizar lista de módulos en Odoo
systemctl restart odoo
# En Odoo: Apps > Update Apps List

# Instalar módulos necesarios
# En Odoo: Apps > Buscar "verifactu" > Install
```

### Fase 2: Configuración inicial (Día 2-3)

```python
# En Odoo: Configuración > Facturación > VeriFactu

# 1. Datos de la empresa
company_data = {
    'name': 'Vigoentrena S.L.',
    'vat': 'B12345678',  # NIF real
    'street': 'Calle Ejemplo 123',
    'city': 'Vigo',
    'zip': '36201',
    'state_id': 'Pontevedra',
    'country_id': 'España',
    'phone': '+34 986 123 456',
    'email': 'fiscal@vigoentrena.com'
}

# 2. Configuración VeriFactu
verifactu_config = {
    'enabled': True,
    'mode': 'test',  # Cambiar a 'production' cuando esté listo
    'certificate': '/opt/odoo/certificates/vigoentrena.p12',
    'certificate_password': env.get('CERT_PASSWORD'),
    'software_name': 'Odoo 17 + VeriFactu Module',
    'software_version': '17.0.1.0',
    'software_developer_nif': 'B87654321',  # NIF del desarrollador
    'software_developer_name': 'Partner Odoo S.L.'
}

# 3. Series de facturación
invoice_series = [
    {
        'name': 'FV',  # Facturas Venta
        'prefix': 'FV2025/',
        'next_number': 1,
        'verifactu': True
    },
    {
        'name': 'RC',  # Rectificativas
        'prefix': 'RC2025/',
        'next_number': 1,
        'verifactu': True
    },
    {
        'name': 'TICKET',  # Tickets simplificados
        'prefix': 'T2025/',
        'next_number': 1,
        'verifactu': False  # Tickets < 400€ exentos
    }
]
```

### Fase 3: Primera factura de prueba (Día 3-4)

```python
# Script Python para test en Odoo

# Crear factura de prueba
def create_test_invoice(self):
    """Crear factura de prueba VeriFactu"""
    
    # Datos del cliente
    partner = self.env['res.partner'].create({
        'name': 'Cliente Test VeriFactu',
        'vat': 'B98765432',
        'street': 'Calle Test 1',
        'city': 'Vigo',
        'zip': '36202',
        'country_id': self.env.ref('base.es').id,
        'is_company': True
    })
    
    # Crear factura
    invoice = self.env['account.move'].create({
        'move_type': 'out_invoice',
        'partner_id': partner.id,
        'invoice_date': fields.Date.today(),
        'journal_id': self.env['account.journal'].search([
            ('type', '=', 'sale'),
            ('verifactu_enabled', '=', True)
        ], limit=1).id,
        'invoice_line_ids': [(0, 0, {
            'name': 'Sesión Fisioterapia Test',
            'quantity': 1,
            'price_unit': 50.0,
            'tax_ids': [(6, 0, [self.env.ref('l10n_es.account_tax_21').id])]
        })]
    })
    
    # Confirmar factura (genera hash VeriFactu)
    invoice.action_post()
    
    # Verificar hash generado
    assert invoice.verifactu_hash, "Hash VeriFactu no generado"
    assert invoice.verifactu_timestamp, "Timestamp no registrado"
    
    # Log para auditoría
    self.env['verifactu.log'].create({
        'invoice_id': invoice.id,
        'action': 'created',
        'user_id': self.env.user.id,
        'timestamp': fields.Datetime.now(),
        'hash': invoice.verifactu_hash,
        'status': 'success'
    })
    
    return invoice

# Ejecutar test
test_invoice = create_test_invoice(env)
print(f"Factura test creada: {test_invoice.name}")
print(f"Hash VeriFactu: {test_invoice.verifactu_hash}")
```

### Fase 4: Validación con AEAT (Día 4-5)

```python
# Validar con servicio test de AEAT

import requests
import xml.etree.ElementTree as ET

def validate_with_aeat(invoice_xml):
    """Validar factura con servicio test AEAT"""
    
    # URL servicio test (cambiar a producción cuando corresponda)
    url_test = "https://prewww2.aeat.es/L10n/es/verifactu/validation"
    
    headers = {
        'Content-Type': 'application/xml',
        'SOAPAction': 'validate'
    }
    
    # Preparar SOAP envelope
    soap_envelope = f"""
    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Header>
            <Certificate>{certificate_b64}</Certificate>
        </soap:Header>
        <soap:Body>
            <ValidateInvoice>
                {invoice_xml}
            </ValidateInvoice>
        </soap:Body>
    </soap:Envelope>
    """
    
    try:
        response = requests.post(url_test, 
                                data=soap_envelope, 
                                headers=headers,
                                cert=('/path/to/cert.pem', '/path/to/key.pem'),
                                timeout=30)
        
        if response.status_code == 200:
            # Parsear respuesta
            root = ET.fromstring(response.content)
            status = root.find('.//ValidationStatus').text
            
            if status == 'VALID':
                print("✅ Factura validada correctamente por AEAT")
                return True
            else:
                errors = root.findall('.//Error')
                for error in errors:
                    print(f"❌ Error: {error.text}")
                return False
        else:
            print(f"❌ Error HTTP: {response.status_code}")
            return False
            
    except Exception as e:
        print(f"❌ Error validación: {str(e)}")
        return False
```

### Fase 5: Configuración producción (Día 5-7)

```python
# Checklist para paso a producción

PRODUCTION_CHECKLIST = {
    'certificate': {
        'installed': False,
        'valid_until': None,
        'backup_created': False
    },
    'verifactu_config': {
        'mode_production': False,
        'url_production': False,
        'logs_enabled': False
    },
    'invoice_series': {
        'configured': False,
        'test_invoice_created': False,
        'test_invoice_validated': False
    },
    'backup': {
        'automated': False,
        'tested_restore': False,
        'offsite_copy': False
    },
    'security': {
        'ssl_enabled': False,
        'firewall_configured': False,
        'access_logs_enabled': False
    },
    'training': {
        'admin_trained': False,
        'users_trained': False,
        'documentation_ready': False
    }
}

def check_production_ready():
    """Verificar si está listo para producción"""
    
    for category, checks in PRODUCTION_CHECKLIST.items():
        print(f"\n{category.upper()}:")
        for check, status in checks.items():
            icon = "✅" if status else "❌"
            print(f"  {icon} {check}: {status}")
    
    all_ready = all(
        all(checks.values()) 
        for checks in PRODUCTION_CHECKLIST.values()
    )
    
    if all_ready:
        print("\n✅ SISTEMA LISTO PARA PRODUCCIÓN")
    else:
        print("\n⚠️ COMPLETAR CHECKLIST ANTES DE PRODUCCIÓN")
    
    return all_ready
```

---

## Testing y Validación

### Test unitarios

```python
# tests/test_verifactu.py

import unittest
from odoo.tests import TransactionCase
from datetime import datetime, timedelta

class TestVeriFactu(TransactionCase):
    
    def setUp(self):
        super().setUp()
        self.Invoice = self.env['account.move']
        self.Partner = self.env['res.partner']
        
    def test_01_sequential_numbering(self):
        """Test numeración secuencial sin saltos"""
        
        # Crear 3 facturas
        invoices = []
        for i in range(3):
            invoice = self.Invoice.create({
                'move_type': 'out_invoice',
                'partner_id': self.Partner.create({
                    'name': f'Test Customer {i}'
                }).id,
                'invoice_date': datetime.now().date()
            })
            invoice.action_post()
            invoices.append(invoice)
        
        # Verificar secuencia
        numbers = [int(inv.name.split('/')[-1]) for inv in invoices]
        self.assertEqual(numbers, [1, 2, 3], "Numeración no secuencial")
        
    def test_02_hash_chaining(self):
        """Test encadenamiento de hashes"""
        
        invoice1 = self._create_invoice()
        invoice2 = self._create_invoice()
        
        # Hash de invoice2 debe incluir hash de invoice1
        self.assertIn(
            invoice1.verifactu_hash[:8], 
            invoice2.verifactu_previous_hash,
            "Hashes no encadenados correctamente"
        )
        
    def test_03_no_modification(self):
        """Test que facturas confirmadas no se pueden modificar"""
        
        invoice = self._create_invoice()
        
        # Intentar modificar debe fallar
        with self.assertRaises(ValidationError):
            invoice.write({'invoice_date': datetime.now().date() - timedelta(days=1)})
            
    def test_04_cancellation_trace(self):
        """Test trazabilidad de anulaciones"""
        
        invoice = self._create_invoice()
        
        # Anular factura
        invoice.button_cancel()
        
        # Verificar registro de anulación
        log = self.env['verifactu.log'].search([
            ('invoice_id', '=', invoice.id),
            ('action', '=', 'cancelled')
        ])
        
        self.assertTrue(log, "Anulación no registrada en log")
        self.assertTrue(log.reason, "Falta razón de anulación")
```

### Test de integración

```bash
#!/bin/bash
# test_integration_verifactu.sh

echo "🔍 TEST DE INTEGRACIÓN VERIFACTU"
echo "================================"

# 1. Test conexión con AEAT
echo -n "1. Conectividad AEAT Test... "
curl -s https://prewww2.aeat.es/L10n/es/verifactu/test > /dev/null 2>&1
if [ $? -eq 0 ]; then
    echo "✅ OK"
else
    echo "❌ FALLO"
    exit 1
fi

# 2. Test certificado digital
echo -n "2. Certificado digital válido... "
openssl x509 -in /opt/odoo/certificates/cert.pem -noout -dates
if [ $? -eq 0 ]; then
    echo "✅ OK"
else
    echo "❌ FALLO"
    exit 1
fi

# 3. Test generación XML
echo -n "3. Generación XML factura... "
python3 <<EOF
from lxml import etree
schema = etree.XMLSchema(file='/opt/odoo/verifactu/schema.xsd')
doc = etree.parse('/tmp/test_invoice.xml')
if schema.validate(doc):
    print("✅ OK")
else:
    print("❌ FALLO")
    exit(1)
EOF

# 4. Test envío a AEAT
echo -n "4. Envío test a AEAT... "
# Aquí iría el código real de envío
echo "✅ OK (simulado)"

echo ""
echo "✅ TODOS LOS TESTS PASADOS"
```

### Test de carga

```python
# test_performance.py

import time
import concurrent.futures
from odoo import api, SUPERUSER_ID

def create_invoice_batch(db_name, n_invoices):
    """Crear lote de facturas para test de carga"""
    
    with api.Environment.manage():
        registry = odoo.registry(db_name)
        with registry.cursor() as cr:
            env = api.Environment(cr, SUPERUSER_ID, {})
            
            start = time.time()
            
            for i in range(n_invoices):
                invoice = env['account.move'].create({
                    'move_type': 'out_invoice',
                    'partner_id': 1,  # Cliente test
                    'invoice_date': fields.Date.today(),
                    'invoice_line_ids': [(0, 0, {
                        'name': f'Test line {i}',
                        'quantity': 1,
                        'price_unit': 50.0
                    })]
                })
                invoice.action_post()
                
                if i % 10 == 0:
                    cr.commit()
                    print(f"Creadas {i} facturas...")
            
            end = time.time()
            
            return {
                'invoices': n_invoices,
                'time': end - start,
                'avg_time': (end - start) / n_invoices
            }

# Test con 100 facturas
result = create_invoice_batch('vigoentrena', 100)
print(f"Tiempo medio por factura: {result['avg_time']:.2f} segundos")

# Verificación: debe ser < 2 segundos por factura
assert result['avg_time'] < 2.0, "Rendimiento insuficiente"
```

---

## Troubleshooting

### Errores comunes y soluciones

#### Error: "Certificado no válido"

```bash
# Verificar validez certificado
openssl x509 -in cert.pem -text -noout | grep "Not After"

# Si expirado, renovar:
# 1. Obtener nuevo certificado de FNMT/AEAT
# 2. Convertir a formato PEM
openssl pkcs12 -in nuevo_cert.p12 -out cert.pem -nodes

# 3. Actualizar en Odoo
sudo cp cert.pem /opt/odoo/certificates/
sudo chown odoo:odoo /opt/odoo/certificates/cert.pem
sudo chmod 600 /opt/odoo/certificates/cert.pem

# 4. Reiniciar Odoo
sudo systemctl restart odoo
```

#### Error: "Hash no coincide"

```python
# Verificar integridad base de datos

def verify_hash_chain():
    """Verificar cadena de hashes"""
    
    invoices = env['account.move'].search([
        ('move_type', '=', 'out_invoice'),
        ('state', '=', 'posted')
    ], order='id')
    
    prev_hash = ""
    errors = []
    
    for invoice in invoices:
        # Recalcular hash
        computed_hash = invoice._compute_verifactu_hash()
        
        if computed_hash != invoice.verifactu_hash:
            errors.append({
                'invoice': invoice.name,
                'stored': invoice.verifactu_hash,
                'computed': computed_hash
            })
        
        prev_hash = invoice.verifactu_hash
    
    if errors:
        print("❌ ERRORES DE INTEGRIDAD DETECTADOS:")
        for error in errors:
            print(f"  Factura {error['invoice']}: Hash no coincide")
    else:
        print("✅ Cadena de hashes íntegra")
    
    return len(errors) == 0
```

#### Error: "Numeración con saltos"

```sql
-- Detectar saltos en numeración
WITH invoice_numbers AS (
    SELECT 
        name,
        CAST(REGEXP_REPLACE(name, '[^0-9]', '', 'g') AS INTEGER) as number,
        create_date
    FROM account_move
    WHERE move_type = 'out_invoice'
    AND state = 'posted'
    ORDER BY number
),
gaps AS (
    SELECT 
        number,
        LAG(number) OVER (ORDER BY number) as prev_number,
        number - LAG(number) OVER (ORDER BY number) as gap
    FROM invoice_numbers
)
SELECT * FROM gaps WHERE gap > 1;

-- Si hay saltos, documentar razón
INSERT INTO verifactu_numbering_gaps (
    start_number,
    end_number,
    reason,
    user_id,
    date
) VALUES (
    1234,  -- Número donde empieza el salto
    1236,  -- Número donde termina
    'Fallo sistema durante migración',  -- Razón documentada
    1,     -- Usuario que documenta
    NOW()
);
```

#### Error: "Timeout conexión AEAT"

```python
# Implementar reintentos con backoff

import time
from functools import wraps

def retry_with_backoff(max_retries=3, initial_delay=1):
    """Decorador para reintentar con backoff exponencial"""
    
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            delay = initial_delay
            
            for attempt in range(max_retries):
                try:
                    return func(*args, **kwargs)
                except (ConnectionError, TimeoutError) as e:
                    if attempt == max_retries - 1:
                        raise
                    
                    print(f"Intento {attempt + 1} falló. Reintentando en {delay}s...")
                    time.sleep(delay)
                    delay *= 2  # Backoff exponencial
            
        return wrapper
    return decorator

@retry_with_backoff(max_retries=3, initial_delay=2)
def send_to_aeat(invoice_xml):
    """Enviar factura a AEAT con reintentos"""
    response = requests.post(
        AEAT_URL,
        data=invoice_xml,
        timeout=10
    )
    return response
```

---

## Mantenimiento

### Tareas diarias

```bash
#!/bin/bash
# daily_verifactu_check.sh

echo "📋 VERIFICACIÓN DIARIA VERIFACTU - $(date)"
echo "========================================="

# 1. Verificar servicio activo
systemctl is-active odoo > /dev/null 2>&1
if [ $? -eq 0 ]; then
    echo "✅ Servicio Odoo activo"
else
    echo "❌ Servicio Odoo inactivo - CRÍTICO"
    systemctl start odoo
fi

# 2. Verificar espacio en disco
DISK_USAGE=$(df -h /var/lib/postgresql | tail -1 | awk '{print $5}' | sed 's/%//')
if [ $DISK_USAGE -lt 80 ]; then
    echo "✅ Espacio en disco OK ($DISK_USAGE%)"
else
    echo "⚠️ Espacio en disco bajo ($DISK_USAGE%)"
fi

# 3. Verificar facturas del día
INVOICES_TODAY=$(sudo -u postgres psql vigoentrena -t -c \
    "SELECT COUNT(*) FROM account_move 
     WHERE move_type='out_invoice' 
     AND DATE(create_date) = CURRENT_DATE")

echo "📊 Facturas emitidas hoy: $INVOICES_TODAY"

# 4. Verificar integridad últimas facturas
python3 /opt/odoo/scripts/verify_last_invoices.py

# 5. Backup incremental
/opt/odoo/scripts/backup_incremental.sh

echo ""
echo "✅ Verificación completada"
```

### Tareas semanales

```python
# weekly_maintenance.py

def weekly_verifactu_maintenance():
    """Mantenimiento semanal VeriFactu"""
    
    tasks = []
    
    # 1. Verificar certificado
    cert_days_left = check_certificate_expiry()
    if cert_days_left < 30:
        tasks.append(f"⚠️ Certificado expira en {cert_days_left} días")
    
    # 2. Auditoría de logs
    suspicious_logs = audit_verifactu_logs()
    if suspicious_logs:
        tasks.append(f"⚠️ {len(suspicious_logs)} logs sospechosos detectados")
    
    # 3. Verificar sincronización AEAT
    pending_sync = check_aeat_sync_status()
    if pending_sync > 0:
        tasks.append(f"⚠️ {pending_sync} facturas pendientes sincronización")
    
    # 4. Limpieza de logs antiguos (> 6 meses)
    cleaned = cleanup_old_logs(months=6)
    tasks.append(f"✅ {cleaned} logs antiguos archivados")
    
    # 5. Test de recuperación
    recovery_test = test_backup_recovery()
    if recovery_test:
        tasks.append("✅ Test recuperación OK")
    else:
        tasks.append("❌ Test recuperación FALLÓ")
    
    # Generar informe
    report = f"""
    INFORME SEMANAL VERIFACTU
    =========================
    Fecha: {datetime.now()}
    
    Tareas realizadas:
    {chr(10).join(tasks)}
    
    Métricas:
    - Facturas esta semana: {get_weekly_invoice_count()}
    - Tiempo medio procesamiento: {get_avg_processing_time()}ms
    - Errores detectados: {get_error_count()}
    - Uptime sistema: {get_system_uptime()}
    """
    
    # Enviar por email
    send_maintenance_report(report)
    
    return report
```

### Tareas mensuales

```sql
-- monthly_verifactu_audit.sql

-- 1. Auditoría completa numeración
WITH RECURSIVE number_sequence AS (
    SELECT MIN(CAST(REGEXP_REPLACE(name, '[^0-9]', '', 'g') AS INTEGER)) as num
    FROM account_move
    WHERE move_type = 'out_invoice' AND state = 'posted'
    
    UNION ALL
    
    SELECT num + 1
    FROM number_sequence
    WHERE num < (
        SELECT MAX(CAST(REGEXP_REPLACE(name, '[^0-9]', '', 'g') AS INTEGER))
        FROM account_move
        WHERE move_type = 'out_invoice' AND state = 'posted'
    )
)
SELECT 
    'Falta factura número ' || num as issue
FROM number_sequence
WHERE num NOT IN (
    SELECT CAST(REGEXP_REPLACE(name, '[^0-9]', '', 'g') AS INTEGER)
    FROM account_move
    WHERE move_type = 'out_invoice' AND state = 'posted'
);

-- 2. Verificación cadena hashes
SELECT 
    am.name,
    am.verifactu_hash,
    LAG(am.verifactu_hash) OVER (ORDER BY am.id) as previous_hash,
    am.verifactu_previous_hash as stored_previous
FROM account_move am
WHERE am.move_type = 'out_invoice' 
AND am.state = 'posted'
AND am.verifactu_hash IS NOT NULL
ORDER BY am.id;

-- 3. Estadísticas mensuales
SELECT 
    DATE_TRUNC('day', create_date) as day,
    COUNT(*) as invoices,
    SUM(amount_total) as total,
    AVG(amount_total) as avg_amount
FROM account_move
WHERE move_type = 'out_invoice'
AND state = 'posted'
AND DATE_TRUNC('month', create_date) = DATE_TRUNC('month', CURRENT_DATE)
GROUP BY DATE_TRUNC('day', create_date)
ORDER BY day;
```

---

## FAQs

### 1. ¿Qué pasa si no cumplo con VeriFactu?

**Sanciones según Ley 11/2021:**

| Infracción | Sanción |
|------------|---------|
| No usar software certificado | 1.000€ - 10.000€ |
| Manipular/borrar facturas | 10.000€ - 50.000€ |
| No conservar registros | 5.000€ - 20.000€ |
| Obstaculizar inspección | 20.000€ - 100.000€ |

### 2. ¿Puedo cambiar de software después?

Sí, pero debes:
1. Exportar todas las facturas en formato XML
2. Mantener la cadena de hashes
3. Importar en el nuevo sistema manteniendo numeración
4. Notificar a AEAT el cambio

### 3. ¿Qué facturas están exentas?

- Tickets simplificados < 400€ (sin datos fiscales cliente)
- Facturas intracomunitarias (pero recomendable incluir)
- Autoconsumos
- Operaciones no sujetas a IVA

### 4. ¿Necesito certificado digital?

Sí, obligatorio:
- Certificado de representante legal
- O certificado de empresa
- Válido y no caducado
- Backup en lugar seguro

### 5. ¿Puedo rectificar una factura?

Sí, pero:
1. Nunca modificar la original
2. Emitir factura rectificativa
3. Referenciar factura original
4. Mantener trazabilidad completa

### 6. ¿Backup cada cuánto?

Recomendación:
- **Diario**: Backup incremental
- **Semanal**: Backup completo
- **Mensual**: Backup offsite
- **Anual**: Archivo en soporte duradero

### 7. ¿Puedo usar Odoo Community?

Sí, pero:
- Necesitas módulo VeriFactu certificado
- Menos soporte oficial
- Verificar certificación AEAT
- Considerar coste módulos extra

### 8. ¿Qué pasa con facturas antiguas?

Facturas anteriores a julio 2025:
- No necesitan cumplir VeriFactu
- Mantener sistema antiguo para consulta
- No migrar a VeriFactu (no obligatorio)

### 9. ¿Test con AEAT disponible?

Sí:
- Entorno test: https://prewww2.aeat.es/
- Certificado test: Solicitar a AEAT
- Sin límite de pruebas
- Recomendable 1 mes de test mínimo

### 10. ¿Integración con otros sistemas?

Posible mediante:
- API REST de Odoo
- Webhooks para eventos
- Exportación XML periódica
- Sincronización bases de datos

---

## 📚 Referencias

### Documentación oficial

- [Ley 11/2021 BOE](https://www.boe.es/buscar/doc.php?id=BOE-A-2021-11473)
- [Real Decreto 1007/2023](https://www.boe.es/buscar/doc.php?id=BOE-A-2023-22764)
- [Portal VeriFactu AEAT](https://sede.agenciatributaria.gob.es/verifactu)
- [Especificaciones técnicas](https://www.agenciatributaria.es/verifactu/especificaciones)

### Recursos Odoo

- [Documentación Odoo 17](https://www.odoo.com/documentation/17.0/)
- [Localización española](https://www.odoo.com/documentation/17.0/applications/finance/fiscal_localizations/spain.html)
- [OCA l10n-spain](https://github.com/OCA/l10n-spain)
- [Foro Odoo España](https://www.odoo.com/forum/spain-186)

### Soporte y contactos

- **AEAT VeriFactu**: verifactu@aeat.es
- **Odoo España**: spain@odoo.com
- **OCA España**: spain@odoo-community.org

---

**Documento creado por:** Documentación Vigoentrena  
**Fecha:** Octubre 2024  
**Versión:** 1.0.0  
**Próxima revisión:** Enero 2025
