<script>
  import Intro from './Intro.svelte';
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
      responsibilities: [
        "Long Short Equity Portfolio Automation",
      ]
    },
    {
      logo: '/assets/gse.png',
      company: 'GSE-M Technology Sdn. Bhd',
      title: 'Enterprise Resource Planning Assistant',
      dates: 'July 2023 → Today',
      responsibilities: [
        "Implemented ERP system",
        "Trained staff on system usage"
      ]
    },
    {
      logo: 'assets/britishredcross.png',
      company: 'British Red Cross',
      title: 'Data Analyst',
      dates: 'October 2020 → July 2021',
      responsibilities: [
        "Analysed complaints data to identify trends and areas for improvement",
        "Developed dashboards to visualize data insights for stakeholders"
      ]
    },
    {
      logo: 'assets/subplace.png',
      company: 'Subplace',
      title: 'Software Reliability Intern',
      dates: 'March 2021 → Today',
      responsibilities: [
        "Implemented monitoring tools to track system performance and reliability",
        "Conducted root cause analysis for system outages and performance issues",
        "Advocated for best practices in software development and testing like agile methodologies and test-driven development",
        "Created documentation for incident response procedures"
      ]
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
      title: "Beat the Bookies",
      description: "Premier League betting prediction model using machine learning.",
      tools: ["Python", "Plotly", "Pandas", "Flask"],
      image: "/assets/projects/bookies.png",
      pdf: "/assets/projects/bookies.pdf",
      link: "#"

    },
    {
      title: "RIE Final Year Project",
      description: "RIE Noise Reduction Algorithm for Lagged Covariance Matrices",
      tools: ["Python", "NumPy", "SciPy", "Matplotlib"],
      image: "/assets/projects/rie.png",
      pdf: "assets/projects/rie.pdf",
      link: "#",
      github: "https://github.com/Bryan-Cheong/RIE-Singular-Value-Cleaning-of-Lagged-Covariance-Matrices"
    },
    {
      title: "Text Analytics Project on Song Lyrics",
      description: "Analysed song lyrics to identify patterns in popular music across different genres and decades.",
      tools: ["R", "sentimentr", "ggplot2", "dplyr", "quanteda"],
      image: "/assets/projects/song.png",
      pdf: "/assets/projects/song.pdf",
      link: "#"
    },
    {
      title: "Logistics and Supply Chain Optimisation Game",
      description: "Optimised logistics and supply chain operations using simulation and optimization techniques.",
      tools: ["Python", "R"],
      image: "/assets/projects/logistics.png",
      pdf: "/assets/projects/logistics.pdf",
      link: "#"
    },
    {
      title: "Titanic Exploratory Data Analysis",
      description: "Conducted exploratory data analysis on Titanic dataset, visualizing survival rates and passenger demographics.",
      tools: ["R", "ggplot2", "dplyr", "tidyverse"],
      image: "/assets/projects/titanic.png",
      pdf: "/assets/projects/titanic.pdf",
      link: "#"
    },
    {
      title: "Energy Forecasting Model",
      description: "Developed a forecasting model for energy consumption using time series analysis.",
      tools: ["Python", "Pandas", "NumPy", "Statsmodels", "XGBoost"],
      image: "/assets/projects/energy_forecasting.png",
      pdf: "/assets/projects/energy_forecasting.pdf",
      link: "#"
    },
    {
      title: "Energy Risk, Hedging, and Real Options Valuation",
      description: "Developed a model to assess energy risk and evaluate hedging strategies using real options valuation.",
      tools: ["Python", "NumPy", "SciPy", "Matplotlib"],
      image: "/assets/projects/scraping.png",
      pdf: "/assets/projects/scraping.pdf",
      link: "#"
    },
    {
      title: "A/B Testing Analysis",
      description: "Conducted A/B testing for a marketing campaign, resulting in a 15% increase in conversion rates.",
      tools: ["Python", "R", "SQL"],
      image: "/assets/projects/abtesting.png",
      link: "#"
    },
    {
      title: "Tetris AI",
      description: "Implemented a Tetris heuristics evaluation AI, scored 28,000+ points using 400 blocks, 80th percentile in UCL's cohort",
      tools: ["Python", "NumPy", "Pygame"],
      image: "/assets/projects/tetris.png",
      link: "#"
    },
    {
      title: "Public Perception of Benefit Fraud",
      description: "Analysed eight variables in the 2019 British Social Survey on benefit fraud with two-sided t-tests, linear regression and more using R. Found public estimates (34.6%) far exceeded the government's (1.1%), with discrepancies influenced by political affiliation and education level. Highlighted the need for targeted education to address public misconceptions",
      tools: ["R", "ggplot2", "SQL", "Power BI"],
      image: "/assets/projects/segmentation.png",
      link: "#"
    }
  ];

  let navbarHeight = $state(70);
  let isPageLoaded = $state(false);
  
  onMount(() => {
    if (browser) {
      // Get the header element height
      const header = document.querySelector('header');
      if (header) {
        navbarHeight = header.offsetHeight;
      }
      
      setTimeout(() => {
        isPageLoaded = true;
      }, 100);
    }
  });
</script>

<main class="flex flex-col flex-1" style="min-height: calc(100vh - {navbarHeight}px);">
  <Intro isPageLoaded={isPageLoaded} />
  
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