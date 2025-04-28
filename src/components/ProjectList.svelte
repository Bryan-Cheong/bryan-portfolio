<script>
  let { items = [] } = $props();
</script>

<div class="flex flex-col gap-12">
  {#each items as project}
    <div
      class="bg-white rounded-lg shadow-sm border border-[var(--color-border-light)] overflow-hidden flex flex-col group hover:shadow-md hover:scale-102 transition duration-300"
    >
      <!-- Content (left) -->
      <div class="p-6 flex-1">
        <h3 class="mb-2">{project.title}</h3>
        <p class="text-secondary mb-4">{project.description}</p>

        <!-- Tools -->
        <div class="flex gap-2 flex-wrap mb-4">
          {#each project.tools as tool}
          <small class="tool-badge">{tool}</small>
          {/each}
        </div>

        <!-- Links -->
        <small class="flex gap-4 accent">
          {#if project.github}
            <a href={project.github} target="_blank" rel="noopener noreferrer" class="hover:underline flex items-center gap-1">
              <i class="fa-brands fa-github"></i> GitHub
            </a>
          {/if}
          {#if project.pdf}
            <a href={project.pdf} target="_blank" rel="noopener noreferrer" class="hover:underline flex items-center gap-1">
              <i class="fa-solid fa-file-pdf"></i> View Report
            </a>
          {/if}
        </small>
      </div>

      {#if project.image}
        <div class="w-full h-full relative overflow-hidden p-4">
          <img
            src={project.image}
            alt={project.title}
            class="w-full h-full object-cover"
          />
        </div>
      {/if}
    </div>
  {/each}
</div>
