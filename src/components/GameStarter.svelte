<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  // your script goes here
  export let gameArray;
  const chooseAvatar = (id) => {
    dispatch("chooseAvatar", id);
  };
</script>

{#each gameArray as game (game.id)}
  <!-- content here -->
  <div
    style="border-color: {game.color}; top: {game.position.top}; left: {game
      .position.left}"
    class="cursor-pointer game-card bg-white rounded-full p-6 w-[150px] h-[150px] flex justify-center items-center border-8 absolute transform -translate-x-1/2 -translate-y-1/2"
    on:click={() => chooseAvatar(game.id)}
  >
    <img src={game.image} alt={game.name} class="w-16" />
  </div>
{/each}
