<script>
  import Button from './Button.svelte';
  import StickyTitleSection from './StickyTitleSection.svelte';
  import ExperienceList from './ExperienceList.svelte';
  import { browser } from '$app/environment';
  import { onMount } from 'svelte';
  
  const experienceItems = [
    {
      logo: '/assets/anavio.avif',
      company: 'Anavio Capital Partners',
      title: 'Quantitative Analytics Platform Intern',
      dates: 'August 2021 → Today',
      website: 'https://www.anaviocap.com/'
    },
    {
      logo: '/assets/gse.png',
      company: 'General System Engineering',
      title: 'Enterprise Resource Planning Assistant',
      dates: 'July 2023 → Today',
      website: 'https://www.gse.com.my/'
    },
    {
      logo: 'assets/britishredcross.png',
      company: 'British Red Cross',
      title: 'Data Analyst',
      dates: 'October 2020 → July 2021',
      website: 'https://www.redcross.org.uk/'
    },
    {
      logo: 'assets/subplace.png',
      company: 'Subplace',
      title: 'Software Reliability Intern',
      dates: 'March 2021 → Today',
      website: 'https://subplace.com/'
    }
  ];

  // Calculate navbar height and adjust positioning
  let navbarHeight = 0;
  
  onMount(() => {
    if (browser) {
      // Get the header element height
      const header = document.querySelector('header');
      navbarHeight = header ? header.offsetHeight : 0;
    }
  });
</script>

<main class="flex flex-col flex-1 px-6 sm:px-8 md:px-10 lg:px-4" style="min-height: calc(100vh - {navbarHeight}px);">
  <section id="introPage" class="w-full max-w-3xl mx-auto flex flex-col justify-center" style="min-height: calc(100vh - {navbarHeight}px - 3rem);">
    <!-- Text content (left-aligned) -->
    <div class="flex flex-col gap-6 md:gap-8 lg:gap-10 pb-32">
      <h2 class="text-3xl sm:text-4xl md:text-5xl text-left">
        Analytical. Adaptable. <br />
        Always Learning.
      </h2>
      <p class="text-lg sm:text-xl md:text-2xl max-w-3xl text-left">
        I turn data into stories, models into strategy, and insight into action.
      </p>
      <!-- Call-to-Action Buttons -->
      <div class="flex flex-wrap gap-4 justify-start mt-2">
        <Button 
          href="mailto:wei.cheong24@imperial.ac.uk"
          variant="primary"
          icon="fa-regular fa-envelope text-sm"
        >
          Contact Me
        </Button>
        
        <Button 
          href="/assets/CV.pdf"
          target="_blank"
          variant="secondary"
          icon="fa-solid fa-download text-sm"
        >
          Download CV
        </Button>
      </div>
    </div>
  </section>
  
  <StickyTitleSection title="Experience">
    <ExperienceList items={experienceItems} />
  </StickyTitleSection>
  

  <!-- Projects Section using StickyTitleSection -->
  <StickyTitleSection title="Projects">
    <!-- Project 1 -->
    <div class="bg-white rounded-lg shadow-md p-6">
      <h3 class="text-xl font-medium mb-2">Project Title 1</h3>
      <p class="text-neutral-600 mb-4">
        Brief description of the project, technologies used, and outcomes achieved.
      </p>
      <div class="flex gap-2 flex-wrap mb-4">
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Python</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Data Analysis</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Visualization</span>
      </div>
      <a href="#" class="text-blue-900 hover:underline">View Project →</a>
    </div>
    
    <!-- Project 2 -->
    <div class="bg-white rounded-lg shadow-md p-6">
      <h3 class="text-xl font-medium mb-2">Project Title 2</h3>
      <p class="text-neutral-600 mb-4">
        Brief description of the project, technologies used, and outcomes achieved.
      </p>
      <div class="flex gap-2 flex-wrap mb-4">
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">SQL</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Power BI</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Data Modeling</span>
      </div>
      <a href="#" class="text-blue-900 hover:underline">View Project →</a>
    </div>

    <!-- Project 3 -->
    <div class="bg-white rounded-lg shadow-md p-6">
      <h3 class="text-xl font-medium mb-2">Project Title 2</h3>
      <p class="text-neutral-600 mb-4">
        Brief description of the project, technologies used, and outcomes achieved.
      </p>
      <div class="flex gap-2 flex-wrap mb-4">
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">SQL</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Power BI</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Data Modeling</span>
      </div>
      <a href="#" class="text-blue-900 hover:underline">View Project →</a>
    </div>

    <!-- Project 4 -->
    <div class="bg-white rounded-lg shadow-md p-6">
      <h3 class="text-xl font-medium mb-2">Project Title 2</h3>
      <p class="text-neutral-600 mb-4">
        Brief description of the project, technologies used, and outcomes achieved.
      </p>
      <div class="flex gap-2 flex-wrap mb-4">
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">SQL</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Power BI</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Data Modeling</span>
      </div>
      <a href="#" class="text-blue-900 hover:underline">View Project →</a>
    </div>

    <!-- Project 5 -->
    <div class="bg-white rounded-lg shadow-md p-6">
      <h3 class="text-xl font-medium mb-2">Project Title 2</h3>
      <p class="text-neutral-600 mb-4">
        Brief description of the project, technologies used, and outcomes achieved.
      </p>
      <div class="flex gap-2 flex-wrap mb-4">
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">SQL</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Power BI</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Data Modeling</span>
      </div>
      <a href="#" class="text-blue-900 hover:underline">View Project →</a>
    </div>

    <!-- Project 6 -->
    <div class="bg-white rounded-lg shadow-md p-6">
      <h3 class="text-xl font-medium mb-2">Project Title 2</h3>
      <p class="text-neutral-600 mb-4">
        Brief description of the project, technologies used, and outcomes achieved.
      </p>
      <div class="flex gap-2 flex-wrap mb-4">
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">SQL</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Power BI</span>
        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded text-sm">Data Modeling</span>
      </div>
      <a href="#" class="text-blue-900 hover:underline">View Project →</a>
    </div>
  </StickyTitleSection>
</main>