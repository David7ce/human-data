# Diseño: interfaz única + nuevas categorías de datos

## Contexto

`human-data` es un template de UI (Svelte + Vite) que muestra datos ficticios
de una persona demo en paneles "glowing card" neón. Actualmente son 4 cards
en un grid (`repeat(auto-fit, minmax(320px, 1fr))`), agrupando: identity+biometric,
health, finance, contacts+location+social.

## Objetivo

1. Convertir el layout de 4 cards en una sola interfaz (un solo panel, scroll
   vertical, sin grid de cards separadas).
2. Añadir categorías/campos que faltaban: huella dactilar, pareja/hijos/familia,
   ADN, datos bancarios, intereses, tipo de psicología, hobbies, descripción,
   clasificación despectiva (hippie/pijo/choni/gangster), firma manual,
   bienes inmuebles, curriculum vitae, espiritualidad, música favorita,
   trabajo actual, mascotas. (Contactos ya existía.)

## Layout

`App.svelte` envuelve avatar + nombre + carnet + **todas** las secciones dentro
de un único `<GlowingCard>`. Se elimina `.board` grid; el contenedor pasa a ser
una columna centrada (`max-width: 760px`, `margin: 0 auto`). No se crean
componentes nuevos — `Section.svelte` (lista genérica label/value) y
`GlowingCard.svelte` (chrome del panel) se reutilizan sin cambios.

Huella dactilar y firma manual se representan como campos de texto
(`{label, value}`) igual que el resto — sin SVG ni imágenes generadas.

## Categorías y orden final (`src/data/person.js`)

1. **identity** (DATOS PERSONALES) — existente + `Firma manual`
2. **biometric** (DATOS BIOMÉTRICOS) — existente + `Huella dactilar`, `ADN`
3. **personality** (PERFIL Y PERSONALIDAD) — nueva: `Descripción`,
   `Tipo de psicología`, `Espiritualidad`, `Intereses`, `Hobbies`,
   `Música favorita`, `Clasificación`
4. **family** (FAMILIA) — nueva: `Pareja`, `Hijos`, `Familia`, `Mascotas`
5. **health** (SALUD) — sin cambios
6. **work** (TRABAJO) — nueva: `Trabajo actual`, `Empleador` (movido desde
   `location`), `Curriculum Vitae`
7. **finance** (DOCUMENTOS Y FINANZAS) — existente + `Datos bancarios`,
   `Bienes inmuebles`
8. **contacts** (CONTACTOS) — sin cambios
9. **location** (UBICACIÓN Y ACTIVIDAD) — existente menos `Empleador`
10. **social** (REDES SOCIALES) — sin cambios

## Archivos afectados

- `src/data/person.js` — 3 arrays nuevos (`personality`, `family`, `work`),
  campos añadidos a `identity`, `biometric`, `finance`; `Empleador` movido de
  `location` a `work`.
- `src/App.svelte` — un solo `GlowingCard` con todas las `Section`, sin grid.

No cambios en `Section.svelte`, `GlowingCard.svelte`, `Avatar.svelte`.

## Fuera de alcance

Sin componentes nuevos, sin persistencia/backend, sin validación de datos
(sigue siendo data ficticia hardcodeada), sin tests (proyecto no los tiene).
