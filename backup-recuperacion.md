# Backup y Recuperación - Odoo 17

**Documento**: Backup y Recuperación  
**Versión**: 1.0  
**Fecha**: Octubre 2025  
**Autor**: Equipo Vigoentrena  
**Destinatario**: Personal técnico y administradores de sistema

---

## 📋 Índice

1. [Introducción](#introducción)
2. [Componentes a Respaldar](#componentes-a-respaldar)
3. [Estrategias de Backup](#estrategias-de-backup)
4. [Método 1: Backups en Odoo Online](#método-1-backups-en-odoo-online)
5. [Método 2: Backups en Odoo.sh](#método-2-backups-en-odoosh)
6. [Método 3: Backups Manuales (Instalación Propia)](#método-3-backups-manuales-instalación-propia)
7. [Backup Remoto y Almacenamiento en la Nube](#backup-remoto-y-almacenamiento-en-la-nube)
8. [Restauración de Backups](#restauración-de-backups)
9. [Plan de Recuperación ante Desastres (DRP)](#plan-de-recuperación-ante-desastres-drp)
10. [Pruebas de Restauración](#pruebas-de-restauración)
11. [Checklist y Mejores Prácticas](#checklist-y-mejores-prácticas)
12. [Troubleshooting](#troubleshooting)

---

## 1. Introducción

### 1.1. ¿Por qué son críticos los backups?

**Escenarios de pérdida de datos**:
- 🔥 Fallo hardware del servidor
- 👾 Ataque ransomware o malware
- ❌ Error humano (borrado accidental)
- 🔌 Corrupción de base de datos
- 🌍 Desastre natural (incendio, inundación)
- 🔒 Pérdida de acceso al proveedor SaaS

**Consecuencias sin backup**:
```
Sin backup adecuado:
❌ Pérdida de datos clientes
❌ Pérdida histórico facturas (problema legal)
❌ Pérdida registros contables
❌ Imposible recuperar negocio
❌ Multas por RGPD (no proteger datos)

Coste promedio downtime: €5,000 - €100,000/día
```

**Regla de oro backups**:
```
Regla 3-2-1:
✅ 3 copias de tus datos
✅ 2 medios diferentes (disco + nube)
✅ 1 copia offsite (fuera de oficina)
```

### 1.2. Objetivo de este Documento

Esta guía te enseñará a:
- ✅ Configurar backups automáticos en Odoo
- ✅ Realizar backups manuales
- ✅ Almacenar backups de forma segura
- ✅ Restaurar sistema completo desde backup
- ✅ Implementar plan de recuperación ante desastres

---

## 2. Componentes a Respaldar

### 2.1. Base de Datos PostgreSQL

**¿Qué contiene?**
- Todos los datos de Odoo (clientes, facturas, productos, etc.)
- Configuraciones de módulos
- Usuarios y permisos
- Logs de actividad

**Tamaño típico**:
```
Inicio (100 clientes): 50-200 MB
Pequeña empresa (500 clientes): 200 MB - 1 GB
Mediana empresa (5,000 clientes): 1-10 GB

Vigoentrena estimado (año 1): ~500 MB
```

**Formato backup**:
- `.sql` - SQL plano (grande, legible)
- `.sql.gz` - Comprimido (recomendado, 10x más pequeño)
- `custom` - Formato custom PostgreSQL (comprimido, rápido restaurar)

### 2.2. Filestore (Archivos Adjuntos)

**¿Qué contiene?**
- Documentos adjuntos (facturas PDF, consentimientos)
- Imágenes productos
- Fotos pacientes
- Archivos subidos por usuarios
- Logos, firmas digitales

**Ubicación**:
```
Odoo Online/Odoo.sh: Gestionado automáticamente
Instalación manual:
  - /opt/odoo/.local/share/Odoo/filestore/NOMBRE_BD/
```

**Tamaño típico**:
```
Inicio: 100 MB - 500 MB
Con fotos evolución pacientes: 1-5 GB/año

Vigoentrena estimado (año 1): ~2 GB
```

**Formato backup**:
- `.tar.gz` - Archivo comprimido
- `.zip` - Archivo comprimido (compatible Windows)

### 2.3. Configuración Odoo

**¿Qué contiene?**
- Archivo `odoo.conf` (solo instalación manual)
- Módulos custom (`/addons/`)
- Configuraciones servidor

**Tamaño**: Generalmente < 100 MB

### 2.4. Certificados y Claves

**⚠️ MUY IMPORTANTE**:
- Certificado digital empresa (VeriFactu)
- Certificados SSL (.pem, .crt, .key)
- Claves API (pasarelas pago, WhatsApp, etc.)

**Almacenar de forma segura y separada** (no solo en servidor).

### 2.5. Tamaño Total Backup

**Estimación Vigoentrena**:
```
Base de datos:     500 MB comprimida
Filestore:         2 GB
Config + custom:   50 MB
Certificados:      5 MB
─────────────────────────────
TOTAL:            ~2.5 GB

Con compresión: ~1.5-2 GB por backup completo
```

**Retención sugerida**:
```
Diarios: 7 días  → 7 × 2 GB = 14 GB
Semanales: 4 semanas → 4 × 2 GB = 8 GB
Mensuales: 12 meses → 12 × 2 GB = 24 GB
─────────────────────────────
TOTAL almacenamiento: ~50 GB
```

---

## 3. Estrategias de Backup

### 3.1. Tipos de Backup

#### A. Backup Completo (Full)
```
Ventajas:
✅ Restauración rápida (1 solo archivo)
✅ Simple de gestionar
✅ Independiente de otros backups

Desventajas:
❌ Ocupa más espacio
❌ Tarda más tiempo en crear

Uso: Al menos 1 vez por semana
```

#### B. Backup Incremental
```
Ventajas:
✅ Rápido de crear
✅ Ocupa poco espacio
✅ Solo cambios desde último backup

Desventajas:
❌ Restauración más lenta (necesita todos incrementales + full)
❌ Más complejo gestionar

Uso: Diario (entre backups full)
```

#### C. Backup Diferencial
```
Ventajas:
✅ Compromiso entre full e incremental
✅ Restauración más rápida que incremental

Desventajas:
❌ Ocupa más espacio que incremental

Uso: Opcional, si tienes mucho cambio diario
```

### 3.2. Frecuencia de Backups

**Recomendación Vigoentrena**:

```
┌─────────────────────────────────────────┐
│ BACKUP DIARIO (Automático)             │
├─────────────────────────────────────────┤
│ Hora: 03:00 AM (fuera horario)         │
│ Tipo: Incremental o Full               │
│ Retención: 7 días                       │
│ Destino: Disco local + Cloud           │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ BACKUP SEMANAL (Automático)            │
├─────────────────────────────────────────┤
│ Día: Domingo 02:00 AM                   │
│ Tipo: Full                              │
│ Retención: 4 semanas                    │
│ Destino: Disco local + Cloud           │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ BACKUP MENSUAL (Automático)            │
├─────────────────────────────────────────┤
│ Día: Primer domingo del mes 01:00 AM   │
│ Tipo: Full                              │
│ Retención: 12 meses                     │
│ Destino: Cloud (almacenamiento largo)  │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ BACKUP PRE-ACTUALIZACIÓN (Manual)      │
├─────────────────────────────────────────┤
│ Cuándo: Antes de actualizar Odoo       │
│ Tipo: Full                              │
│ Retención: Hasta verificar update OK   │
│ Destino: Disco local + Cloud           │
└─────────────────────────────────────────┘
```

### 3.3. RPO y RTO

**RPO (Recovery Point Objective)**:
- ¿Cuántos datos puedes permitirte perder?
- Vigoentrena: **24 horas** (backup diario)
- Crítico (fintech, salud crítica): **1 hora** o menos

**RTO (Recovery Time Objective)**:
- ¿Cuánto tiempo puedes estar sin sistema?
- Vigoentrena: **4-8 horas** (aceptable 1 día laborable)
- Crítico: **1 hora** o menos

```
Ejemplo escenario desastre:

Servidor se rompe: Martes 10:00 AM

RPO = 24h → Último backup: Lunes 03:00 AM
  Datos perdidos: Martes 00:00 - 10:00 (10 horas)
  Aceptable ✅

RTO = 8h → Restaurar en nuevo servidor
  Sistema operativo: 14:00 PM
  Downtime total: 4 horas ✅
```

---

## 4. Método 1: Backups en Odoo Online

### 4.1. Backups Automáticos (Incluidos)

Odoo Online incluye backups automáticos:

```
Frecuencia: DIARIA
Hora: Automática (madrugada hora europea)
Retención: 
  - 7 backups diarios
  - 4 backups semanales
  - 3 backups mensuales
  
Almacenamiento: Infraestructura Odoo (redundante)
Coste: INCLUIDO en suscripción
```

**No necesitas configurar nada**, Odoo gestiona automáticamente.

### 4.2. Backup Manual On-Demand

Realizar backup manual cuando necesites:

#### Paso 1: Acceder a Backups

```
Ajustes → Base de datos → Backup

O directamente:
https://www.odoo.com/my/databases
```

#### Paso 2: Solicitar Backup

```
Seleccionar tu base de datos: vigoentrena

Botón: [ Backup ]

Opciones:
  ☑ Incluir filestore (archivos adjuntos)
  Formato: zip (recomendado)
  
Confirmar: [ Crear Backup ]
```

#### Paso 3: Descargar Backup

```
Esperar procesamiento: 2-15 minutos (según tamaño)

Cuando esté listo:
  Botón: [ Descargar ]
  
Archivo descargado:
  vigoentrena_2025-10-04_15-30.zip
  Tamaño: ~1-3 GB
```

#### Paso 4: Almacenar Backup

```
Recomendación:
1. Guardar en ordenador local
2. Subir a Google Drive / Dropbox
3. Guardar copia en disco externo (mensual)

NO dejar solo en Descargas del navegador
```

### 4.3. Cuándo Hacer Backup Manual

**Escenarios críticos**:
```
✅ Antes de cambios importantes:
   - Actualizar plan (Standard → Custom)
   - Instalar módulo nuevo importante
   - Cambiar configuración crítica
   - Importación masiva de datos

✅ Antes de limpieza de datos:
   - Borrar clientes duplicados
   - Limpiar facturas antiguas
   - Reorganizar productos

✅ Periódicamente (seguridad extra):
   - Mensual: Descargar y guardar externo
   - Antes de vacaciones (por si acaso)
```

### 4.4. Restaurar Backup en Odoo Online

**⚠️ ADVERTENCIA**: Restaurar sobrescribe TODO. Backup actual primero.

#### Opción A: Restaurar en la misma base de datos

```
Ajustes → Base de datos → Restore

Subir archivo: vigoentrena_2025-10-04.zip
Password maestro: tu_master_password

⚠️ ESTO SOBRESCRIBIRÁ todos los datos actuales

Confirmar: [ Restaurar ]

Esperar: 5-30 minutos
```

**Consecuencia**: Pierdes todo lo posterior al backup.

#### Opción B: Restaurar en nueva base de datos (RECOMENDADO)

```
1. Ir a: https://www.odoo.com/my/databases

2. Botón: [ + Nueva Base de Datos ]

3. Seleccionar: [ Restaurar desde backup ]

4. Subir archivo: vigoentrena_2025-10-04.zip

5. Nombre nueva BD: vigoentrena_restore_test

6. Confirmar

7. Probar restauración en nueva BD

8. Si todo OK:
   - Eliminar BD antigua
   - Renombrar nueva BD al nombre original
```

**Ventaja**: No pierdes datos actuales si algo sale mal.

### 4.5. Limitaciones Odoo Online

```
❌ No control sobre frecuencia backups automáticos
❌ No backups incrementales (solo full)
❌ No acceso directo a PostgreSQL dump
❌ Depende de Odoo para restaurar

✅ Pero: Muy confiable, redundante, simple
```

### 4.6. Exportar Datos Críticos (Seguridad Extra)

Además de backups, exportar datos críticos periódicamente:

#### Exportar clientes

```
Contactos → Seleccionar todos → Acción → Exportar

Formato: Excel (.xlsx)
Campos:
  - Nombre
  - Email
  - Teléfono
  - Dirección
  - CIF/DNI
  - Notas

Guardar: clientes_vigoentrena_2025-10-04.xlsx
```

#### Exportar facturas

```
Facturación → Facturas → Seleccionar todas → Exportar

Campos:
  - Número factura
  - Cliente
  - Fecha
  - Total
  - Estado
  - Referencia

Guardar: facturas_vigoentrena_2025-10-04.xlsx
```

#### Exportar productos/servicios

```
Ventas → Productos → Exportar

Guardar: productos_vigoentrena_2025-10-04.xlsx
```

**Ventaja**: Si Odoo falla totalmente, al menos tienes datos clave en Excel.

---

## 5. Método 2: Backups en Odoo.sh

### 5.1. Backups Automáticos Incluidos

Odoo.sh backups automáticos:

```
Por rama (production, staging, dev):

DIARIO:
  Hora: 03:00 AM CET
  Retención: 7 días
  Tipo: Full (BD + filestore)
  
SEMANAL (Domingo):
  Retención: 4 semanas
  
MENSUAL (Primer domingo):
  Retención: 3 meses
  
Pre-deploy:
  Automático antes de cada deploy
  Retención: 7 días
```

### 5.2. Acceder a Backups en Odoo.sh

#### Paso 1: Ir a proyecto

```
odoo.sh → Tu proyecto (vigoentrena)
```

#### Paso 2: Seleccionar rama

```
Seleccionar: production
(o staging, development)
```

#### Paso 3: Ver backups

```
Tab: Backups

Lista de backups:
┌────────────────────────────────────────────┐
│ 2025-10-04 03:00 AM  Daily    Download    │
│ 2025-10-03 03:00 AM  Daily    Download    │
│ 2025-10-02 03:00 AM  Daily    Download    │
│ ...                                        │
│ 2025-09-30 02:00 AM  Weekly   Download    │
│ ...                                        │
│ 2025-09-01 01:00 AM  Monthly  Download    │
└────────────────────────────────────────────┘
```

### 5.3. Crear Backup Manual On-Demand

```
Tab: Backups → Botón [ Create Backup ]

Razón (opcional): "Backup antes de actualizar módulo X"

Confirmar

Backup en proceso: 2-10 minutos

Disponible para descargar cuando termine
```

### 5.4. Descargar Backup

```
Lista backups → Seleccionar backup → [ Download ]

Archivo descargado:
  production_vigoentrena_2025-10-04_030000.zip
  
Contenido:
  - dump.sql (base de datos)
  - filestore/ (archivos adjuntos)
  - manifest.json (metadatos)
```

### 5.5. Restaurar Backup en Odoo.sh

#### Opción A: Restaurar en misma rama

```
⚠️ PELIGROSO: Sobrescribe BD actual

Tab: Backups → Seleccionar backup → [ Restore ]

Confirmar: "Sí, sobrescribir BD actual"

Proceso:
1. Odoo.sh detiene rama
2. Restaura BD desde backup
3. Restaura filestore
4. Reinicia rama

Tiempo: 5-15 minutos

Downtime: SÍ (rama no disponible durante restauración)
```

#### Opción B: Restaurar en rama nueva (RECOMENDADO)

```
1. Crear rama nueva:
   git checkout -b restore-test-2025-10-04
   git push origin restore-test-2025-10-04

2. Odoo.sh crea BD para rama nueva automáticamente

3. En Odoo.sh:
   Rama: restore-test-2025-10-04
   Tab: Backups
   Botón: [ Import Database ]
   
4. Seleccionar backup:
   Origen: production
   Backup: 2025-10-04 03:00 AM
   
5. Confirmar importación

6. Probar en:
   restore-test-2025-10-04.vigoentrena.odoo.sh

7. Si todo OK, decidir:
   - Mergear a production
   - O eliminar rama test
```

### 5.6. Backup con Script Personalizado

Para backups adicionales a almacenamiento propio:

#### Script Python para descargar backups Odoo.sh

```python
#!/usr/bin/env python3
"""
Script para descargar backups de Odoo.sh vía API
"""

import requests
import os
from datetime import datetime

# Configuración
ODOO_SH_TOKEN = "tu_token_api_odoo_sh"
PROJECT_ID = "vigoentrena"
BRANCH = "production"
BACKUP_DIR = "/backups/odoo-sh"

# Headers autenticación
headers = {
    "Authorization": f"Bearer {ODOO_SH_TOKEN}",
    "Content-Type": "application/json"
}

# Listar backups
url = f"https://api.odoo.sh/v1/projects/{PROJECT_ID}/branches/{BRANCH}/backups"
response = requests.get(url, headers=headers)

if response.status_code == 200:
    backups = response.json()
    
    # Descargar último backup
    last_backup = backups[0]
    backup_id = last_backup['id']
    
    # Descargar
    download_url = f"{url}/{backup_id}/download"
    backup_response = requests.get(download_url, headers=headers, stream=True)
    
    # Guardar archivo
    filename = f"{PROJECT_ID}_{BRANCH}_{datetime.now().strftime('%Y%m%d')}.zip"
    filepath = os.path.join(BACKUP_DIR, filename)
    
    with open(filepath, 'wb') as f:
        for chunk in backup_response.iter_content(chunk_size=8192):
            f.write(chunk)
    
    print(f"Backup descargado: {filepath}")
else:
    print(f"Error: {response.status_code} - {response.text}")
```

**Obtener token API Odoo.sh**:
```
Odoo.sh → Settings → API Tokens
Generar nuevo token
Copiar y guardar seguro (no se vuelve a mostrar)
```

**Usar script**:
```bash
# Instalar dependencias
pip3 install requests

# Configurar
nano download_backup.py
# Pegar script, configurar variables

# Ejecutar
python3 download_backup.py

# Automatizar con cron
crontab -e

# Añadir (diario 04:00 AM)
0 4 * * * /usr/bin/python3 /opt/scripts/download_backup.py >> /var/log/backup_download.log 2>&1
```

---

## 6. Método 3: Backups Manuales (Instalación Propia)

### 6.1. Script de Backup Completo

**Ubicación**: `/opt/odoo/backup.sh`

```bash
#!/bin/bash

##############################################
# Script Backup Completo Odoo 17
# Vigoentrena
##############################################

# ===== CONFIGURACIÓN =====
DB_NAME="vigoentrena_prod"              # Nombre base de datos
DB_USER="odoo"                          # Usuario PostgreSQL
ODOO_HOME="/opt/odoo"                   # Home Odoo
FILESTORE_PATH="$ODOO_HOME/.local/share/Odoo/filestore/$DB_NAME"
BACKUP_DIR="$ODOO_HOME/backups"         # Directorio backups
RETENTION_DAYS=7                        # Días retener backups
TIMESTAMP=$(date +%Y%m%d_%H%M%S)        # Timestamp

# Backup semanal y mensual
DAY_OF_WEEK=$(date +%u)                 # 1=Lunes, 7=Domingo
DAY_OF_MONTH=$(date +%d)                # Día del mes

# ===== CREAR DIRECTORIOS =====
mkdir -p "$BACKUP_DIR/daily"
mkdir -p "$BACKUP_DIR/weekly"
mkdir -p "$BACKUP_DIR/monthly"

# ===== LOG =====
LOG_FILE="/var/log/odoo/backup.log"
exec > >(tee -a "$LOG_FILE") 2>&1

echo "======================================"
echo "Backup Odoo - $(date)"
echo "======================================"

# ===== BACKUP BASE DE DATOS =====
echo "[1/4] Backup base de datos..."

DB_BACKUP_FILE="$BACKUP_DIR/daily/db_${DB_NAME}_${TIMESTAMP}.sql.gz"

sudo -u postgres pg_dump "$DB_NAME" | gzip > "$DB_BACKUP_FILE"

if [ $? -eq 0 ]; then
    echo "✅ BD respaldada: $DB_BACKUP_FILE"
    DB_SIZE=$(du -h "$DB_BACKUP_FILE" | cut -f1)
    echo "   Tamaño: $DB_SIZE"
else
    echo "❌ Error respaldando BD"
    exit 1
fi

# ===== BACKUP FILESTORE =====
echo "[2/4] Backup filestore..."

FS_BACKUP_FILE="$BACKUP_DIR/daily/filestore_${DB_NAME}_${TIMESTAMP}.tar.gz"

if [ -d "$FILESTORE_PATH" ]; then
    tar -czf "$FS_BACKUP_FILE" -C "$(dirname "$FILESTORE_PATH")" "$(basename "$FILESTORE_PATH")"
    
    if [ $? -eq 0 ]; then
        echo "✅ Filestore respaldado: $FS_BACKUP_FILE"
        FS_SIZE=$(du -h "$FS_BACKUP_FILE" | cut -f1)
        echo "   Tamaño: $FS_SIZE"
    else
        echo "❌ Error respaldando filestore"
        exit 1
    fi
else
    echo "⚠️  Filestore no existe: $FILESTORE_PATH"
fi

# ===== BACKUP CONFIGURACIÓN =====
echo "[3/4] Backup configuración..."

CONFIG_BACKUP_FILE="$BACKUP_DIR/daily/config_${TIMESTAMP}.tar.gz"

tar -czf "$CONFIG_BACKUP_FILE" \
    /etc/odoo/odoo.conf \
    "$ODOO_HOME/custom-addons" \
    2>/dev/null

if [ $? -eq 0 ]; then
    echo "✅ Configuración respaldada: $CONFIG_BACKUP_FILE"
else
    echo "⚠️  Advertencia al respaldar configuración"
fi

# ===== COPIAS SEMANALES Y MENSUALES =====
echo "[4/4] Copias semanales/mensuales..."

# Semanal (Domingo)
if [ "$DAY_OF_WEEK" -eq 7 ]; then
    echo "📅 Creando backup semanal..."
    cp "$DB_BACKUP_FILE" "$BACKUP_DIR/weekly/db_${DB_NAME}_weekly_${TIMESTAMP}.sql.gz"
    cp "$FS_BACKUP_FILE" "$BACKUP_DIR/weekly/filestore_${DB_NAME}_weekly_${TIMESTAMP}.tar.gz"
fi

# Mensual (Primer domingo del mes)
if [ "$DAY_OF_WEEK" -eq 7 ] && [ "$DAY_OF_MONTH" -le 7 ]; then
    echo "📆 Creando backup mensual..."
    cp "$DB_BACKUP_FILE" "$BACKUP_DIR/monthly/db_${DB_NAME}_monthly_${TIMESTAMP}.sql.gz"
    cp "$FS_BACKUP_FILE" "$BACKUP_DIR/monthly/filestore_${DB_NAME}_monthly_${TIMESTAMP}.tar.gz"
fi

# ===== LIMPIEZA BACKUPS ANTIGUOS =====
echo "🧹 Limpiando backups antiguos..."

# Diarios: retener solo últimos 7 días
find "$BACKUP_DIR/daily" -type f -mtime +$RETENTION_DAYS -delete

# Semanales: retener solo últimas 4 semanas
find "$BACKUP_DIR/weekly" -type f -mtime +28 -delete

# Mensuales: retener solo últimos 12 meses
find "$BACKUP_DIR/monthly" -type f -mtime +365 -delete

# ===== VERIFICACIÓN INTEGRIDAD =====
echo "🔍 Verificando integridad backup..."

# Test gunzip
gunzip -t "$DB_BACKUP_FILE" 2>/dev/null

if [ $? -eq 0 ]; then
    echo "✅ Integridad BD OK"
else
    echo "❌ Error integridad BD"
    exit 1
fi

# Test tar
tar -tzf "$FS_BACKUP_FILE" > /dev/null 2>&1

if [ $? -eq 0 ]; then
    echo "✅ Integridad filestore OK"
else
    echo "❌ Error integridad filestore"
    exit 1
fi

# ===== RESUMEN =====
echo "======================================"
echo "✅ Backup completado exitosamente"
echo "======================================"
echo "Archivos creados:"
echo "  - BD: $DB_BACKUP_FILE"
echo "  - Filestore: $FS_BACKUP_FILE"
echo "  - Config: $CONFIG_BACKUP_FILE"
echo ""
echo "Espacio usado backups:"
du -sh "$BACKUP_DIR"/*
echo "======================================"

# ===== NOTIFICAR (opcional) =====
# Enviar email notificación
# echo "Backup Odoo completado" | mail -s "✅ Backup Odoo OK - $(date +%Y-%m-%d)" admin@vigoentrena.com

exit 0
```

### 6.2. Configurar Script

```bash
# Crear archivo
nano /opt/odoo/backup.sh

# Pegar contenido script

# Permisos ejecución
chmod +x /opt/odoo/backup.sh

# Permisos usuario odoo
chown odoo:odoo /opt/odoo/backup.sh

# Crear directorio backups
mkdir -p /opt/odoo/backups
chown odoo:odoo /opt/odoo/backups
```

### 6.3. Automatizar con Cron

```bash
# Editar crontab del usuario odoo
sudo -u odoo crontab -e

# Añadir líneas:

# Backup diario 03:00 AM
0 3 * * * /opt/odoo/backup.sh

# Opcional: Limpiar logs antiguos (cada mes)
0 0 1 * * find /var/log/odoo -name "*.log" -mtime +30 -delete
```

**Verificar cron**:
```bash
# Ver crontab actual
sudo -u odoo crontab -l

# Ver logs cron
grep CRON /var/log/syslog

# Probar script manualmente
sudo -u odoo /opt/odoo/backup.sh
```

### 6.4. Notificaciones Email

Modificar script para enviar email al completar:

```bash
# Instalar mailutils
apt install mailutils -y

# Configurar servidor SMTP
# (usar Gmail, servidor SMTP propio, etc.)

# Añadir al final del script backup.sh:

# Email notificación
EMAIL="admin@vigoentrena.com"

if [ $? -eq 0 ]; then
    echo "Backup Odoo completado exitosamente - $(date)" | \
    mail -s "✅ Backup Odoo OK - $(date +%Y-%m-%d)" "$EMAIL"
else
    echo "Backup Odoo FALLÓ - $(date)" | \
    mail -s "❌ Backup Odoo ERROR - $(date +%Y-%m-%d)" "$EMAIL"
fi
```

---

## 7. Backup Remoto y Almacenamiento en la Nube

### 7.1. ¿Por qué Backup Remoto?

```
Escenario: Incendio en oficina 🔥

Backup solo en servidor local → TODO perdido ❌

Backup también en cloud → Datos seguros ✅
```

**Regla 3-2-1**:
```
3 copias:
  - Original (servidor producción)
  - Backup local (disco servidor)
  - Backup remoto (cloud)

2 medios:
  - Disco SSD servidor
  - Cloud (Google Drive, AWS S3, etc.)

1 offsite:
  - Cloud (fuera de oficina física)
```

### 7.2. Opciones de Almacenamiento Cloud

| Proveedor | Coste | Capacidad | Ventajas |
|-----------|-------|-----------|----------|
| **Google Drive** | €1.99/mes | 100 GB | Fácil, interfaz familiar |
| **Dropbox** | €9.99/mes | 2 TB | Sincronización rápida |
| **AWS S3** | ~€2/mes | 100 GB | Profesional, escalable |
| **Backblaze B2** | ~€0.50/mes | 100 GB | Muy económico |
| **OVH Object Storage** | ~€1/mes | 100 GB | Europeo, RGPD |

**Recomendación Vigoentrena**: 
- **Google Drive** (inicio, simple)
- **AWS S3** (profesional, largo plazo)

### 7.3. Configurar Rclone (Universal)

**Rclone** = rsync para cloud. Soporta 40+ proveedores.

#### Instalación

```bash
# Instalar rclone
curl https://rclone.org/install.sh | sudo bash

# Verificar
rclone version
```

#### Configuración Google Drive

```bash
# Iniciar configuración interactiva
rclone config

# Crear nuevo remote
n) New remote
name> gdrive

# Elegir tipo
Storage> drive  (o número de Google Drive en lista)

# Client ID y Secret (dejar vacío para usar de rclone)
client_id> (Enter - vacío)
client_secret> (Enter - vacío)

# Scope (acceso completo)
scope> 1  (Full access)

# Root folder ID (vacío = raíz)
root_folder_id> (Enter - vacío)

# Service Account (No)
service_account_file> (Enter - vacío)

# Configuración avanzada (No)
Edit advanced config> n

# Auto config (Sí si tienes navegador)
Use auto config> y

# Se abrirá navegador → Login Google → Autorizar rclone

# Compartir Drive con equipo (opcional)
Configure this as a Shared Drive> n

# Confirmar configuración
y) Yes this is OK

# Salir
q) Quit config
```

#### Configuración AWS S3

```bash
rclone config

n) New remote
name> s3backup

Storage> s3

Provider> AWS

Access Key ID> tu_aws_access_key
Secret Access Key> tu_aws_secret_key

Region> eu-west-1  (Irlanda, RGPD compliant)

Endpoint> (Enter - vacío, usa default)

Location constraint> eu-west-1

ACL> private

# Resto: Enter (defaults)

y) Yes this is OK
q) Quit
```

### 7.4. Script Backup Remoto

Modificar script backup para subir a cloud:

```bash
# Añadir al final de /opt/odoo/backup.sh

# ===== BACKUP REMOTO =====
echo "☁️  Subiendo a cloud..."

# Google Drive
rclone copy "$BACKUP_DIR/daily" gdrive:vigoentrena-backups/daily \
    --log-file=/var/log/odoo/rclone.log \
    --log-level INFO

if [ "$DAY_OF_WEEK" -eq 7 ]; then
    # Semanales solo domingo
    rclone copy "$BACKUP_DIR/weekly" gdrive:vigoentrena-backups/weekly \
        --log-file=/var/log/odoo/rclone.log
fi

if [ "$DAY_OF_WEEK" -eq 7 ] && [ "$DAY_OF_MONTH" -le 7 ]; then
    # Mensuales primer domingo
    rclone copy "$BACKUP_DIR/monthly" gdrive:vigoentrena-backups/monthly \
        --log-file=/var/log/odoo/rclone.log
fi

echo "✅ Backup remoto completado"

# Verificar espacio usado en cloud
rclone size gdrive:vigoentrena-backups
```

### 7.5. Encriptar Backups (Opcional, Recomendado)

Para backups con datos sensibles:

#### Encriptar con GPG

```bash
# Generar clave GPG (una vez)
gpg --full-generate-key

# Elegir:
#   Tipo: RSA and RSA
#   Tamaño: 4096 bits
#   Validez: 0 (no expira)
#   Nombre: Vigoentrena Backup
#   Email: backup@vigoentrena.com

# Modificar script backup para encriptar
# Añadir después de crear backup BD:

echo "🔐 Encriptando backup..."

# Encriptar BD
gpg --encrypt --recipient backup@vigoentrena.com \
    "$DB_BACKUP_FILE"

# Ahora tenemos vigoentrena_prod_20251004.sql.gz.gpg

# Subir versión encriptada a cloud
rclone copy "$DB_BACKUP_FILE.gpg" gdrive:vigoentrena-backups/encrypted/
```

#### Desencriptar cuando sea necesario

```bash
# Descargar desde cloud
rclone copy gdrive:vigoentrena-backups/encrypted/db_vigoentrena_20251004.sql.gz.gpg ./

# Desencriptar
gpg --decrypt db_vigoentrena_20251004.sql.gz.gpg > db_vigoentrena_20251004.sql.gz

# Ahora puedes restaurar como normal
```

### 7.6. Monitoreo Backups Cloud

#### Ver backups en Google Drive

```bash
# Listar backups
rclone ls gdrive:vigoentrena-backups

# Espacio usado
rclone size gdrive:vigoentrena-backups

# Verificar último backup
rclone lsl gdrive:vigoentrena-backups/daily | tail -1
```

#### Sincronizar bidireccional (NO recomendado para backups)

```bash
# Solo COPY (unidireccional), nunca SYNC para backups
# SYNC puede borrar archivos si fuente está vacía accidentalmente

# ✅ Correcto
rclone copy /source /dest

# ❌ Peligroso para backups
rclone sync /source /dest  # Puede borrar todo en dest si source vacío
```

---

## 8. Restauración de Backups

### 8.1. Restaurar Base de Datos PostgreSQL

#### Desde archivo .sql.gz

```bash
# 1. Detener Odoo
systemctl stop odoo

# 2. (Opcional) Backup preventivo BD actual
sudo -u postgres pg_dump vigoentrena_prod | gzip > vigoentrena_current_backup.sql.gz

# 3. Borrar BD actual (⚠️ PELIGRO)
sudo -u postgres dropdb vigoentrena_prod

# 4. Crear BD nueva vacía
sudo -u postgres createdb -O odoo vigoentrena_prod

# 5. Restaurar desde backup
gunzip < /opt/odoo/backups/daily/db_vigoentrena_prod_20251004_030000.sql.gz | \
    sudo -u postgres psql vigoentrena_prod

# 6. Verificar restauración
sudo -u postgres psql vigoentrena_prod -c "SELECT COUNT(*) FROM res_partner;"

# 7. Iniciar Odoo
systemctl start odoo

# 8. Verificar en web
# Abrir https://app.vigoentrena.com
# Login y comprobar datos
```

### 8.2. Restaurar Filestore

```bash
# 1. Detener Odoo
systemctl stop odoo

# 2. Backup filestore actual (por si acaso)
mv /opt/odoo/.local/share/Odoo/filestore/vigoentrena_prod \
   /opt/odoo/.local/share/Odoo/filestore/vigoentrena_prod.old

# 3. Extraer backup filestore
tar -xzf /opt/odoo/backups/daily/filestore_vigoentrena_prod_20251004_030000.tar.gz \
    -C /opt/odoo/.local/share/Odoo/filestore/

# 4. Permisos
chown -R odoo:odoo /opt/odoo/.local/share/Odoo/filestore/vigoentrena_prod

# 5. Iniciar Odoo
systemctl start odoo

# 6. Verificar
# Abrir Odoo → Abrir factura con PDF adjunto
# Verificar que se descarga correctamente
```

### 8.3. Restaurar Sistema Completo (Desastre Total)

**Escenario**: Servidor muerto, necesitas reconstruir todo en servidor nuevo.

#### Paso 1: Preparar Nuevo Servidor

```bash
# Seguir guía instalación:
# docs/01-guia-tecnica/instalacion-odoo17.md

# Hasta el punto de tener:
# - Ubuntu instalado
# - PostgreSQL instalado
# - Odoo instalado (pero sin BD)
# - Nginx configurado
# - Firewall configurado
```

#### Paso 2: Descargar Backups desde Cloud

```bash
# Instalar rclone en nuevo servidor
curl https://rclone.org/install.sh | sudo bash

# Configurar gdrive (ver sección 7.3)
rclone config

# Descargar último backup
mkdir -p /opt/odoo/restore
cd /opt/odoo/restore

# Descargar BD
rclone copy gdrive:vigoentrena-backups/daily \
    ./ \
    --include "db_vigoentrena_prod_*.sql.gz" \
    --max-age 2d

# Descargar filestore
rclone copy gdrive:vigoentrena-backups/daily \
    ./ \
    --include "filestore_vigoentrena_prod_*.tar.gz" \
    --max-age 2d

# Listar archivos descargados
ls -lh
```

#### Paso 3: Restaurar

```bash
# Restaurar BD
gunzip < db_vigoentrena_prod_XXXXXX.sql.gz | \
    sudo -u postgres psql -d vigoentrena_prod

# Restaurar filestore
tar -xzf filestore_vigoentrena_prod_XXXXXX.tar.gz \
    -C /opt/odoo/.local/share/Odoo/filestore/

# Permisos
chown -R odoo:odoo /opt/odoo/.local/share/Odoo/filestore/

# Iniciar Odoo
systemctl start odoo
```

#### Paso 4: Configurar DNS

```bash
# Cambiar DNS del dominio app.vigoentrena.com
# para apuntar al nuevo servidor IP

# Esperar propagación DNS (5-30 minutos)

# Verificar
nslookup app.vigoentrena.com
# Debe mostrar nueva IP
```

#### Paso 5: Configurar SSL

```bash
# Obtener certificado SSL nuevo servidor
certbot --nginx -d app.vigoentrena.com
```

#### Paso 6: Verificación Final

```bash
# Checklist:
☐ Odoo accesible via HTTPS
☐ Login funciona
☐ Datos clientes presentes
☐ Facturas completas
☐ Archivos adjuntos descargan
☐ Email saliente funciona
☐ TPV funciona (si aplica)
☐ Backups automáticos reconfigurados
```

**Tiempo estimado recuperación total**: 4-8 horas (según experiencia).

---

## 9. Plan de Recuperación ante Desastres (DRP)

### 9.1. Definir Escenarios

| Escenario | Probabilidad | Impacto | RPO | RTO |
|-----------|--------------|---------|-----|-----|
| Fallo disco servidor | Media | Alto | 24h | 4h |
| Servidor comprometido (ransomware) | Baja | Crítico | 24h | 8h |
| Datacenter caído | Muy baja | Crítico | 24h | 12h |
| Error humano (borrado datos) | Media | Medio | 24h | 2h |
| Desastre natural | Muy baja | Crítico | 24h | 24h |

### 9.2. Procedimientos por Escenario

#### Escenario 1: Fallo Disco

```
1. Detectar fallo:
   - Monitoreo alerta
   - Odoo no responde
   - SSH no conecta

2. Diagnosticar:
   - ¿Disco físicamente muerto?
   - ¿Posible recuperar datos?

3. Acción inmediata:
   a) Si disco recuperable:
      - Arrancar en modo recovery
      - Copiar datos críticos
   
   b) Si disco muerto:
      - Provisionar servidor nuevo
      - Restaurar desde backup cloud
      
4. Comunicación:
   - Email clientes: "Mantenimiento temporal, volvemos en X horas"
   - WhatsApp equipo: Situación y tiempos

5. Post-incidente:
   - Revisar causa fallo
   - Reforzar monitoreo discos (SMART)
```

#### Escenario 2: Ransomware

```
🚨 CRÍTICO: NO pagar rescate

1. Aislar inmediatamente:
   - Desconectar servidor de red
   - Detener propagación

2. Evaluar daño:
   - ¿BD encriptada?
   - ¿Backups también afectados?

3. Restaurar desde backup limpio:
   - Servidor nuevo desde cero
   - Restaurar backup ANTERIOR a infección
   - NUNCA restaurar backup infectado

4. Análisis forense:
   - ¿Cómo entraron?
   - ¿Qué vulnerabilidad explotaron?

5. Reforzar seguridad:
   - Cambiar todas las contraseñas
   - Actualizar sistema
   - Instalar fail2ban
   - Revisar puertos abiertos

6. Reportar:
   - Policía (denuncia)
   - AEPD (si datos personales afectados)
```

#### Escenario 3: Error Humano

```
Ejemplo: Usuario borra 50 clientes por accidente

1. STOP:
   - NO tocar nada más
   - No seguir usando sistema

2. Determinar alcance:
   - ¿Qué se borró exactamente?
   - ¿Cuándo sucedió?

3. Restaurar desde backup:
   Opción A: Restaurar solo datos borrados
   - Exportar datos actuales (no borrados)
   - Restaurar BD desde backup anterior a borrado
   - Re-importar datos actuales
   - Resultado: Datos borrados + datos nuevos
   
   Opción B: Si simple
   - Recuperar solo registros borrados de backup
   - Importar vía CSV

4. Prevención futura:
   - Permisos: Solo admin puede borrar
   - Confirmación doble al borrar masivo
   - Capacitar equipo
```

### 9.3. Checklist Pre-Desastre

```
☐ Backups funcionando y verificados mensualmente
☐ Backups remotos en al menos 2 ubicaciones
☐ Procedimientos documentados y actualizados
☐ Contactos de emergencia (hosting, partner Odoo, etc.)
☐ Credenciales de emergencia guardadas seguro
☐ Acceso a backups desde múltiples cuentas
☐ Servidor alternativo identificado (plan B)
☐ Equipo entrenado en procedimientos
☐ Tiempos RTO/RPO definidos y comunicados
☐ Póliza seguro (opcional, cubre pérdida datos)
```

### 9.4. Roles y Responsabilidades

```
DRP Lead: [Nombre responsable técnico]
  - Coordinar recuperación
  - Tomar decisiones técnicas
  - Comunicar con stakeholders

Técnico Backup: [Nombre]
  - Ejecutar restauración
  - Verificar integridad datos

Comunicación: [Nombre]
  - Avisar clientes
  - Actualizar estado
  - Redes sociales (si aplica)

Soporte Partner: [Nombre Partner Odoo]
  - Asistencia técnica especializada
  - Escalación si necesario

Contacto Hosting: [Nombre/Empresa]
  - Proveedor VPS/Cloud
  - Soporte infraestructura
```

### 9.5. Comunicación Durante Crisis

**Template Email Clientes**:

```
Asunto: Mantenimiento Temporal - Vigoentrena

Estimados clientes,

Estamos realizando un mantenimiento no programado en nuestros sistemas 
para resolver un incidente técnico.

Impacto:
- Reservas online: No disponible temporalmente
- Citas programadas: No afectadas, se mantienen
- Atención centro: Normal

Tiempo estimado resolución: [X horas]

Disculpen las molestias. Mantendremos informados.

Saludos,
Equipo Vigoentrena
```

**Template WhatsApp Equipo**:

```
🚨 ALERTA TÉCNICA 🚨

Sistema Odoo caído por [razón].

Acciones:
- Activado plan recuperación
- Estimado: [X horas]
- Mantener aten. clientes normal
- NO usar sistema hasta aviso

Updates cada hora.
```

---

## 10. Pruebas de Restauración

### 10.1. ¿Por qué Probar Restauraciones?

```
"Backup no probado = No backup"

Escenario real:
- Empresa tiene backups hace 2 años
- Servidor falla
- Intentan restaurar
- ❌ Backups corruptos, no sirven
- Pérdida total de datos
```

**Prueba trimestral obligatoria**.

### 10.2. Procedimiento Prueba Restauración

**Frecuencia**: Cada 3 meses (mínimo)

#### Paso 1: Planificar Prueba

```
Cuándo: Sábado o domingo (poco tráfico)
Duración: 2-4 horas
Equipo: Al menos 1 técnico
Entorno: Servidor pruebas (NO producción)
```

#### Paso 2: Seleccionar Backup

```
# Elegir backup reciente (menos de 7 días)
# Debería tener:
- BD completa
- Filestore completo
- Configuración

Backup elegido: 
  db_vigoentrena_prod_20251001_030000.sql.gz
  filestore_vigoentrena_prod_20251001_030000.tar.gz
```

#### Paso 3: Preparar Entorno Prueba

```bash
# Opción A: VPS temporal (€5-10 una vez)
# Contratar VPS en Hetzner/DigitalOcean
# Instalar Odoo siguiendo guía

# Opción B: Docker local
docker-compose down -v  # Limpiar
docker-compose up -d    # Recrear

# Opción C: Rama staging en Odoo.sh
# Restaurar backup en rama staging
```

#### Paso 4: Ejecutar Restauración

```bash
# Seguir procedimientos sección 8
# Restaurar BD
# Restaurar filestore
# Iniciar Odoo
# Verificar acceso
```

#### Paso 5: Verificar Datos

```
Checklist verificación:

☐ Login funciona (usuario admin + usuario normal)
☐ Datos clientes:
  - Abrir 5 clientes aleatorios
  - Verificar info completa
☐ Facturas:
  - Buscar facturas último mes
  - Abrir 3 facturas
  - Descargar PDF
  - Verificar números secuenciales
☐ Productos:
  - Listar todos productos
  - Verificar precios
☐ Citas:
  - Ver calendario última semana
  - Verificar asistencias
☐ Filestore:
  - Abrir 5 documentos adjuntos aleatorios
  - Verificar se descargan OK
☐ Configuración:
  - Verificar CIF empresa
  - Verificar plan contable
  - Verificar usuarios
☐ Módulos:
  - Verificar módulos instalados
  - Verificar VeriFactu configurado
```

#### Paso 6: Documentar Resultados

```
INFORME PRUEBA RESTAURACIÓN

Fecha: 2025-10-04
Responsable: [Nombre]
Backup probado: db_vigoentrena_prod_20251001_030000

RESULTADOS:

Tiempo restauración BD: 8 minutos ✅
Tiempo restauración filestore: 12 minutos ✅
Tiempo total: 20 minutos ✅

Verificaciones:
✅ Login OK
✅ Clientes completos
✅ Facturas completas
✅ PDFs descargan OK
✅ Calendario OK
⚠️ 2 archivos adjuntos no abren (investigar)

CONCLUSIÓN: Backup funcional ✅

ACCIONES:
- Investigar 2 archivos problemáticos
- Siguiente prueba: 2026-01-04

Firmado: [Nombre]
```

### 10.3. Cronograma Pruebas

```
Año 2025:

Q4 2025: 
  - Octubre: Prueba inicial (setup)
  
Q1 2026:
  - Enero: Prueba Q1
  
Q2 2026:
  - Abril: Prueba Q2
  
Q3 2026:
  - Julio: Prueba Q3
  
Q4 2026:
  - Octubre: Prueba Q4 + Prueba completa DRP
```

---

## 11. Checklist y Mejores Prácticas

### 11.1. Checklist Diario

```
☐ Verificar backup nocturno ejecutó OK
  - Revisar log: /var/log/odoo/backup.log
  - Verificar archivos creados en /opt/odoo/backups/daily

☐ Verificar espacio disco
  - df -h /opt/odoo/backups
  - Alerta si > 80% usado

☐ Verificar backup subió a cloud (si configurado)
  - rclone size gdrive:vigoentrena-backups/daily
  - Ver logs rclone
```

### 11.2. Checklist Semanal

```
☐ Revisar logs backups última semana
  - Buscar errores: grep ERROR /var/log/odoo/backup.log

☐ Verificar backups semanales creados
  - ls -lh /opt/odoo/backups/weekly/

☐ Verificar espacio total usado backups
  - du -sh /opt/odoo/backups/*

☐ Probar descargar 1 backup cloud aleatoriamente
```

### 11.3. Checklist Mensual

```
☐ Verificar backups mensuales creados
  - ls -lh /opt/odoo/backups/monthly/

☐ Revisar retención backups funcionando
  - Backups >30 días deben estar borrados

☐ Actualizar documentación DRP si hay cambios

☐ Revisar contactos de emergencia actualizados
```

### 11.4. Checklist Trimestral

```
☐ PRUEBA DE RESTAURACIÓN COMPLETA
  - Seguir procedimiento sección 10.2
  - Documentar resultados
  - Corregir problemas encontrados

☐ Revisar y actualizar procedimientos DRP

☐ Capacitar/repasar procedimientos con equipo

☐ Verificar acceso a credenciales emergencia
```

### 11.5. Mejores Prácticas

#### ✅ Hacer

```
✅ Automatizar todo (scripts + cron)
✅ Verificar backups funcionan (pruebas trimestrales)
✅ Backup remoto siempre (regla 3-2-1)
✅ Encriptar backups con datos sensibles
✅ Documentar procedimientos claramente
✅ Monitorear backups (alertas si fallan)
✅ Retener múltiples versiones (diario/semanal/mensual)
✅ Backup antes de cambios importantes
✅ Guardar certificados y claves separado
✅ Probar restauración en entorno NO producción
```

#### ❌ No Hacer

```
❌ Confiar solo en backup automático sin verificar
❌ Guardar backups SOLO en mismo servidor
❌ No probar nunca la restauración
❌ Borrar backups viejos prematuramente
❌ Backup sin filestore (archivos adjuntos)
❌ Ignorar errores en logs backup
❌ Backup sin documentar procedimiento restauración
❌ Usar sync en lugar de copy para cloud
❌ No encriptar backups con datos clientes
❌ Asumir que "alguien más" hace backup
```

---

## 12. Troubleshooting

### 12.1. Backup Falla (Script No Ejecuta)

**Síntoma**: No se crean archivos backup

**Diagnóstico**:
```bash
# Verificar cron configurado
sudo -u odoo crontab -l

# Ver logs cron
grep CRON /var/log/syslog | grep backup

# Probar script manual
sudo -u odoo /opt/odoo/backup.sh
```

**Soluciones**:
```bash
# Si script falla manual:
# - Revisar permisos: chmod +x /opt/odoo/backup.sh
# - Revisar logs: /var/log/odoo/backup.log
# - Verificar PostgreSQL corriendo

# Si cron no ejecuta:
# - Verificar servicio cron: systemctl status cron
# - Reinstalar cron: systemctl restart cron
# - Revisar sintaxis crontab
```

### 12.2. Backup Tarda Mucho

**Síntoma**: Backup tarda >1 hora

**Diagnóstico**:
```bash
# Ver tamaño BD
sudo -u postgres psql -c "SELECT pg_database_size('vigoentrena_prod');"

# Ver tamaño filestore
du -sh /opt/odoo/.local/share/Odoo/filestore/vigoentrena_prod
```

**Soluciones**:
```bash
# 1. Comprimir más agresivo (tiempo vs tamaño)
# En script backup, cambiar:
gzip > file.sql.gz
# Por:
gzip -9 > file.sql.gz  # Máxima compresión (más lento)

# 2. Backup incremental filestore (solo cambios)
# Usar rsync en lugar de tar:
rsync -az --delete /filestore/ /backup/filestore/

# 3. Vacuum PostgreSQL (reduce tamaño BD)
sudo -u postgres vacuumdb --all --analyze

# 4. Limpiar datos obsoletos
# - Borrar attachments viejos
# - Archivar facturas >5 años
```

### 12.3. No Puedo Restaurar Backup

**Síntoma**: Error al restaurar desde backup

**Error común 1**: "database already exists"
```bash
# Solución: Borrar BD primero
sudo -u postgres dropdb vigoentrena_prod
sudo -u postgres createdb -O odoo vigoentrena_prod
# Luego restaurar
```

**Error común 2**: "gunzip: invalid compressed data"
```bash
# Solución: Backup corrupto
# - Probar backup anterior
# - Verificar espacio disco al crear backup
# - Comprobar integridad: gunzip -t file.sql.gz
```

**Error común 3**: "permission denied"
```bash
# Solución: Permisos incorrectos
chown odoo:odoo /ruta/backup.sql.gz
# Restaurar como usuario odoo o postgres
```

### 12.4. Backup Cloud No Sube

**Síntoma**: rclone falla al subir

**Diagnóstico**:
```bash
# Probar manual
rclone copy /test.txt gdrive:/ -v

# Ver logs
tail -f /var/log/odoo/rclone.log
```

**Soluciones**:
```bash
# Error autenticación:
# - Reconfigurar rclone: rclone config
# - Verificar token no expiró

# Error red:
# - Verificar internet: ping 8.8.8.8
# - Verificar firewall: ufw allow out 443/tcp

# Cuota cloud excedida:
# - Verificar espacio: rclone about gdrive:
# - Limpiar backups viejos cloud
# - Ampliar plan almacenamiento
```

### 12.5. Restauración Parcialmente Funciona

**Síntoma**: Odoo carga pero faltan datos o errores

**Diagnóstico**:
```bash
# Ver logs Odoo al iniciar
journalctl -u odoo -f

# Errores comunes:
# - "module X not found" → Falta módulo
# - "relation Y does not exist" → BD incompleta
# - "FATAL: password authentication failed" → Credenciales incorrectas
```

**Soluciones**:
```bash
# Falta módulo custom:
# - Restaurar también /opt/odoo/custom-addons/
# - Instalar módulos faltantes

# BD incompleta:
# - Restaurar nuevamente (archivo corrupto?)
# - Probar backup anterior

# Errores módulos:
# - Actualizar módulos: odoo-bin -u all -d BD
# - Reinstalar módulo problemático
```

---

## 13. Conclusión

### 13.1. Resumen

Has aprendido a:
- ✅ Configurar backups automáticos (Odoo Online, Odoo.sh, manual)
- ✅ Crear scripts backup personalizados
- ✅ Almacenar backups en cloud de forma segura
- ✅ Restaurar sistema completo desde backups
- ✅ Implementar plan de recuperación ante desastres
- ✅ Probar restauraciones regularmente

### 13.2. Próximos Pasos

1. **Implementar backups hoy**:
   - Odoo Online: Ya tienes (verificar)
   - Odoo.sh: Ya tienes (verificar)
   - Manual: Configurar script y cron

2. **Configurar backup remoto** (esta semana):
   - Instalar rclone
   - Configurar Google Drive o S3
   - Probar subida backup

3. **Primera prueba restauración** (próximo mes):
   - Entorno test
   - Backup de hace 7 días
   - Documentar resultados

4. **Revisar trimestral**:
   - Probar restauración completa
   - Actualizar documentación DRP
   - Capacitar equipo

### 13.3. Checklist Final Implementación

```
☐ Backups automáticos configurados
☐ Frecuencia adecuada (diario mínimo)
☐ Backup remoto cloud funcionando
☐ Scripts probados y funcionando
☐ Logs de backup monitoreados
☐ Alertas configuradas (email si falla)
☐ Procedimientos restauración documentados
☐ Plan DRP creado
☐ Roles y responsabilidades asignados
☐ Primera prueba restauración completada
☐ Cronograma pruebas trimestrales
☐ Equipo capacitado procedimientos
```

---

## 14. Recursos Adicionales

### 14.1. Documentación Oficial

- **PostgreSQL Backup**: https://www.postgresql.org/docs/current/backup.html
- **Odoo Backups**: https://www.odoo.com/documentation/17.0/administration/maintain/backup.html
- **Rclone Docs**: https://rclone.org/docs/

### 14.2. Herramientas Útiles

- **pgBackRest**: https://pgbackrest.org/ (backups PostgreSQL avanzados)
- **Barman**: https://www.pgbarman.org/ (gestión backups PostgreSQL)
- **Restic**: https://restic.net/ (backups encriptados eficientes)
- **Borg Backup**: https://www.borgbackup.org/ (deduplicación)

### 14.3. Proveedores Backup Cloud

- **Backblaze B2**: https://www.backblaze.com/b2/cloud-storage.html
- **AWS S3**: https://aws.amazon.com/s3/
- **Google Cloud Storage**: https://cloud.google.com/storage
- **Wasabi**: https://wasabi.com/ (compatible S3, económico)

### 14.4. Monitoreo y Alertas

```bash
# Instalar Healthchecks.io (gratis)
# Ping cuando backup completa OK
# Alerta si no recibe ping en 25 horas

curl -fsS --retry 3 https://hc-ping.com/TU_UUID

# Añadir al final de backup.sh:
if [ $? -eq 0 ]; then
    curl -fsS https://hc-ping.com/TU_UUID
fi
```

---

**Documento creado para**: Vigoentrena  
**Versión**: 1.0  
**Última actualización**: Octubre 2025  
**Contacto**: backup@vigoentrena.com

---

**IMPORTANTE**: Prueba tus backups hoy. No esperes al desastre.

```
"El mejor momento para implementar backups fue ayer.
El segundo mejor momento es hoy."
```
