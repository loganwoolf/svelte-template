<script lang="ts">
  let term: string = ''

  $: definition = getDefinition(term)


  async function getDefinition (term) {
    const response = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${term}`)
    const text = await response.text()
    console.log({text})
  }

  function clearTerm() {
    term = ''
  }
</script>

<header>
  <h1>Lightspeed Dictionary</h1>
  <p>Redefining fast on every keypress</p>
</header>
<main>
  <form class="form">
    <input bind:value={term} type="text" autocomplete="off">
    <button on:click={clearTerm} type="button">Clear</button>
  </form>
  <div class="result">
    {#await definition}

    {:then }

    {/await}
  </div>
</main>
<footer>
  <p>Made in 🍁 by Logan Woolf</p>
</footer>

<style>
</style>
