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
  <!-- Browser Tab Title -->
  <title>Bryan Cheong | Portfolio</title>
  <meta name="description" content="Bryan Cheong's portfolio - blending data science with industry insight. From financial modelling and demand forecasting to creative side projects, explore end-to-end analytics work powered by Python, SQL, and R." />

  <!-- Open Graph (LinkedIn, Facebook) -->
  <meta property="og:type" content="website" />
  <meta property="og:title" content="Bryan Cheong | Portfolio" />
  <meta property="og:description" content="Bryan Cheong's portfolio - blending data science with industry insight. From financial modelling and demand forecasting to creative side projects, explore end-to-end analytics work powered by Python, SQL, and R." />
  <meta property="og:image" content="https://bryancheong.dev/landscape_icon.png" />
  <meta property="og:url" content="https://bryancheong.dev" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Bryan Cheong | Portfolio" />
  <meta name="twitter:description" content="Bryan Cheong's portfolio - blending data science with industry insight. From financial modelling and demand forecasting to creative side projects, explore end-to-end analytics work powered by Python, SQL, and R." />
  <meta name="twitter:image" content="https://bryancheong.dev/landscape_icon.png" />

  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Person",
    "name": "Bryan Cheong",
    "url": "https://bryancheong.dev",
    "jobTitle": "Data Analyst",
    "description": "Portfolio of Bryan Cheong - blending data science with industry insight. From financial modelling and demand forecasting to creative side projects, explore end-to-end analytics work powered by Python, SQL, and R.",
    "image": "https://bryancheong.dev/landscape_icon.png",
    "sameAs": [],
    "mainEntityOfPage": {
      "@type": "WebPage",
      "@id": "https://bryancheong.dev"
    },
    "author": {
      "@type": "Person",
      "name": "Bryan Cheong"
    },
    "datePublished": "2025-05-01",
    "dateModified": "2025-05-21"
  }
  </script>
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