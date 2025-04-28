<script>
  import GameGrid from "./GameGrid.svelte";
  import GameInfo from "./GameInfo.svelte";

  export let page
</script>

<main>
  <GameInfo/>
  <GameGrid/>

  <button 
  class="btn itim-regular"
  on:click={()=>page='title'}>Back to Home</button>
</main>

<style>
  main {
    text-align: center;
  }

  button {
    margin-top: 1rem;
    padding: 0.5rem 2rem;
    border-radius: 4px;
  }
</style>