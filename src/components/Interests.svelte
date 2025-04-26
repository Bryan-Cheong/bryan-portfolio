<script>
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
</script>

<div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-8 pt-20 pb-10">
  {#each interests as interest}
    <div class="flex flex-col items-center text-center group">
      <!-- Icon Circle with hover animation only -->
      <div 
        class="w-16 h-16 rounded-full bg-blue-100 text-blue-900 flex items-center justify-center mb-3 transition-all duration-300 transform group-hover:scale-110 group-hover:bg-blue-200"
      >
        <i class={`${interest.icon} text-xl`}></i>
      </div>
      
      <!-- Name -->
      <span class="font-medium">
        {interest.name}
      </span>
    </div>
  {/each}
</div>