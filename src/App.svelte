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
  .group-title {
    text-align: center;
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 5px;
    margin: 0;
    color: #0ff;
    text-shadow: 0 0 8px #0ff;
  }
</style>

<div class="board">
  <GlowingCard>
    <Avatar src="{import.meta.env.BASE_URL}foto.jpg" alt="Foto de perfil" />
    <h2 class="neon-title">Juan Pérez Gómez</h2>
    <div class="id-card">CARNET: 1234-5678-90</div>

    <div class="group-title">BIOMÉTRICO Y SALUD</div>
    <Section title="DATOS BIOMÉTRICOS" items={person.biometric} />
    <Section title="SALUD" items={person.health} />

    <div class="group-title">IDENTIDAD Y DOCUMENTOS</div>
    <Section title="CONTACTOS" items={person.contacts} />
    <Section title="DATOS PERSONALES" items={person.identity} />
    <Section title="DOCUMENTOS Y FINANZAS" items={person.finance} />

    <div class="group-title">PRESENCIA DIGITAL</div>
    <Section title="REDES SOCIALES" items={person.social} />
    <Section title="UBICACIÓN Y ACTIVIDAD" items={person.location} />

    <div class="group-title">PSICOLOGÍA Y COMPORTAMIENTO</div>
    <Section title="COMPORTAMIENTO Y ENTRENAMIENTO" items={person.behavior} />
    <Section title="DATOS SENSIBLES" items={person.sensitive} />
    <Section title="PERFIL Y PERSONALIDAD" items={person.personality} />

    <div class="group-title">VIDA PERSONAL</div>
    <Section title="FAMILIA" items={person.family} />
    <Section title="MEMORIA Y BIOGRAFÍA" items={person.biography} />

    <div class="group-title">VIDA PROFESIONAL</div>
    <Section title="TRABAJO" items={person.work} />
  </GlowingCard>
</div>
