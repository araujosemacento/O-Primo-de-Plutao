<script>
  let { spotlightPos, radius } = $props();

  let maskImage = $derived(`radial-gradient(circle ${radius}px at ${spotlightPos.x}px ${spotlightPos.y}px, transparent 100%, black 100%)`);
</script>

<div
  class="absolute top-0 left-0 w-full h-full bg-zinc-950/75 pointer-events-none z-10 backdrop-blur-lg"
  style:mask-image={maskImage}
  style:-webkit-mask-image={maskImage}
>
  <div class="flex flex-col items-center justify-center h-full text-zinc-800 pointer-events-none select-none"></div>
</div>
