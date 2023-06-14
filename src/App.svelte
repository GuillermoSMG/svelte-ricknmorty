<script>
  import Character from './lib/Character.svelte';

  let characters = [];
  let page = 1;
  async function loadCharacters() {
    const response = await fetch(
      `https://rickandmortyapi.com/api/character?page=${page}`
    );
    const data = await response.json();
    characters = data.results;
  }
  loadCharacters();

  function nextPage() {
    page++;
    loadCharacters();
  }

  function prevPage() {
    if (page > 1) {
      page--;
      loadCharacters();
    }
  }
</script>

<h1 class="title">Rick and Morty</h1>

<div class="container">
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>

  <div class="buttons-container">
    <button
      class="button"
      on:click={prevPage}
      disabled={page === 1}
    >
      Prev
    </button>
    <button
      class="button"
      on:click={nextPage}
    >
      Next
    </button>
  </div>
</div>
