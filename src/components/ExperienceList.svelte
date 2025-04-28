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

<div class="flex flex-col divide-y divide-[var(--color-border-light)]">
  {#each items as item, index}
  <div class="py-[clamp(1.25rem,4vw,2rem)] px-2 transition-smooth bg-hover-light group">
      <!-- Header section -->
      <button 
        onclick={() => toggleExpand(index)}
        class="flex flex-row gap-[clamp(1rem,3vw,1.5rem)] items-center w-full text-left cursor-pointer"
        aria-expanded={expandedItems.includes(index)}
        aria-controls={`content-${index}`}
        aria-label={`Toggle details for ${item.company}`}
      >
        <!-- Logo/Icon -->
        <div class="flex-shrink-0">
          <img 
            src={item.logo} 
            alt={item.company} 
            class="w-24 h-24 sm:w-32 sm:h-32 object-contain" 
          />
        </div>

        <!-- Text Info -->
        <div class="flex flex-col justify-center flex-grow">
          <h4 class="group-hover:text-[var(--color-accent)] transition-smooth flex items-center">
            {item.company}
            <i class={`fa-solid fa-chevron-down ml-2 text-sm opacity-70 transition-transform duration-300 ${
              expandedItems.includes(index) ? 'rotate-180' : ''
            }`}></i>
          </h4>
          <p class="text-secondary">{item.title}</p>
          <small class="text-tertiary">{item.dates}</small>
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
            <div class="flex-shrink-0 w-32"></div>
            <div class="w-[clamp(1rem,3vw,1.5rem)]"></div>
            <!-- Content -->
            <div class="flex-grow">
              <ul class="list-disc pl-5 space-y-2">
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