<script>
  export let elapsed = 0
</script>

<header class="game-info itim-regular">
  <dl>
    <!-- <div class="score">
      <dt>Score</dt>
      <dd>999,999</dd>
    </div>
    <div class="round">
      <dt>Round</dt>
      <dd>99</dd>
    </div> -->
    <div class="time">
      <dt>시간</dt>
      <dd>{elapsed}</dd>
    </div>
  </dl>
</header>

<style lang="scss">
  .game-info {
    position: absolute;
    background: rgba(255, 255, 255, 0.5);
    left: 0;
    top: 0;
    width: 100vw;
    dl {
      display: block;
      margin: 10px auto;
      padding: 10px 30px;
      dt, dd {
        font-size: min(10vw, 44px);
      }
      .round , .time {
        text-align: center;
        color: #fff;
        -webkit-text-stroke: 6px rgba(0,0,0,1);
        paint-order: stroke fill;
        display: flex;
        justify-content: center;
        gap: 10%;
      }
      .score{
        color: #fff;
        text-shadow: 2px 2px #000
      }
    }
  }
</style>