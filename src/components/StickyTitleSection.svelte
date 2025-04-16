<script>
  let { title = "Section", id = undefined } = $props();
</script>

<section {id} class="mt-32 mb-16">
  <div class="max-w-[1400px] mx-auto px-6 sm:px-8 md:px-10 lg:px-4">
    <div class="flex flex-col lg:flex-row gap-8">
      <!-- Left column: Sticky section title -->
      <div class="lg:w-1/4 lg:sticky lg:top-24 self-start">
        <div class="mt-8 border-t-2 border-neutral-800 w-12 mb-4 pt-2"></div>
        <h2 class="text-2xl sm:text-3xl lg:text-4xl">{title}</h2>
      </div>

      <!-- Right column: Content -->
      <div class="lg:w-3/4 flex flex-col gap-12">
        <slot />
      </div>
    </div>
  </div>
</section>