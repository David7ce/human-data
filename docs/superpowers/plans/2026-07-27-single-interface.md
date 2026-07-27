# Single Interface + New Data Categories Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the 4-card grid in this Svelte demo template with a single scrolling panel, and add the missing fake-data categories the user requested (fingerprint, family, DNA, banking, interests, psychology type, hobbies, description, derogatory classification, manual signature, real estate, CV, spirituality, favorite music, current job, pets).

**Architecture:** No new components. `src/data/person.js` gets 3 new exported arrays (`personality`, `family`, `work`) plus extra `{label, value}` entries on 3 existing arrays (`identity`, `biometric`, `finance`); `Empleador` moves from `location` to `work`. `src/App.svelte` renders every `Section` inside one `GlowingCard` instead of four, and the outer `.board` becomes a centered single column instead of a grid.

**Tech Stack:** Svelte 4, Vite 4. No test framework in this repo — verification is `npm run build` (catches Svelte/JS syntax errors) plus a visual check via `npm run dev`.

## Global Constraints

- All data stays fake/demo, per `README.md`: "this app is a UI template, it does not collect, store, or connect to any real personal data source." Do not name a real person or use real-looking sensitive values (no real IBAN/DNI patterns beyond what's already masked in the file).
- Keep every category as a flat `{ label, value }[]` array — `Section.svelte` is generic and must not need changes.
- Category order in `App.svelte` must match the approved spec: identity → biometric → personality → family → health → work → finance → contacts → location → social.
- Spec: `docs/superpowers/specs/2026-07-27-single-interface-design.md`.

---

### Task 1: Extend `src/data/person.js` with new categories and fields

**Files:**
- Modify: `src/data/person.js` (currently 53 lines, full file shown below in context)

**Interfaces:**
- Produces: named exports `identity`, `biometric`, `health`, `finance`, `contacts`, `location`, `social` (existing, some with added entries), plus new exports `personality`, `family`, `work` — all `{ label: string, value: string }[]`. Task 2 imports all of these via `import * as person from './data/person.js'` and reads `person.<name>`.

- [ ] **Step 1: Replace the full contents of `src/data/person.js`**

```javascript
// Fake/demo data for a fictional person — this app is a UI template,
// it does not collect or store real personal data.

export const identity = [
  { label: "Dirección", value: "Calle Neón 2077, Ciudad Cibernética" },
  { label: "Fecha de Nacimiento", value: "15/04/2090" },
  { label: "Nacionalidad", value: "Neo Española" },
  { label: "Sexo", value: "Masculino" },
  { label: "Firma manual", value: "Rúbrica registrada · patrón #FS-2231" },
];

export const biometric = [
  { label: "Altura", value: "1.75 m" },
  { label: "Peso", value: "72 kg" },
  { label: "Edad", value: "34 años" },
  { label: "Color de ojos", value: "Azul neón" },
  { label: "Color de cabello", value: "Plata metálico" },
  { label: "Huella dactilar", value: "Patrón dactilar #4471-B · índice derecho" },
  { label: "ADN", value: "Perfil genético #GX-88213 · archivado" },
];

export const personality = [
  { label: "Descripción", value: "Ingeniero curioso, introvertido, madrugador. Le gusta resolver problemas antes que el café se enfríe." },
  { label: "Tipo de psicología", value: "INTP · analítico-introvertido" },
  { label: "Espiritualidad", value: "Agnóstico, practica meditación" },
  { label: "Intereses", value: "Robótica, astronomía, criptografía" },
  { label: "Hobbies", value: "Ajedrez, ciclismo urbano, sintetizadores" },
  { label: "Música favorita", value: "Synthwave, IDM" },
  { label: "Clasificación", value: "Techie discreto (no hippie, no pijo, no choni, no gangster)" },
];

export const family = [
  { label: "Pareja", value: "María Pérez" },
  { label: "Hijos", value: "1 (Lucía, 6 años)" },
  { label: "Familia", value: "Padres residentes en Valencia · 1 hermano" },
  { label: "Mascotas", value: "Gato · \"Pixel\", 3 años" },
];

export const health = [
  { label: "Tipo de sangre", value: "O+" },
  { label: "Alergias", value: "Penicilina" },
  { label: "Medicación actual", value: "Ninguna" },
  { label: "Condiciones crónicas", value: "Ninguna" },
  { label: "Última revisión médica", value: "12/01/2026" },
  { label: "Contacto médico", value: "Dra. Ana Ruiz · +34 600 111 222" },
];

export const work = [
  { label: "Trabajo actual", value: "Ingeniero de Software Senior" },
  { label: "Empleador", value: "Neo Corp" },
  { label: "Curriculum Vitae", value: "12 años exp. · Ing. Informática (UPV) · CV-2026.pdf" },
];

export const finance = [
  { label: "DNI", value: "12345678-X · válido hasta 2030" },
  { label: "Pasaporte", value: "AB1234567 · válido hasta 2032" },
  { label: "Licencia de conducir", value: "Clase B · válida hasta 2029" },
  { label: "IBAN", value: "ES91 2100 •••• •••• •••• 0123" },
  { label: "Datos bancarios", value: "Cuenta corriente · saldo •••• 42.000 € · Banco Neo" },
  { label: "Bienes inmuebles", value: "Piso en Madrid (propietario) · Trastero" },
  { label: "Seguro médico", value: "Póliza #98234 · Sanitas" },
];

export const contacts = [
  { label: "Teléfono", value: "+34 600 123 456" },
  { label: "Email", value: "juan.perez@example.com" },
  { label: "Contacto de emergencia", value: "María Pérez · +34 600 654 321" },
];

export const location = [
  { label: "Ubicación actual", value: "Madrid, España" },
  { label: "Última actividad", value: "Hoy, 14:32" },
];

export const social = [
  { label: "GitHub", value: "@juanperez" },
  { label: "LinkedIn", value: "/in/juanperez" },
  { label: "X / Twitter", value: "@juanperez_dev" },
];
```

- [ ] **Step 2: Verify it's valid JS**

Run: `node --check src/data/person.js`
Expected: no output, exit code 0.

- [ ] **Step 3: Commit**

```bash
git add src/data/person.js
git commit -m "feat: add family, work, personality categories and extra fields to person data"
```

---

### Task 2: Collapse `App.svelte` into a single panel

**Files:**
- Modify: `src/App.svelte`

**Interfaces:**
- Consumes: `person.identity`, `person.biometric`, `person.personality`, `person.family`, `person.health`, `person.work`, `person.finance`, `person.contacts`, `person.location`, `person.social` (all produced by Task 1). Also consumes existing `GlowingCard`, `Avatar`, `Section` components — no changes to those files.

- [ ] **Step 1: Replace the full contents of `src/App.svelte`**

```svelte
<script>
  import GlowingCard from './components/GlowingCard.svelte';
  import Avatar from './components/Avatar.svelte';
  import Section from './components/Section.svelte';
  import * as person from './data/person.js';
</script>

<style>
  :global(body) {
    margin: 0;
    background: linear-gradient(135deg, #000015, #0a0a1a);
    font-family: 'Orbitron', monospace, 'Courier New', Courier, monospace;
    color: #0ff;
    min-height: 100vh;
    padding: 40px 20px;
  }

  .board {
    display: flex;
    justify-content: center;
    max-width: 760px;
    margin: 0 auto;
  }

  .neon-title {
    text-align: center;
    font-size: 1.9rem;
    letter-spacing: 2px;
    margin: 0 0 -12px;
    text-shadow: 0 0 8px #0ff;
  }
  .id-card {
    text-align: center;
    font-size: 1rem;
    letter-spacing: 4px;
    margin: 0;
    font-weight: 700;
    color: #ff00ff;
    text-shadow: 0 0 6px #ff00ff;
  }
</style>

<div class="board">
  <GlowingCard>
    <Avatar src="https://i.pravatar.cc/130?u=futuristic" alt="Foto de perfil futurista" />
    <h2 class="neon-title">Juan Pérez Gómez</h2>
    <div class="id-card">CARNET: 1234-5678-90</div>

    <Section title="DATOS PERSONALES" items={person.identity} />
    <Section title="DATOS BIOMÉTRICOS" items={person.biometric} />
    <Section title="PERFIL Y PERSONALIDAD" items={person.personality} />
    <Section title="FAMILIA" items={person.family} />
    <Section title="SALUD" items={person.health} />
    <Section title="TRABAJO" items={person.work} />
    <Section title="DOCUMENTOS Y FINANZAS" items={person.finance} />
    <Section title="CONTACTOS" items={person.contacts} />
    <Section title="UBICACIÓN Y ACTIVIDAD" items={person.location} />
    <Section title="REDES SOCIALES" items={person.social} />
  </GlowingCard>
</div>
```

- [ ] **Step 2: Build to verify no compile errors**

Run: `npm run build`
Expected: exits 0, `dist/` produced, no Svelte compiler errors about unknown props or unclosed tags.

- [ ] **Step 3: Manual visual check**

Run: `npm run dev`, open the printed local URL in a browser.
Expected: one glowing panel, all 10 section titles visible in the order listed above, no leftover grid/multiple-card layout, no console errors.

- [ ] **Step 4: Commit**

```bash
git add src/App.svelte
git commit -m "feat: collapse card grid into a single scrolling panel"
```
