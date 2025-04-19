<script>
  let {
    href = "#",
    target = undefined,
    rel = undefined,
    text = "",
    className = "",
    onclick = undefined
  } = $props();
</script>

<style>
  .nav-link-underline {
    position: absolute;
    bottom: -1px;
    left: 0;
    height: 2px;
    width: 100%;
    background-color: #1e3a8a; /* blue-900 */
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.5s ease-out;
  }
  
  .nav-link:hover .nav-link-underline {
    transform: scaleX(1);
    transform-origin: left;
  }

  .nav-active {
    color: #1e3a8a !important; /* blue-900 */
    font-weight: 600;
  }
</style>
<a
  {href}
  {target}
  {rel}
  {onclick}
  class={`relative group nav-link duration-200 hover:text-blue-900 text-neutral-800 font-medium text-base sm:text-lg transition-transform duration-300 hover:-translate-y-1 ${className}`}
>
  <span>{text}</span>
  <span class="nav-link-underline"></span>
</a>