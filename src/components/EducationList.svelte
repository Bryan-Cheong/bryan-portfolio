<script>
  let { items = [] } = $props();
</script>

<div class="flex flex-col divide-y divide-neutral-300">
  {#each items as item}
    <a 
      href={item.website || "#"} 
      target="_blank" 
      class="flex flex-row py-[clamp(1.25rem,4vw,2rem)] px-2 transition-colors duration-300 hover:bg-white/50 group items-center"
    >
      <!-- Institution Initial in Circle - Note the items-center class added -->
      <div class="flex-shrink-0 w-16 h-16 flex items-center justify-center rounded-full bg-blue-100 text-blue-900 mr-[clamp(1rem,3vw,1.5rem)] font-bold text-2xl">
        {item.institution[0]}
      </div>

      <!-- Text Info - Responsive font sizes -->
      <div class="flex flex-col justify-center text-left">
        <div class="font-semibold text-neutral-900 text-[clamp(1.125rem,2vw,1.25rem)] group-hover:text-blue-900 transition-colors duration-300">{item.institution}</div>
        <div class="text-neutral-700 text-[clamp(1rem,1.5vw,1.125rem)] font-medium">{item.degree}</div>
        {#if item.field}
          <div class="text-neutral-600 text-[clamp(0.875rem,1.25vw,1rem)]">{item.field}</div>
        {/if}
        <div class="text-neutral-500 text-[clamp(0.875rem,1vw,1rem)] mt-[clamp(0.75rem,2vw,1rem)]">{item.dates}</div>
      </div>
    </a>
  {/each}
</div>