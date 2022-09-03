<script>
  import { doubleSlide, doubleSlide_txt, drawLogo } from '../components/transitions/transitions';
  import { onMount } from 'svelte';
  import { top, bottom } from '../components/elements/LogoShape';
  import { fade } from 'svelte/transition';

  let delay1 = 200, delay2 = 750;

  let text_transition_visible = false;
  onMount(async () => {
    text_transition_visible = true;
  });

  function handleClick() {
    alert('Hi');
  }
</script>

<main class="page">
  {#if text_transition_visible}
    <svg version="1.1" xmlns="http://www.w3.org/2000/svg" width=130 height=130 viewBox="0 0 1000 1000" class="center-itself mb-7">
      <defs>
        <path id="logo-top" in:drawLogo="{{duration: 1600}}" d={top}/>
        <clipPath id="clip-top">
          <use xlink:href="#logo-top"/>
        </clipPath>
        <path id="logo-bottom" in:drawLogo="{{duration: 1600}}" d={bottom}/>
        <clipPath id="clip-bottom">
          <use xlink:href="#logo-bottom"/>
        </clipPath>
      </defs>
      <g>
        <use xlink:href="#logo-top" clip-path="url(#clip-top)" style="fill: transparent; stroke: white; stroke-width: 40;"/>
        <use xlink:href="#logo-bottom" clip-path="url(#clip-bottom)" style="fill: transparent; stroke: white; stroke-width: 40;"/>
        
        <path in:fade="{{delay: 1300, duration: 500}}" style="fill: white;" d={top}/>
        <path in:fade="{{delay: 1300, duration: 500}}" style="fill: white;" d={bottom}/>
      </g>
    </svg>

    <div class="center-itself container items-center mb-12">
        <div class="box" in:doubleSlide="{{delay: delay1}}"></div>
        <h1 class="page-title center-itself" in:doubleSlide_txt="{{delay: delay1}}">Crack 'n' Code Thailand</h1>
    </div>

    <div class="center-itself container items-center mb-2">
      <div class="box" in:doubleSlide="{{delay: delay2}}"></div>
      <h2 class="text-xl center-itself font-bold" in:doubleSlide_txt="{{delay: delay2}}">Next Contest</h2>
    </div>

    <div class="center-itself container items-center">
      <div class="box" in:doubleSlide="{{delay: delay2}}"></div>
      <p class="center-itself" in:doubleSlide_txt="{{delay: delay2}}">September 3, 2022 @ 19:00-22:00 (UTC+7)</p>
    </div>
    
    <button in:fade="{{delay: 1500, duration: 300}}" class="mt-10 py-2 px-4 rounded-lg uppercase font-medium bg-rose-600" on:click|once={handleClick}>
      Register
    </button>
  {/if}

  
</main>

<style lang="scss">

  .box {
    width: 100%;
    height: 100%;
    background-color: transparent;
    z-index: -1;
    position: fixed;
    left: 0%;
  }

  .container {
    width: fit-content;
    height: fit-content;
  }

  .center-itself {
    position: relative;
    transform: translateX(-50%);
    left: 50%;
  }
</style>
