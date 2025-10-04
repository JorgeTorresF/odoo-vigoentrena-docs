# Instalación de Odoo 17

## 🎯 Introducción

Esta guía cubre todas las formas de instalar Odoo 17, desde la más simple (Odoo Online) hasta la más compleja (instalación desde código fuente en Linux).

**Elige tu camino según tu perfil**:

| Perfil | Opción Recomendada | Dificultad | Tiempo Setup |
|--------|-------------------|------------|--------------|
| Sin conocimientos técnicos | Odoo Online | ⭐ | 5 minutos |
| Usuario intermedio | Odoo.sh | ⭐⭐ | 15 minutos |
| Desarrollador | Docker | ⭐⭐⭐ | 30 minutos |
| DevOps / SysAdmin | Instalación Linux | ⭐⭐⭐⭐ | 2-4 horas |

---

## 🚀 Opción 1: Odoo Online (SaaS) - MÁS RÁPIDO

### ¿Qué es?
Odoo completamente gestionado en la nube. Sin instalación, sin mantenimiento.

### ✅ Ventajas
- Setup en 5 minutos
- Sin mantenimiento técnico
- Backups automáticos
- Actualizaciones automáticas
- Soporte oficial incluido
- Escalable instantáneamente

### ❌ Desventajas
- Módulos custom limitados (solo Apps Store oficial)
- Menos control técnico
- Datos en servidores Odoo (Europa)

### 💰 Coste
```
Standard: ~24€/usuario/mes
  └── Módulos básicos

Custom: ~37€/usuario/mes
  └── Todos los módulos Enterprise

One App Free: Gratis
  └── 1 aplicación, usuarios ilimitados (limitado)
```

### 📝 Instalación Paso a Paso

#### 1. Crear Cuenta
```
1. Ir a: https://www.odoo.com/trial
2. Completar formulario:
   - Email
   - Nombre empresa: Vigoentrena
   - País: España
   - Teléfono
   - Número de empleados: 1-5
3. Click "Start Now"
4. Confirmar email
```

#### 2. Configuración Inicial
```
1. Elegir plan:
   - Para Vigoentrena: Custom (necesitas varios módulos)
   
2. Seleccionar módulos iniciales:
   ✅ CRM
   ✅ Sales
   ✅ Accounting
   ✅ Calendar
   ✅ Appointment
   ✅ Point of Sale
   ✅ Website
   ✅ Email Marketing

3. Configurar datos empresa:
   - Nombre: Vigoentrena
   - NIF: [Tu NIF]
   - Dirección
   - Logo
   - Moneda: EUR
   - Idioma: Español

4. Instalar localización española:
   Apps > Buscar "Spain" > Instalar "Spain - Accounting"
```

#### 3. Primeros Pasos
```
1. Crear primer usuario:
   Settings > Users & Companies > Users > Create

2. Configurar calendario:
   Calendar > Configuration

3. Configurar productos:
   Sales > Products > Create
   - Sesión Individual 60 min
   - Bono 10 sesiones
   - etc.

4. Probar sistema
```

### ⚙️ Configuraciones Importantes

#### Localización España
```
Apps > Search "Spain" > Install:
├── Spain - Accounting (l10n_es)
├── Spain - Accounting Reports
└── Spain - Intrastat

Settings > Accounting > Fiscal Localization:
├── Fiscal Country: Spain
├── Chart of Accounts: Spanish PGC
└── Tax Configuration: IVA 21%
```

#### Email Saliente
```
Settings > Technical > Email > Outgoing Mail Servers

Configurar SMTP:
├── Gmail (recomendado):
│   ├── SMTP: smtp.gmail.com
│   ├── Port: 587
│   ├── Security: TLS
│   ├── Username: tucorreo@gmail.com
│   └── Password: [App Password, no contraseña normal]
│
└── Propio dominio:
    ├── SMTP: mail.tudominio.com
    ├── Port: 587
    ├── Security: TLS
    └── Credenciales de tu hosting
```

#### Zona Horaria
```
Settings > General Settings > System:
└── Timezone: Europe/Madrid

Users > [Tu usuario] > Preferences:
└── Timezone: Europe/Madrid
```

### 🔒 Seguridad
```
Settings > Users & Companies:

1. Activar 2FA (Two-Factor Authentication):
   - Para usuarios admin obligatorio
   - Settings > Users > Edit > Two-Factor Authentication

2. Política de contraseñas:
   - Mínimo 8 caracteres
   - Al menos 1 mayúscula, 1 número, 1 símbolo
   
3. Revisar permisos:
   - No dar accesos "Administration" a todos
   - Crear grupos específicos por rol
```

### 📈 Monitoreo
```
Odoo Online incluye:
├── Dashboard de uso
├── Logs de acceso
├── Alertas de seguridad
└── Reportes de rendimiento

Acceso: Settings > Dashboard (solo admin)
```

---

## 🛠️ Opción 2: Odoo.sh - DESARROLLO + PRODUCCIÓN

### ¿Qué es?
Plataforma cloud de Odoo con Git integrado. Ideal para desarrollo con múltiples entornos.

### ✅ Ventajas
- Control total sobre código
- Git integrado (branches, commits, push)
- Entornos: Development, Staging, Production
- Módulos custom sin restricciones
- Base de datos replicable
- Shell access
- Logs en tiempo real

### ❌ Desventajas
- Más caro (~200-400€/mes)
- Requiere conocimientos Git/Linux
- Más responsabilidad de mantenimiento

### 💰 Coste
```
Development: ~200€/mes
  └── Para desarrollo y testing

Production: ~400€/mes
  └── Para producción en vivo
  
Workers adicionales: +€/mes
```

### 📝 Instalación Paso a Paso

#### 1. Crear Proyecto Odoo.sh
```
1. Ir a: https://www.odoo.sh
2. Sign up con cuenta Odoo
3. Click "Create Project"
4. Completar:
   - Project Name: vigoentrena
   - Odoo Version: 17.0
   - Region: Europe (Frankfurt o Ireland)
5. Elegir plan: Development o Production
```

#### 2. Configurar Git
```bash
# En tu máquina local:

# 1. Instalar Git (si no lo tienes)
sudo apt install git  # Linux
brew install git      # macOS

# 2. Clonar repositorio del proyecto
git clone git@git.odoo.sh:vigoentrena.git
cd vigoentrena

# 3. Estructura inicial
vigoentrena/
├── .gitignore
├── odoo/              # Odoo core (submodule)
├── custom-addons/     # Tus módulos custom
└── odoo.conf          # Configuración
```

#### 3. Crear Módulo Custom
```bash
# En tu local:
cd vigoentrena/custom-addons

# Crear módulo vigoentrena_clinic
mkdir vigoentrena_clinic
cd vigoentrena_clinic

# Estructura módulo
vigoentrena_clinic/
├── __init__.py
├── __manifest__.py
├── models/
│   ├── __init__.py
│   └── patient.py
├── views/
│   └── patient_views.xml
├── security/
│   └── ir.model.access.csv
└── data/
```

**__manifest__.py**:
```python
{
    'name': 'Vigoentrena Clinic Management',
    'version': '17.0.1.0.0',
    'category': 'Healthcare',
    'summary': 'Gestión clínica para Vigoentrena',
    'author': 'Tu Nombre',
    'website': 'https://www.vigoentrena.com',
    'license': 'LGPL-3',
    'depends': [
        'base',
        'sale_management',
        'calendar',
        'contacts',
    ],
    'data': [
        'security/ir.model.access.csv',
        'views/patient_views.xml',
    ],
    'installable': True,
    'application': False,
    'auto_install': False,
}
```

#### 4. Commit y Push
```bash
# Añadir módulo al repo
git add custom-addons/vigoentrena_clinic/
git commit -m "Add vigoentrena_clinic module"
git push origin main

# Odoo.sh automáticamente:
# 1. Detecta el push
# 2. Crea/actualiza el build
# 3. Ejecuta tests
# 4. Despliega si todo OK
```

#### 5. Gestionar Branches
```bash
# Crear branch desarrollo
git checkout -b development
git push origin development

# Odoo.sh crea automáticamente:
# - Nueva base de datos para esta branch
# - URL: vigoentrena-development.odoo.sh

# Para producción:
git checkout main
git merge development
git push origin main

# Odoo.sh actualiza producción
```

#### 6. Acceder a Shell (SSH)
```bash
# Desde panel Odoo.sh:
# 1. Ir a tu proyecto
# 2. Click en branch (ej: production)
# 3. Tab "Shell"
# 4. Copiar comando SSH

ssh vigoentrena-production-12345@ssh.odoo.sh

# Dentro del shell:
# - Acceso a filesystem completo
# - Ejecutar comandos odoo-bin
# - Ver logs
# - Debugging
```

### ⚙️ Configuraciones Avanzadas

#### Variables de Entorno
```python
# En Odoo.sh panel > Settings > Environment Variables

# Ejemplo: API Key externa
WHATSAPP_API_KEY=tu_api_key_aqui

# Uso en código:
import os
api_key = os.environ.get('WHATSAPP_API_KEY')
```

#### Configurar Subdominios Custom
```
Odoo.sh panel > Settings > Domain Names:

Añadir:
├── vigoentrena.com → production
├── staging.vigoentrena.com → staging
└── dev.vigoentrena.com → development

Requiere configurar DNS:
CNAME vigoentrena.com → production.odoo.sh
```

#### Backups Automáticos
```
Odoo.sh incluye:
├── Backups diarios automáticos
├── Retención: 30 días
├── Descarga manual desde panel
└── Restauración 1-click

Manual:
Panel > Backups > Download Database
```

---

## 🐳 Opción 3: Docker - DESARROLLO LOCAL

### ¿Qué es?
Odoo en contenedores Docker. Ideal para desarrollo local sin ensuciar tu sistema.

### ✅ Ventajas
- Aislamiento total del sistema
- Setup rápido y replicable
- Fácil de destruir/recrear
- Múltiples versiones Odoo en paralelo
- No necesitas instalar PostgreSQL ni Python

### ❌ Desventajas
- Requiere conocimientos Docker básicos
- Rendimiento algo menor que instalación nativa
- Más recursos RAM/CPU

### 📝 Instalación Paso a Paso

#### 1. Instalar Docker

**Linux (Ubuntu/Debian)**:
```bash
# Actualizar sistema
sudo apt update
sudo apt upgrade -y

# Instalar Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Añadir usuario a grupo docker
sudo usermod -aG docker $USER
newgrp docker

# Verificar
docker --version
docker-compose --version
```

**macOS**:
```bash
# Descargar Docker Desktop desde:
https://www.docker.com/products/docker-desktop

# Instalar .dmg
# Abrir Docker Desktop
# Verificar en terminal:
docker --version
```

**Windows**:
```
1. Activar WSL2
2. Descargar Docker Desktop
3. Instalar
4. Verificar en PowerShell:
   docker --version
```

#### 2. Crear docker-compose.yml

```bash
# Crear directorio proyecto
mkdir vigoentrena-odoo
cd vigoentrena-odoo

# Crear estructura
mkdir -p addons config data

# Crear docker-compose.yml
```

**docker-compose.yml**:
```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: odoo
      POSTGRES_PASSWORD: odoo_password_seguro
    volumes:
      - ./data/postgresql:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    restart: unless-stopped

  odoo:
    image: odoo:17.0
    depends_on:
      - postgres
    ports:
      - "8069:8069"
      - "8072:8072"  # Longpolling (chat)
    volumes:
      - ./addons:/mnt/extra-addons
      - ./config:/etc/odoo
      - ./data/odoo:/var/lib/odoo
    environment:
      - HOST=postgres
      - USER=odoo
      - PASSWORD=odoo_password_seguro
    restart: unless-stopped
    command: -- --dev=reload
```

#### 3. Configuración Odoo

**config/odoo.conf**:
```ini
[options]
admin_passwd = admin_master_password_cambiar
db_host = postgres
db_port = 5432
db_user = odoo
db_password = odoo_password_seguro
addons_path = /mnt/extra-addons,/usr/lib/python3/dist-packages/odoo/addons
xmlrpc_port = 8069
longpolling_port = 8072

# Desarrollo
list_db = True
dev_mode = reload,xml

# Logs
log_level = info
logfile = False  # Logs a stdout (visible en docker logs)

# Performance
workers = 0  # 0 para desarrollo (single thread)
max_cron_threads = 1
```

#### 4. Arrancar Odoo

```bash
# Desde directorio vigoentrena-odoo/

# Primera vez (crea contenedores):
docker-compose up -d

# Ver logs:
docker-compose logs -f odoo

# Esperar mensaje:
# "odoo.modules.loading: Modules loaded."

# Acceder:
http://localhost:8069

# Crear base de datos:
# - Master Password: admin_master_password_cambiar
# - Database Name: vigoentrena
# - Email: admin@vigoentrena.com
# - Password: [tu password]
# - Language: Spanish
# - Country: Spain
# - Demo data: Sí (para pruebas) o No (producción)
```

#### 5. Desarrollar Módulos Custom

```bash
# Crear módulo en addons/
cd addons
mkdir vigoentrena_clinic

# Copiar estructura del ejemplo anterior

# Reiniciar Odoo para detectar nuevo módulo:
docker-compose restart odoo

# Instalar módulo:
# Apps > Update Apps List > Search "Vigoentrena" > Install
```

#### 6. Comandos Útiles

```bash
# Ver contenedores corriendo
docker-compose ps

# Parar Odoo
docker-compose stop

# Arrancar Odoo
docker-compose start

# Reiniciar Odoo
docker-compose restart odoo

# Ver logs en tiempo real
docker-compose logs -f odoo

# Acceder a shell Odoo
docker-compose exec odoo bash

# Acceder a PostgreSQL
docker-compose exec postgres psql -U odoo -d vigoentrena

# Limpiar todo (¡CUIDADO! Borra datos)
docker-compose down -v

# Backup base de datos
docker-compose exec postgres pg_dump -U odoo vigoentrena > backup.sql

# Restaurar base de datos
docker-compose exec -T postgres psql -U odoo -d vigoentrena < backup.sql
```

### ⚙️ Configuraciones Avanzadas Docker

#### Múltiples Versiones Odoo
```yaml
# docker-compose-v16.yml
services:
  odoo16:
    image: odoo:16.0
    ports:
      - "8069:8069"
    ...

# docker-compose-v17.yml
services:
  odoo17:
    image: odoo:17.0
    ports:
      - "8070:8069"
    ...

# Arrancar v16:
docker-compose -f docker-compose-v16.yml up -d

# Arrancar v17:
docker-compose -f docker-compose-v17.yml up -d
```

#### Desarrollo con Hot Reload
```yaml
# Ya incluido en docker-compose.yml:
command: -- --dev=reload,xml

# Esto recarga automáticamente:
# - reload: Código Python
# - xml: Vistas XML
```

---

## 💻 Opción 4: Instalación Linux (Ubuntu 22.04) - PRODUCCIÓN

### ¿Qué es?
Instalación desde código fuente en servidor Linux. Máximo control y rendimiento.

### ✅ Ventajas
- Rendimiento óptimo
- Control total del sistema
- Ideal para producción
- Sin costes de hosting (si tienes servidor)

### ❌ Desventajas
- Más complejo de instalar
- Responsabilidad total de mantenimiento
- Requiere conocimientos Linux avanzados
- Actualizaciones manuales

### 📝 Instalación Paso a Paso

#### 0. Requisitos Previos
```
Servidor Linux:
├── Ubuntu 22.04 LTS (recomendado) o Debian 11+
├── RAM: Mínimo 2GB, recomendado 4GB+
├── CPU: 2 cores+
├── Disco: 20GB+ libre
└── Acceso root o sudo
```

#### 1. Actualizar Sistema

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y git python3-pip python3-dev python3-venv \
    python3-wheel libpq-dev libxml2-dev libxslt1-dev libldap2-dev \
    libsasl2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev \
    libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev \
    libfribidi-dev libxcb1-dev libpq-dev wget curl node-less npm
```

#### 2. Instalar PostgreSQL

```bash
# Instalar PostgreSQL 14
sudo apt install -y postgresql postgresql-contrib

# Verificar instalación
sudo systemctl status postgresql

# Crear usuario Odoo
sudo su - postgres
createuser -s odoo
psql

# En psql:
ALTER USER odoo WITH PASSWORD 'password_seguro_aqui';
\q
exit
```

#### 3. Crear Usuario Sistema Odoo

```bash
sudo adduser --system --home=/opt/odoo --group odoo
```

#### 4. Instalar wkhtmltopdf (Para PDFs)

```bash
# Descargar versión con patched Qt
cd /tmp
wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.jammy_amd64.deb

# Instalar
sudo apt install -y ./wkhtmltox_0.12.6.1-3.jammy_amd64.deb

# Verificar
wkhtmltopdf --version
```

#### 5. Descargar Odoo 17

```bash
# Como usuario odoo
sudo su - odoo
cd /opt/odoo

# Clonar Odoo 17
git clone https://www.github.com/odoo/odoo --depth 1 --branch 17.0 --single-branch odoo17

# Crear directorio para módulos custom
mkdir /opt/odoo/custom-addons
```

#### 6. Instalar Dependencias Python

```bash
# Crear virtual environment
cd /opt/odoo/odoo17
python3 -m venv venv

# Activar venv
source venv/bin/activate

# Actualizar pip
pip install --upgrade pip

# Instalar dependencias Odoo
pip install -r requirements.txt

# Deactivar venv (temporal)
deactivate

# Volver a usuario normal
exit
```

#### 7. Configurar Odoo

```bash
# Crear archivo configuración
sudo nano /etc/odoo17.conf
```

**/etc/odoo17.conf**:
```ini
[options]
; This is the password that allows database operations:
admin_passwd = CAMBIAR_ESTE_PASSWORD_MASTER
db_host = localhost
db_port = 5432
db_user = odoo
db_password = password_seguro_aqui
addons_path = /opt/odoo/odoo17/addons,/opt/odoo/custom-addons
xmlrpc_port = 8069
longpolling_port = 8072

; Logs
logfile = /var/log/odoo17/odoo.log
log_level = info

; Performance (ajustar según recursos)
workers = 4
max_cron_threads = 2
limit_memory_hard = 2684354560
limit_memory_soft = 2147483648
limit_request = 8192
limit_time_cpu = 600
limit_time_real = 1200

; Security
list_db = False
db_filter = ^vigoentrena$
```

```bash
# Crear directorio logs
sudo mkdir /var/log/odoo17
sudo chown odoo:odoo /var/log/odoo17

# Permisos archivo conf
sudo chmod 640 /etc/odoo17.conf
sudo chown odoo:odoo /etc/odoo17.conf
```

#### 8. Crear Servicio Systemd

```bash
sudo nano /etc/systemd/system/odoo17.service
```

**/etc/systemd/system/odoo17.service**:
```ini
[Unit]
Description=Odoo 17
Documentation=https://www.odoo.com
After=network.target postgresql.service

[Service]
Type=simple
User=odoo
Group=odoo
ExecStart=/opt/odoo/odoo17/venv/bin/python3 /opt/odoo/odoo17/odoo-bin -c /etc/odoo17.conf
WorkingDirectory=/opt/odoo/odoo17
StandardOutput=journal+console
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

```bash
# Recargar systemd
sudo systemctl daemon-reload

# Habilitar inicio automático
sudo systemctl enable odoo17

# Iniciar Odoo
sudo systemctl start odoo17

# Verificar estado
sudo systemctl status odoo17

# Ver logs
sudo journalctl -u odoo17 -f
```

#### 9. Configurar Nginx (Reverse Proxy)

```bash
# Instalar Nginx
sudo apt install -y nginx

# Crear configuración
sudo nano /etc/nginx/sites-available/vigoentrena
```

**/etc/nginx/sites-available/vigoentrena**:
```nginx
upstream odoo {
    server 127.0.0.1:8069;
}

upstream odoo_longpolling {
    server 127.0.0.1:8072;
}

# Redirigir HTTP a HTTPS
server {
    listen 80;
    server_name vigoentrena.com www.vigoentrena.com;
    return 301 https://vigoentrena.com$request_uri;
}

# HTTPS
server {
    listen 443 ssl http2;
    server_name vigoentrena.com;

    # SSL (configurar después de obtener certificado)
    ssl_certificate /etc/ssl/certs/vigoentrena.crt;
    ssl_certificate_key /etc/ssl/private/vigoentrena.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Logging
    access_log /var/log/nginx/vigoentrena.access.log;
    error_log /var/log/nginx/vigoentrena.error.log;

    # Headers
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;

    # Timeouts
    proxy_connect_timeout 3600s;
    proxy_send_timeout 3600s;
    proxy_read_timeout 3600s;

    # Max upload size
    client_max_body_size 100M;

    # Gzip
    gzip on;
    gzip_types text/css text/less text/plain text/xml application/xml application/json application/javascript;

    # Longpolling (chat)
    location /longpolling {
        proxy_pass http://odoo_longpolling;
    }

    # Odoo
    location / {
        proxy_redirect off;
        proxy_pass http://odoo;
    }

    # Cache static files
    location ~* /web/static/ {
        proxy_cache_valid 200 60m;
        proxy_buffering on;
        expires 864000;
        proxy_pass http://odoo;
    }
}
```

```bash
# Activar sitio
sudo ln -s /etc/nginx/sites-available/vigoentrena /etc/nginx/sites-enabled/

# Desactivar sitio default
sudo rm /etc/nginx/sites-enabled/default

# Test configuración
sudo nginx -t

# Reiniciar Nginx
sudo systemctl restart nginx
```

#### 10. Obtener Certificado SSL (Let's Encrypt)

```bash
# Instalar Certbot
sudo apt install -y certbot python3-certbot-nginx

# Obtener certificado (modifica configuración Nginx automáticamente)
sudo certbot --nginx -d vigoentrena.com -d www.vigoentrena.com

# Seguir instrucciones (ingresar email, aceptar términos)

# Renovación automática (ya incluida)
sudo systemctl status certbot.timer

# Test renovación manual
sudo certbot renew --dry-run
```

#### 11. Configurar Firewall

```bash
# Instalar UFW (si no está)
sudo apt install -y ufw

# Configurar reglas
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https

# Activar
sudo ufw enable

# Verificar
sudo ufw status
```

#### 12. Crear Base de Datos

```bash
# Acceder a Odoo:
https://vigoentrena.com

# Crear base de datos:
# - Master Password: [el de odoo17.conf]
# - Database Name: vigoentrena
# - Email: admin@vigoentrena.com
# - Password: [password admin]
# - Language: Español
# - Country: España
# - Demo data: No

# IMPORTANTE: Después de crear, desactivar gestión DB:
# En /etc/odoo17.conf:
list_db = False

# Reiniciar Odoo:
sudo systemctl restart odoo17
```

### ⚙️ Mantenimiento Post-Instalación

#### Actualizar Odoo
```bash
# Como usuario odoo
sudo su - odoo
cd /opt/odoo/odoo17

# Backup primero!
# Ver doc backup-recuperacion.md

# Pull cambios
git pull origin 17.0

# Activar venv
source venv/bin/activate

# Actualizar dependencias (si hay cambios)
pip install --upgrade -r requirements.txt

# Deactivate
deactivate
exit

# Reiniciar servicio
sudo systemctl restart odoo17

# Actualizar módulos
# Acceder a Odoo > Apps > Update Apps List
# Buscar módulos a actualizar > Upgrade
```

#### Logs y Debugging
```bash
# Ver logs Odoo
sudo tail -f /var/log/odoo17/odoo.log

# Ver logs systemd
sudo journalctl -u odoo17 -f

# Ver logs Nginx
sudo tail -f /var/log/nginx/vigoentrena.access.log
sudo tail -f /var/log/nginx/vigoentrena.error.log

# Logs PostgreSQL
sudo tail -f /var/log/postgresql/postgresql-14-main.log
```

---

## 🔍 Verificación de Instalación

Independientemente del método elegido, verifica:

### Checklist Post-Instalación

- [ ] Odoo accesible en navegador
- [ ] Login funciona
- [ ] Crear base de datos funciona
- [ ] Módulos se instalan correctamente
- [ ] Localización española instalada
- [ ] Email saliente configurado
- [ ] Zona horaria correcta
- [ ] Usuarios adicionales se pueden crear
- [ ] Permisos funcionan
- [ ] Backup funciona (test)
- [ ] SSL configurado (si producción)
- [ ] Logs visibles y sin errores críticos

---

## 🆘 Troubleshooting

### Problema: No carga Odoo
```bash
# Verificar servicio
sudo systemctl status odoo17

# Ver logs
sudo journalctl -u odoo17 -n 50

# Verificar PostgreSQL
sudo systemctl status postgresql

# Test conectividad DB
psql -U odoo -h localhost -d postgres
```

### Problema: Error "Access Denied"
```
Causa: Password DB incorrecta

Solución:
1. Verificar password en /etc/odoo17.conf
2. Verificar password en PostgreSQL:
   sudo su - postgres
   psql
   ALTER USER odoo WITH PASSWORD 'nueva_password';
3. Actualizar odoo17.conf
4. Reiniciar: sudo systemctl restart odoo17
```

### Problema: Módulo no aparece
```
Causa: addons_path incorrecto

Solución:
1. Verificar ruta en /etc/odoo17.conf:
   addons_path = /opt/odoo/odoo17/addons,/opt/odoo/custom-addons

2. Verificar permisos:
   sudo chown -R odoo:odoo /opt/odoo/custom-addons

3. Reiniciar y actualizar lista:
   sudo systemctl restart odoo17
   Apps > Update Apps List
```

### Problema: Puerto 8069 ya en uso
```bash
# Ver qué usa el puerto
sudo lsof -i :8069

# Si es otro Odoo:
sudo systemctl stop odoo17

# Si es otro proceso:
sudo kill [PID]
```

---

## 📚 Recursos Adicionales

### Documentación Oficial
- [Odoo Install Docs](https://www.odoo.com/documentation/17.0/administration/install.html)
- [Odoo Deploy Docs](https://www.odoo.com/documentation/17.0/administration/deploy.html)

### Comunidad
- [Odoo Forum - Installation](https://www.odoo.com/forum/help-1/tag/install-89)
- [Stack Overflow - Odoo](https://stackoverflow.com/questions/tagged/odoo)

### Videos
- YouTube: "Odoo 17 Installation"
- Odoo eLearning: Cursos de implementación

---

## 🚀 Siguientes Pasos

Una vez instalado Odoo:

1. **Configurar servidor** (si Linux): Ver [Configuración Servidor](./configuracion-servidor.md)
2. **Entender arquitectura**: Ver [Arquitectura Sistema](./arquitectura-sistema.md)
3. **Configurar seguridad**: Ver [Seguridad y Permisos](./seguridad-permisos.md)
4. **Setup backups**: Ver [Backup y Recuperación](./backup-recuperacion.md)

---

**Fecha de creación**: 2025-01-XX  
**Versión**: 1.0  
**Autor**: Documentación Vigoentrena  
**Última actualización**: 2025-01-XX
