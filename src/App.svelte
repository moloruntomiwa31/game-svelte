<script>
  import NavBar from "./components/fixed/NavBar.svelte";
  import Footer from "./components/fixed/Footer.svelte";
  import Modal from "./components/Modal.svelte";
  import paper from "./assets/images/icon-paper.svg";
  import scissors from "./assets/images/icon-scissors.svg";
  import rock from "./assets/images/icon-rock.svg";
  import GameStarter from "./components/GameStarter.svelte";
  import Game from "./components/Game.svelte";
  import gameSets from "./components/stores/Games";

  let showModal = false;
  $: games = $gameSets;
  let result = "";
  let userScore = 0;

  const addModal = () => {
    showModal = !showModal;
  };

  const gameArray = [
    {
      id: 1,
      name: "paper",
      image: paper,
      color: "hsl(230, 89%, 62%)",
      position: { top: "30%", left: "40%" },
    },
    {
      id: 2,
      name: "scissors",
      image: scissors,
      color: "hsl(39, 89%, 49%)",
      position: { top: "30%", left: "60%" },
    },
    {
      id: 3,
      name: "rock",
      image: rock,
      color: "hsl(349, 71%, 52%)",
      position: { top: "65%", left: "50%" },
    },
  ];

  const computerChoice = () => {
    const random = Math.floor(Math.random() * 3) + 1;
    let computerAvatar = gameArray.find((game) => game.id === random);
    gameSets.update((game) => {
      return [...game, computerAvatar];
    });
    setTimeout(() => {
      determineWinner();
    }, 1500);
  };
  const chooseAvatar = (e) => {
    gameSets.update((game) => {
      return [...game, gameArray.find((game) => game.id === e.detail)];
    });
    setTimeout(() => {
      computerChoice();
    }, 1000);
  };
  const determineWinner = () => {
    const [userChoice, computerChoice] = games;
    if (userChoice.id === computerChoice.id) {
      result = "It's a tie!";
    } else if (
      (userChoice.id === 1 && computerChoice.id === 3) ||
      (userChoice.id === 2 && computerChoice.id === 1) ||
      (userChoice.id === 3 && computerChoice.id === 2)
    ) {
      result = "You win";
      userScore++;
    } else {
      result = "You lose";
    }
  };

  const playAgain = () => {
    gameSets.set([]);
    result = "";
  };
</script>

<NavBar {userScore} />
<main class="h-[60vh]">
  {#if showModal}
    <!-- content here -->
    <Modal on:click={addModal} />
  {/if}
  <div class="body {games.length ? 'flex-layout' : ''}">
    {#if !games.length}
      <!-- content here -->
      <GameStarter {gameArray} on:chooseAvatar={chooseAvatar} />
    {:else}
      <!-- content here -->
      <Game {result} on:click={playAgain} />
    {/if}
  </div>
</main>
<Footer on:click={addModal} />

<style>
  /* your styles go here */
  .body {
    background-image: url("./assets/images/bg-triangle.svg");
    background-repeat: no-repeat;
    background-position: center;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  .flex-layout {
    background-image: none;
    flex-direction: row;
    justify-content: space-around;
  }
</style>
