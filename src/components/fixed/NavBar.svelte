<script>
  // your script goes here
  import logo from "../../assets/images/logo.svg";
  export let userScore;
</script>

<header class="min-w-full h-[30vh] flex justify-center items-center p-6">
  <div
    class="min-w-[400px] max-w-[600px] p-4 flex justify-between items-center border-4 rounded-xl"
  >
    <div class="image-wrapper">
      <img src={logo} alt="Image Logo" aria-hidden="true" />
    </div>

    <div
      class="bg-white grid place-content-center text-center p-4 rounded-xl w-[100px]"
    >
      <h2 class="uppercase font-bold text-[#062133] text-xs">Score</h2>
      <h1 class="font-extrabold text-6xl text-[#062133]">{userScore}</h1>
    </div>
  </div>
</header>

<style>
</style>
