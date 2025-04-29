<script>
  import GamePlay from "./lib/components/GamePlay.svelte";
  import GameScore from "./lib/components/GameScore.svelte";
  import GameTitle from "./lib/components/GameTitle.svelte";

  const gameTitle = "폭싹 속았수다"
</script>

<svelte:head>
	<title>{gameTitle}</title>
</svelte:head>  

<main>
<GameTitle title={gameTitle}/>
</main>

<style>

</style>
