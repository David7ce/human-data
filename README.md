STATUS: active

# Ficha Biométrica Futurista

Frontend UI template (Svelte + Vite) that displays the important categories of
data linked to one person, as a set of neon "glowing card" panels: identity,
biometrics, health, finance & legal documents, contacts, location/activity,
and social profiles.

All data in `src/data/person.js` is fake/demo data for a fictional person —
this app is a UI template, it does not collect, store, or connect to any real
personal data source.

## Structure

- `src/data/person.js` — the data, grouped by category (`identity`,
  `biometric`, `health`, `finance`, `contacts`, `location`, `social`). Each
  group is a flat `{ label, value }[]` array consumed by `Section.svelte`.
- `src/App.svelte` — composes the categories into cards on a responsive grid
  (`repeat(auto-fit, minmax(320px, 1fr))`).
- `src/components/` — `GlowingCard` (panel chrome), `Avatar`, `Section`
  (generic label/value list, reused for every category).

## Dev

```
npm install
npm run dev
npm run build
```

## Adding a category

Add a `{ label, value }[]` array to `src/data/person.js`, then render it with
`<Section title="..." items={person.yourGroup} />` inside a `<GlowingCard>` in
`App.svelte`. No changes needed to `Section.svelte` — it's generic.
