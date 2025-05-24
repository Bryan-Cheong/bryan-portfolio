<script>
  let {
    href = undefined,
    type = "button", 
    variant = "primary", // primary or secondary
    target = undefined,
    rel = undefined,
    icon = undefined,  // Font Awesome icon class
    fullWidth = false,
    children,
    class: className = ""
  } = $props();

  $effect(() => {
    if (target === "_blank" && !rel) {
      rel = "noopener noreferrer";
    }
  });

  const variantStyles = {
    primary: {
      base: "bg-blue-900 text-white",
      bg: "bg-blue-950"
    },
    secondary: {
      base: "border-2 border-blue-900 text-blue-900",
      bg: "bg-blue-900/10"
    }
  };

  const buttonClasses = `
    relative overflow-hidden px-5 py-2 
    group rounded-lg
    ${variantStyles[variant].base}
    transform transition hover:scale-105 active:scale-95
    ${fullWidth ? 'w-full' : ''}
    flex items-center justify-center
    ${className}
  `;
</script>

<style>
  .btn-bg-animate {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.3s ease-out;
    z-index: 0;
  }

  .group:hover .btn-bg-animate {
    transform: scaleX(1);
    transform-origin: left;
  }
</style>

{#if href}
  <a 
    {href}
    {target}
    {rel}
    class = {buttonClasses}
  >
    <div class={`btn-bg-animate ${variantStyles[variant].bg}`}></div>
    <div class="relative z-[1] flex items-center gap-2">
      {#if icon}
        <i class={icon}></i>
      {/if}
      <span>{@render children()}</span>
    </div>
  </a>
{:else}
  <button 
    {type}
    class={buttonClasses}
  >
    <div class={`btn-bg-animate ${variantStyles[variant].bg}`}></div>
    <div class="relative z-[1] flex items-center gap-2">
      {#if icon}
        <i class={icon}></i>
      {/if}
      <span>{@render children()}</span>
    </div>
  </button>
{/if}
