<script>
  import Button from './Button.svelte';
  
  let { isPageLoaded = false } = $props();
</script>

<style>
  .intro-entrance {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease-out, transform 0.5s ease-out;
  }
  
  .intro-entrance.loaded {
    opacity: 1;
    transform: translateY(0);
  }
  
  /* Staggered animations with short delays */
  .intro-entrance-1 { transition-delay: 0.05s; }
  .intro-entrance-2 { transition-delay: 0.15s; }
  .intro-entrance-3 { transition-delay: 0.25s; }
</style>

<section id="introPage" class="w-full max-w-3xl mx-auto flex flex-col justify-center px-[clamp(1rem,5vw,2.5rem)]" style="min-height: calc(100vh - var(--navbar-height, 70px) - 3rem);">
  <!-- Text content -->
  <div class="flex flex-col gap-[clamp(1.5rem,4vw,2.5rem)] pb-[clamp(4rem,10vh,8rem)]">
    <h1 class={`text-[clamp(1.75rem,5vw,3.5rem)] text-left intro-entrance intro-entrance-1 ${isPageLoaded ? 'loaded' : ''}`}>
      Analytical. Adaptable. <br />
      Always Learning.
    </h1>
    <p class={`text-[clamp(1rem,2vw,1.25rem)] max-w-3xl text-left intro-entrance intro-entrance-2 ${isPageLoaded ? 'loaded' : ''}`}>
      I turn data into stories, models into strategy, and insight into action.
    </p>
    <!-- Call-to-Action Buttons -->
    <div class={`flex flex-wrap gap-[clamp(0.75rem,2vw,1rem)] justify-start mt-[clamp(0.5rem,1vw,0.75rem)] intro-entrance intro-entrance-3 ${isPageLoaded ? 'loaded' : ''}`}>
      <Button 
        href="mailto:wei.cheong24@imperial.ac.uk"
        variant="primary"
        icon="fa-regular fa-envelope text-sm"
      >
        Contact Me
      </Button>
      
      <Button 
        href="/assets/CV.pdf"
        target="_blank"
        variant="secondary"
        icon="fa-solid fa-download text-sm"
      >
        Download CV
      </Button>
    </div>
  </div>
</section>