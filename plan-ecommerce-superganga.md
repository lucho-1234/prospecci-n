# SuperGanga — Plan para el ecommerce nacional

Documento de arranque. Objetivo: montar una tienda online que venda el stock de **los dos locales**
a todo Uruguay, con actualización automática de inventario y autonomía total del cliente.

Estado: **borrador de decisión**. Nada de esto se ejecuta hasta cerrar el Paso 0.

---

## 1. Lo primero: el sitio web NO es el problema difícil

Antes de hablar de tecnología, la verdad incómoda del proyecto:

| Lo que parece el trabajo | Lo que realmente es el trabajo |
|---|---|
| "Hacer la página" | Cargar el catálogo (fotos, descripciones, medidas, precios) |
| "Que se actualice sola" | Que el stock de los dos locales viva en **un solo sistema confiable** |
| "Vender más" | Conseguir que alguien entre a la página |
| "Envíos a todo el país" | Que haya alguien empaquetando y despachando todos los días |

Un bazar tiene fácil 2.000–8.000 SKUs y casi ninguno tiene foto propia ni descripción. **Ese es el
cuello de botella real del proyecto, y no lo resuelve ningún desarrollador.** Si esto no se planifica,
el proyecto muere con la web hecha y 40 productos cargados.

Corolario práctico: **no se lanza con todo el catálogo.** Se lanza con los 150–300 productos que más
rotan y mejor margen dejan, y se va ampliando. Es más rápido, más barato y se aprende antes.

---

## 2. Diagnóstico de las tres referencias que le gustan a tu papá

Las miré por dentro. Dato importante:

- **electroventas.com.uy** → corre sobre **Fenicio** (plataforma uruguaya; se delata por el CDN `f.fcdn.app`)
- **tselectronica.com.uy** → mismo patrón de SPA con ruteo `#/`, casi con seguridad **Fenicio** también
- **bazardelcocinero.com.uy** → **WooCommerce** (WordPress)

Traducción: **dos de las tres webs que le gustan son la misma plataforma uruguaya, comprada hecha.**
No son desarrollos a medida. El "estilo" que quiere ya viene resuelto de fábrica.

Esto es una excelente noticia y ahorra meses.

---

## 3. Recomendación central: comprar plataforma, no desarrollar a medida

**No construyas esto desde cero.** No por capacidad técnica, sino porque un ecommerce serio en Uruguay
tiene que resolver, además del catálogo:

- Pasarela de pagos certificada (PCI), cuotas sin recargo, OCA/Visa/Master
- **Facturación electrónica (CFE) ante DGI** — obligatorio, y solo es trámite si la plataforma ya lo trae
- Integración con couriers y etiquetas de envío
- Sincronía de stock multi-depósito
- Seguridad, backups, uptime, mantenimiento eterno

Hacer eso a medida son **4 a 8 meses** y después queda el mantenimiento colgando de una sola persona.
Una plataforma lo trae resuelto y se lanza en semanas.

### Comparativa de los tres caminos reales

| | **Fenicio** | **Tiendanube** | **WooCommerce** |
|---|---|---|---|
| Origen | 🇺🇾 Uruguaya, desde 2010 | 🌎 Regional (LatAm) | Open source, autogestionado |
| Costo | Mayor (plan + setup) | Desde ~USD 18/mes + comisión | Hosting barato, pero el trabajo lo pagás en horas |
| Integración con ERP uruguayo (Memory/Zureo) | ✅ Nativa vía webservices | ⚠️ Vía terceros | 🔧 Se programa |
| Multi-depósito (2 locales) | ✅ | ⚠️ Limitado | 🔧 Plugin |
| CFE / DGI | ✅ | ⚠️ Verificar | 🔧 Plugin uruguayo |
| PedidosYa Envíos | ✅ **Integración nativa ya existente** | ⚠️ Verificar | 🔧 |
| Es lo que usan sus referencias | ✅ (2 de 3) | ❌ | ✅ (1 de 3) |
| Riesgo de quedar solo | Bajo (soporte local) | Bajo | **Alto** — si se va quien lo mantiene, se cae |

**Recomendación:**

- Si el stock ya vive en **Memory o Zureo** y el catálogo es grande → **Fenicio.** Es la opción que
  literalmente le da lo que pidió, incluido PedidosYa, y es soporte local en Montevideo.
- Si quieren **validar con poca plata primero** → **Tiendanube**, catálogo acotado, y se migra si funciona.
- **WooCommerce** solo si hay alguien comprometido a mantenerlo por años. Es la opción más barata en
  factura y la más cara en dependencia.

---

## 4. Paso 0 — Las 6 preguntas que hay que responder ANTES de tocar nada

Sin estas respuestas, cualquier decisión técnica es a ciegas.

1. **¿En qué sistema vive el stock hoy?** (Memory / Zureo / otro software / Excel / papel)
   → *Es la pregunta que define todo el proyecto.* Sin API o export automatizable, "que se actualice
   sola" no existe: alguien va a cargar stock a mano todos los días.
2. **¿Cuántos SKUs hay entre los dos locales, y cuántos tienen foto y descripción usable?**
3. **¿Los dos locales son la misma razón social?** ¿Quién factura la venta online? ¿De qué local sale
   la mercadería cuando los dos tienen el producto?
4. **¿Ya emiten facturación electrónica (CFE) ante DGI?** ¿Con qué proveedor?
5. **¿Quién carga el catálogo?** Nombre y apellido, y cuántas horas por semana. (Sin esto no hay proyecto.)
6. **¿Quién empaqueta y despacha, y en qué horario?** Un pedido que sale a los 4 días mata la tienda.

---

## 5. Corrección importante sobre los envíos

Tu papá menciona PedidosYa para mover los productos. Ojo con esto:

- **PedidosYa Envíos es última milla** — fuerte en Montevideo y zona metropolitana, entregas en el día.
  Excelente para la capital.
- **Para "todo Uruguay" no alcanza.** El estándar uruguayo para el interior son las agencias de
  encomiendas: **DAC, UES, Correo Uruguayo, Turismo Van** y similares.

Entonces el esquema realista de envíos es en tres capas:

| Zona | Método | Promesa |
|---|---|---|
| Montevideo | PedidosYa Envíos | Mismo día / 24 h |
| Interior | DAC / UES / Correo | 24–72 h a agencia |
| Los dos locales | **Retiro en tienda** | 1–2 h |

**No subestimes el retiro en tienda.** En las tres webs de referencia está destacado arriba de todo.
Es el envío más barato (gratis), el más rápido, y trae gente al local — que es exactamente lo que
necesitan dos locales con las ventas flojas.

*(Verificar cobertura y tarifas actuales de PedidosYa Envíos antes de prometer nada al cliente.)*

---

## 6. Sobre el "seguimiento por Gmail"

Importante para no arrancar torcido: hay que separar dos cosas.

- **Mails transaccionales** (confirmación de compra, "tu pedido salió", código de seguimiento):
  los manda **la plataforma**, automáticos, desde un dominio propio. **Nunca desde un Gmail personal**
  — se van a spam y no escala.
- **Atención humana** (consultas, reclamos): ahí sí, Google Workspace con `ventas@superganga.com.uy`,
  que se lee como un Gmail normal.

Requisito técnico: **dominio propio + SPF, DKIM y DMARC configurados.** Sin eso los mails de la tienda
caen en correo no deseado y el cliente cree que no le llegó nada.

Primer paso concreto y barato: **registrar el dominio `.com.uy` ya** (ANTEL/NIC.uy), antes que cualquier
otra cosa. Cuesta poco y bloquea el nombre.

---

## 7. Fases de ejecución

| Fase | Qué pasa | Duración |
|---|---|---|
| **0. Decisión** | Responder las 6 preguntas · elegir plataforma · registrar dominio | 1–2 sem |
| **1. Catálogo** | Los 150–300 productos del lanzamiento: fotos, títulos, precios, medidas y peso (el peso define el costo de envío) | 3–4 sem ⚠️ *la fase que se subestima* |
| **2. Montaje** | Tienda armada, categorías, diseño, textos, páginas legales | 2 sem |
| **3. Plomería** | Pasarela de pagos · CFE/DGI · couriers · sincronía de stock | 1–2 sem |
| **4. Piloto cerrado** | 10–15 compras reales de conocidos, de punta a punta, hasta la entrega. **Acá se rompen cosas y está bien.** | 1 sem |
| **5. Apertura** | Lanzamiento + tráfico pago | — |

Total realista: **8 a 12 semanas** hasta vender en serio. Cualquiera que prometa 3 semanas está
salteando la Fase 1.

---

## 8. La parte que nadie planifica: el tráfico

Una tienda nueva recibe **cero visitas** el día que abre. Google no la conoce y nadie la busca.
"Aumentar las ventas" no lo produce la web, lo produce la gente que entra a la web.

Presupuestar desde el día 1:
- Google Merchant / Shopping (la gente busca "olla presión precio uruguay" con intención de comprar)
- Meta Ads con catálogo conectado y remarketing
- Los locales físicos como canal: cartelería y QR en caja empujando a la web

Sin un presupuesto de tráfico, el proyecto es una vidriera en un callejón sin salida.

---

## 9. Métricas — cómo saber a los 90 días si funcionó

- Pedidos por semana y ticket promedio
- % de ventas del interior (mide si el objetivo "alcance nacional" se cumplió de verdad)
- Tasa de conversión (visitas → compras). Referencia: **1–2% es sano** para retail
- Costo de adquisición vs. margen por pedido
- % de pedidos despachados en menos de 24 h
- Quiebres de stock: pedidos vendidos sin mercadería real → mide si la sincronía anda

---

## 10. Errores caros a evitar

1. **Lanzar con el catálogo entero.** Se lanza con lo que rota. El resto se carga después.
2. **Vender lo que no hay.** Si el stock no está sincronizado de verdad, el primer cliente al que le
   cancelan el pedido no vuelve más, y lo cuenta.
3. **Mails transaccionales desde Gmail personal.** Spam garantizado.
4. **Precios web distintos a los del local sin explicarlo.** Genera desconfianza y reclamos en caja.
5. **Fotos malas.** En bazar, la foto **es** el producto. Fondo blanco, luz pareja, mismo encuadre
   siempre. Con un celular decente y una caja de luz alcanza.
6. **No tener quién conteste.** Un WhatsApp visible que responde rápido convierte más que cualquier
   rediseño.
7. **Prometer envíos que no se pueden cumplir.** Mejor prometer 72 h y entregar en 48, que al revés.

---

## 11. Próximo paso inmediato

1. Que tu papá responda las **6 preguntas del Paso 0** (sobre todo la #1: dónde vive el stock).
2. **Registrar el dominio `.com.uy`** — hoy mismo, cuesta poco.
3. Pedir demo y cotización a **Fenicio**, y en paralelo abrir una prueba gratis de **Tiendanube** para
   comparar con algo tocable en la mano.
4. Elegir los **150–300 productos del lanzamiento** con el criterio de rotación + margen.

Con la respuesta a la #1 se define el resto del proyecto.
