<script>
  import { fade } from "svelte/transition";
  import gameSets from "./stores/Games";
  // your script goes here
  //   export let games;
  export let result;

  $: games = $gameSets;
  console.log(games);
  
</script>

{#each games as game, index (game.id + "-" + index)}
  <!-- content here -->
  <div class="picked">
    <h2 class="text-xl font-bold uppercase">
      {index === 0 ? "You Picked" : "House Picked"}
    </h2>
    <div
      style="border-color: {game.color};"
      class="game-card bg-white rounded-full p-6 w-[150px] h-[150px] flex justify-center items-center border-8"
    >
      <img src={game.image} alt={game.name} class="w-16" />
    </div>
  </div>
  {#if index === 0 && games.length === 2}
    <!-- content here -->
    <div class="result" transition:fade>
      <h2 class="text-2xl font-bold uppercase">{result}</h2>
      {#if result}
        <!-- content here -->
        <button class="play-again" on:click>Play Again</button>
      {/if}
    </div>
  {/if}
{/each}

<style>
  /* your styles go here */
  .picked {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 3rem;
  }
  .result {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }
  .play-again {
    padding: 0.5rem 1rem;
    background-color: white;
    color: red;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
</style>
