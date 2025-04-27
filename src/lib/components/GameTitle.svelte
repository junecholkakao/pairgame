<script>
  import GamePlay from "./GamePlay.svelte";
  import GameScore from "./GameScore.svelte";

  export let title;
  let page = "title";
</script>

<main>
  {#if page === "title"}
    <section class="itim-regular">
      <h1>{title}</h1>
      <div class="btn-group">
        <button class="btn" on:click={()=>page='play'}>Start</button>
        <button class="btn" on:click={()=>page='score'}>Score</button>
      </div>
    </section>
  {:else if page === "play"}
    <GamePlay bind:page/>
  {:else if page === "score"}
    <GameScore bind:page/>
  {/if}
</main>

<style>
  section {
    h1 {
      font-size: 16vw;
      color: #ff3e00;
      -webkit-text-stroke: 10px rgb(0,0,0,0.5);
      paint-order: stroke fill;
    }
    text-align: center;
  }

  .btn-group {
    display: flex;
    flex-direction: column;
    margin-top: 40px;
    button {
      padding: 10px;
      font-size: 32px;
      background: transparent;
      border: none;
      &:hover {
        text-decoration: underline;
      }
    }
  }
</style>
