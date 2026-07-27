<script>
  export let title = "";
  export let items = [];

  let open = false;
</script>

<style>
  .section-title {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    width: 100%;
    background: none;
    border: none;
    border-bottom: 2px solid #ff00ff;
    margin: 0 0 12px;
    padding: 0 0 6px;
    font: inherit;
    font-weight: 700;
    font-size: 1.1rem;
    letter-spacing: 3px;
    text-align: left;
    color: #ff00ff;
    text-shadow: 0 0 10px #ff00ff;
    cursor: pointer;
  }
  .arrow {
    display: inline-block;
    transition: transform 0.15s ease;
  }
  .arrow.open {
    transform: rotate(90deg);
  }
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
    font-size: 1rem;
    line-height: 1.6;
    color: #0ff;
    text-shadow: 0 0 5px #0ff;
  }
  li {
    margin-bottom: 10px;
    position: relative;
    padding-left: 16px;
  }
  li::before {
    content: "▹";
    position: absolute;
    left: 0;
    color: #ff00ff;
    text-shadow: 0 0 8px #ff00ff;
  }
  span {
    font-weight: 700;
    color: #ff00ff;
    letter-spacing: 1.2px;
  }
</style>

<section>
  <button
    type="button"
    class="section-title"
    aria-expanded={open}
    on:click={() => (open = !open)}
  >
    {title}
    <span class="arrow" class:open>▸</span>
  </button>
  {#if open}
    <ul>
      {#each items as item}
        <li><span>{item.label}:</span> {item.value}</li>
      {/each}
    </ul>
  {/if}
</section>
