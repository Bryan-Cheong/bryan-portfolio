<script>
  import Button from './Button.svelte';
  import { onMount, onDestroy } from 'svelte';
  import { browser } from '$app/environment';
  
  let { isPageLoaded = false } = $props();
  
  function scrollToNext() {
    // Build navigation order dynamically
    const projectSection = document.getElementById('projects');
    
    // Collect all project IDs dynamically
    const projectIds = [];
    if (projectSection) {
      let projectIndex = 0;
      while (true) {
        const projectElement = document.getElementById(`project-${projectIndex}`);
        if (projectElement) {
          projectIds.push(`project-${projectIndex}`);
          projectIndex++;
        } else {
          break;
        }
      }
    }
    
    // Build complete navigation order: intro > experience > projects > education > about > interests
    const sections = [
      'introPage',
      'experience',
      ...projectIds,
      'education',
      'about',
      'interests'
    ];
    
    const currentScroll = window.scrollY + window.innerHeight / 2; // Middle of viewport
    let currentIndex = -1;
    
    // Find which section we're currently in
    for (let i = 0; i < sections.length; i++) {
      const element = document.getElementById(sections[i]);
      if (element) {
        const rect = element.getBoundingClientRect();
        const elementTop = rect.top + window.scrollY;
        const elementBottom = elementTop + rect.height;
        
        if (currentScroll >= elementTop && currentScroll <= elementBottom) {
          currentIndex = i;
          break;
        }
      }
    }
    
    // If not found, find the closest section above current scroll
    if (currentIndex === -1) {
      for (let i = sections.length - 1; i >= 0; i--) {
        const element = document.getElementById(sections[i]);
        if (element) {
          const rect = element.getBoundingClientRect();
          const elementTop = rect.top + window.scrollY;
          
          if (currentScroll >= elementTop) {
            currentIndex = i;
            break;
          }
        }
      }
    }
    
    // Scroll to next section
    const nextIndex = currentIndex + 1;
    if (nextIndex < sections.length) {
      const nextSection = document.getElementById(sections[nextIndex]);
      if (nextSection) {
        nextSection.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    }
  }
  
  function handleKeyDown(event) {
    // Only trigger if spacebar is pressed and not in an input/textarea
    if (event.code === 'Space' && event.target.tagName !== 'INPUT' && event.target.tagName !== 'TEXTAREA') {
      event.preventDefault();
      scrollToNext();
    }
  }
  
  onMount(() => {
    if (browser) {
      window.addEventListener('keydown', handleKeyDown);
    }
  });
  
  onDestroy(() => {
    if (browser) {
      window.removeEventListener('keydown', handleKeyDown);
    }
  });
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
  
  /* Scroll indicator arrow */
  .scroll-indicator {
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%) translateY(-5px);
    opacity: 0;
    transition: opacity 0.5s ease-out 0.4s, transform 0.5s ease-out 0.4s;
  }
  
  .scroll-indicator.loaded {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  
  .scroll-arrow {
    animation: bounce 2s infinite;
    cursor: pointer;
    transition: opacity 0.2s ease;
  }
  
  .scroll-arrow:hover {
    opacity: 0.7;
  }
  
  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translateY(0);
    }
    40% {
      transform: translateY(-6px);
    }
    60% {
      transform: translateY(-3px);
    }
  }
</style>

<section id="introPage" class="w-full max-w-3xl mx-auto flex flex-col justify-center px-[clamp(1rem,5vw,2.5rem)] relative" style="min-height: calc(100vh - var(--navbar-height, 70px) - 3rem);">
  <!-- Text content -->
  <div class="flex flex-col gap-[clamp(1.5rem,4vw,2.5rem)] -mt-[clamp(2rem,5vh,4rem)]">
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
        variant="secondary"
        icon="fa-regular fa-envelope text-sm"
      >
        Contact Me
      </Button>
      
      <Button 
        href="/assets/CV.pdf"
        target="_blank"
        variant="primary"
        icon="fa-solid fa-download text-sm"
        class="vwo-cv-cta"
      >
        Download CV
      </Button>
    </div>
  </div>
  
  <!-- Scroll Indicator Arrow -->
  <div class={`scroll-indicator ${isPageLoaded ? 'loaded' : ''} pb-16 flex flex-col items-center gap-2`}>
    <button 
      onclick={scrollToNext}
      class="scroll-arrow text-[var(--color-text-muted)] opacity-50"
      aria-label="Scroll to next section"
    >
      <i class="fa-solid fa-chevron-down text-lg"></i>
    </button>
    <span class="text-xs text-[var(--color-text-muted)] opacity-40">Press space to learn more</span>
  </div>
</section>