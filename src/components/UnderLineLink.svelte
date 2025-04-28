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
    left: 0;
    bottom: -4px;
    height: 2px;
    width: 100%;
    background-color: var(--color-accent);
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.5s ease-out;
  }

  .nav-link:hover .nav-link-underline {
    transform: scaleX(1);
    transform-origin: left;
  }

  .nav-active {
    color: var(--color-accent); /* blue-900 */
    font-weight: 550;
  }
</style>

<a
  {href}
  {target}
  {rel}
  {onclick}
  class={`nav-link ${className}`}
>
  <span>{text}</span>
  <span class="nav-link-underline"></span>
</a>