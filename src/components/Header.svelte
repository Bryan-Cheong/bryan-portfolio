<script>
  import { browser } from '$app/environment';
  import { page } from '$app/stores';
  import UnderLineLink from './UnderLineLink.svelte';
  import { onMount } from 'svelte';
  
  let { y } = $props();
  let isMenuOpen = $state(false);
  let scrollProgress = $state(0);
  let activeSection = $state('');
  let isPageLoaded = $state(false);
  let navItemsLoaded = $state(false);
  
  let tabs = [
    {name: "Experience", link: "#experience", id: "experience"},
    {name: "Projects", link: "#projects", id: "projects"},
    {name: "Education", link: "#education", id: "education"},
    {name: "About", link: "#about", id: "about"}
  ];
  
  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  let animateHeaderTimeout;
  let animateNavTimeout;

  // Use a different approach for animation timing
  onMount(() => {
    if (browser) {
      console.log("Header component mounted");
      
      // Force animation with a different approach that should work reliably
      requestAnimationFrame(() => {
        animateHeaderTimeout = setTimeout(() => {
          console.log("Starting header animation");
          
          // IMPORTANT: Force a reflow before changing classes
          document.body.offsetHeight; 
          
          // Set a custom attribute for animation to avoid CSS conflicts
          document.querySelector('header').setAttribute('data-loaded', 'true');
          
          isPageLoaded = true;
          
          // Start nav items animation shortly after
          animateNavTimeout = setTimeout(() => {
            console.log("Starting nav items animation");
            navItemsLoaded = true;
          }, 100);
        }, 600);
      });
    }
    
    return () => {
      // Clean up timeouts to prevent memory leaks
      if (animateHeaderTimeout) clearTimeout(animateHeaderTimeout);
      if (animateNavTimeout) clearTimeout(animateNavTimeout);
    };
  });
  
  // Update scroll progress when y changes
  $effect(() => {
    if (browser) {
      scrollProgress = Math.min((y / (document.body.scrollHeight - window.innerHeight)) * 100, 100);

      // Check which section is in view
      const sections = tabs.map(tab => document.getElementById(tab.id));
      
      for (let i = 0; i < sections.length; i++) {
        const section = sections[i];
        if (section) {
          const rect = section.getBoundingClientRect();
          // If the section is in the viewport
          if (rect.top <= 150 && rect.bottom >= 150) {
            activeSection = tabs[i].id;
            break;
          }
        }
      }
      
      // Default to first section if we're at the top
      if (y < 100) {
        activeSection = '';
      }
    }
  });
</script>

<style> 
  header[data-loaded="true"] {
    opacity: 1 !important;
    transform: translateY(0) !important;
  }
  
  .header-entrance {
    opacity: 0;
    transform: translateY(-10px);
    transition: opacity 0.4s ease-out, transform 0.4s ease-out;
  }
  
  /* Add more specific selector to ensure it overrides */
  header.header-entrance.loaded {
    opacity: 1;
    transform: translateY(0);
  }
  
  .nav-item {
    opacity: 0;
    transform: translateY(-8px);
    transition: opacity 0.3s ease-out, transform 0.3s ease-out;
  }
  
  .nav-item.loaded {
    opacity: 1;
    transform: translateY(0);
  }
  
  .nav-item-1 { transition-delay: 0.05s; }
  .nav-item-2 { transition-delay: 0.1s; }
  .nav-item-3 { transition-delay: 0.15s; }
  .nav-item-4 { transition-delay: 0.2s; }
  .nav-item-5 { transition-delay: 0.25s; }
  
  /* Mobile menu item animations */
  @keyframes fadeInDown {
    from {
      opacity: 0;
      transform: translateY(-20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .animate-fade-in-down-0,
  .animate-fade-in-down-1,
  .animate-fade-in-down-2,
  .animate-fade-in-down-3,
  .animate-fade-in-down-4 {
    animation: fadeInDown 0.4s ease-out forwards;
  }
</style>

<header 
  class={"sticky z-[30] top-0 w-full transition-all duration-300 header-entrance " + (
    isPageLoaded ? "loaded " : ""
  ) + (
    y > 0 ? " py-[clamp(1rem,1vw,1.5rem)] bg-stone-200/95 backdrop-blur-sm border-neutral-800" : "py-[clamp(1rem,1vw,1.5rem)] bg-transparent border-transparent"
  )}
  data-loaded={isPageLoaded ? "true" : "false"}
>
  <div class="max-w-[1400px] mx-auto px-[clamp(1rem,5vw,2.5rem)] flex items-center justify-between">
    <!-- Logo with hover effect -->
    <a href="/" class="relative h-auto overflow-hidden flex items-center group">
      <div class="relative">
        <h1 class="text-[clamp(1.1rem,3vw,1.5rem)]">
          Bryan<span class="text-blue-900 ml-1 relative overflow-hidden inline-flex w-[clamp(8rem,24vw,11rem)]">
            <span class="transform transition-transform duration-500 group-hover:-translate-y-full whitespace-nowrap">Cheong</span>
            <span class="absolute transform transition-transform duration-500 translate-y-full group-hover:translate-y-0 whitespace-nowrap">&mdash;&thinsp;Data Analyst</span>
          </span>
        </h1>
      </div>
    </a>

    <div class="flex items-center gap-6">
      <nav aria-label="Main navigation" class="md:flex items-center gap-6 hidden">
        {#each tabs as tab, i}
          <div class={`nav-item nav-item-${i+1} ${navItemsLoaded ? 'loaded' : ''}`}>
            <UnderLineLink 
              href={tab.link} 
              text={tab.name} 
              className={activeSection === tab.id ? 'text-blue-900 nav-active' : ''}
            />
          </div>
        {/each}
      </nav>

      <button onclick={toggleMenu} 
              class="md:hidden relative z-[35] w-7 h-7 focus:outline-none p-1 cursor-pointer flex items-center justify-center" 
              aria-label="Menu">
        <div class="relative w-5 h-4">
          <!-- Hamburger Icon -->
          <span class={`absolute h-0.5 w-5 bg-neutral-800 transform transition-all duration-300 ${isMenuOpen ? 'rotate-45 top-[7px]' : 'top-0'}`}></span>
          <span class={`absolute h-0.5 w-5 bg-neutral-800 top-[7px] transform transition-all duration-300 ${isMenuOpen ? 'opacity-0' : 'opacity-100'}`}></span>
          <span class={`absolute h-0.5 w-5 bg-neutral-800 transform transition-all duration-300 ${isMenuOpen ? '-rotate-45 top-[7px]' : 'top-[14px]'}`}></span>
        </div>
      </button>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 h-[3px] bg-blue-900 transition-all duration-300" 
       style={`width: ${scrollProgress}%`}></div>
</header>

<div class={"fixed inset-0 pt-16 bg-stone-200/95 z-[25] md:hidden flex flex-col items-center justify-center gap-8 " + 
  (isMenuOpen ? "opacity-100 pointer-events-auto" : "opacity-0 pointer-events-none") + 
  " transition-opacity duration-300"}>
  {#each tabs as tab}
    <UnderLineLink 
      href={tab.link} 
      text={tab.name} 
      className={`!text-2xl font-medium ${activeSection === tab.id ? 'text-blue-900 nav-active' : ''}`}
      onclick={() => isMenuOpen = false}
    />
  {/each}
</div>