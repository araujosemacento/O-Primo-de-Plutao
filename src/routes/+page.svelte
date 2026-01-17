<script>
  import { onMount } from 'svelte';
  import BackgroundLayer from '$lib/components/BackgroundLayer.svelte';
  import OverlayLayer from '$lib/components/OverlayLayer.svelte';

  const SPOTLIGHT_RADIUS = 150;
  
  let position = $state({ x: 0, y: 0 });
  let isActive = $state(false);

  onMount(() => {
     if (typeof window !== 'undefined') {
       position = {
          x: window.innerWidth * 0.05,
          y: window.innerHeight * 0.05
       };
     }
  });

  function handlePointerMove(e) {
    if (isActive) {
      position = {
        x: Math.max(0, Math.min(e.clientX, window.innerWidth)),
        y: Math.max(0, Math.min(e.clientY, window.innerHeight))
      };
    }
  }

  function handleMouseDown() {
    isActive = true;
  }
</script>

<div
  class="relative w-full h-screen overflow-hidden bg-black font-sans text-white touch-none"
  role="button"
  tabindex="0"
  onpointermove={handlePointerMove}
  onmousedown={handleMouseDown}
>
  <!-- 1. Background Component: Wide Gradient -->
  <BackgroundLayer spotlightPos={position} />

  <!-- 2. Overlay Component: Dark clipping layer -->
  <OverlayLayer spotlightPos={position} radius={SPOTLIGHT_RADIUS} />
</div>
