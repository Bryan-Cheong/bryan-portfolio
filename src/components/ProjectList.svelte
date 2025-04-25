<script>
  let { items = [] } = $props();
</script>

<div class="flex flex-col gap-12">
  {#each items as project}
    <div
      class="bg-white rounded-lg shadow-sm border border-neutral-200 overflow-hidden flex flex-col lg:flex-row group hover:shadow-md transition-shadow duration-300"
    >
      <!-- Content (left) -->
      <div class="p-6 flex-1">
        <h3 class="text-xl font-semibold mb-2 text-neutral-900">{project.title}</h3>
        <p class="text-neutral-600 mb-4">{project.description}</p>

        <!-- Tools -->
        <div class="flex gap-2 flex-wrap mb-4">
          {#each project.tools as tool}
            <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-xs font-medium shadow-sm">{tool}</span>
          {/each}
        </div>

        <!-- Links -->
        <div class="flex gap-4 text-sm text-blue-900 font-medium">
          {#if project.link}
            <a href={project.link} target="_blank" rel="noopener noreferrer" class="hover:underline flex items-center gap-1">
              <i class="fa-solid fa-arrow-up-right-from-square"></i> View Project
            </a>
          {/if}
          {#if project.github}
            <a href={project.github} target="_blank" rel="noopener noreferrer" class="hover:underline flex items-center gap-1">
              <i class="fa-brands fa-github"></i> GitHub
            </a>
          {/if}
          {#if project.pdf}
            <a href={project.pdf} target="_blank" rel="noopener noreferrer" class="hover:underline flex items-center gap-1">
              <i class="fa-solid fa-file-pdf"></i> View PDF
            </a>
          {/if}
        </div>
      </div>

      <!-- Image (right on desktop) -->
      {#if project.image}
        <div class="lg:w-1/2 h-64 lg:h-auto relative overflow-hidden">
          <img
            src={project.image}
            alt={project.title}
            class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-105"
          />
        </div>
      {/if}
    </div>
  {/each}
</div>
