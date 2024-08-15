<script>
  // your script goes here
  import close from "../assets/images/icon-close.svg";
  import rules from "../assets/images/image-rules.svg";
  import { fade } from "svelte/transition";
</script>

<div
  transition:fade
  class="overlay w-full fixed top-0 h-screen flex justify-center items-center"
>
  <div class="modal bg-white h-[400px] w-[80%] md:w-[500px] rounded-xl">
    <div class="modal-header flex justify-between items-center p-6 w-full">
      <h2 class="text-4xl font-bold uppercase text-[#062133]">Rules</h2>
      <button class="close-button" on:click>
        <img src={close} alt="close image" class="w-10" />
      </button>
    </div>
    <div class="modal-body">
      <img src={rules} alt="" />
    </div>
  </div>
</div>

<style>
  /* your styles go here */
  .overlay {
    background-color: rgba(0, 0, 0, 0.658);
    z-index: 999;
  }
  .modal {
    display: grid;
    place-items: center;
  }
</style>
