<script>
  import { onMount } from 'svelte';
  
  // Interests with icons
  const interests = [
    { 
      icon: "fa-solid fa-plane", 
      name: "Travelling"
    },
    { 
      icon: "fa-solid fa-microchip", 
      name: "Building Computers"
    },
    { 
      icon: "fa-solid fa-basketball", 
      name: "Basketball"
    },
    { 
      icon: "fa-solid fa-dumbbell", 
      name: "Fitness"
    },
    { 
      icon: "fa-solid fa-person-swimming", 
      name: "Triathlon"
    },
    { 
      icon: "fa-solid fa-utensils", 
      name: "Cooking"
    },
    { 
      icon: "fa-solid fa-mountain", 
      name: "Bouldering"
    },
    { 
      icon: "fa-solid fa-chess-board", 
      name: "Board Games"
    }
  ];
  
  // Animation states
  let isReady = $state(false);
  let visibleItems = $state([]);
  let sectionRef;
  
  onMount(() => {
    if (typeof IntersectionObserver !== 'undefined') {
      const observer = new IntersectionObserver((entries) => {
        const [entry] = entries;
        
        if (entry.isIntersecting) {
          // Start the animation sequence when section is visible
          setTimeout(() => {
            isReady = true;
            
            interests.forEach((_, index) => {
              setTimeout(() => {
                visibleItems = [...visibleItems, index];
              }, 150 * index);
            });
          }, 300);
          
          // Unobserve after triggering the animation
          observer.unobserve(entry.target);
        }
      }, {
        threshold: 0.1 // Trigger when 10% of the section is visible
      });
      
      // Start observing the section
      observer.observe(sectionRef);
    }
  });
</script>

<!-- Removed min-height, kept padding for proper alignment -->
<div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-8 pt-20 pb-10" bind:this={sectionRef}>
  {#each interests as interest, i}
    <div class="flex flex-col items-center text-center group">
      <!-- Icon Circle with Animation -->
      <div 
        class="w-16 h-16 rounded-full flex items-center justify-center mb-3 transition-all duration-500"
        class:bg-blue-100={visibleItems.includes(i)}
        class:text-blue-900={visibleItems.includes(i)}
        class:bg-neutral-200={isReady && !visibleItems.includes(i)}
        class:text-transparent={isReady && !visibleItems.includes(i)}
        class:scale-90={isReady && !visibleItems.includes(i)}
        class:scale-100={visibleItems.includes(i)}
        class:transform={true}
        class:group-hover:scale-110={visibleItems.includes(i)}
        class:group-hover:bg-blue-200={visibleItems.includes(i)}
      >
        <i class={`${interest.icon} text-xl transition-opacity duration-500 ${visibleItems.includes(i) ? 'opacity-100' : 'opacity-0'}`}></i>
      </div>
      
      <!-- Name with Animation -->
      <span 
        class="font-medium transition-all duration-500"
        class:opacity-0={!visibleItems.includes(i) && isReady}
        class:opacity-100={visibleItems.includes(i)}
        class:transform={true}
        class:translate-y-2={isReady && !visibleItems.includes(i)}
        class:translate-y-0={visibleItems.includes(i)}
      >
        {interest.name}
      </span>
    </div>
  {/each}
</div>