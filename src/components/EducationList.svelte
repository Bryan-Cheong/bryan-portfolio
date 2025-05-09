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
  <div class="transition-smooth bg-hover-light group" 
       style="padding: var(--spacing-item-y) var(--spacing-item-x);">
      <!-- Header section -->
      <button 
          onclick={() => toggleExpand(index)}
          class="flex flex-row gap-[clamp(1rem,3vw,1.5rem)] items-center w-full text-left cursor-pointer"
          aria-expanded={expandedItems.includes(index)}
          aria-controls={`education-content-${index}`}
          aria-label={`Toggle details for ${item.institution}`}
        >
          <!-- Logo/Icon -->
          <div class="flex-shrink-0">
            <img 
              src={item.logo} 
              alt={item.institution} 
              style="width: var(--logo-size); height: var(--logo-size);"
              class="object-contain" 
            />
          </div>

          <!-- Text Info -->
          <div class="flex flex-col justify-center flex-grow">
            <h4 class="group-hover:text-[var(--color-accent)] transition-smooth flex items-center">
              {item.institution}
              <i class={`fa-solid fa-chevron-down ml-2 text-sm text-muted transition-transform duration-300 ${
                expandedItems.includes(index) ? 'rotate-180' : ''
              }`}></i>
            </h4>
            <p class="text-secondary">{item.degree}</p>
            <small class="text-tertiary">{item.dates}</small>
          </div>
        </button>
        
        <!-- Expandable content with Svelte transitions -->
        {#if expandedItems.includes(index)}
          <div 
            id={`education-content-${index}`}
            transition:slide={{ duration: 300, easing: cubicOut }}
          >
            <!-- Aligned content -->
            <div class="flex">
              <div class="flex-shrink-0" style="width: var(--logo-size);"></div>
              <div class="w-[clamp(1rem,3vw,1.5rem)]"></div>
              <!-- Content -->
              <div class="flex-grow">
                {#if !item.courses && !item.achievements}
                  <ul class="list-disc pl-5 space-y-2">
                    <li>Placeholder</li>
                  </ul>
                {:else}
                  <!-- Courses Section -->
                  {#if item.courses && item.courses.length > 0}
                    <div class="mb-4">
                      <p style="font-weight: var(--font-weight-medium);" class="text-[var(--color-text-secondary)] mb-2">Modules</p>
                      <ul class="list-disc pl-5 space-y-2">
                        {#each item.courses as course}
                          <li>{course}</li>
                        {/each}
                      </ul>
                    </div>
                  {/if}
                  
                  <!-- Achievements Section -->
                  {#if item.achievements && item.achievements.length > 0}
                    <div>
                      <p style="font-weight: var(--font-weight-medium);" class="text-[var(--color-text-secondary)] mb-2">Achievements</p>
                      <ul class="list-disc pl-5 space-y-2">
                        {#each item.achievements as achievement}
                          <li>{achievement}</li>
                        {/each}
                      </ul>
                    </div>
                  {/if}
                {/if}
              </div>
            </div>
          </div>
        {/if}
      </div>
    {/each}
  </div>