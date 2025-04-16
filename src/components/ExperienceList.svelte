<script>
  let { items = [] } = $props();
</script>

<div class="flex flex-col divide-y divide-neutral-300">
  {#each items as item}
    <a 
      href={item.website || "#"} 
      target="_blank" 
      rel="noopener noreferrer"
      class="flex flex-row gap-4 sm:gap-6 py-6 sm:py-8 px-2 transition-colors duration-300 hover:bg-white/50 group"
    >
      <!-- Logo/Icon - Responsive sizing -->
      <div class="flex-shrink-0 self start">
          <img 
            src={item.logo} 
            alt={item.company} 
            class="w-16 h-16 sm:w-20 md:w-24 sm:h-20 md:h-24 object-contain" 
          />
      </div>

      <!-- Text Info - Responsive font sizes -->
      <div class="flex flex-col justify-center text-left">
        <div class="font-semibold text-neutral-900 text-lg sm:text-xl group-hover:text-blue-900 transition-colors duration-300">{item.company}</div>
        <div class="text-neutral-700 text-base sm:text-lg font-medium">{item.title}</div>
        <div class="text-neutral-500 text-sm sm:text-base mt-4">{item.dates}</div>
      </div>
    </a>
  {/each}
</div>