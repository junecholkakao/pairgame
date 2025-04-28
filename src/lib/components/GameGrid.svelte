<script>
    // 카드 데이터
    const card_data = [
    {
      id: 0,
      name: 'html',
      imgUrl: 'images/html.png',
    },
    {
      id: 1,
      name: 'css',
      imgUrl: 'images/css.png',
    },
    {
      id: 2,
      name: 'js',
      imgUrl: 'images/js.png',
    },
    {
      id: 3,
      name: 'react',
      imgUrl: 'images/react.png',
    },
    {
      id: 4,
      name: 'vue',
      imgUrl: 'images/vue.png',
    },
    {
      id: 5,
      name: 'svelte',
      imgUrl: 'images/svelte.png',
    },
    {
      id: 6,
      name: 'sass',
      imgUrl: 'images/sass.png',
    },
    {
      id: 7,
      name: 'github',
      imgUrl: 'images/github.png',
    },
    {
      id: 8,
      name: 'quest',
      imgUrl: 'images/quest.png',
    },
  ]

  // 카드 목록
  // id:카드번호, flipped: 뒤집혀진 상태, matched: 매칭된 상태
  let cards = [
    { id: 0, flipped: false, matched: false },
    { id: 0, flipped: false, matched: false },
    { id: 1, flipped: false, matched: false },
    { id: 1, flipped: false, matched: false },
    { id: 2, flipped: false, matched: false },
    { id: 2, flipped: false, matched: false },
    { id: 3, flipped: false, matched: false },
    { id: 3, flipped: false, matched: false },
    { id: 4, flipped: false, matched: false },
    { id: 4, flipped: false, matched: false },
    { id: 5, flipped: false, matched: false },
    { id: 5, flipped: false, matched: false },
    { id: 6, flipped: false, matched: false },
    { id: 6, flipped: false, matched: false },
    { id: 7, flipped: false, matched: false },
    { id: 7, flipped: false, matched: false },
  ]


  let open1 = null
  let open2 = null

  let isGameCleared = false

  function shuffle() {
    cards = cards.sort(()=> 0.5-Math.random())
  }

  function flipCard(i) {
    if (!cards[i].flipped) {
      // remember current pick as card 1 or 2 
      if (open2 !== null) 
        return
      else if (open1 !== null)
        open2 = i
      else 
        open1 = i

      cards[i].flipped = true;
      console.log ("flipped a card.")
      console.log( open1, open2)

      if (open1 !== null && open2 !== null && cards[open1].id === cards[open2].id ) {
        cards[open1].matched = true
        cards[open2].matched = true
        open1 = null
        open2 = null
      } else if (open2 !== null) {
        setTimeout(()=> {
          cards[open1].flipped = false
          cards[open2].flipped = false
          open1 = null
          open2 = null
        }, 500)
      }
    }

    if (cards.every(card=>card.matched)) isGameCleared = true
  }

  const startGame = () => {
    for (let i=0; i<cards.length; i++) {
      cards[i].flipped = false
      cards[i].matched = false
    }
    isGameCleared = false
    shuffle()
    shuffle()
  }

  startGame()
</script>
<h1>Game Grid</h1>
<ul class="game-grid">
  {#each cards as card, i}
  <li
    class={(card.flipped ? "card " : "card hidden ") + (card.matched ? "green_bg": "")}
    >
    <button
    on:click={()=>flipCard(i)} 
      >
      <img src={card_data[card.id].imgUrl} alt="">
    </button>
  </li>    
  {/each}
</ul>
<br>
<button 
class="btn itim-regular"
on:click={startGame}>restart</button>
<br>
<p>{isGameCleared}</p>

<style lang="scss">
  .game-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    list-style-type: none;
    grid-gap: 2%;
    padding: 10px;

    .card {
      background: #fff;
      aspect-ratio: 1 / 1;
      padding: 20%;
      border-radius: 18%;
      img {
        width: 100%;
        object-fit: contain;
        display: block;
        aspect-ratio: 1 / 1;
      }
    }

    .card.hidden {
      background: rgba(0,0,0,0.5);
      img {opacity: 0;}
      background-image: url('images/quest.png');
      background-repeat: no-repeat;
      background-size: 30%;
      background-position: center;
    }

    button {
      background: transparent;
      border: none;
    }

    .green_bg {
      background: rgb(255, 255, 0);
    }
  }
</style>