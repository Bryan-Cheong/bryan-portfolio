<script>
  import { browser } from '$app/environment';
  import { onMount } from 'svelte';
  
  let { title = "Section", id = undefined, children} = $props();
  let isVisible = $state(false);
  let sectionRef;
  
  onMount(() => {
    if (browser) {
      // Set up Intersection Observer to detect when section is in view
      const observer = new IntersectionObserver(
        (entries) => {
          if (entries[0].isIntersecting) {
            isVisible = true;
            observer.disconnect(); // Only need to detect once
          }
        },
        { threshold: 0.1 } // Fire when 10% of the element is visible
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

<section {id} class="mt-40 mb-16" bind:this={sectionRef}>
  <div class="max-w-[1400px] mx-auto px-[clamp(1rem,5vw,2.5rem)]">
    <div class="flex flex-col lg:flex-row gap-8">
      <!-- Left column: Sticky section title -->
      <div class={`lg:w-1/3 lg:sticky lg:top-24 self-start section-entrance title-entrance ${isVisible ? 'visible' : ''}`}>
        <div class="border-t-2 border-neutral-800 w-12 mb-4 pt-2"></div>
        <h2 class="text-[clamp(1.5rem,4vw,2.25rem)]">{title}</h2>
      </div>

      <!-- Right column: Content -->
      <div class={`lg:w-2/3 flex flex-col gap-12 section-entrance content-entrance ${isVisible ? 'visible' : ''}`}>
        {@render children()}
      </div>
    </div>
  </div>
</section>