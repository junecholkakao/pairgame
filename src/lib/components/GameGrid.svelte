<script>
  import Modal from "./Modal.svelte";

  export let goHome
  export let elapsed
  let touched = false
  let intervalId
  let startTimeStamp
  let milliseconds

    // 카드 데이터
    const card_data = [
    {
      id: 0,
      name: '오애순',
      imgUrl: 'images/aesun.jpg',
    },
    {
      id: 1,
      name: '양관식',
      imgUrl: 'images/guansik.jpg',
    },
    {
      id: 2,
      name: '나이 든 오애순',
      imgUrl: 'images/old_aesun.jpg',
    },
    {
      id: 3,
      name: '나이 든 양관식',
      imgUrl: 'images/old_guansik.jpg',
    },
    {
      id: 4,
      name: '부상길',
      imgUrl: 'images/sangkil.jpg',
    },
    {
      id: 5,
      name: '박영란',
      imgUrl: 'images/youngran.jpg',
    },
    {
      id: 6,
      name: '박충섭',
      imgUrl: 'images/chungsub.jpg',
    },
    {
      id: 7,
      name: '양은명',
      imgUrl: 'images/eunmyoung.jpg',
    },
    {
      id: 8,
      name: '부현숙',
      imgUrl: 'images/hyunsuk.jpg',
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
    { id: 8, flipped: false, matched: false },
    { id: 8, flipped: false, matched: false },
  ]


  let open1 = null
  let open2 = null

  let isGameCleared = false

  function shuffle() {
    cards = cards.sort(()=> 0.5-Math.random())
  }

  function flipCard(i) {
    if (!cards[i].flipped) {
      // remember current open cards 
      if (open2 !== null) 
        // two cards open. stop processing.
        return 
      else if (open1 !== null)
        // remember as second card
        open2 = i
      else 
        // remember as first card
        open1 = i

      // first click of the whole deck starts interval timer
      if (!touched) {
        touched = true
        startTimeStamp = Date.now()
        intervalId = setInterval(()=>{
          elapsed += 1
        }, 1000)
      }

      // open the card
      cards[i].flipped = true;
      console.log ("flipped a card.")
      console.log( open1, open2)

      if (open1 !== null && open2 !== null && cards[open1].id === cards[open2].id ) {
        // if two cards are the same kind, they are matched.
        cards[open1].matched = true
        cards[open2].matched = true
        open1 = null
        open2 = null
      } else if (open2 !== null) {
        // if second card is mismatched, start timer to close
        setTimeout(()=> {
          cards[open1].flipped = false
          cards[open2].flipped = false
          open1 = null
          open2 = null
        }, 500)
      }
    }

    if (cards.every(card=>card.matched)) {
      milliseconds = Date.now() - startTimeStamp
      isGameCleared = true
      clearInterval(intervalId)
    }
  }

  const restart = () => {
    for (let i=0; i<cards.length; i++) {
      cards[i].flipped = false
      cards[i].matched = false
    }
    isGameCleared = false
    shuffle()
    shuffle()

    elapsed = 0
    touched = false
  }

  restart()
</script>



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
{#if isGameCleared}
  <Modal {restart} {milliseconds} {goHome}/>
{/if}



<style lang="scss">
  .game-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    list-style-type: none;
    grid-gap: 2%;
    padding: 10px;
    margin-bottom: 40px;

    .card {
      background: #fff;
      aspect-ratio: 1 / 1;
      padding: 5%;
      border-radius: 14%;
      img {
        width: 100%;
        object-fit: contain;
        display: block;
        aspect-ratio: 1 / 1;
        border-radius: 10%;
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