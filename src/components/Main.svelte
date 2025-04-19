<script>
  import Button from './Button.svelte';
  import StickyTitleSection from './StickyTitleSection.svelte';
  import TitleSection from './TitleSection.svelte';
  import ExperienceList from './ExperienceList.svelte';
  import EducationList from './EducationList.svelte';
  import ProjectList from './ProjectList.svelte';
  import About from './About.svelte';
  import Interests from './Interests.svelte';
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
      company: 'GSE-M Technology Sdn. Bhd',
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

  const educationItems = [
    {
      institution: 'Imperial College London',
      degree: 'MSc in Business Analytics',
      dates: '2024 → 2025',
      website: 'https://www.imperial.ac.uk/'
    },
    {
      institution: 'University College London',
      degree: 'BSc in Computer Science',
      dates: '2021 → 2024',
      website: 'https://www.ucl.ac.uk/'
    }
  ];

  const projectItems = [
    {
      title: "Data Visualization Dashboard",
      description: "Created an interactive dashboard for visualizing complex financial data, enabling stakeholders to make data-driven decisions quickly and efficiently.",
      tools: ["Python", "Plotly", "Pandas", "Flask"],
      image: "/assets/projects/dashboard.jpg",
      link: "#"
    },
    {
      title: "Machine Learning Stock Predictor",
      description: "Developed a predictive model using historical stock data and machine learning algorithms to forecast market trends with 78% accuracy.",
      tools: ["Python", "TensorFlow", "scikit-learn", "NumPy"],
      image: "/assets/projects/stocks.jpg",
      link: "#"
    },
    {
      title: "Customer Segmentation Analysis",
      description: "Applied clustering algorithms to identify distinct customer segments, helping a retail client optimize their marketing strategy and increase ROI by 23%.",
      tools: ["R", "ggplot2", "SQL", "Power BI"],
      image: "/assets/projects/segmentation.jpg",
      link: "#"
    },
    {
      title: "Natural Language Processing Tool",
      description: "Built a sentiment analysis tool that processes customer feedback and extracts actionable insights, improving response times by 45%.",
      tools: ["Python", "NLTK", "spaCy", "Streamlit"],
      image: "/assets/projects/nlp.jpg",
      link: "#"
    }
  ];

  // Calculate navbar height and adjust positioning
  let navbarHeight = $state(70);
  
  onMount(() => {
    if (browser) {
      // Get the header element height
      const header = document.querySelector('header');
      if (header) {
        navbarHeight = header.offsetHeight;
      }
    }
  });
</script>

<main class="flex flex-col flex-1" style="min-height: calc(100vh - {navbarHeight}px);">
  <section id="introPage" class="w-full max-w-3xl mx-auto flex flex-col justify-center px-[clamp(1rem,5vw,2.5rem)]" style="min-height: calc(100vh - {navbarHeight}px - 3rem);">
    <!-- Text content with fluid typography -->
    <div class="flex flex-col gap-[clamp(1.5rem,4vw,2.5rem)] pb-[clamp(4rem,10vh,8rem)]">
      <h2 class="text-[clamp(1.75rem,5vw,3.5rem)] text-left">
        Analytical. Adaptable. <br />
        Always Learning.
      </h2>
      <p class="text-[clamp(1rem,2vw,1.25rem)] max-w-3xl text-left">
        I turn data into stories, models into strategy, and insight into action.
      </p>
      <!-- Call-to-Action Buttons -->
      <div class="flex flex-wrap gap-[clamp(0.75rem,2vw,1rem)] justify-start mt-[clamp(0.5rem,1vw,0.75rem)]">
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
  
  <StickyTitleSection title="Experience" id="experience">
    <ExperienceList items={experienceItems} />
  </StickyTitleSection>


  <TitleSection title="Projects" id="projects">
    <ProjectList items={projectItems} />
  </TitleSection>
  
  <StickyTitleSection title="Education" id="education">
    <EducationList items={educationItems} />
  </StickyTitleSection>

  <StickyTitleSection title="About Me" id="about">
    <About />
  </StickyTitleSection>

  <StickyTitleSection title="Interests" id="interests">
    <Interests />
  </StickyTitleSection>
</main>