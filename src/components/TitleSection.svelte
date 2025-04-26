<script>
  import { browser } from '$app/environment';
  import { onMount } from 'svelte';
  
  let { title = "Section", id = undefined } = $props();
  let isVisible = $state(false);
  let sectionRef;
  
  onMount(() => {
    if (browser) {
      const observer = new IntersectionObserver(
        (entries) => {
          if (entries[0].isIntersecting) {
            isVisible = true;
            observer.disconnect();
          }
        },
        { threshold: 0.1 }
      );
      
      if (sectionRef) {
        observer.observe(sectionRef);
      }
      
      return () => {
        if (sectionRef) observer.disconnect();
      };
    }
  });
</script>

<style>
  .section-entrance {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease-out, transform 0.5s ease-out;
  }
  
  .section-entrance.visible {
    opacity: 1;
    transform: translateY(0);
  }
  
  .title-entrance {
    transition-delay: 0.05s;
  }
  
  .content-entrance {
    transition-delay: 0.15s;
  }
</style>

<section {id} class="mt-40 mb-16 pt-6" bind:this={sectionRef}>
  <div class="max-w-[1400px] mx-auto px-[clamp(1rem,5vw,2.5rem)]">
    <div class={`section-entrance title-entrance ${isVisible ? 'visible' : ''}`}>
      <div class="border-t-2 border-neutral-800 w-12 mb-4 pt-2"></div>
      <h2 class="text-[clamp(1.5rem,4vw,2.25rem)] mb-12">{title}</h2>
    </div>
    <div class={`flex flex-col gap-12 section-entrance content-entrance ${isVisible ? 'visible' : ''}`}>
      <slot />
    </div>
  </div>
</section>