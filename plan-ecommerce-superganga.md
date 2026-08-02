# Plan de ecommerce — SuperGanga (bazares, Montevideo)

**Fecha:** 2026-08-02
**Para:** Luciano Carpio Mouret
**Cliente:** SuperGanga — 2 locales en Montevideo. Decisor operativo: el supervisor general (padre de Luciano).

**Restricciones reales del proyecto (confirmadas):**

| Variable | Estado |
|---|---|
| Sistema de stock actual | **Sin confirmar** → es la Etapa 0 |
| Presupuesto mensual | **Menos de $10.000 UYU/mes** (plataforma + mantenimiento + pauta) |
| Quién construye y mantiene | **Sin definir** → hay recomendación en este documento |
| Alcance de la v1 | **Montevideo primero**, interior en la etapa 2 |

---

## 1. La verdad incómoda antes de empezar

Hay que decirlo claro porque condiciona todo lo demás:

**El objetivo "que la página se actualice sola con el stock" es el objetivo más caro y más frágil de la lista.** No es un tema de la web: es un tema del sistema de gestión de los locales. Si el stock de SuperGanga vive en un ERP con base de datos (Zureo, Memory, Scanntech, Bsale), es un puente de software y se resuelve. Si vive en planillas de Excel que cada local actualiza cuando se acuerda, la sincronización automática va a reflejar datos falsos — y vender online algo que no está en depósito es peor que no tener web: es un cliente enojado, un reembolso y una reseña de 1 estrella.

**Regla que no se negocia:** la web nunca puede ser más confiable que el inventario que la alimenta. Primero el inventario, después el ecommerce.

Segundo punto: **con menos de $10.000 UYU/mes no se compite de frente con Electroventas ni DECOHogar.** Ellos están en Fenicio, con equipo y pauta. Eso no es un problema si el plan es el correcto — pero el plan correcto no es "hacer una tienda parecida a la de ellos". Es ocupar un espacio que ellos no ocupan y crecer reinvirtiendo las propias ventas. Más sobre esto en la sección 7.

Tercero: **el objetivo declarado es "aumentar ventas", pero los dos locales ya tienen problemas de ventas hoy.** Una web no arregla un problema de ventas: lo amplifica en un canal nuevo. Vale la pena que tu papá conteste, aunque sea para adentro: ¿las ventas bajaron por menos tráfico en la calle, por precios, por surtido, o porque la gente se fue a comprar online a otro lado? Si la respuesta es la última, este proyecto es exactamente la solución. Si es surtido o precio, la web sola no lo salva.

---

## 2. Lo que ya sabemos de las tres referencias (y qué copiar de cada una)

| Sitio | Plataforma | Qué copiarle |
|---|---|---|
| [Electroventas](https://electroventas.com.uy/) | **Fenicio** (confirmado: figura en su lista de clientes) | Envío gratis desde $2.000 · "Envíos flash, llega en 2 horas" en Montevideo · descuentos por tarjeta bien visibles |
| [TS Electrónica](https://tselectronica.com.uy/) | Muy probablemente Fenicio (URLs con `#/`) | Envío gratis desde $3.000 · **"Retiro en tienda en 1 hora"** · WhatsApp visible en el header |
| [Bazar del Cocinero](https://www.bazardelcocinero.com.uy/) | **WooCommerce** | Envío gratis desde $3.500 · categorías por uso (Coctelería, Repostería, Cuchillería) en vez de por proveedor · reseñas de clientes en la home |

**El patrón que comparten las tres y que hay que copiar sí o sí:** todas tienen un **umbral de envío gratis** ($2.000 / $3.000 / $3.500). No es casualidad ni generosidad. Un envío en Montevideo cuesta ~$200 y el ticket promedio de bazar anda por los $500-800. Sin umbral, el envío se come el margen o espanta al cliente. Con umbral, el cliente arma un carrito más grande para no pagarlo. **Es la palanca de rentabilidad más importante de todo el proyecto.**

**Dato de oro para vos, aparte:** DECOHogar —que ya está en tu CRM de prospección, con el contacto de Virginia— también usa Fenicio, igual que Divino, El Capitán, Prodeco y Bertoni. En el rubro hogar/bazar uruguayo, **Fenicio es el estándar de facto.** Guardate ese dato: te sirve para este proyecto y te sirve para prospectar.

---

## 3. ETAPA 0 — Descubrimiento (semana del 3 al 9 de agosto)

**Nada se decide hasta terminar esta etapa.** Es una semana, cuesta $0 y evita el error de $50.000.

### 3.1. Las preguntas exactas para hacer en el local

No se las hagas solo a tu papá: la persona que sabe de verdad es **quien factura y quien hace el inventario**. Andá con esta lista:

**Sobre el sistema:**
1. ¿Con qué programa se hace una factura acá? ¿Cómo se llama? (que te muestren la pantalla y sacá foto)
2. ¿Ese mismo programa descuenta el stock cuando se vende, o el stock se lleva aparte?
3. ¿Quién es el proveedor del sistema y hay alguien a quien llamar por soporte? ¿Cuánto se le paga por mes?
4. ¿El sistema puede **exportar** la lista de productos a Excel? (pedí que lo hagan delante tuyo y llevate el archivo — este archivo es el que decide todo)
5. ¿Los dos locales usan el mismo programa y la misma base, o cada uno la suya?

**Sobre la calidad del dato:**
6. ¿Todos los productos tienen código de barras o código interno? ¿El mismo código significa el mismo producto en los dos locales?
7. Si el sistema dice que hay 5 de un producto, ¿realmente hay 5? ¿Cuándo fue el último inventario físico?
8. ¿Cuántos productos distintos hay en total?
9. ¿Los precios están cargados y actualizados en el sistema, o se pisan a mano?

**Sobre la facturación:**
10. ¿La empresa emite **factura electrónica (CFE)**? ¿Con qué proveedor?

**Sobre la operativa:**
11. Si mañana entran 5 pedidos por día: ¿quién los arma, quién los embala y en qué momento del día?
12. ¿Hay cajas, bolsas, cinta, papel para embalar? ¿Hay lugar físico para dejar los pedidos armados?
13. ¿Quién contesta el WhatsApp hoy y cuánto tarda?

### 3.2. Las tres respuestas posibles y qué significa cada una

| Si el stock está en… | Significa | Camino |
|---|---|---|
| **ERP con base de datos** (Zureo, Memory, Scanntech, Bsale…) | Mejor escenario. Existe API o exportación programable. | Sincronización automática real. Es el objetivo cumplido. |
| **Excel / planillas** | Escenario intermedio, el más común. | Sincronización **semiautomática**: una planilla maestra + un script que la sube. Funciona bien si hay disciplina. |
| **Papel o "en la cabeza"** | El proyecto ecommerce **se pausa**. | Etapa previa: digitalizar el inventario. 2-4 semanas de trabajo antes de tocar la web. |

### 3.3. La otra conversación de la Etapa 0: el segundo local

Esto no es técnico y es el riesgo más subestimado del proyecto. Tu papá quiere vender stock de un local que **no gestiona**. Antes de escribir una línea de código, tienen que estar cerrados estos tres puntos, idealmente por escrito aunque sea en un WhatsApp:

- **¿El encargado del otro local está de acuerdo?** Si se entera cuando ya está la web hecha, la sabotea sin quererlo: no actualiza stock, no arma pedidos, no contesta.
- **¿De quién es la venta?** Si el local B pone el producto y la venta figura en el local A, el local B pierde plata y deja de colaborar en dos semanas. Definan la regla ahora: la venta online se acredita al local que despacha, o se reparte, o va a una unidad "online" aparte. Cualquiera sirve; la que no sirve es "ya lo vemos después".
- **¿Quién prepara el pedido si el producto está en el otro local?** ¿Se traslada a un local central, o despacha cada uno lo suyo?

**Sugerencia fuerte:** arrancá la v1 **solo con el stock del local de tu papá.** Menos productos, cero política interna, salís antes. Cuando la web venda y se vea, el otro local va a querer entrar solo — y ahí negociás desde otro lugar. Es mucho más fácil sumar un local a algo que funciona que convencerlo de algo que no existe.

---

## 4. Decisión de plataforma (con números reales)

### 4.1. Lo que se descarta y por qué

| Opción | Veredicto |
|---|---|
| **Fenicio** | Es la plataforma correcta para el rubro y la que usa la competencia. Integra con ERPs locales (Zureo homologado), medios de pago y cuotas uruguayas. **Pero está fuera del presupuesto de <$10.000/mes.** Pedí cotización igual — sirve para saber a dónde migrar en 2 años. |
| **Shopify** | Shopify Payments no opera en Uruguay → hay que usar pasarela externa **y encima Shopify cobra 0,5-2% extra por venta**. Además la e-factura DGI no es nativa. Pagás en dólares por features que no vas a usar. **Descartada.** |
| **Tiendanube** | **Ojo con esta.** En su página oficial de planes figuran Brasil, Argentina, México, Colombia y Chile — **Uruguay no aparece**. Hay agencias uruguayas que igual la ofrecen. Si alguien te la propone, exigí confirmación por escrito de tres cosas: que facturan a empresa uruguaya, que integra Mercado Pago **Uruguay**, y que conecta con un proveedor de e-factura DGI. Sin las tres, es un callejón sin salida. |

### 4.2. La recomendación: **WooCommerce**

Es exactamente lo que usa **Bazar del Cocinero**, una de las referencias que eligió tu papá — o sea, ya sabemos que el resultado visual que él quiere se logra con esto.

**Por qué gana en este caso concreto:**
- **Costo mensual casi nulo**: hosting USD 8-20/mes. Todo el resto del presupuesto queda libre para pauta, que es lo que genera ventas.
- **Sin comisión de plataforma** sobre cada venta (solo la de la pasarela de pago, que es inevitable).
- **Es de ellos.** No hay proveedor que se lleve la tienda si se pelean. Los datos, los clientes, el catálogo: propios.
- **Es donde Claude Code aporta valor de verdad**: el puente de stock con el ERP uruguayo no existe como plugin y hay que escribirlo. Ahí sí.
- **Tiene plugins uruguayos** para e-factura y para couriers, y todo el ecosistema WordPress detrás.

**El costo real de elegirla:** WooCommerce necesita mantenimiento (actualizaciones, backups, seguridad). No es "lo hago y me olvido". Eso nos lleva a la sección siguiente.

### 4.3. Quién la mantiene — mi recomendación

Respondiste "todavía no está definido". Definilo así: **la construís y la mantenés vos, con un contrato real, aunque sea tu papá.**

Tres razones:

1. **Tu propio pricing ya encaja en el presupuesto.** Tu tarifa es $10.000 UYU de implementación + $2.500 UYU/mes de mantenimiento. Entra holgado dentro del techo de $10.000/mes. Los números cierran solos.
2. **Cobrar no es un detalle: es lo que hace que el proyecto exista.** Un proyecto gratis para la familia es el primero que se abandona cuando aparece otra cosa. Uno facturado tiene fecha, alcance y obligación de las dos partes.
3. **Y la razón más importante:** SuperGanga es tu **primer caso de éxito documentado**. Tu CRM está lleno de bazares — Bazar News, Bazar El Tío, Bazar Los Tres, Gift Shop, Amatista, DECOHogar. Hoy los prospectás con un mensaje. En seis meses los prospectás con: *"le armé el ecommerce a SuperGanga, pasaron de vender solo en el mostrador a facturar X online, mirá"*. Eso cambia por completo tu tasa de respuesta.

**Blindá el bus factor desde el día 1** (es la objeción legítima de "y si Luciano no está"):
- Todos los accesos (dominio, hosting, Mercado Pago, Google) a nombre de **la empresa**, con el mail de la empresa. Nunca a tu nombre personal.
- Un documento de una carilla: dónde está cada cosa, con qué usuario, a quién llamar.
- Un video de 10 minutos grabado con el celular: cómo cargar un producto, cómo marcar un pedido como enviado. Con eso, cualquier persona del local sigue operando aunque vos no estés.

---

## 5. Cronograma por etapas

Fecha de referencia: **hoy, domingo 2 de agosto de 2026.** El objetivo es llegar con la tienda rodada a **Black Friday (última semana de noviembre)**, que es el pico del año en bazar y electro. Se llega bien, pero sin dormirse.

### Etapa 0 — Descubrimiento · semana del 3/8
Todo lo de la sección 3. **Entregable:** el Excel exportado del sistema + las 13 respuestas + el acuerdo sobre el segundo local.
**Puerta de control:** si el stock es papel, se para acá y se digitaliza primero.

### Etapa 1 — Fundaciones · semanas del 10/8 y 17/8
- Comprar el dominio (`superganga.com.uy` o el que esté libre) — **a nombre de la empresa**.
- Contratar hosting y levantar WooCommerce.
- Google Workspace con dominio propio (`ventas@superganga.com.uy`). Esto resuelve tu objetivo de "seguimiento por Gmail" bien hecho, en vez de un gmail personal.
- Confirmar/contratar proveedor de **e-factura DGI**.
- Abrir/verificar cuenta **Mercado Pago Uruguay** a nombre de la empresa.
- Definir el **umbral de envío gratis** (ver sección 6.2).

### Etapa 2 — Catálogo · semanas del 24/8 y 31/8
**Es la etapa que más trabajo lleva y la que todos subestiman.**
- Elegir los **primeros 100-200 productos**, no todo el catálogo. Criterio: los que más rotan, los que tienen mejor margen, y los que se embalan sin drama (nada de vajilla frágil ni cosas de 8 kg en la v1).
- Fotografiar esos productos. Ver sección 8 para el flujo con IA.
- Escribir títulos y descripciones. Título con formato: `Producto + marca + medida/capacidad` — así lo busca la gente en Google.
- Armar categorías **por uso, no por proveedor** (copiando a Bazar del Cocinero): Cocina, Repostería, Organización, Baño, Bazar escolar, Regalería.

### Etapa 3 — Sincronización de stock · semanas del 7/9 y 14/9
El puente entre el sistema del local y la web. La forma depende de lo que salga en la Etapa 0.
- **Con ERP:** script que consulta el ERP y actualiza WooCommerce cada 15-30 minutos.
- **Con Excel:** planilla maestra en Google Sheets + script que la sincroniza. Se define quién la actualiza y a qué hora.
- **En los dos casos, dos reglas de seguridad innegociables:**
  - **Colchón de stock:** si el sistema dice 3, la web muestra 1. Nunca vender la última unidad. Evita el 90% de los pedidos sin stock.
  - **Nunca vender en negativo:** si el stock llega a 0, el producto se marca "sin stock" solo, no se oculta (la página sigue posicionando en Google).

### Etapa 4 — Pagos, envíos y prueba · semanas del 21/9 y 28/9
- Conectar Mercado Pago y **probar con una compra real de $50** de punta a punta.
- Configurar zonas de envío: Montevideo (con umbral gratis), retiro en local, interior desactivado por ahora.
- Configurar los mails automáticos (sección 6.3).
- **Prueba en frío:** que 3 personas que no participaron del proyecto —una de ellas de más de 55 años— compren algo sin ayuda. Mirales la pantalla y anotá dónde se traban. Donde se traba una persona se traban cien.

### Etapa 5 — Lanzamiento suave · semana del 5/10
Abrir **sin anunciar todavía**. Vender a conocidos, clientes del mostrador y seguidores. Objetivo: 10-20 pedidos reales para descubrir los problemas de la operativa con público amigo.

### Etapa 6 — Lanzamiento con pauta · desde el 19/10
Recién acá se pone plata en Meta Ads. Sección 7.

### Etapa 7 — Black Friday · última semana de noviembre
Con la tienda ya rodada, seis semanas de operativa encima y el flujo aceitado.

### Etapa 8 — Interior del país · diciembre en adelante
Solo cuando Montevideo funcione solo.

---

## 6. Presupuesto real (en pesos uruguayos)

### 6.1. Costos

**Una sola vez (setup):**

| Concepto | Costo estimado |
|---|---|
| Dominio `.com.uy` (anual) | ~$1.500 – 2.500 |
| Implementación (tu trabajo) | $10.000 |
| Fotografía de producto | $0 si se hace con celular + IA (sección 8) |
| **Total arranque** | **~$12.000 – 13.000** |

**Mensual:**

| Concepto | Costo | Nota |
|---|---|---|
| Hosting | $400 – 800 | USD 8-20 |
| Proveedor e-factura DGI | $600 – 2.500 | **Pedí el crédito fiscal de DGI**: hasta 80 UI/mes (~$549) si la empresa facturó menos de 750.000 UI el ejercicio anterior. Puede dejarlo casi en cero. |
| Google Workspace | $0 – 500 | Se puede arrancar con el plan gratuito |
| Mantenimiento (tu trabajo) | $2.500 | |
| **Subtotal fijo** | **~$3.500 – 6.300** | |
| **Queda para pauta Meta** | **~$3.700 – 6.500** | Es poco pero alcanza para empezar |

**Costos variables por venta (no son gasto fijo, salen del margen):**
- **Mercado Pago:** ~4% a 6% + IVA según el plazo de acreditación que elijas. Cobrar a 14-21 días en vez de al instante te ahorra 1-2 puntos por venta — con márgenes de bazar, eso es mucha plata al año. *(Verificá el número exacto en tu panel: cambia.)*
- **Envío en Montevideo:** ~$200 estándar, ~$300 mismo día.
- **Envío al interior (etapa 2):** ~$250 en adelante según peso y destino.

### 6.2. La cuenta que define el umbral de envío gratis

Esta es **la cuenta más importante del proyecto**. Hacela con tu papá con números reales:

```
Ticket promedio del local:        $ ____
Margen bruto (%):                 ____ %
Ganancia por venta:               $ ____
Costo del envío:                  $ 200
Comisión Mercado Pago (~5%):      $ ____
──────────────────────────────────────────
Ganancia real de una venta online: $ ____
```

Si ese número da negativo o casi cero al ticket promedio actual, **el umbral de envío gratis no es opcional: es la única forma de que el canal sea rentable.** Regla práctica: poné el umbral en **2 a 3 veces el ticket promedio del local**. Las tres referencias lo tienen entre $2.000 y $3.500 — no lo eligieron al azar.

Debajo del umbral, el envío lo paga el cliente. Y siempre, siempre, ofrecé **retiro gratis en el local**: no cuesta nada, elimina el costo de envío de la ecuación, y —clave— mete a la persona adentro del local, donde compra otra cosa. TS Electrónica lo destaca en portada ("Retiro en tienda en 1 hora") justamente por eso.

### 6.3. El objetivo "seguimiento por Gmail", bien resuelto

Son dos cosas distintas y las dos se resuelven en la Etapa 4:

**Para el cliente** — mails automáticos desde `ventas@superganga.com.uy`, con cuatro momentos:
1. "Recibimos tu pedido #123" (inmediato, con el detalle)
2. "Tu pedido está en preparación"
3. "Tu pedido salió — llega hoy/mañana" (con código de seguimiento si aplica)
4. A los 7 días: "¿Cómo te fue con tu compra?" (pedido de reseña)

El paso 3 es el que más reduce los mensajes de "¿dónde está mi pedido?". Cada mail que mandás automático es un WhatsApp que alguien no tiene que contestar a mano.

**Para tu papá** — que todos los pedidos lleguen a una casilla de la empresa que puedan ver varias personas, con etiquetas por estado. Nada de que los pedidos caigan en el gmail personal de una sola persona: si esa persona está de licencia, se frena la operación.

---

## 7. La parte de ventas (lo que decide si esto funciona o no)

Una tienda nueva no tiene visitas. Ese es el motivo real por el que mueren estos proyectos: la web queda linda y no entra nadie. El plan de tráfico importa tanto como la web.

### 7.1. El orden correcto de las palancas

**1. La base de clientes que ya tienen (gratis, y es lo primero).**
Toda persona que compró en el mostrador ya confía en SuperGanga. Desde ahora, antes de que exista la web: **empezá a pedir el WhatsApp o el mail en la caja.** "¿Te mando las ofertas por WhatsApp?" Si en tres meses juntan 300 contactos, el día del lanzamiento tenés 300 personas a las que avisar gratis. Esto vale más que los primeros $10.000 de pauta y hay que arrancarlo **esta semana**, no en octubre.

**2. Google, gratis y permanente.**
Cada producto bien cargado es una página que puede aparecer cuando alguien busca "olla a presión Montevideo". Es tráfico que no se paga y no se apaga. Por eso los títulos importan (`Olla a presión Essen 6 litros`, no `Olla 6L`). Y **Google Business Profile** de los dos locales, con fotos y horarios: la búsqueda "bazar cerca mío" es tráfico regalado.

**3. Meta Ads (tu especialidad) — pero recién en la Etapa 6.**
No pongas un peso antes de que la tienda venda a conocidos. Con presupuesto chico, el orden es:
- **Primero remarketing**, no captación. Anunciarle a quien ya visitó la web es 5-10 veces más barato que buscar gente nueva. Para eso el **píxel de Meta tiene que estar instalado desde el día 1 de la Etapa 1**, aunque no haya pauta: necesita meses juntando datos antes de que sirva.
- **Segundo, catálogo dinámico.** Subís el feed de productos y Meta le muestra a cada persona el producto que miró. Es lo que mejor rinde en ecommerce y es exactamente lo que sabés hacer.
- **Tercero, captación fría** por intereses/geo Montevideo — recién cuando lo anterior funcione.
- Con ~$5.000/mes: **no dispares a todo el catálogo.** Elegí 5-10 productos "gancho" (buena foto, precio competitivo, fáciles de embalar) y concentrá ahí. Presupuesto chico repartido en 200 productos no aprende nada.

**4. WhatsApp Business — el canal más subestimado.**
En Uruguay muchísima gente quiere comprar online pero necesita preguntar antes. Botón de WhatsApp visible en toda la web, catálogo de WhatsApp Business sincronizado, respuestas rápidas guardadas. **Y algo que sé que aplica a tu caso:** tu propio dato de prospección dice que tu canal fuerte es el contacto directo — mensajes fríos ~3,6% de respuesta contra 33% en persona/teléfono. La misma lógica aplica a la venta de SuperGanga: **la web abre, la conversación cierra.** No diseñes la tienda como si el cliente fuera a comprar solo y en silencio. Diseñala para que le sea fácil preguntar.

### 7.2. Dónde puede ganar SuperGanga contra los grandes

No en precio ni en surtido. En estas tres:

- **Velocidad en Montevideo.** Un bazar con local físico puede entregar hoy. Es la ventaja real contra cualquiera que despache de un depósito.
- **Retiro en el local en 1 hora.** Cero costo logístico, y el cliente entra al local.
- **Atención con nombre y apellido.** WhatsApp contestado por una persona que sabe del producto. Las cadenas grandes no pueden dar eso.

### 7.3. Métricas — solo 5, revisadas los lunes

Nada de dashboards. Cinco números en una planilla:

| Métrica | Qué mirar |
|---|---|
| Visitas a la web | ¿Entra gente? |
| Pedidos | El número que importa |
| Tasa de conversión (pedidos ÷ visitas) | Sano: **1-2%**. Si hay tráfico y no hay pedidos, el problema es la web o el precio, no la pauta |
| Ticket promedio online | ¿El umbral de envío gratis está funcionando? |
| Costo por venta (pauta ÷ pedidos) | Si supera la ganancia por venta, se está perdiendo plata en cada pedido |

**El primer objetivo no es facturar: es llegar a 20 pedidos reales.** Con 20 pedidos ya sabés dónde se rompe la operativa, qué se pregunta la gente y cuánto tarda armar un paquete. Recién ahí tiene sentido acelerar con plata.

---

## 8. Herramientas: dónde la IA suma de verdad y dónde no

### 8.1. Nano Banana (Gemini) — para las fotos. Acá suma muchísimo.

Es la herramienta de mayor impacto por peso del proyecto, porque **la foto del producto es el 80% de la decisión de compra online** y hoy las fotos que hay son fotos de celular en la góndola.

Flujo concreto de trabajo:
1. Fotografiá cada producto con el celular sobre una **cartulina blanca**, con luz de ventana, sin flash. 30 segundos por producto.
2. Pasala por Nano Banana para: recortar el fondo y dejarlo blanco puro, emparejar la iluminación, enderezar el producto.
3. Generá **imágenes de ambiente** ("esta cacerola sobre una mesada de cocina moderna") para las categorías y para los anuncios. Esto es lo que le da a la web el aspecto de las referencias que le gustan a tu papá.
4. Generá los **banners** de home y las imágenes de categoría.

**Dos reglas que no se rompen:**
- **La foto principal del producto tiene que mostrar el producto real, sin inventar nada.** Recortar fondo y corregir luz: sí. Agregarle detalles, cambiarle el color o mejorarle el acabado: **no**. Si llega algo distinto a lo que se vio en la foto, es devolución, reseña mala y un cliente perdido para siempre. Las imágenes generadas van en banners y ambientaciones, siempre distinguibles de la foto de producto.
- **Todas las fotos, mismo encuadre y mismo fondo.** La prolijidad de una grilla de catálogo viene de la consistencia, no de que cada foto sea espectacular.

### 8.2. Claude Code — sí para esto, no para aquello

**Donde aporta valor real:**
- **El puente de sincronización de stock.** Es la joya del proyecto: no existe un plugin que conecte un ERP uruguayo con WooCommerce. Hay que escribirlo, y es exactamente la clase de trabajo donde rinde.
- **Carga masiva del catálogo**: transformar el Excel exportado del sistema en el CSV que WooCommerce importa, limpiando y normalizando por el camino. Ahorra semanas de tipeo.
- **Personalización del theme**: dejar la web con la cara de las referencias.
- **Integraciones**: e-factura, couriers, feed de productos para Meta.
- **Reportes** automáticos de ventas para tu papá.

**Donde NO conviene usarlo:**
- **Construir el motor de ecommerce desde cero.** Carrito, checkout, gestión de usuarios, seguridad de pagos: todo eso ya está resuelto y probado por millones de tiendas en WooCommerce. Reescribirlo son cuatro meses de trabajo para llegar a algo peor, y con datos de pago de por medio, "peor" significa riesgo real. Usá lo que existe y poné el esfuerzo donde no existe nada.

### 8.3. Otras

- **Google Sheets** como planilla maestra de productos si no hay ERP.
- **Google Analytics 4 + Meta Pixel**, instalados en la Etapa 1 aunque no se miren hasta la 6.
- **WhatsApp Business** (gratis) con catálogo y respuestas rápidas.

---

## 9. Riesgos, ordenados por probabilidad de que pasen

| # | Riesgo | Qué tan probable | Cómo se mitiga |
|---|---|---|---|
| 1 | **Se vende algo que no hay en stock** | Alta | Colchón de stock (nunca vender la última unidad) + inventario físico antes de arrancar |
| 2 | **El catálogo queda desactualizado** porque nadie lo mantiene | Alta | Una persona responsable con nombre y apellido + 30 min fijos por semana en la agenda |
| 3 | **Nadie entra a la web** | Alta | Empezar a juntar contactos en la caja YA + plan de tráfico de la sección 7 |
| 4 | **El segundo local no colabora** | Media-alta | Acuerdo previo por escrito, o arrancar solo con un local |
| 5 | **El envío se come el margen** | Media | Umbral de envío gratis + retiro en local + no vender productos pesados en la v1 |
| 6 | **Se abandona a los 3 meses** por falta de resultados | Media | Expectativa realista desde el día 1: los primeros 6 meses son de construcción, no de ganancia |
| 7 | **La web se cae o la hackean** | Baja | Backups automáticos diarios + actualizaciones mensuales (parte del mantenimiento) |

**El riesgo #6 merece un párrafo aparte.** Que tu papá entienda esto antes de empezar evita el peor final posible: un ecommerce nuevo tarda entre 6 y 12 meses en ser un canal de venta serio. Los primeros meses se factura poco y se aprende mucho. Si la expectativa es "en noviembre facturamos como el local", el proyecto se cancela en enero justo cuando estaba por empezar a rendir. **La expectativa correcta para 2026 es: la tienda existe, funciona, vende algo todos los días y llegó a Black Friday rodada. Facturar en serio es 2027.**

---

## 10. Qué hacer esta semana (del 3 al 9 de agosto)

Cinco cosas, ninguna cuesta plata:

1. **Ir al local con las 13 preguntas de la sección 3.1** y volver con el Excel exportado del sistema.
2. **Tener la conversación del segundo local** con tu papá (sección 3.3) y decidir si la v1 sale con uno o con dos.
3. **Hacer la cuenta de la sección 6.2** con el ticket promedio y el margen reales.
4. **Empezar a juntar contactos en la caja hoy mismo.** "¿Te mando las ofertas por WhatsApp?" No requiere web, no requiere nada, y en octubre vale oro.
5. **Chequear si `superganga.com.uy` está libre** en nic.com.uy y reservarlo antes de que lo tome otro.

Con el Excel del sistema y las respuestas en la mano, se define plataforma, alcance de la v1 y cronograma cerrado.
