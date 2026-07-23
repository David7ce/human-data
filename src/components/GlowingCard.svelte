<script>
  export let className = "";
</script>

<style>
  .card {
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    gap: 24px;
    background: rgba(10, 10, 26, 0.85);
    border: 2px solid #0ff;
    border-radius: 16px;
    box-shadow:
      0 0 8px #0ff,
      0 0 20px #0ff;
    width: 100%;
    padding: 30px 28px 40px;
    position: relative;
    color: #0ff;
  }
  .card::before,
  .card::after {
    content: "";
    position: absolute;
    border: 1.5px solid #ff00ff;
    border-radius: 12px;
    top: -12px;
    left: -12px;
    right: -12px;
    bottom: -12px;
    opacity: 0.2;
    filter: drop-shadow(0 0 4px #ff00ff);
    animation: pulseGlow 3s ease-in-out infinite alternate;
  }
  .card::after {
    border-color: #0ff;
    top: -24px;
    left: -24px;
    right: -24px;
    bottom: -24px;
    animation-delay: 1.5s;
  }
  @keyframes pulseGlow {
    0%, 100% { opacity: 0.15; }
    50% { opacity: 0.35; }
  }
</style>

<div class="card {className}">
  <slot />
</div>
