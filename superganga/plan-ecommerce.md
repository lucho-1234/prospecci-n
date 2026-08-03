# SuperGanga — Plan de e-commerce nacional

**Cliente:** SuperGanga (bazar, Montevideo) — 2 locales.
**Referente:** el supervisor general (padre de Luciano), a cargo de 1 de los 2 locales.
**Fecha del documento:** 2026-08-03
**Estado:** borrador de diagnóstico. Hay 4 datos pendientes que definen el stack (ver §8).

---

## 1. Objetivos declarados y su traducción operativa

| Objetivo del cliente | Qué significa en la práctica | Dificultad |
|---|---|---|
| Aumentar ventas | Canal nuevo + demanda nueva (ads/SEO/marketplace), no solo "poner la tienda" | Media |
| Alcance nacional (todo Uruguay) | Logística al interior + pagos remotos + confianza | **Alta** |
| Autonomía del cliente | Catálogo buscable, stock real, checkout sin fricción, autogestión de seguimiento | Media |
| Stock que se actualiza solo | Integración con el sistema de gestión de ambos locales | **La más alta** |
| Seguimiento por Gmail | Mails transaccionales automáticos + casilla operativa para el equipo | Baja |
| Comodidad: rapidez, claridad, sencillez | UX, tiempos de entrega reales, política de cambios clara | Media |

---

## 2. Correcciones al plan original (leer antes de decidir nada)

### 2.1 PedidosYa NO da alcance nacional

Es el supuesto más caro del plan. **PedidosYa Envíos es logística de última milla**: el punto de
retiro y el de entrega tienen que estar **en la misma localidad**, con un máximo aproximado de
**10 km de distancia** y **hasta 10 kg**, en el tamaño de la mochila del repartidor. Sirve para
entregar en Montevideo el mismo día — que es un diferencial real — pero **no lleva un paquete a
Salto, Rivera o Maldonado.**

Para "todo Uruguay" hay que armar un esquema **multi-transportista**:

| Destino / necesidad | Transportista | Notas |
|---|---|---|
| Montevideo, mismo día / express | PedidosYa Envíos (o similar) | ≤10 kg, ≤10 km, 8:00–22:00 |
| Montevideo y área metro | UES | Entrega rápida metro |
| Interior — cobertura amplia | Correo Uruguayo (plataforma **Ahíva**) | Estándar ~3 días hábiles, prioritario ~1 día desde MVD; autogestión de envío, seguimiento y cobro |
| Interior — encomiendas / agencias | DAC | Correo privado con presencia nacional e integraciones a e-commerce |
| Cualquier destino, costo cero | **Retiro en local** | Gratis, usa los 2 locales como puntos de retiro — subestimado y clave |

> **Acción:** pedir cotización de tarifas y condiciones a DAC, UES y Correo Uruguayo (Ahíva) con
> el peso/volumen típico de un pedido de bazar. Sin esos números no se puede fijar precio de envío.

### 2.2 La economía unitaria del bazar es el riesgo comercial #1

Un bazar vende mucho volumen de ticket bajo. Si el envío al interior cuesta $250–400 y el
producto vale $200, **el envío cuesta más que el producto** y no hay conversión posible.

Mitigaciones, en orden de impacto:

1. **Mínimo de compra para envío** (ej. $1.500) — obliga a armar canasta, sube el ticket.
2. **Envío gratis por umbral** (ej. > $2.500–3.000), con el costo absorbido en margen.
3. **Retiro gratis en cualquiera de los 2 locales** — convierte muy bien y no cuesta nada.
4. **Combos / packs** (set de cocina, kit de organización, canasta de fiesta) en vez de piezas sueltas.
5. **Curar el catálogo:** online van los SKU de **mayor margen y mayor valor unitario**, no los 4.000 artículos del salón.

### 2.3 Precondición organizacional: el otro local

El objetivo es vender el stock **de ambos locales**, pero el referente maneja **uno solo**. Antes
de escribir una línea de código hay que cerrar con el otro local:

- ¿Quién despacha cuándo el artículo está en el otro local?
- ¿Cómo se imputa la venta y a quién le cuenta el resultado?
- ¿Quién repone y con qué prioridad?
- ¿El otro local descuenta stock en el mismo sistema y en el momento?

Si el otro local no descuenta en tiempo real, la web va a vender algo que ya se vendió en
mostrador → cancelaciones → reseñas malas → se quema el canal en el arranque.

> **Recomendación:** arrancar publicando **solo el stock del local que él controla**, y sumar el
> segundo local recién cuando haya acuerdo escrito y sincronización probada. Es mejor una tienda
> chica que cumple que una grande que cancela.

### 2.4 Factura electrónica (CFE / DGI)

Toda venta necesita comprobante fiscal electrónico. No es opcional ni "se ve después": define qué
plataforma sirve. Hay que conectar la tienda al mismo emisor de e-factura que ya usan en el local
(o contratar uno). **Confirmar con el contador antes de elegir plataforma.**

### 2.5 "Que se actualice sola" depende enteramente del sistema de gestión actual

No es una función que se activa: es una integración. El escenario cambia radicalmente según qué
usan hoy:

| Si usan… | Camino |
|---|---|
| **Zureo** | Es el mejor caso. Tiene integración homologada con plataformas locales (Fenicio) y conexión por webservices con AgileCommerce. Sync casi real. |
| **Memory, Zeta, Doria, Facturapp, Bit u otro ERP uruguayo** | Hay integraciones existentes o se desarrolla contra su API/export. Verificar caso por caso. |
| **Un POS sin API** | Export programado de CSV + import a la tienda (cada 2–6 h). Funciona, no es tiempo real. |
| **Excel / papel** | **Primero hay que ordenar el inventario.** Sin maestro de artículos con código único, no hay automatización posible. Esto puede ser un proyecto en sí. |

---

## 3. Stack recomendado

### Opción A — Arranque rápido y barato (recomendada para el MVP)

**Tiendanube + Mercado Pago + multi-transportista + app de e-factura**

- Diseñada para la región, integración nativa con Mercado Pago (el medio de pago que mejor
  convierte con tarjetas locales uruguayas).
- Costo mensual predecible en moneda local + comisión por transacción.
- Autonomía total del cliente lista de fábrica (buscador, filtros, carrito, cuenta, seguimiento).
- Mails transaccionales y carrito abandonado incluidos.
- **Límite:** el manejo multi-depósito (2 locales) y el sync con ERP local es más flojo. Para el
  MVP con un solo local, no molesta.

### Opción B — Si el catálogo es grande y el ERP es serio

**Fenicio** (plataforma uruguaya, homologada con Zureo, integraciones locales de pago,
logística y e-factura) o **AgileCommerce** (webservices contra Zureo, Zeta, Doria, Facturapp;
también integra Mercado Libre).

Más caro y con implementación más lenta, pero resuelve de verdad stock multi-local + CFE +
logística nacional. Es a donde hay que migrar si el proyecto funciona.

### Opción C — Desarrollo a medida (WooCommerce / Next.js)

**No recomendada para arrancar.** Todo lo que las opciones A y B traen resuelto (pagos,
e-factura, transportistas, seguridad, mantenimiento) pasa a ser trabajo y costo recurrente.
Solo tiene sentido con volumen alto y un desarrollador sostenido en el tiempo.

### Canal paralelo a considerar seriamente: Mercado Libre

Para **alcance nacional**, MELI ya tiene el tráfico y la logística resueltos. Es el camino más
corto al objetivo "todo Uruguay", y sirve de validación: qué SKU se venden fuera de Montevideo,
a qué precio, con qué costo de envío. La web propia queda para margen y marca; MELI para volumen
y descubrimiento. No son excluyentes — AgileCommerce, por ejemplo, integra ambos.

---

## 4. Medios de pago

- **Mercado Pago** — base obligatoria (tarjetas locales, cuotas, billetera).
- **Redpagos / Abitab** — pago en efectivo, importante en el interior y en público no bancarizado.
- **Transferencia bancaria** — ticket alto, sin comisión.
- Nota: **Shopify Payments no está disponible en Uruguay**; con Shopify hay que usar pasarela
  externa *y además* pagar a Shopify una comisión extra por venta. Es un argumento fuerte a favor
  de Tiendanube o de una plataforma local.
- Plexo / Geocom son procesadoras más "enterprise": recién convienen con facturación mensual alta.

---

## 5. Seguimiento por Gmail

Dos cosas distintas que conviene no mezclar:

**a) Mails automáticos al cliente** (los hace la plataforma):
1. Confirmación de pedido
2. Pago acreditado
3. Pedido despachado + **número de seguimiento del transportista**
4. Entregado / listo para retirar
5. Pedido de reseña a los 5–7 días
6. Carrito abandonado (a las 4 h y a las 24 h)

**b) Operación interna:**
- Casilla del dominio propio (`ventas@superganga.com.uy`) con **Google Workspace**, no un Gmail
  personal — un Gmail personal para volumen transaccional termina en spam y no es profesional.
- Etiquetas/filtros por estado: `Nuevo`, `A despachar`, `Despachado`, `Incidencia`.
- Alerta al celular por cada pedido nuevo (la app de la plataforma lo hace mejor que el mail).
- **Además:** WhatsApp Business como canal de atención. En Uruguay, para el público de bazar,
  convierte más que el mail.

---

## 6. Fases

### Fase 0 — Diagnóstico y datos (semana 1) ← **estamos acá**
- [ ] Identificar el sistema de gestión actual y si tiene API/exportación
- [ ] Exportar el maestro de artículos (código, descripción, precio, costo, stock por local)
- [ ] Acordar con el otro local, o decidir arrancar con uno solo
- [ ] Confirmar con el contador el emisor de e-factura
- [ ] Cotizar DAC / UES / Correo (Ahíva) con peso y volumen reales
- [ ] Comprar dominio + Google Workspace
- [ ] Definir los **150–300 SKU** del arranque: mejor margen, fácil de embalar, no frágil, no voluminoso

### Fase 1 — MVP vendiendo (semanas 2–4)
- [ ] Tienda armada con esos SKU, fotos propias y descripciones claras
- [ ] Mercado Pago + Redpagos/Abitab + transferencia
- [ ] 3 opciones de entrega: **retiro en local (gratis)** / Montevideo / interior
- [ ] Mails transaccionales + WhatsApp
- [ ] Políticas visibles: envíos, cambios y devoluciones, tiempos
- [ ] **Meta: 50–100 pedidos reales** antes de invertir fuerte en automatización

### Fase 2 — Automatización de stock (semanas 5–8)
- [ ] Conexión sistema de gestión ↔ tienda
- [ ] Sync de stock y precios (mínimo cada 2–4 h; ideal, tiempo real)
- [ ] Reserva de stock al confirmar el pago
- [ ] Alerta de quiebre y ocultamiento automático del artículo sin stock
- [ ] Recién acá: sumar el stock del segundo local

### Fase 3 — Demanda y alcance nacional (mes 3 en adelante)
- [ ] Meta Ads segmentado al interior (**acá entra el trabajo de Luciano**)
- [ ] Google Shopping / catálogo
- [ ] Publicar en Mercado Libre como segundo canal
- [ ] Email marketing a la base de compradores
- [ ] Contenido: usos, combos, temporada (escolar, fiestas, día de la madre)

---

## 7. Métricas a mirar desde el día 1

- Ticket promedio (el número que decide si el envío es viable)
- Tasa de conversión de la tienda
- % de pedidos con retiro en local vs. envío
- % de pedidos del interior vs. Montevideo (mide el objetivo "alcance nacional")
- Pedidos cancelados por falta de stock (**mide si la sincronización funciona**)
- Costo de adquisición vs. margen por pedido

---

## 8. Datos pendientes que definen el stack

1. **¿Qué sistema usan hoy para stock y facturación?** (Zureo, Memory, otro, Excel)
2. **¿Los dos locales comparten la misma base de stock?**
3. **¿Cuántos SKU tiene el catálogo y cuál es el ticket promedio en el local?**
4. **¿Quién construye y mantiene la tienda: Luciano, o se contrata implementador?**

---

## 9. Fuentes verificadas

- PedidosYa Envíos (última milla, misma localidad): https://envios.pedidosya.com.uy/
- Correo Uruguayo, paquetes nacionales y Ahíva: https://www.correo.com.uy/paquetes-nacionales
- DAC, envíos e integraciones e-commerce: https://www.dac.com.uy/envios-en-uruguay
- UES: https://www.ues.com.uy/
- Fenicio + Zureo (ERP homologado): https://fenicio.io/
- AgileCommerce, integraciones ERP y Mercado Libre: https://www.agilecommerce.com.uy/
- Tiendanube, planes y precios: https://www.tiendanube.com/planes-y-precios

> **Nota de verificación:** buscando "SuperGanga bazar Montevideo" no encontré presencia online
> con ese nombre exacto. **No lo tomo como que no existe** — puede estar bajo otra razón social,
> otra grafía ("Super Ganga") o solo en redes. Confirmar el nombre comercial exacto y si ya hay
> web, Instagram o publicaciones en Mercado Libre antes de dar nada por sentado.
