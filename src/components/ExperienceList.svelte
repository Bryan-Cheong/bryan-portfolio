<script>
  import { slide } from 'svelte/transition';
  import { cubicOut } from 'svelte/easing';
  
  let { items = [] } = $props();
  let expandedItems = $state([]);

  function toggleExpand(index) {
    if (expandedItems.includes(index)) {
      expandedItems = expandedItems.filter(i => i !== index);
    } else {
      expandedItems = [...expandedItems, index];
    }
  }
</script>

<div class="flex flex-col divide-y divide-neutral-300">
  {#each items as item, index}
    <div class="py-[clamp(1.25rem,4vw,2rem)] px-2 transition-colors duration-300 hover:bg-white/50 group">
      <!-- Header section -->
      <button 
        onclick={() => toggleExpand(index)}
        class="flex flex-row gap-[clamp(1rem,3vw,1.5rem)] items-center w-full text-left cursor-pointer"
        aria-expanded={expandedItems.includes(index)}
        aria-controls={`content-${index}`}
      >
        <!-- Logo/Icon -->
        <div class="flex-shrink-0">
          <img 
            src={item.logo} 
            alt={item.company} 
            class="w-24 h-24 object-contain" 
          />
        </div>

        <!-- Text Info -->
        <div class="flex flex-col justify-center flex-grow">
          <div class="font-semibold text-neutral-900 text-[clamp(1.125rem,2vw,1.25rem)] group-hover:text-blue-900 transition-colors duration-300 flex items-center">
            {item.company}
            <i class={`fa-solid fa-chevron-down ml-2 text-sm opacity-70 transition-transform duration-300 ${
              expandedItems.includes(index) ? 'rotate-180' : ''
            }`}></i>
          </div>
          <div class="text-neutral-700 text-[clamp(1rem,1.5vw,1.125rem)] font-medium">{item.title}</div>
          <div class="text-neutral-500 text-[clamp(0.875rem,1vw,1rem)] mt-[clamp(0.75rem,2vw,1rem)]">{item.dates}</div>
        </div>
      </button>
      
      <!-- Expandable content with Svelte transitions -->
      {#if expandedItems.includes(index)}
        <div 
          id={`content-${index}`}
          transition:slide={{ duration: 300, easing: cubicOut }}
          class="mt-4"
        >
          <!-- Aligned content -->
          <div class="flex">
            <div class="flex-shrink-0 w-24"></div>
            <div class="w-[clamp(1rem,3vw,1.5rem)]"></div>
            <!-- Content -->
            <div class="flex-grow">
              <ul class="list-disc pl-5 text-neutral-700 space-y-2">
                {#if item.responsibilities}
                  {#each item.responsibilities as responsibility}
                    <li>{responsibility}</li>
                  {/each}
                {:else}
                  <li>Placeholder</li>
                {/if}
              </ul>
            </div>
          </div>
        </div>
      {/if}
    </div>
  {/each}
</div>