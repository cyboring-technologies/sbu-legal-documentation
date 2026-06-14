# Veredicto Ejecutivo — SBU-Legal

**Fecha de auditoría:** 14 de junio de 2026  
**Estado:** Final  
**Alcance:** repositorios, documentación estratégica, producto publicado, arquitectura, prompts, outputs, pricing, SEO, UX, competencia y comparación interna.  
**Limitación:** no se proporcionó acceso directo a Stripe, Google Search Console ni Google Ads. La ausencia de métricas en el repositorio no prueba cero ventas, pero sí prueba que no existe evidencia comercial auditable disponible para justificar inversión.

## 1. Diagnóstico corto

1. SBU-Legal tiene una infraestructura técnicamente competente, pero no una tesis comercial defendible.
2. El producto vende redacción legal probabilística en una categoría donde el comprador exige exactitud, trazabilidad y responsabilidad.
3. No existe dataset jurídico local, RAG, fuente normativa verificada ni validación semántica del output.
4. La diferenciación principal, incineración y privacidad, no compensa el riesgo de recibir un escrito incorrecto.
5. La arquitectura one-shot y sin reintentos aumenta la ansiedad precisamente cuando el usuario tiene un plazo urgente.
6. La documentación declara “Live / Monetizing”, pero solo contiene proyecciones y supuestos pre-lanzamiento.
7. Después de aproximadamente 95 días desde el lanzamiento del 11 de marzo, no hay métricas reales auditables de tráfico, ventas, CAC, CR o disputas.
8. El landing promete capacidades y garantías que contradicen el código y los términos legales.
9. Las 24 AntiPages producen 48 URLs localizadas, pero gran parte del contenido es duplicado, genérico y no adapta realmente audiencia ni idioma.
10. Las búsquedas transaccionales observadas favorecen formularios gratuitos, recursos oficiales, plantillas y competidores con bases jurídicas verificadas.
11. El margen bruto técnico puede superar 90%, pero el costo real es confianza, mantenimiento jurídico, soporte y riesgo reputacional.
12. El capital cognitivo tiene mejor retorno inmediato en SBU-Admisión y mejor tesis de prueba en VoiceOps.

## 2. Veredicto

* **Decisión:** No vale la pena rescatar la SBU-Legal actual. Archivar el negocio y conservar activos técnicos seleccionados.
* **Clasificación:** KILL
* **Convicción:** Alta
* **Razón principal:** El producto intenta vender outputs jurídicos de alto riesgo sin una ventaja estructural de exactitud, fuentes verificables o revisión responsable; su principal diferenciador es privacidad, mientras el criterio de compra dominante es confianza jurídica.

## 3. Tesis comercial actual

* **Cliente:** Inconsistente. El resumen estratégico menciona pymes, freelancers e individuos; el landing habla casi exclusivamente a litigantes, socios de firma y consultores.
* **Dolor:** La redacción procesal consume tiempo y genera bloqueo de página en blanco. El dolor es real para abogados.
* **Urgencia:** Alta cuando existe un plazo procesal, pero esa misma urgencia eleva la exigencia de confiabilidad y soporte.
* **Intención de pago:** No probada. No hay ventas, CR, CAC ni entrevistas documentadas en los activos auditados.
* **Diferenciación:** Débil. Usa GPT-4o con fallback a Gemini, skeletons y prompts; no posee corpus jurídico local, citas verificadas, workflow profesional acumulativo ni garantía de calidad.
* **Canal de adquisición:** SEO programático de long tail y ads exact-match, ambos sin evidencia empírica disponible.
* **Riesgo legal:** Alto por output jurisdiccional no verificado, claims de “listo para presentar”, promesas de precisión y contradicciones con la exención de garantías.
* **Soporte humano requerido:** Declarado como cero, pero en la práctica sería necesario para fallos, disputas, outputs defectuosos, dudas de uso y mantenimiento por jurisdicción.

## 4. Análisis brutal

### Qué funciona

* El dominio `documentos.legal` es claro, memorable y reciclable.
* El motor de upload, preview, generación, DOCX, descarga e incineración demuestra capacidad técnica reutilizable.
* El Gateway con quote firmado y captura/cancelación manual de Stripe es un activo transaccional reusable.
* La infraestructura scale-to-zero mantiene bajo el costo fijo técnico.
* El sitio compila correctamente y el flujo publicado responde.
* La privacidad efímera puede ser valiosa como atributo secundario para documentos sensibles.

### Qué no funciona

* No existe prueba de que alguien quiera pagar por “una ejecución irreversible” de un borrador legal.
* La promesa central está invertida: el negocio enfatiza cómo destruye datos, no por qué el documento será jurídicamente correcto.
* El validator solo revisa longitud, headers y contaminación de tags; explícitamente evita validación semántica.
* El sistema pide al LLM aplicar normas específicas sin conectarlo a legislación o jurisprudencia verificadas.
* La compra ocurre sin sample real, preview de calidad, fuentes, garantía sustantiva, revisión profesional ni prueba social verificable.
* El pricing de `$5 + $1 por página` cobra por tamaño del input, no por valor, complejidad jurídica o riesgo.
* Los “testimonios” son perfiles/personas sin nombres, firmas, citas reales o evidencia de uso.
* La arquitectura no instrumenta el funnel definido por la estrategia. La documentación dice medir E1-E6, pero el repositorio no contiene analítica de conversión implementada.
* La suite crítica no es confiable: el landing compila, pero sus unit tests no arrancan; el engine terminó con 9 de 14 pruebas fallando; la validación del Gateway también falló.

### Contradicciones de confianza

* El landing afirma selección dinámica por sección entre GPT-4o, Claude y Gemini, SAGA Pattern y Microsoft Azure.
* El código ejecuta GPT-4o para el documento completo y usa Gemini como fallback; no hay Claude ni Azure en el runtime auditado.
* El landing promete “precisión de grado judicial”, textos “consistentes y verificables” y soporte de ingeniería si falla la estructura.
* Los términos declaran que Cyboring no garantiza que el documento sea apto para ningún propósito legal específico.
* El schema SEO afirma que el escrito cumple requisitos de fondo y forma y está listo para presentar.
* Estas contradicciones reducen confianza y crean riesgo reputacional antes de que exista escala.

### Supuestos que parecen falsos

* **“Privacidad absoluta supera la barrera de confianza.”** No. Para un escrito procesal, exactitud y responsabilidad pesan más.
* **“One-shot reduce fricción.”** No. En un acto legal urgente, no reintentar ni recuperar eleva el riesgo percibido.
* **“Categorías procesales genéricas capturan intención transaccional.”** No hay evidencia. Las personas buscan documentos, materias, plazos, tribunales y jurisdicciones específicas.
* **“La jurisdicción se puede inferir del archivo.”** No es una base suficiente para aplicar derecho vigente y reglas locales.
* **“Margen >90% implica negocio viable.”** Solo prueba que el compute es barato; no prueba demanda, CAC ni calidad.
* **“Cero intervención humana es sostenible.”** No mientras el producto prometa outputs de litigio listos para presentar.

### Piezas faltantes para facturar de forma defendible

* Un nicho único con buyer, jurisdicción y acto legal específicos.
* Evidencia de willingness to pay antes de construir más.
* Corpus legal verificado y actualizado por jurisdicción.
* Evaluación sustantiva con abogados habilitados y dataset de casos.
* Fuentes/citas trazables dentro del output.
* Telemetría real del funnel.
* Prueba social real, samples anonimizados y expectativa contractual coherente.
* Política de recuperación, corrección y soporte compatible con la urgencia legal.

### Piezas que sobran

* La ideología de “Rubicon”, “Sovereign Engine” e “incineración” como centro del producto.
* El inventario proyectado de 96 AntiPages antes de demostrar demanda.
* Las páginas B2B/B2C/direct que terminan mostrando casi el mismo contenido.
* Claims institucionales, bancarios y judiciales no respaldados.
* Complejidad documental y de prompts creada antes de validar una venta repetible.

## 5A. Si vale la pena rescatarla: plan de rescate

No aplica. Cualquier versión potencialmente viable debe validarse como una nueva tesis vertical antes de reabrir la SBU actual.

## 5B. Si no vale la pena: razones para archivar

| Criterio | Evidencia encontrada | Severidad | Consecuencia |
|---|---|---:|---|
| Demanda no probada | La documentación disponible contiene proyecciones; el reporte económico se declara pre-lanzamiento y “not yet empirically validated”. | Crítica | No existe fundamento para invertir más capital cognitivo. |
| Supuesto comercial roto | Se asume que usuarios urgentes aceptarán un output irreversible, sin recuperación y sin garantía jurídica. | Crítica | La urgencia aumenta el rechazo, disputas y necesidad de soporte. |
| Indiferenciación frente a IA generalista | GPT-4o/Gemini + prompts + skeletons, sin corpus local ni verificación. ChatGPT y Claude ya aceptan archivos y producen documentos. | Crítica | El usuario puede obtener capacidad similar gratis o dentro de una suscripción existente. |
| Diferenciación inferior a legaltech especializada | Competidores ofrecen legislación verificada, jurisprudencia, formularios, firma, trazabilidad o workflows completos. | Alta | Privacidad one-shot no crea moat suficiente. |
| Calidad jurídica no validada | El validator evita validación semántica y no verifica normas, citas, fondo o forma. | Crítica | Un output estructuralmente válido puede ser jurídicamente incorrecto. |
| Riesgo legal y reputacional | “Listo para presentar” y “grado judicial” contradicen los términos sin garantías. | Crítica | Reclamos, chargebacks, pérdida de confianza y exposición reputacional. |
| Adquisición débil | 53 URLs en sitemap, pero búsquedas exactas de AntiPages no devolvieron resultados; las queries observadas muestran recursos gratuitos y autoridades. | Alta | SEO lento, programático y con baja probabilidad de recuperar founder time. |
| SEO duplicado | Las rutas `en` y `es` renderizan el mismo AntiPage en español; audiencia y variante no alteran sustancialmente el contenido visible. | Alta | Riesgo de duplicación, baja relevancia y no indexación. |
| Funnel no medible | Los eventos E1-E6 están definidos en docs, pero no hay implementación de analytics o resultados exportados. | Alta | No se puede optimizar ni demostrar conversión. |
| Soporte humano oculto | Claims de soporte, fallos técnicos, outputs defectuosos y disputas chocan con “Human Intervention: 0”. | Alta | El activo autónomo se convierte en empleo reactivo. |
| Mantenimiento jurisdiccional | Expandir México, Colombia y Chile exige reglas, formatos, actualización y QA diferentes. | Alta | La complejidad aumenta por país; no es clonación barata. |
| Costo de oportunidad | Admisión ya tiene tráfico, pagos y feedback; VoiceOps tiene una prueba acotada con dolor más claro. | Crítica | Cada semana en Legal retrasa apuestas con mejor evidencia o EV. |

## 6. Comparación contra otras SBUs

| Dimensión | SBU-Legal | SBU-Admisión | SBU-VoiceOps |
|---|---|---|---|
| Probabilidad de facturar | Baja; no hay evidencia auditable y la confianza es difícil | Alta relativa; ya existe tráfico, pago y feedback real | Media; tesis y validación controlada antes de automatizar |
| Dolor y urgencia | Reales, pero mezclados con riesgo jurídico extremo | Claros: examen próximo, ansiedad y resultado concreto | Claros: entrevista/llamada laboral y mejora de ingreso |
| Complejidad | Alta por jurisdicción, exactitud y responsabilidad | Media; dataset cerrado y producto estable | Media; voz y scoring, sin responsabilidad jurídica |
| Tiempo a mercado creíble | Largo; estar live no equivale a ser confiable | Ya está en mercado | Corto para prueba de willingness to pay |
| Defensibilidad | Baja; prompts y privacidad | Alta relativa; dataset local cerrado y expansión parametrizada | Media; escenarios, rubrics y datos de readiness acumulables |
| Riesgo operativo | Alto | Medio, principalmente estacional | Medio, controlable si no incluye coaching |
| Potencial de expansión | Débil: cada país agrega derecho y QA | Fuerte si existe dataset local equivalente | Fuerte: escenarios y dolor transferibles en LATAM |
| Dependencia del founder | Alta y disfrazada como mantenimiento/QA | Baja-media | Baja-media si permanece automatizada |
| Margen bruto >85% | Posible técnicamente, dudoso con soporte real | Compatible | Posible, aunque voz reduce margen |
| Recomendación | KILL | PUSH | INCUBATE / prueba controlada |

SBU-Legal no merece capital cognitivo frente a Admisión. Tampoco merece precedencia sobre una prueba de VoiceOps, porque VoiceOps puede validar intención de pago sin asumir responsabilidad jurídica ni mantener derecho por jurisdicción.

## 7. Activos reciclables

### Conservar

* Dominio `documentos.legal`, únicamente como activo estacionado o para una futura tesis validada.
* Gateway de pagos con quote firmado, manual capture/cancel y token de ejecución.
* Pipeline de ingestión PDF/DOCX, preview, extracción, generación de DOCX y descarga.
* Patrón de almacenamiento efímero e incineración como opción de privacidad.
* Componentes de landing, i18n, temas, CTA y layouts.
* Documentación de arquitectura y aprendizajes de one-shot economics.

### Reutilizar

* El motor transaccional para transformaciones de documentos de menor responsabilidad.
* El patrón “pagar por resultado” en SBUs donde el output pueda verificarse objetivamente.
* R2/Durable Objects, CostManifest y Stripe Gateway como infraestructura compartida.
* El sistema de preview y HITL para workflows con validación explícita y recuperación.
* El dominio como lead magnet o directorio solo si existe un partner jurídico responsable.

### Eliminar o archivar definitivamente

* La tesis de “documentos procesales genéricos listos para presentar”.
* Las AntiPages duplicadas y el plan de escalar a 96 páginas sin señal.
* Claims de grado judicial, bancario, Azure, Claude, SAGA y garantía que no reflejen runtime verificable.
* Los prompts legales actuales como producto comercial defendible.
* La regla de no retries aplicada a outputs legales urgentes.
* Proyecciones llamadas MRR o monetización sin datos observados.

### Documentar como aprendizaje

* Validar pago antes de construir arquitectura extensa.
* No usar margen técnico como sustituto de demanda.
* En categorías de alta confianza, la responsabilidad y la trazabilidad son parte del producto.
* No permitir que una doctrina interna de arquitectura gobierne contra la necesidad del cliente.
* Claims comerciales deben derivarse del runtime real y de evidencia verificable.

## 8. Señal mínima para reabrir

Reabrir solo como una nueva tesis vertical y únicamente si, dentro de una validación de máximo 4 semanas, se cumplen **todos** estos criterios:

1. **Wedge definido:** un solo buyer profesional, un solo acto legal y una sola jurisdicción.
2. **Pago antes de construir:** al menos 15 depósitos/preventas no afiliadas a precio mínimo de `$49`, o 5 firmas pagando un piloto mínimo de `$250`.
3. **Calidad verificada:** 30 outputs anonimizados evaluados por abogado habilitado en la jurisdicción, con al menos 90% utilizables, cero autoridades inventadas y ahorro de revisión de al menos 50%.
4. **Adquisición verificable:** al menos 100 clicks de intención exacta con conversión pagada mínima de 2% y CAC máximo de 30% del AOV.
5. **Operación autónoma:** soporte manual menor a 10% de compradores y refund/dispute/complaint rate menor a 5%.

Si falta uno de estos criterios, la SBU permanece cerrada. Impresiones, elogios, demos o usuarios gratuitos no cuentan como señal de reapertura.

## 9. Decisión final

**Mi recomendación es: ARCHIVAR SBU-Legal como negocio, retirar sus claims de producción y reciclar su infraestructura; no invertir una semana adicional hasta obtener preventas y validación jurídica objetiva de un único workflow vertical.**

## Evidencia y fuentes consultadas

### Evidencia interna principal

* `Documentation/4_Business_Strategy_and_Economics/EXECUTIVE_SUMMARY_V3.3_SBU_LEGAL.md`: declara monetización, pero presenta proyecciones y `JUR_1`.
* `Documentation/4_Business_Strategy_and_Economics/ECONOMIC_LAUNCH_VALIDATION_REPORT.md`: se identifica como pre-lanzamiento y no validado empíricamente.
* `Documentation/1_Core_Architecture_and_Systems/PROMPT_SYSTEM_STATE_V2.md`: confirma ausencia de validación semántica y no retries.
* `sbu-legal-engine/src/domain/OutputValidator.js`: valida estructura, no derecho.
* `sbu-legal-engine/src/index.js`: GPT-4o primario y Gemini fallback.
* `sbu-legal-landing/src/messages/es.json`: claims comerciales y contradicciones.
* `sbu-legal-landing/src/components/AntiPage.tsx`: contenido genérico y hardcoded en español.
* `sbu-legal-landing/src/app/(landing)/[locale]/[slug]/page.tsx`: claims de “listo para presentar”.
* `sbu-legal-landing/src/app/(landing)/sitemap.ts`: duplicación de AntiPages en `en` y `es`.

### Fuentes externas

* Sitio y sitemap publicados: [documentos.legal](https://documentos.legal/) y [sitemap.xml](https://documentos.legal/sitemap.xml)
* Capacidades generalistas actuales: [ChatGPT Projects y archivos](https://help.openai.com/en/articles/10169521-projects-in-chatgpt), [Claude upload de archivos](https://support.anthropic.com/en/articles/8241126-what-kinds-of-documents-can-i-upload-to-claude-ai), [Claude creación de Word/PDF](https://support.anthropic.com/en/articles/12111783-create-and-edit-files-with-claude)
* Competencia especializada observada: [Iurexia](https://www.iurexia.com/), [Lexius México](https://lexius.io/mx/), [EasyLex](https://easylex.com/contratos), [SDV Generador de Documentos](https://sdv.com.mx/herramientas/generador-documentos/)
* Sustitutos gratuitos/autoridad: [Justia México, requisitos de contestación](https://mexico.justia.com/federales/codigos/codigo-nacional-de-procedimientos-civiles-y-familiares/libro-segundo/titulo-segundo/capitulo-i/seccion-segunda/)
* Riesgo profesional de IA legal: [ABA Formal Opinion 512](https://www.americanbar.org/news/abanews/aba-news-archives/2024/07/aba-issues-first-ethics-guidance-ai-tools/)
