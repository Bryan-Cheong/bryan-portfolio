<script>
  import { browser } from '$app/environment';
  import { page } from '$app/stores';
  import UnderLineLink from './UnderLineLink.svelte';
  import { onMount, onDestroy } from 'svelte';
  
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

  onMount(() => {
  if (browser) {
    // Start header animation after 600ms
    animateHeaderTimeout = setTimeout(() => {
      isPageLoaded = true;

      // Start nav items animation after 100ms
      animateNavTimeout = setTimeout(() => {
        navItemsLoaded = true;
      }, 100);
    }, 600);
  }

  return () => {
    clearTimeout(animateHeaderTimeout);
    clearTimeout(animateNavTimeout);
  };
});
  
  // Update scroll progress when y changes
  $effect(() => {
    if (browser) {
      if (isMenuOpen) {
        // Prevent scrolling on body when menu is open
        document.body.style.overflow = 'hidden';
        document.body.style.touchAction = 'none'; // For mobile devices
      } else {
        // Restore scrolling when menu is closed
        document.body.style.overflow = '';
        document.body.style.touchAction = '';
      }

      // Clean up on component destruction
      onDestroy(() => {
        if (browser) {
          document.body.style.overflow = '';
          document.body.style.touchAction = '';
          document.body.style.position = '';
          document.body.style.width = '';
          document.body.style.top = '';
        }
      });

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
  class="sticky z-[30] top-0 w-full transition-all duration-300 header-entrance"
  class:loaded={isPageLoaded}
  class:bg-[var(--color-surface-95)]={y > 0}
  class:backdrop-blur-sm={y > 0}
  class:bg-transparent={y <= 0}
  style="padding-top: var(--spacing-header-footer-y); 
         padding-bottom: var(--spacing-header-footer-y);"
>
  <div class="mx-auto px-[clamp(1rem,5vw,2.5rem)] flex items-center justify-between"
       style="max-width: var(--max-container-width);
       padding-left: var(--spacing-header-footer-x); 
       padding-right: var(--spacing-header-footer-x);">
    <!-- Logo with hover effect -->
    <a href="/" aria-label="Bryan Cheong — Homepage" class="relative h-auto overflow-hidden flex items-center group">
      <div class="relative">
        <span class="brand-logo">
          Bryan<span class="accent ml-1 relative overflow-hidden inline-flex min-w-[11rem]">
            <span class="transform transition-transform duration-500 group-hover:-translate-y-full whitespace-nowrap">Cheong</span>
            <span class="transform transition-transform duration-500 absolute  translate-y-full group-hover:translate-y-0 whitespace-nowrap">&ndash;&thinsp;Data Analyst</span>
          </span>
        </span>
      </div>
    </a>

    <div class="flex items-center gap-6">
      <nav aria-label="Main Navigation Bar" class="md:flex items-center gap-6 hidden">
        {#each tabs as tab, i}
          <div class="nav-item" class:loaded={navItemsLoaded} style={`transition-delay: ${i * 0.05}s`}>
            <UnderLineLink 
              href={tab.link} 
              text={tab.name} 
              className={activeSection === tab.id ? 'accent nav-active' : ''}
            />
          </div>
        {/each}
      </nav>
      <button onclick={toggleMenu} 
              class="md:hidden relative z-[35] w-7 h-7 focus:outline-none p-1 cursor-pointer flex items-center justify-center" 
              aria-label="Toggle Navigation Menu"
              aria-expanded={isMenuOpen}
              aria-controls="mobile-menu">
        <div class="relative w-5 h-4">
          <!-- Hamburger Icon -->
          <span class={`absolute h-0.5 w-5 bg-neutral-800 transform transition-all duration-300 ${isMenuOpen ? 'rotate-45 top-[7px]' : 'top-0'}`}></span>
          <span class={`absolute h-0.5 w-5 bg-neutral-800 top-[7px] transform transition-all duration-300 ${isMenuOpen ? 'opacity-0' : 'opacity-100'}`}></span>
          <span class={`absolute h-0.5 w-5 bg-neutral-800 transform transition-all duration-300 ${isMenuOpen ? '-rotate-45 top-[7px]' : 'top-[14px]'}`}></span>
        </div>
      </button>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 h-[3px] bg-[var(--color-accent)] transition-all duration-150" 
       style={`width: ${scrollProgress}%`}></div>
</header>

<div
  id="mobile-menu"
  class="fixed inset-0 pt-16 bg-[var(--color-surface-95)] z-[25] md:hidden flex flex-col items-center justify-center gap-8 transition-opacity duration-300"
  class:opacity-100={isMenuOpen}
  class:pointer-events-auto={isMenuOpen}
  class:opacity-0={!isMenuOpen}
  class:pointer-events-none={!isMenuOpen}
  role="dialog"
  aria-modal="true"
  aria-label="Mobile Navigation Menu"
  aria-hidden={!isMenuOpen}
>

  {#each tabs as tab, i}
    <div class="nav-item animate-fade-in-down-{i}">
      <UnderLineLink 
        href={tab.link} 
        text={tab.name} 
        className={`${activeSection === tab.id ? 'accent nav-active' : ''}`}
        onclick={() => isMenuOpen = false}
      />
    </div>
  {/each}
</div>