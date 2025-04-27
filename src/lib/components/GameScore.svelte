<script>
  export let page
</script>
<main>
  <h1 class="itim-regular">Game Score</h1>
  <div class="score">
    <p class="hi-score">Hi score: <span>999,999,999</span></p>
    <p class="your-score">Your score: <span>999,999</span></p>
  </div>
  <button 
  class="btn itim-regular"
  on:click={()=>page='title'}>Back to Home</button>
</main>
<style lang="scss">
  main {
    text-align: center;
    h1 {
      font-size: 12vw;
      color: #ff3e00;
      -webkit-text-stroke: 10px rgb(255,255,255,1);
      paint-order: stroke fill;
    }
    .score {
      font-size: 36px;
      font-weight: bold;
      margin: 70px 0;
      p { margin-bottom: 10px;}
    }
  }
</style>