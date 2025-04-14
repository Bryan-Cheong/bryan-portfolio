<script>
  let { y } = $props();
  let tabs = [
    {name: "Projects", link: "#projects"},
    {name: "About Me", link: "#about"}
  ];
</script>

<header class={"sticky z-[10] top-0 duration-200 px-6 flex items-center justify-between border border-solid " + (
  y > 0 ? " py-4 bg-stone-200 border-neutral-800" : "py-6 bg-transparent border-transparent"
)}>
  <h1 class="text-neutral-800 text-xl sm:text-2xl">
    <span class="font-bold lato">Bryan Cheong</span>
  </h1>
  <div class="sm:flex items-center gap-4 hidden">
    {#each tabs as tab, index}
      <a href={tab.link} class="duration-200 hover:text-blue-900 text-neutral-800">
        <p>{tab.name}</p>
      </a>
    {/each}
  </div>
  <a href="mailto:wei.cheong24@imperial.ac.uk" 
     target="_blank"
     class="relative overflow-hidden px-5 py-2 group rounded-full bg-blue-900
     text-white"
  >
    <div
      class="absolute top-0 right-full w-full h-full bg-slate-950 opacity-50
      group-hover:translate-x-full z-0 duration-200"
    ></div>
    <h4 class="relative z-[1]">Get in Touch</h4>
  </a>
</header>