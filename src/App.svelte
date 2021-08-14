<script>
  let cells = Array.from({ length: 40 }).map((_, idx) => ({
    bg: '#fff',
    id: idx,
  }));

  let currentColor = '#000';

  const handleColorUpdate = (id) => (e) => {
    if (e.buttons === 1) {
      cells[id].bg = currentColor;
    }
  };

  const handleCurrentColorUpdate = (e) => {
    currentColor = e.target.value;
  };
</script>

<main>
  <input
    type="color"
    class="colorPicker"
    value={currentColor}
    on:change={handleCurrentColorUpdate}
  />
  <div class="box">
    {#each cells as cell (cell.id)}
      <!-- svelte-ignore a11y-mouse-events-have-key-events -->
      <div
        class="cell"
        on:mouseover|preventDefault={handleColorUpdate(cell.id)}
        on:contextmenu={(e) => e.preventDefault()}
        on:mousedown|preventDefault={handleColorUpdate(cell.id)}
        style="background-color: {cell.bg};"
      />
    {/each}
  </div>
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    flex-direction: column;
  }
  .box {
    display: grid;
    grid-template-columns: repeat(8, 1fr);
    grid-template-rows: repeat(5, 1fr);
    height: 60%;
    border: 1px solid #000;
    width: 70%;
  }

  .cell {
    border: 1px solid #000;
    transition: all 100ms linear;
    cursor: pointer;
  }

  .cell:hover {
    transform: scale(1.07);
  }

  .colorPicker {
    height: 5rem;
    width: 5rem;
    margin-bottom: 2rem;
    padding: 5px;
  }
</style>
