# Relevamiento SuperGanga — qué preguntar y qué mirar

Guía para la conversación con el supervisor. Objetivo: salir con los datos que faltan para cerrar
el plan. **Tiempo estimado: 40 minutos, mejor en el local que con el local cerrado.**

Anotá las respuestas en este mismo archivo, abajo de cada pregunta.

---

## BLOQUE A — El sistema de gestión (lo más importante)

De acá sale si el stock se puede automatizar o no.

### A1. ¿Cómo se identifica el sistema?

No hace falta que él sepa el nombre técnico. Hay cuatro formas de averiguarlo, de la más fácil
a la menos:

1. **Mirar el ticket o la factura que sale de la caja.** Al pie suele figurar el nombre del
   software o del emisor de factura electrónica.
2. **Mirar la pantalla de la PC de caja.** El nombre del programa aparece en la barra de arriba
   o en el logo de la pantalla de inicio. Sacale una **foto a la pantalla** — con eso alcanza.
3. **Preguntarle al contador.** Sabe con qué emiten los CFE, seguro.
4. **Preguntar quién les da soporte técnico** cuando el sistema se cae. Esa empresa es la que lo
   instaló.

Nombres frecuentes en el comercio uruguayo, por si aparece alguno: **Zureo, Memory, Zeta Software,
Doria Sistemas, Facturapp, Bit, Real2B**. Si es Zureo, estamos en el mejor escenario.

> Respuesta:

### A2. ¿Cada artículo tiene su propio código de barras y precio en el sistema?

**Esta es la pregunta más importante de todo el relevamiento.** Muchos bazares cobran por rubro
("bazar $150", "juguetería $300") sin cargar cada artículo por separado. Si es así, **no existe
stock por artículo** y no hay nada que sincronizar: primero habría que crear el maestro de
artículos desde cero, que es un proyecto en sí mismo (meses de trabajo de mostrador).

Forma concreta de chequearlo: **buscar 3 artículos distintos en el sistema y ver si cada uno tiene
código, precio y cantidad propios.**

> Respuesta:

### A3. ¿El stock que dice el sistema coincide con lo que hay en el salón?

Preguntar: *¿cuándo fue el último inventario? ¿Cuánto se desvía normalmente?*

Si el sistema dice 8 y hay 3, publicar ese stock online genera cancelaciones. Un desvío grande
no frena el proyecto, pero obliga a poner un **colchón de seguridad** (ej. publicar disponible
solo si el sistema marca 3 o más).

> Respuesta:

### A4. ¿Se puede exportar el listado de artículos a Excel o CSV?

Casi todos los sistemas tienen un botón de exportar. Si sale un Excel con código, descripción,
precio y stock, ya tenemos con qué trabajar aunque no haya API.

> Respuesta:

---

## BLOQUE B — El catálogo y el negocio

### B1. ¿Cuántos artículos distintos hay en el local?
> Respuesta:

### B2. ¿Cuál es el ticket promedio de una venta en mostrador?
Define si el envío es viable. Si el ticket es de $300, hay que trabajar mucho en combos.
> Respuesta:

### B3. ¿Cuáles son los 20 artículos que más se venden?
> Respuesta:

### B4. ¿Cuáles son los de mejor margen?
No siempre coinciden con los anteriores. **Los que están en las dos listas son los del arranque.**
> Respuesta:

### B5. ¿Qué se vende que sea fácil de embalar y mandar?
Descartar: frágil, muy voluminoso, muy pesado, muy barato.
> Respuesta:

### B6. ¿Ya les pidieron alguna vez enviar al interior? ¿Cuántas veces?
Si ya hay demanda espontánea, es la mejor validación posible de que esto funciona.
> Respuesta:

---

## BLOQUE C — Operación (el cuello de botella real)

Las tiendas chicas no fracasan por la tecnología, fracasan porque **nadie tiene tiempo de atender
los pedidos**. Estas preguntas valen tanto como las del sistema.

### C1. ¿Quién va a preparar y despachar los pedidos, con nombre y horario?
> Respuesta:

### C2. ¿Quién contesta consultas de clientes, y en qué horario?
> Respuesta:

### C3. ¿Quién saca las fotos de los productos y cuántas puede hacer por día?
Con el celular alcanza si hay buena luz y fondo blanco. Es la tarea que más frena los lanzamientos.
> Respuesta:

### C4. ¿Tienen cajas, papel, cinta y balanza para embalar?
> Respuesta:

### C5. ¿Cuánto puede invertir por mes entre plataforma, dominio y publicidad?
> Respuesta:

---

## BLOQUE D — Administración

### D1. ¿Ya emiten factura electrónica? ¿Con qué proveedor?
> Respuesta:

### D2. ¿Qué dice el contador sobre facturar ventas web?
> Respuesta:

### D3. ¿Tienen cuenta de Mercado Pago a nombre de la empresa?
> Respuesta:

### D4. ¿Cuál es el nombre comercial exacto y la razón social?
Necesario para el dominio, la facturación y las redes. Confirmar también si ya existe algún
Instagram, Facebook, web o publicaciones en Mercado Libre — **aunque estén abandonados**.
> Respuesta:

---

## BLOQUE E — El otro local

Para cuando se dé la conversación. No bloquea el lanzamiento.

- ¿Quién decide ahí y qué relación hay?
- ¿Usan el mismo sistema de gestión?
- ¿Qué gana ese local si la web vende su stock? (sin respuesta clara a esto, no van a colaborar)
- ¿Quién despacha si el artículo está allá?

> Respuesta:

---

## Mientras tanto: lo que se puede hacer YA

Nada de esto depende de las respuestas de arriba. Se puede arrancar esta semana.

- [ ] **Confirmar el nombre comercial exacto** y comprar el dominio (`.com.uy` o `.uy`)
- [ ] Contratar **Google Workspace** y crear `ventas@` (no usar un Gmail personal para esto)
- [ ] **Cotizar envíos** a DAC, UES y Correo Uruguayo (Ahíva) con un paquete tipo:
      *"caja de 30×30×30 cm, 2 kg, de Montevideo a Salto/Rivera/Maldonado — ¿cuánto sale y en
      cuánto llega?"*. Sin este número no se puede fijar el precio de envío.
- [ ] Abrir cuenta de **Mercado Pago** empresa si no existe
- [ ] Crear cuenta de prueba en **Tiendanube** y familiarizarse con el panel
- [ ] **Empezar a sacar fotos** de los productos candidatos — es lo que más tarda
- [ ] Redactar las **políticas**: envíos, cambios y devoluciones, tiempos de entrega
- [ ] Mirar **qué publican los competidores** en Mercado Libre: qué se vende, a qué precio, con qué
      costo de envío. Es investigación de mercado gratis.

---

## Cómo encarar la conversación

Un par de cosas que ayudan, sabiendo que es tu papá y que es el supervisor:

- **No arranques por la tecnología.** Arrancá por "¿qué es lo que más te frustra de las ventas
  hoy?". Las respuestas del Bloque B salen solas.
- **Lo del código de barras (A2) preguntalo mirando el sistema**, no de memoria. La respuesta
  "sí, está todo cargado" es optimista muy seguido, y es el dato que más caro sale equivocarse.
- **Las preguntas de operación (Bloque C) son incómodas** porque exponen que alguien va a tener
  que hacer trabajo nuevo. Mejor sacarlas ahora que en el mes 2.
- Si el Bloque A da mal (no hay artículos cargados), **no es el final del proyecto**: se lanza
  igual con 150 productos cargados a mano, y la automatización queda para más adelante.
