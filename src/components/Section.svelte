<script>
  export let title = "";
  export let items = [];
</script>

<style>
  .section-title {
    font-weight: 700;
    font-size: 1.1rem;
    letter-spacing: 3px;
    margin-bottom: 12px;
    color: #ff00ff;
    border-bottom: 2px solid #ff00ff;
    padding-bottom: 6px;
    text-shadow: 0 0 10px #ff00ff;
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
  <div class="section-title">{title}</div>
  <ul>
    {#each items as item}
      <li><span>{item.label}:</span> {item.value}</li>
    {/each}
  </ul>
</section>
