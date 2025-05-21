<script>
	import '../app.css';
	import Footer from '../components/Footer.svelte';
	import Header from '../components/Header.svelte';

	let { children } = $props();

	let y = $state(0);
	let innerHeight = $state(0);
	let innerWidth = $state(0);

	function scrollToTop() {
			document.body.scrollIntoView()
	}
</script>

<svelte:head>
  <meta property="og:title" content="Bryan Cheong | Portfolio" />
  <meta property="og:image" content="https://bryancheong.dev/icon.jpeg" />
</svelte:head>

<Header y={y} />

<div class="relative flex flex-col max-w-[1400px] mx-auto w-full text-sm
sm:text-base min-h-screen">
  <div class={"fixed bottom-10 right-10 duration-300 flex p-10 z-[10] " + (
          y > 0 ? ' opacity-100 pointer-events-auto': ' pointer-events-none opacity-0'
  )}>
    <button onclick={scrollToTop} 
            class="ml-auto bg-blue-900 hover:bg-blue-950 text-stone-200 p-3 rounded-full shadow-lg"
            aria-label="Scroll to top">
        <i class="fa-solid fa-arrow-up grid place-items-center aspect-square"></i>
    </button>
  </div>
  {@render children()}
  <Footer />
</div>

<svelte:window bind:scrollY={y} bind:innerHeight bind:innerWidth />