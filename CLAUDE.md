# Prospección de Clientes — Montevideo

Proyecto de prospección para **Luciano Carpio Mouret**: gestión de Meta Ads + funnels simples
para negocios locales (restaurantes, bazares, clínicas). Precios: $10.000 UYU implementación
+ $2.500 UYU/mes mantenimiento.

## Archivos

- `informe-prospeccion-montevideo.html` — dashboard/CRM con los 50 prospectos, scores y pipeline
- `prospectos-montevideo.json` — datos exportables (campo `estado_contacto`: Pendiente / Contactado / Respondió)

## Estilo de comunicación

- Léxico uruguayo (voseo: "tenés", "querés", "nomás"), nunca español de España ("estáis", "lleváis")
- Icebreakers: máx. 80 palabras, dato específico verificable, pregunta de curiosidad, CERO venta
- Regla de oro del primer contacto: "No vendes. ABRES conversación"
- Follow-ups a las 48-72 h, máximo 2 toques tras el inicial

## ⚠️ Lecciones aprendidas (errores a NO repetir)

1. **Nunca afirmar "no tiene web" o "no tiene email público" sin agotar la verificación.**
   Errores cometidos y corregidos por Luciano a mano:
   - **Estrecho** (Ciudad Vieja): se reportó "email no público" → SÍ tenía email público.
   - **Clínica Odontológica Las Torres**: se llegó a tratar como si no tuviera web → SÍ tiene web (odontolastorres.com).
   - **García Parrilla**: se analizó un dominio incorrecto (parrilladagarcia.com) → la web real es garcia.com.uy.
   - **DECOHogar**: se reportó "sin web" → es una cadena con web propia y píxel instalado.
   - **Primuseum**: se reportó "sin web" → tiene primuseum.com con email de contacto.
2. Antes de reportar un dato negativo, cruzar SIEMPRE: búsqueda del nombre + "email/contacto",
   la página /contacto del sitio, directorios locales (opina.com.uy, guiacomercial.uy, salimostour),
   Instagram/Facebook del negocio, y variantes de dominio (.com.uy, .uy, .com).
3. Un dato negativo erróneo en un mensaje de prospección quema al prospecto: el error lo ve el cliente.
4. Las webs "inestables" pueden ser caídas temporales del proxy de red: reintentar antes de afirmar.

## Pipeline actual (2026-07-08)

- Tanda 1 (redes, 2026-07-06): 10 contactados
- Tanda 2 (email, 2026-07-07): 15 contactados
- Respondieron: **Tandory** (usa Meitre; pivot = alimentar la agenda) y
  **Podología Total / Stella Pérez** (reunión propuesta jueves 14:00 o sábado 10:20 + diagnóstico gratis)
