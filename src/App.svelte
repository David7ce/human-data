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
    <Avatar src="/foto.jpg" alt="Foto de perfil" />
    <h2 class="neon-title">Juan Pérez Gómez</h2>
    <div class="id-card">CARNET: 1234-5678-90</div>

    <Section title="DATOS PERSONALES" items={person.identity} />
    <Section title="DATOS BIOMÉTRICOS" items={person.biometric} />
    <Section title="PERFIL Y PERSONALIDAD" items={person.personality} />
    <Section title="COMPORTAMIENTO Y ENTRENAMIENTO" items={person.behavior} />
    <Section title="MEMORIA Y BIOGRAFÍA" items={person.biography} />
    <Section title="FAMILIA" items={person.family} />
    <Section title="SALUD" items={person.health} />
    <Section title="TRABAJO" items={person.work} />
    <Section title="DOCUMENTOS Y FINANZAS" items={person.finance} />
    <Section title="DATOS SENSIBLES" items={person.sensitive} />
    <Section title="CONTACTOS" items={person.contacts} />
    <Section title="UBICACIÓN Y ACTIVIDAD" items={person.location} />
    <Section title="REDES SOCIALES" items={person.social} />
  </GlowingCard>
</div>
