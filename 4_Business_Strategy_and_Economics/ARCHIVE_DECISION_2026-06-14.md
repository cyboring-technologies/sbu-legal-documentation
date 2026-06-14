# Decisión de Archivo — SBU-Legal / Documentos.legal

**Fecha efectiva:** 2026-06-14  
**Estado:** Archivado / KILL  
**Responsable institucional:** Cyboring Technologies LLC

## Decisión

SBU-Legal deja de operar como unidad comercial activa. Documentos.legal se conserva únicamente
como registro institucional y referencia interna de investigación. No se mantiene una oferta
pública de generación documental, compra, carga de archivos, procesamiento o entrega.

## Motivo operativo

La superficie pública anterior combinaba claims comerciales, páginas de adquisición, rutas de
ejecución y contenido SEO que podían comunicar una capacidad activa o una promesa jurídica mayor
que el estado real del producto. El costo de corregir y sostener esa promesa no se justifica para
una SBU archivada.

## Estado público aprobado

- La única URL indexable es `https://documentos.legal`.
- La página raíz comunica de forma explícita que el proyecto está archivado.
- La página raíz explica qué fue, qué no es y su estado dentro de Cyboring.
- No existen CTA públicos hacia compra, carga, generación, descarga o ejecución.
- Las rutas heredadas de locales, servicios, precios, FAQ, blog y anti-pages fueron retiradas.
- Las rutas operativas `/engine`, `/prepare` y `/terminal` presentan estado archivado y cuentan con
  redirecciones de borde hacia la raíz.
- Sitemap, robots, RSS, metadata y schema describen únicamente el archivo institucional.

## Condición legal y privacidad

La superficie archivada es informativa. No ofrece asesoría legal, representación ni documentos
aptos para procedimientos. No solicita documentos ni datos para prestar servicios. El alojamiento
puede conservar registros técnicos mínimos de acceso por seguridad y operación.

## Infraestructura conservada

Se preservan, sin exposición comercial desde la landing:

- El repositorio y código del engine.
- El gateway y sus contratos técnicos.
- Componentes reutilizables de procesamiento, pago y UI.
- Configuración de despliegue y documentación técnica histórica.
- El dominio y la marca como activos institucionales.

Esta preservación no implica disponibilidad pública, soporte, continuidad ni reactivación.

## Contenido retirado

- Landing comercial localizada.
- Páginas de servicios, precios, contacto, FAQ, términos y privacidad anteriores.
- Anti-pages y sus datos estructurados.
- Blog y RSS promocional.
- Metadatos y schema de servicio/oferta.
- Captura pública de interés por correo.

## Riesgos residuales y controles

1. Los repositorios conservan infraestructura y documentación histórica que no debe interpretarse
   como oferta pública.
2. Cualquier despliegue futuro de las configuraciones operativas normales del engine o gateway
   podría reactivar el servicio; los archivos `wrangler.archive.toml` deben conservarse como estado
   de producción mientras la decisión KILL siga vigente.

## Ejecución en producción

Completada el 2026-06-14:

- Export archivado publicado en Cloudflare Pages, proyecto `sbu-legal-landing`.
- Deployment Pages de ejecución: `4c6a12e9-2fa6-47d2-b4b7-2e577f97c9b6`.
- `engine.documentos.legal` restringido con respuesta `410 Gone`, `no-store` y `noindex`.
- Versión archivada del Worker engine: `3c00d344-75df-41c2-86ab-a1e06a3efdc5`.
- `gateway.documentos.legal` restringido con respuesta `410 Gone`, bloqueando cotizaciones,
  intenciones de pago y webhooks públicos.
- Versión archivada del Worker gateway: `c0927c03-7caa-4767-9f11-2da92c740ad0`.
- Verificación pública: raíz archivada en `200`, rutas heredadas de landing en `302` hacia `/`, y
  todas las rutas probadas de engine/gateway en `410`.

## Criterio para cualquier reactivación

Cualquier reactivación futura requiere una nueva decisión ejecutiva, revisión legal, alcance de
producto explícito, controles de privacidad, validación de claims y una estrategia comercial
aprobada. No existe reactivación implícita por conservar código o dominio.
