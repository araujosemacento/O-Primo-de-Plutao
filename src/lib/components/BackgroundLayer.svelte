<script>
  let { spotlightPos } = $props();

  let innerWidth = $state(0);
  let innerHeight = $state(0);

  let isPortrait = $derived(innerHeight > innerWidth);

  let parallaxValue = $derived((innerHeight > 0 && innerWidth > 0) ? (isPortrait
    ? (spotlightPos.y / innerHeight) * -200
    : (spotlightPos.x / innerWidth) * -200) : 0);

  let style = $derived(isPortrait
    ? `width: 100%; height: 300vh; transform: translateY(${parallaxValue}vh); flex-direction: column; background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 15%, #312e81 30%, #4338ca 45%, #4f46e5 60%, #6366f1 75%, #818cf8 90%, #a5b4fc 100%);`
    : `width: 300vw; height: 100%; transform: translateX(${parallaxValue}vw); flex-direction: row; background: linear-gradient(45deg, #0f172a 0%, #1e1b4b 15%, #312e81 30%, #4338ca 45%, #4f46e5 60%, #6366f1 75%, #818cf8 90%, #a5b4fc 100%);`);

  let itemClass = $derived(isPortrait
    ? "w-full h-[100vh] flex items-center justify-center pointer-events-none opacity-20"
    : "w-[100vw] h-full flex items-center justify-center pointer-events-none opacity-20");
</script>

<svelte:window bind:innerWidth bind:innerHeight />

<div
  class="absolute top-0 left-0 transition-transform duration-300 ease-out flex"
  {style}
>
  <div class={itemClass}>
    <span class="text-white text-6xl md:text-9xl font-black select-none">
      VOIDS
    </span>
  </div>
  <div class={itemClass}>
    <span class="text-white text-6xl md:text-9xl font-black select-none">
      BEYOND
    </span>
  </div>
  <div class={itemClass}>
    <span class="text-white text-6xl md:text-9xl font-black select-none">
      LIGHT
    </span>
  </div>
</div>
