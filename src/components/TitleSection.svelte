<script>
  let { title = "Section", id = undefined } = $props();
</script>

<section {id} class="mt-40 mb-16 pt-6">
  <div class="max-w-[1400px] mx-auto px-[clamp(1rem,5vw,2.5rem)]">
    <div class="border-t-2 border-neutral-800 w-12 mb-4 pt-2"></div>
    <h2 class="text-[clamp(1.5rem,4vw,2.25rem)] mb-12">{title}</h2>
    <div class="flex flex-col gap-12">
      <slot />
    </div>
  </div>
</section>