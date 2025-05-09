<script>
  // Interests with icons
  const interests = [
    { 
      icon: "fa-solid fa-basketball", 
      name: "Basketball"
    },
    { 
      icon: "fa-solid fa-person-swimming", 
      name: "Triathlon"
    },
    { 
      icon: "fa-solid fa-dumbbell", 
      name: "Fitness"
    },
    { 
      icon: "fa-solid fa-mountain", 
      name: "Bouldering"
    },
    { 
      icon: "fa-solid fa-plane", 
      name: "Travelling"
    },
    { 
      icon: "fa-solid fa-utensils", 
      name: "Cooking"
    },
    { 
      icon: "fa-solid fa-microchip", 
      name: "Building Computers"
    },
    { 
      icon: "fa-solid fa-chess-board", 
      name: "Board Games"
    }
  ];
</script>

<div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-8 pt-20 pb-10">
  {#each interests as interest}
    <div class="flex flex-col items-center text-center group">
      <!-- Icon Circle with hover animation only -->
      <div 
        class="w-16 h-16 rounded-full flex items-center justify-center mb-3 transition-smooth transform group-hover:scale-110"
        style="background-color: var(--color-accent-light); color: var(--color-accent);"
      >
        <i class={`${interest.icon}`} style="font-size: var(--font-size-lg);"></i>
      </div>
      
      <!-- Name -->
      <span style="font-weight: var(--font-weight-medium);">
        {interest.name}
      </span>
    </div>
  {/each}
</div>