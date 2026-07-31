# Plan de e-commerce — SuperGanga (bazares, Montevideo)

**Objetivo del negocio:** vender online el stock de los dos locales, con alcance nacional,
con autonomía del cliente y actualización automática de inventario.

**Estado de partida (según relevamiento):**

- Dos locales, **inventarios separados y sin unificar**.
- Entre 300 y 1.500 SKUs distintos.
- Sin presupuesto asignado todavía.
- Referencias visuales: tselectronica.com.uy, electronica.uy, bazarnews.com.uy,
  bazardelcocinero.com.uy, electroventas.com.uy.

---

## 0. Tres correcciones al planteo inicial

Antes del paso a paso, tres cosas que hay que reacomodar o el proyecto se cae solo.

### 0.1 PedidosYa no te da alcance nacional

PedidosYa Envíos resuelve **radio corto en Montevideo y algunas ciudades**, con topes de peso
y volumen que un bazar rompe enseguida (una olla a presión, un juego de copas, un ventilador).
Sirve, pero como *una* opción de envío, no como la columna vertebral.

Para "todo Uruguay" el esquema real es una **matriz de envíos**:

| Destino | Medio | Plazo típico | Quién paga |
|---|---|---|---|
| Montevideo, urgente | PedidosYa Envíos / Pedidos Ya Flex | mismo día | cliente |
| Montevideo, normal | reparto propio o mensajería local | 24-48 h | gratis sobre monto X |
| Interior, ciudades grandes | DAC / UES | 24-72 h | cliente |
| Interior, localidades chicas | Correo Uruguayo (Paquetón) | 3-7 días | cliente |
| Interior, terminal de bondi | Agencia (Turismo Van, Agencia Central, COT, Núñez) | 24-48 h | cliente, retira en terminal |
| Retiro en local | — | inmediato | **gratis** |

> **Verificar antes de decidir:** tarifas y cobertura vigentes de DAC, UES y Correo Uruguayo,
> y si alguna tiene integración/API con la plataforma que elijas. Las tarifas cambian y no
> conviene hardcodearlas.

**Consejo de conversión:** "Retiro en local gratis" es la opción que más convierte y no te
cuesta nada. Ponela primera en el checkout. Además trae gente al local, que compra más cosas.

### 0.2 "Que se actualice sola" no es viable en fase 1 — y hay un atajo

Con dos inventarios que no se hablan, la sincronización automática es un proyecto de meses.
Pero el problema que la sincronización resuelve —**vender algo que no tenés**— se puede
resolver hoy, sin código:

> **Apartá stock físico para la web.** Un estante, una estantería o un rincón del depósito.
> Lo que está ahí es lo que la web puede vender. Nadie más lo toca.

Ventajas: el stock online es un número chico y controlable, no hay carrera entre el mostrador
y la web, y una persona lo actualiza en 15 minutos por día. Es lo que hace todo comercio real
cuando arranca online. La sincronización automática viene después, cuando el volumen la
justifique (fase 3).

### 0.3 Bazar News es competencia directa — y está en tu CRM de prospección

Uno de los sitios de referencia que pasaste, **bazarnews.com.uy**, es un prospecto activo
del CRM de Luciano (contacto conseguido en puerta fría el 14/07). Copiar su estructura de
catálogo está perfecto. Pero tenelo presente: si SuperGanga sale a competir con ellos, hay un
conflicto de interés que conviene resolver antes, no después.

---

## Fase 0 — Fundaciones (semanas 1 a 3). Sin esto no se arranca

Esta fase no tiene nada de web. Es la que más se saltea y la que más proyectos mata.

### 0.A Unificar el inventario en una sola fuente de verdad

1. **Un SKU único por producto**, compartido entre los dos locales. Si el local A le dice
   "olla 24" y el local B "OLLA-24CM", son el mismo producto y necesitan el mismo código.
2. **Una planilla maestra** (Google Sheets sirve perfecto para arrancar) con columnas:
   `SKU | Nombre | Categoría | Proveedor | Costo | Precio venta | Stock local A | Stock local B | Stock web | Foto | Descripción`
3. Definir **quién la actualiza y cuándo**. Un nombre y un horario concretos, no "el que pueda".

> Claude Code te sirve acá: pasale los dos listados en CSV y pedile que detecte duplicados,
> normalice nombres y proponga un SKU unificado. Lo que a mano son dos semanas, así son dos días.

### 0.B Elegir el catálogo online (NO son los 1.500)

Elegí **200 a 300 SKUs** con este criterio:

- Alta rotación (se venden solos, ya sabés que hay demanda).
- Buen margen (el envío se come el margen de los productos baratos).
- **Enviables**: livianos, no frágiles, no voluminosos. Un juego de copas de vidrio a Rivera
  es un reclamo esperando a pasar.
- Que no dependan de que el cliente los toque antes de comprar.

Regla práctica: si un producto pesa más de 5 kg o vale menos de $300 UYU, dejalo para el local.

### 0.C Chequeos legales y administrativos

- [ ] **Facturación electrónica (CFE / DGI)**: en Uruguay es obligatoria. ¿SuperGanga ya emite
      e-tickets? ¿Con qué proveedor? La web tiene que poder emitir comprobante por cada venta.
      Si hoy no facturan electrónicamente, esto es un bloqueante duro, no un detalle.
- [ ] **RUT y razón social** — necesarios para registrar un dominio `.com.uy` y para las
      pasarelas de pago.
- [ ] **Quién firma**: tu papá es supervisor general. ¿Tiene autoridad para aprobar el gasto
      y el proyecto, o hay un dueño/gerencia que tiene que dar el OK? Conseguí ese sí por
      escrito antes de invertir semanas.
- [ ] **Política de cambios y devoluciones** escrita. Por ley de defensa del consumidor en
      Uruguay, en venta a distancia el cliente tiene derecho de arrepentimiento. Hay que
      tenerla publicada.

---

## Fase 1 — La tienda mínima vendible (semanas 3 a 8)

### 1.1 Elegir plataforma

Me pediste que decida yo. **Recomendación: plataforma llave en mano, no desarrollo a medida.**

El motivo es concreto: si la web la programás vos a medida, vos quedás como el único que puede
mantenerla, para siempre. El día que estés ocupado, con parcial o de viaje, la tienda de tu
papá se queda sin poder cambiar un precio. Para un bazar de 300 SKUs eso es un riesgo que no
compensa ninguna ventaja técnica.

Candidatos, en orden:

| Opción | A favor | En contra |
|---|---|---|
| **Tiendanube / Nuvemshop** | Pensada para LatAm, panel en español, Mercado Pago nativo, apps de envío, tu papá carga productos solo | Costo mensual + verificar que opere y facture en Uruguay |
| **Shopify** | El mejor producto del mercado, temas parecidos a tus referencias | Shopify Payments no opera en UY → dependés de pasarela externa con comisión extra; más caro |
| **WooCommerce (WordPress)** | Barato, control total, plugins locales de envío/pago | El mantenimiento, backups y seguridad quedan de tu lado — volvés al problema del párrafo de arriba |
| **Mercado Shops** | Alcance nacional instantáneo, envíos resueltos por Mercado Envíos | No es web propia, comisión alta, poca marca |

> **Verificá antes de contratar:** que la plataforma elegida opere formalmente en Uruguay,
> facture con RUT uruguayo y tenga integración real con Mercado Pago UY. Esto cambia seguido;
> confirmalo con soporte por escrito, no con un blog.

**Mi recomendación operativa:** Tiendanube (o Woo si el presupuesto es mínimo) **+ Mercado Libre
en paralelo** (ver 3.1).

### 1.2 Marca y dominio

- Verificar disponibilidad de `superganga.com.uy` en **NIC.uy / ANTEL**. Los `.com.uy` requieren
  RUT uruguayo. Registrar también el `.uy` si está libre, para que no te lo agarre otro.
- Email profesional: **Google Workspace con dominio propio** — `ventas@superganga.com.uy`.
  No uses un Gmail personal para la tienda: mata la confianza y no escala.

### 1.3 Fotos de producto — acá entra la IA, con un límite claro

Tenés 200-300 productos que fotografiar. El estándar de tus sitios de referencia es
**fondo blanco, producto centrado, misma proporción en todos**.

Flujo recomendado:

1. **Foto real de cada producto**, con el celular. Luz de ventana, fondo liso, trípode barato
   o una caja para apoyar. 3 minutos por producto.
2. **Nano Banana (Gemini Image) o similar** para: recortar el fondo, unificarlo en blanco puro,
   corregir iluminación, cuadrar todo al mismo tamaño. Esto es lo que antes era Photoshop y
   ahora son segundos por imagen.
3. Para las **fotos de ambiente** (la olla sobre una mesa puesta, el juego de copas en un
   living), ahí sí la IA genera el contexto alrededor del producto real.

> ⚠️ **Regla que no se rompe:** la IA **retoca** la foto del producto real, **nunca lo genera**.
> Si el cliente recibe algo que no se parece a la foto, tenés devolución, reseña de una estrella
> y —en venta a distancia— un problema legal. En un bazar, donde la diferencia entre una jarra
> y otra son detalles, esto es especialmente sensible.

### 1.4 Fichas de producto

Cada ficha necesita: nombre claro, medidas, material, marca, precio, stock, foto y una
descripción de 2-3 líneas.

Escribir 300 descripciones a mano son semanas. Con la API de Claude, pasás el CSV del catálogo
y generás títulos y descripciones en lote en un par de horas. **Después las revisás a mano** —
sobre todo medidas y materiales, que son datos que no se pueden inventar.

### 1.5 Pagos

Ofrecé varias vías, porque en Uruguay conviven cuatro hábitos distintos:

- **Mercado Pago** — tarjetas, cuotas, el más usado.
- **Redpagos / Abitab** — pago en efectivo contra una boleta. Subestimado y clave: mucha gente
  del interior compra online y paga en efectivo en la esquina.
- **Transferencia bancaria** (BROU, Itaú, Santander) — cero comisión, ideal para tickets altos.
- **Contra entrega** — solo para Montevideo y con retiro/reparto propio.

> Las cuotas sin interés son *el* argumento de venta en electrodomésticos y bazar. Averiguá
> con la pasarela qué planes de cuotas podés ofrecer y cuánto te cuestan.

### 1.6 Checkout — la autonomía que pidió tu papá se juega acá

- **Compra sin registro obligatorio.** Pedir cuenta antes de comprar hace perder ventas.
- Costo de envío visible **antes** del último paso.
- Calculadora de envío por departamento en la propia ficha de producto.
- Todo el flujo probado en celular. En Uruguay, la enorme mayoría del tráfico de retail es móvil.
- Botón de WhatsApp visible siempre. Mucha gente no compra online: pregunta por WhatsApp y
  después compra. Eso también es venta.

---

## Fase 2 — Seguimiento y operación (semanas 6 a 10, se solapa)

Tu papá pidió "seguimiento por Gmail". Desglosado en lo que realmente hace falta:

**Emails automáticos que manda la plataforma** (se configuran una vez):
1. Confirmación de compra
2. Pago acreditado
3. Pedido despachado + número de seguimiento
4. Pedido entregado / listo para retirar

**Seguimiento comercial** (lo hace una persona):
- Carrito abandonado a las 24 h — recupera entre el 5 % y el 15 % de las ventas perdidas.
  Es la automatización con mejor retorno que existe en e-commerce.
- Post-compra a los 7 días: "¿llegó todo bien?" → pedido de reseña.
- Recompra a los 60-90 días en categorías de consumo.

> **Consejo contraintuitivo:** en Uruguay el **WhatsApp convierte mucho más que el mail** para
> seguimiento comercial. Usá el mail para lo transaccional (que además queda como comprobante)
> y WhatsApp Business para el seguimiento de verdad. WhatsApp Business tiene catálogo, respuestas
> rápidas y etiquetas de cliente, gratis.

**Operación diaria** — definí y escribí esto antes de abrir:
- ¿Quién revisa los pedidos y cada cuánto? (mínimo 2 veces por día)
- ¿Quién arma el paquete y quién lo despacha?
- ¿Qué se le contesta a alguien que compró algo que justo se agotó? (va a pasar)
- ¿Cuál es el plazo prometido? Prometé de más y cumplí; no al revés.

---

## Fase 3 — Automatización de stock (mes 3 en adelante)

Recién acá se ataca "que se actualice sola", y solo si el volumen lo justifica.

**Escalón 1 — Semiautomático (donde vas a estar los primeros meses).**
Planilla maestra en Google Sheets → export CSV → import a la tienda, una vez por día.
Muchas plataformas importan por CSV programado o por URL. Barato y suficiente hasta
~20 pedidos por día.

**Escalón 2 — Sincronizado.**
Un script (acá sí, Claude Code) que lee la planilla o el sistema del local y actualiza stock
y precios por la API de la tienda cada X minutos. Requiere que el paso 0.A esté hecho de verdad.

**Escalón 3 — Integrado.**
El POS de los locales es la fuente de verdad y la web es un canal más. Esto exige que **los dos
locales usen el mismo sistema**, que hoy no pasa. Es una decisión de la empresa, no un tema
técnico, y probablemente el proyecto más caro de esta lista.

> No saltes al escalón 3 porque suena mejor. El escalón 1 con stock apartado (0.2) sostiene
> perfectamente los primeros 6 meses.

---

## Fase 4 — Vender de verdad (desde el día del lanzamiento)

Una tienda sin tráfico no vende. Este es el capítulo que más se subestima.

### 3.1 El alcance nacional real empieza en Mercado Libre, no en tu web

Duro pero cierto: nadie en Tacuarembó conoce SuperGanga y nadie va a buscar
`superganga.com.uy`. Mercado Libre Uruguay ya tiene la audiencia nacional, la confianza y la
logística resuelta con Mercado Envíos.

**Estrategia de dos canales:**
- **Mercado Libre = motor de demanda.** Vendés desde el día uno, a todo el país, sin construir
  audiencia. Pagás comisión, pero vendés.
- **Web propia = margen y marca.** Sin comisión, con tus datos de cliente, tu lista de mails.
  Crece más lento pero es tuya.

En cada paquete que sale por Mercado Libre, meté una tarjetita: *"La próxima comprá directo en
superganga.com.uy y te llevás 10 % off con el código GRACIAS10."* Así convertís el tráfico
alquilado de MELI en clientes propios. Es la jugada más rentable de todo el plan.

### 3.2 Lanzamiento: no abras en silencio

- **Cartel con QR en la caja de los dos locales**, dos semanas antes. Cada cliente que ya compra
  es un cliente que puede comprar online.
- Los clientes que ya tenés en WhatsApp: mensaje de aviso.
- Google Business Profile de los dos locales actualizado con el link.

### 3.3 Meta Ads (ventaja de casa: Luciano ya sabe)

- Instalar el **Píxel de Meta** antes de lanzar, no después. Sin datos históricos, las campañas
  arrancan ciegas.
- Primera campaña: **catálogo + remarketing** a quien visitó y no compró. Es la de mejor ROAS
  y la más barata.
- Recién después, campañas de alcance frío por interés y geografía.
- Presupuesto inicial chico y sostenido: **$300–500 UYU por día durante un mes** enseña más
  que $10.000 en tres días.

### 3.4 Palancas de conversión específicas de bazar

- **Envío gratis a partir de un monto** — calculalo un 30-40 % por encima de tu ticket promedio
  actual. Sube el ticket solo.
- **Combos** (juego de ollas + repasadores, set de mate completo). El bazar es el rubro ideal
  para armar combos: margen más alto y menos comparable con la competencia.
- **Reseñas visibles.** Sin reseñas, un negocio desconocido no vende a distancia. Pedilas
  activamente desde el primer pedido.
- **Fechas fuertes uruguayas**: Día de la Madre, Navidad, Reyes, Black Friday, vuelta a clases.
  En bazar, Día de la Madre y Navidad pueden ser la mitad del año.

---

## Presupuesto orientativo (para llevar a gerencia)

Cifras aproximadas en pesos uruguayos, a validar con cotizaciones reales.

**Inversión inicial (una vez)**

| Ítem | Estimado |
|---|---|
| Dominio `.com.uy` (anual) | $1.500 – 3.000 |
| Diseño e instalación del tema | $0 (tema gratuito) – $15.000 |
| Fotografía de 250 productos | $0 si la hacen ustedes – $25.000 tercerizado |
| Carga de catálogo y descripciones | tiempo interno + IA |
| **Subtotal** | **$3.000 – 45.000** |

**Costos mensuales**

| Ítem | Estimado |
|---|---|
| Plan de la plataforma | $1.500 – 4.000 |
| Google Workspace (1-2 usuarios) | $500 – 1.000 |
| Comisión de pasarela | 3–6 % de lo vendido |
| Comisión Mercado Libre (si se usa) | 12–17 % de lo vendido ahí |
| Pauta en Meta Ads | $9.000 – 15.000 |
| **Subtotal fijo** | **$11.000 – 20.000/mes** + comisiones |

**El número honesto para la gerencia:** con unos **$40.000 UYU iniciales y $15.000 mensuales**
durante 4-6 meses, el proyecto es viable. Con menos, se puede arrancar, pero sin pauta el
crecimiento va a ser muy lento.

---

## Cronograma resumido

| Semana | Qué pasa | Quién |
|---|---|---|
| 1-2 | Unificar SKUs, planilla maestra, chequeos legales | Papá + vos |
| 2-3 | Elegir 250 SKUs, apartar stock físico para web | Papá + locales |
| 3-4 | Contratar plataforma, dominio, mails | Vos |
| 4-6 | Fotos + carga de catálogo | Vos + IA |
| 6-7 | Pagos, envíos, checkout, políticas | Vos |
| 7 | **Pruebas reales**: 5 compras de punta a punta, incluida una devolución | Todos |
| 8 | Lanzamiento suave: QR en los locales, WhatsApp a clientes | Papá |
| 9-12 | Mercado Libre en paralelo + primeras campañas de Meta | Vos |
| Mes 4+ | Automatización de stock según volumen real | Vos |

---

## Riesgos, ordenados por probabilidad de que pasen

1. **Se vende algo que no hay en stock.** Mitigación: stock apartado (0.2) + margen de
   seguridad (si hay 5, publicá 3).
2. **El proyecto muere en la fase 0** porque unificar SKUs es aburrido y nadie lo hace.
   Mitigación: un responsable con nombre y una fecha.
3. **Se lanza y no vende porque no hay tráfico.** Mitigación: Mercado Libre + QR en los locales
   desde el día uno.
4. **Vos quedás como único sostén técnico.** Mitigación: plataforma llave en mano y **capacitar
   a alguien de la empresa** para cargar productos. Grabá dos videos de pantalla explicando cómo.
5. **El costo de envío mata el margen.** Mitigación: solo productos livianos, umbral de envío
   gratis bien calculado.
6. **La gerencia corta el presupuesto al mes 2** porque no ve ventas. Mitigación: acordar de
   entrada que el horizonte es de 6 meses y definir qué métricas se miran mientras tanto
   (visitas, tasa de conversión, ticket promedio), no solo facturación.

---

## Qué falta definir

Preguntas abiertas que hay que responder para afinar este plan:

1. ¿SuperGanga emite **facturación electrónica** hoy? ¿Con qué proveedor?
2. ¿Qué sistema usa cada local para el stock? (nombre concreto del software, si lo hay)
3. ¿Tu papá **decide** o hay que convencer a un dueño/gerencia?
4. ¿Hay alguien en la empresa que pueda dedicarle **horas semanales fijas** a cargar productos
   y despachar pedidos, o recae todo en él?
5. ¿Existe ya marca registrada, logo, redes sociales de SuperGanga?
6. ¿Qué **categorías** son las más fuertes hoy en el mostrador? (define el catálogo online)
7. ¿Cuál es el **ticket promedio** actual? (define el umbral de envío gratis)
8. ¿Hay depósito o los dos locales son también el almacén?
