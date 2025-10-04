# 🏥 Vigoentrena - Sistema ERP Odoo 17

> Sistema integral de gestión empresarial basado en Odoo 17 para centro de fisioterapia y ejercicio personalizado

## 📋 Índice

- [Sobre este proyecto](#sobre-este-proyecto)
- [Estado del proyecto](#estado-del-proyecto)
- [Documentación](#documentación)
- [Módulos implementados](#módulos-implementados)
- [Integraciones](#integraciones)
- [Requisitos](#requisitos)
- [Inicio rápido](#inicio-rápido)
- [Soporte y comunidad](#soporte-y-comunidad)

---

## 🎯 Sobre este proyecto

**Vigoentrena** es un centro especializado en:
- 🩺 Fisioterapia individual personalizada
- 💪 Ejercicio terapéutico grupal
- 🏋️ Entrenamiento personalizado

Este repositorio contiene toda la documentación, configuraciones y recursos necesarios para implementar y mantener un sistema ERP completo basado en **Odoo 17**, diseñado específicamente para las necesidades operativas, comerciales y clínicas de Vigoentrena.

---

## 📊 Estado del proyecto

| Fase | Estado | Descripción |
|------|--------|-------------|
| 📚 Investigación | 🟡 En proceso | Recopilación de documentación y recursos |
| 🏗️ Planificación | ⏸️ Pendiente | Diseño de arquitectura y roadmap |
| ⚙️ Instalación | ⏸️ Pendiente | Instalación de Odoo 17 |
| 🔧 Configuración Core | ⏸️ Pendiente | Módulos básicos esenciales |
| 🏥 Módulos Clínica | ⏸️ Pendiente | Gestión de pacientes y tratamientos |
| 💳 VeriFactu | ⏸️ Pendiente | Integración obligatoria fiscal |
| 📱 WhatsApp Business | ⏸️ Pendiente | Canal de comunicación principal |
| 🌐 Reservas Online | ⏸️ Pendiente | Sistema de booking |
| ✍️ Firma Digital | ⏸️ Pendiente | Consentimientos y documentos |
| 📱 App Móvil | ⏸️ Pendiente | Área personal cliente-profesional |

**Última actualización:** 2025-10-03

---

## 📚 Documentación

La documentación está organizada en dos niveles:

### 👨‍💻 Documentación Técnica
Para desarrolladores, administradores de sistemas e implementadores:
- [Instalación de Odoo 17](docs/01-guia-tecnica/instalacion-odoo17.md)
- [Configuración de servidor](docs/01-guia-tecnica/configuracion-servidor.md)
- [Arquitectura del sistema](docs/01-guia-tecnica/arquitectura-sistema.md)
- [Seguridad y permisos](docs/01-guia-tecnica/seguridad-permisos.md)
- [Backup y recuperación](docs/01-guia-tecnica/backup-recuperacion.md)

### 👥 Documentación Funcional
Para usuarios finales, gestores y personal operativo:
- [¿Qué es Odoo?](docs/00-introduccion/que-es-odoo.md)
- [Odoo para Vigoentrena](docs/00-introduccion/odoo-para-vigoentrena.md)
- [Configuración inicial](docs/02-guia-funcional/configuracion-inicial.md)
- [Manual de usuario final](docs/02-guia-funcional/manual-usuario-final.md)
- [Flujos de trabajo](docs/02-guia-funcional/flujos-trabajo.md)

### 📖 Documentación por Módulos

#### 🎯 Módulos Core (CRÍTICOS)
- [CRM - Gestión de Clientes](docs/03-modulos-core/crm-gestion-clientes.md)
- [Ventas y Cotizaciones](docs/03-modulos-core/ventas-cotizaciones.md)
- [TPV/Punto de Venta](docs/03-modulos-core/tpv-punto-venta.md)
- [Contabilidad y Finanzas](docs/03-modulos-core/contabilidad-finanzas.md)
- [Inventario](docs/03-modulos-core/inventario.md)
- [Calendario y Citas](docs/03-modulos-core/calendario-citas.md)
- [Marketing y Automatización](docs/03-modulos-core/marketing-automatizacion.md)

#### 🏥 Módulos Clínica
- [Gestión de Pacientes](docs/04-modulos-clinica/gestion-pacientes.md)
- [Historiales Clínicos](docs/04-modulos-clinica/historiales-clinicos.md)
- [Sesiones y Tratamientos](docs/04-modulos-clinica/sesiones-tratamientos.md)
- [Consentimientos Informados](docs/04-modulos-clinica/consentimientos-informados.md)

#### 💪 Módulos Ejercicio Grupal
- [Clases y Actividades](docs/05-modulos-ejercicio-grupal/clases-actividades.md)
- [Reservas de Clases](docs/05-modulos-ejercicio-grupal/reservas-clases.md)
- [Gestión de Instructores](docs/05-modulos-ejercicio-grupal/gestion-instructores.md)
- [Control de Aforo](docs/05-modulos-ejercicio-grupal/control-aforo.md)

#### 🔌 Integraciones Críticas
- [VeriFactu - Implementación](docs/06-integraciones-criticas/verifactu-implementacion.md) ⚠️ **OBLIGATORIO**
- [Facturación Electrónica](docs/06-integraciones-criticas/facturacion-electronica.md)
- [AEAT - Agencia Tributaria](docs/06-integraciones-criticas/aeat-hacienda.md)
- [Normativa Fiscal España](docs/06-integraciones-criticas/normativa-fiscal-espana.md)

#### 📱 Comunicaciones
- [WhatsApp Business Setup](docs/07-comunicaciones/whatsapp-business-setup.md) 🔥 **PRIORITARIO**
- [Notificaciones y Recordatorios](docs/07-comunicaciones/notificaciones-recordatorios.md)
- [Marketing por WhatsApp](docs/07-comunicaciones/marketing-whatsapp.md)
- [Plantillas de Mensajes](docs/07-comunicaciones/plantillas-mensajes.md)

#### 🌐 Reservas Online
- [Sistema de Booking](docs/08-reservas-online/sistema-booking.md)
- [Calendario Público](docs/08-reservas-online/calendario-publico.md)
- [Pasarelas de Pago](docs/08-reservas-online/pasarelas-pago.md)
- [Confirmaciones Automáticas](docs/08-reservas-online/confirmaciones-automaticas.md)

#### ✍️ Firma Digital
- [Configuración de Firma](docs/09-firma-digital/configuracion-firma.md)
- [Documentos Firmables](docs/09-firma-digital/documentos-firmables.md)
- [Cumplimiento Legal eIDAS](docs/09-firma-digital/cumplimiento-legal-eidas.md)

#### 📱 App Móvil
- [Análisis de Requisitos](docs/10-app-movil/analisis-requisitos-app.md)
- [API de Odoo para Desarrollo](docs/10-app-movil/api-odoo-desarrollo.md)
- [Arquitectura de la App](docs/10-app-movil/arquitectura-app.md)
- [Funcionalidades Cliente](docs/10-app-movil/funcionalidades-cliente.md)

---

## 🧩 Módulos implementados

### Módulos Nativos de Odoo 17
- [ ] CRM
- [ ] Ventas
- [ ] Punto de Venta (TPV)
- [ ] Contabilidad
- [ ] Inventario
- [ ] Calendario
- [ ] Proyectos
- [ ] Recursos Humanos
- [ ] Marketing Automation
- [ ] Sitio Web
- [ ] Documentos
- [ ] Firma Online

### Módulos de Terceros (OCA/Community)
- [ ] Gestión Clínica
- [ ] Gestión de Pacientes
- [ ] Localización España (l10n_es)
- [ ] VeriFactu
- [ ] WhatsApp Integration
- [ ] Booking System
- [ ] Fitness/Wellness Management

### Módulos Personalizados
- [ ] Vigoentrena Custom (módulo específico)
- [ ] Integraciones personalizadas

---

## 🔌 Integraciones

### Obligatorias (Cumplimiento Legal)
- ⚠️ **VeriFactu** - Sistema de facturación verificable (obligatorio en España)
- 📊 **AEAT** - Agencia Estatal de Administración Tributaria
- 📄 **Facturación electrónica**

### Comunicación
- 📱 **WhatsApp Business API** - Canal principal de comunicación
- 📧 **Email Marketing**
- 🔔 **Notificaciones push**

### Pagos y Financiero
- 💳 **Redsys** (pasarela bancaria española)
- 💰 **Stripe**
- 🏦 **PayPal**
- 💵 **Bizum**

### Firma y Documentación
- ✍️ **DocuSign** / **Firma electrónica**
- 📋 **eIDAS compliant signature**

### Futuras (Fase 2)
- 🤖 **Archon** - Automatización avanzada
- 🔄 **N8N** - Workflow automation
- 🔗 **MCP** (Model Context Protocol)
- 🤝 **A2A** (Agent-to-Agent)

---

## 💻 Requisitos

### Requisitos del Sistema (Mínimos)
- **SO:** Ubuntu 22.04 LTS / Debian 11+ (recomendado)
- **RAM:** 4 GB mínimo, 8 GB recomendado
- **CPU:** 2 cores mínimo, 4+ recomendado
- **Disco:** 40 GB mínimo, SSD recomendado
- **Python:** 3.10+
- **PostgreSQL:** 14+
- **Node.js:** 16+ (para desarrollo)

### Requisitos de Red
- Conexión a Internet estable
- Puerto 8069 (Odoo)
- Puerto 443 (HTTPS)
- Certificado SSL válido

### Opciones de Hosting
1. **Odoo.sh** (Cloud oficial) - Recomendado para empezar
2. **VPS propio** (Hetzner, Digital Ocean, AWS)
3. **On-premise** (servidor local)

---

## 🚀 Inicio rápido

### Para Usuarios sin Experiencia Técnica

1. **Lee primero:**
   - [¿Qué es Odoo?](docs/00-introduccion/que-es-odoo.md)
   - [Odoo para Vigoentrena](docs/00-introduccion/odoo-para-vigoentrena.md)
   - [Glosario de términos](docs/00-introduccion/glosario-terminos.md)

2. **Sigue el plan:**
   - Revisa [TODO.md](TODO.md) para ver el roadmap completo
   
3. **Comienza la implementación:**
   - Si vas a contratar: [Guía de selección de partner](docs/00-introduccion/seleccion-partner.md)
   - Si vas a instalarlo tú: [Instalación paso a paso](docs/01-guia-tecnica/instalacion-odoo17.md)

### Para Desarrolladores/Técnicos

```bash
# 1. Clonar este repositorio
git clone [URL-del-repositorio]
cd vigoentrena-odoo17

# 2. Seguir guía de instalación técnica
# Ver: docs/01-guia-tecnica/instalacion-odoo17.md

# 3. Ejecutar scripts de configuración
./scripts/instalacion/install-odoo17.sh

# 4. Configurar módulos core
./scripts/configuracion/setup-core-modules.sh
```

---

## 📖 Recursos de aprendizaje

### Documentación Oficial
- [Odoo 17 Official Documentation](https://www.odoo.com/documentation/17.0/)
- [Odoo Developer Documentation](https://www.odoo.com/documentation/17.0/developer.html)

### Comunidad
- [Odoo Community Association (OCA)](https://odoo-community.org/)
- [Odoo GitHub](https://github.com/odoo/odoo)
- [OCA GitHub](https://github.com/OCA)

### Cursos y Tutoriales
- Ver [docs/11-recursos-aprendizaje/cursos-tutoriales.md](docs/11-recursos-aprendizaje/cursos-tutoriales.md)

---

## 🤝 Soporte y comunidad

### ¿Necesitas ayuda?

1. **Consulta la documentación** en la carpeta `docs/`
2. **Revisa el [TODO.md](TODO.md)** para ver el estado actual
3. **Busca en issues** si tu problema ya está documentado
4. **Comunidad Odoo:**
   - [Forum Odoo](https://www.odoo.com/forum)
   - [Odoo España](https://www.odoo.com/es_ES/partners)

### Partners Certificados Odoo en España
- Ver [lista de partners](docs/00-introduccion/partners-espana.md)

---

## 📝 Licencia

- **Odoo Community:** LGPL-3.0
- **Odoo Enterprise:** Licencia propietaria
- **Esta documentación:** MIT License

---

## ✅ Contribuir

Esta es documentación interna de Vigoentrena. Si encuentras errores o mejoras:
1. Documenta el cambio
2. Actualiza el archivo correspondiente
3. Mantén la coherencia con el resto de la documentación

---

## 📞 Contacto

**Vigoentrena**
- Web: [www.vigoentrena.com](https://www.vigoentrena.com)
- Email: info@vigoentrena.com
- Ubicación: Vigo, Galicia, España

---

**Última actualización:** Octubre 2025  
**Versión de Odoo:** 17.0  
**Estado:** 🟡 En desarrollo

---

## 🗺️ Roadmap

Ver [TODO.md](TODO.md) para el plan detallado de implementación.

### Fases
1. ✅ **Fase 0:** Investigación y planificación (en curso)
2. ⏳ **Fase 1:** Instalación y configuración core
3. ⏳ **Fase 2:** Módulos clínicos y operativos
4. ⏳ **Fase 3:** Integraciones críticas (VeriFactu, WhatsApp)
5. ⏳ **Fase 4:** Reservas online y pagos
6. ⏳ **Fase 5:** App móvil
7. ⏳ **Fase 6:** Automatización avanzada (Archon, N8N, MCP)

---

**⚡ Nota importante:** Este proyecto está diseñado con documentación didáctica para usuarios sin experiencia previa en Odoo. Cada concepto se explica desde cero.
