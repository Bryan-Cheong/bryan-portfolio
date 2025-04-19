<script>
  let { items = [] } = $props();
</script>

<div class="flex flex-col gap-8">
  {#each items as project}
    <div class="bg-white rounded-lg shadow-md overflow-hidden flex flex-col lg:flex-row">
      <!-- Content Side (Left) -->
      <div class="p-6 flex-1">
        <h3 class="text-xl font-medium mb-2">{project.title}</h3>
        <p class="text-neutral-600 mb-4">
          {project.description}
        </p>
        <div class="flex gap-2 flex-wrap mb-4">
          {#each project.tools as tool}
            <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">{tool}</span>
          {/each}
        </div>
        {#if project.link}
          <a href={project.link} target="_blank" class="text-blue-900 hover:underline inline-flex items-center">
            View Project 
            <span class="ml-1">→</span>
          </a>
        {/if}
      </div>
      
      <!-- Image Side (Right) -->
      <div class="lg:w-1/2 h-64 lg:h-auto relative">
        <img 
          src={project.image} 
          alt={project.title}
          class="w-full h-full object-cover"
        />
      </div>
    </div>
  {/each}
</div>