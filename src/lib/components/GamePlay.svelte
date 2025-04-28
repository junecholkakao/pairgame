<script>
  import GameGrid from "./GameGrid.svelte";
  import GameInfo from "./GameInfo.svelte";

  export let page
  export let goHome
  let elapsed = 0
</script>

<main>
  <GameInfo {elapsed}/>
  <GameGrid bind:elapsed {goHome}/>

  <button 
  class="btn itim-regular"
  on:click={goHome}>그만하기</button>
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