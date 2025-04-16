<script>
  let { items = [] } = $props();
</script>

<div class="flex flex-col divide-y divide-neutral-300">
  {#each items as item}
    <a 
      href={item.website || "#"} 
      target="_blank" 
      rel="noopener noreferrer"
      class="flex flex-row gap-[clamp(1rem,3vw,1.5rem)] py-[clamp(1.25rem,4vw,2rem)] px-2 transition-colors duration-300 hover:bg-white/50 group items-center"
    >
      <!-- Logo/Icon - Responsive sizing -->
      <div class="flex-shrink-0">
          <img 
            src={item.logo} 
            alt={item.company} 
            class="w-24 h-24 object-contain" 
          />
      </div>

      <!-- Text Info - Responsive font sizes -->
      <div class="flex flex-col justify-center text-left">
        <div class="font-semibold text-neutral-900 text-[clamp(1.125rem,2vw,1.25rem)] group-hover:text-blue-900 transition-colors duration-300">{item.company}</div>
        <div class="text-neutral-700 text-[clamp(1rem,1.5vw,1.125rem)] font-medium">{item.title}</div>
        <div class="text-neutral-500 text-[clamp(0.875rem,1vw,1rem)] mt-[clamp(0.75rem,2vw,1rem)]">{item.dates}</div>
      </div>
    </a>
  {/each}
</div>