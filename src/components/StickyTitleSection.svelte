<script>
  let { title = "Section", id = undefined } = $props();
</script>

<section {id} class="mt-40 mb-16">
  <div class="max-w-[1400px] mx-auto px-[clamp(1rem,5vw,2.5rem)]">
    <div class="flex flex-col lg:flex-row gap-8">
      <!-- Left column: Sticky section title -->
      <div class="lg:w-1/3 lg:sticky lg:top-24 self-start">
        <div class="border-t-2 border-neutral-800 w-12 mb-4 pt-2"></div>
        <h2 class="text-[clamp(1.5rem,4vw,2.25rem)]">{title}</h2>
      </div>

      <!-- Right column: Content -->
      <div class="lg:w-2/3 flex flex-col gap-12">
        <slot />
      </div>
    </div>
  </div>
</section>