<script>
  import GamePlay from "./GamePlay.svelte";
  import GameScore from "./GameScore.svelte";

  export let title;
  let page = "title";
  const goHome = () => page = "title"
</script>

<main>
  {#if page === "title"}
    <section class="itim-regular">
      <h1>{title}</h1>

      <h2>당신 덕에 나 인생이 만날 봄이었습니다</h2>
      <h2>다시 만날 봄까지</h2>
      <h2>만날 봄인 듯 살겠습니다</h2>
      
      <div class="btn-group">
        <button class="btn" on:click={()=>page='play'}>시작</button>
        <!-- <button class="btn" on:click={()=>page='score'}>Score</button> -->
      </div>
    </section>
  {:else if page === "play"}
    <GamePlay bind:page {goHome}/>
  {:else if page === "score"}
    <GameScore bind:page/>
  {/if}
</main>

<style>
  section {
    h1 {
      font-size: 12vw;
      color: #b3d1a5;
      -webkit-text-stroke: 10px rgb(0,0,0,0.7);
      paint-order: stroke fill;
      margin: 40px auto;
    }
    h2 {
      font-size: 4vw;
      color: #d3d145;
      -webkit-text-stroke: 10px rgb(0,0,0,0.7);
      paint-order: stroke fill;
      padding: 10px 10px;
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
