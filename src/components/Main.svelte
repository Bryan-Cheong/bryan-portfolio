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
      title: 'Equity Analytics Intern – Long/Short Strategy',
      dates: 'July 2023 → September 2023',
      responsibilities: ["Built an automated equity screening dashboard integrating 15+ capital efficiency metrics to support uncorrelated long/short strategies targeting idiosyncratic returns",
      "Scaled daily coverage from 10 to 200 tickers, reducing manual workload by 80% through automated data ingestion, computation, and reporting",
      "Enhanced pipeline robustness with 100+ Pytest tests and six error-handling decorators, significantly reducing downtime and debugging time",
      "Streamlined communication with management by translating complex logic into clear flowcharts and wireframes, accelerating alignment and halving delivery time"
      ]
    },
    {
      logo: '/assets/gse.png',
      company: 'GSE-M Technology Sdn. Bhd',
      title: 'Enterprise Resource Planning (ERP) Assistant',
      dates: 'May 2023 → July 2023',
      responsibilities: [
        "Collaborated with cross-functional ERP users across five departments to gather 30+ requirements, understand operational challenges, and locate critical bugs",
        "Tailored the ERP with consultants to enhance efficiency by 25% and meet departmental needs",
        "Co-led daily conference room pilots, training 90 employees on the ERP system to ensure smooth system adoption"
      ]
    },
    {
      logo: 'assets/britishredcross.png',
      company: 'British Red Cross',
      title: 'Data Analyst',
      dates: 'September 2022 → April 2023',
      responsibilities: [
        "Developed a Power BI app with 20+ interactive dashboards to analyse complaints data, providing actionable insights for support teams and key stakeholder reports. Enhanced decision-making and reduced complaint resolution time by 50%",
        "Built an ETL pipeline in Power BI Dataflows to extract data from four sources, normalised it into fact and dimension tables, and leveraged DAX for advanced reporting features like geographical drill-downs and slicing, enabling consistent and scalable reporting",
        "Secured future development by presenting a streamlined issue resolution system along with a deployment manual to the Head of Data"
      ]
    },
    {
      logo: 'assets/subplace.png',
      company: 'Subplace',
      title: 'Software Reliability Intern',
      dates: 'June 2022 → August 2022',
      responsibilities: [
        "Improved maintenance efficiency by 60% by enhancing test coverage with systematic test cases and modular templates",
        "Collaborated with software engineers to resolve over 200 issues raised from thorough testing",
        "Advocated for best practices in software development and testing like agile methodologies and test-driven development"
      ]
    }
  ];

  const projectItems = [
    {
      title: "Text Analytics Project on Song Lyrics",
      description: "Applied NLP and ML to analyse 40,000+ song lyrics, uncovering genre trends in sentiment, explicit content, and topics. Used LASSO with uni+bigrams and FastText word embeddings to predict popularity and evaluate genre transferability.",
      tools: ["R", "tidyverse", "quanteda", "textclean", "glmnet", "FastText word embeddings", "sentimentr", "stm",],
      image: "/assets/projects/song.png",
      pdf: "/assets/projects/song.pdf"
    },
    {
      title: "Logistics and Supply Chain Optimisation Game",
      description: "Simulated a multi-region supply chain using hybrid demand forecasting and cost-benefit analysis to guide factory and warehouse expansion. Applied adjusted reorder points and Silver-Meal heuristics to manage seasonal inventory, securing 2nd place in Imperial's cohort.",
      tools: ["Python", "R", "Excel", "SARIMA", "Croston's method", "Silver-Meal heuristic", "Linear regression"],
      image: "/assets/projects/logistics.png",
      pdf: "/assets/projects/logistics.pdf"
    },
    {
      title: "Beat the Bookies",
      description: "Engineered a Premier League match outcome predictor achieving 51% validation accuracy with CatBoost. Feature-engineered tuned Pi-rating variants, applied SHAP-based feature selection, and explored pre-game sentiment analysis using LLMs and the Nitter API.",
      tools: ["Python", "Pandas", "CatBoost", "Random Forest", "SHAP", "Nitter API", "Pi-rating", "VADER"],
      image: "/assets/projects/bookies.png",
      pdf: "/assets/projects/bookies.pdf"
    },
    {
      title: "RIE Cleaning of Lagged Covariance Matrices",
      description: "Designed a cleaning algorithm for lagged covariance matrices using Rotationally Invariant Estimators (RIEs), correcting singular value distortions via spectral projections guided by the Marchenko-Pastur law. The method achieved 100% noise reduction in AR(0) models and ~20% improvement in signal-to-noise ratio for AR(1), with greater gains as dimensionality increased. This improves the accuracy of high-dimensional covariance estimation for applications in portfolio risk modelling, signal processing, and time series forecasting.",
      tools: ["Python", "NumPy", "Pandas", "Matplotlib", "SciPy", "scikit-learn", "Statsmodels", "Marchenko-Pastur law", "SVD", "Rotationally Invariant Estimators", ],
      image: "/assets/projects/rie.png",
      pdf: "assets/projects/rie.pdf",
      github: "https://github.com/Bryan-Cheong/RIE-Singular-Value-Cleaning-of-Lagged-Covariance-Matrices"
    },
    {
      title: "Energy Demand Forecasting Model",
      description: "Forecasted UK electricity demand by engineering lagged, Heating Degree Days (HDDs), and calendar features; progressed from linear models to XGBoost. Achieved 96.3% R² with strong generalisation and low residual autocorrelation.",
      tools: ["Python", "Pandas", "NumPy", "Statsmodels", "XGBoost", "Random Forest", "Ridge Regression", "workalendar"],
      image: "/assets/projects/energy_forecasting.png",
      pdf: "/assets/projects/energy_forecasting.pdf"
    },
    // {
    //   title: "Q-Learning Airport Optimisation",
    //   description: "Optimised airport rubbish collecting machine using Q-learning, achieving 90% efficiency in waste collection.",
    //   tools: ["Python"],
    //   image: "/assets/projects/robotic.png"
    // },
    {
      title: "SvelteKit and TailwindCSS Portfolio",
      description: "Developed a responsive portfolio with SvelteKit and TailwindCSS featuring a comprehensive design system using CSS variables for consistent styling. Implemented accessible components with ARIA attributes, smooth Svelte transitions, SEO optimisation, and Google Analytics integration while ensuring performance through Svelte's compiler design.",
      tools: ["SvelteKit", "TailwindCSS", "JavaScript", "HTML", "CSS", "Vercel", "Google Analytics", "SEO"],
      website: "/"
    },
    // {
    //   title: "A/B Testing Analysis",
    //   description: "Conducted A/B testing for a marketing campaign, resulting in a 15% increase in conversion rates.",
    //   tools: ["Python", "R", "SQL"],
    //   image: "/assets/projects/abtesting.png"
    // },
    // {
    //   title: "Tetris AI",
    //   description: "Implemented a Tetris heuristics evaluation AI, scored 28,000+ points using 400 blocks, 80th percentile in UCL's cohort",
    //   tools: ["Python", "NumPy", "Pygame"],
    //   image: "/assets/projects/tetris.png"
    // },
    // {
    //   title: "Titanic Exploratory Data Analysis",
    //   description: "Conducted exploratory data analysis on Titanic dataset, visualizing survival rates and passenger demographics.",
    //   tools: ["R", "ggplot2", "dplyr", "tidyverse"],
    //   image: "/assets/projects/titanic.png",
    //   pdf: "/assets/projects/titanic.pdf"
    // },
  ];

  const educationItems = [
    {
      logo: '/assets/imperial.png',
      institution: 'Imperial College London',
      degree: 'MSc in Business Analytics',
      dates: '2024 → 2025',
      courses: [
        "Generative AI and Large Language Models",
        "Machine Learning",
        "Financial Analytics",
        "Text Analytics",
        "Digital Marketing Analytics",
        "Logistics and Supply Chain Analytics",
        "Energy Analytics",
        "Network Analytics",
        "Optimisation and Decision Models",
        "Statistics and Econometrics",
        "Data Visualisation",
        "Data Management and Ethics"
      ],
      achievements: []
    },
    {
      logo: '/assets/ucl.png',
      institution: 'University College London',
      degree: 'BSc in Computer Science',
      dates: '2021 → 2024',
      courses: [
        "Data Structures and Algorithms",
        "Machine Learning",
        "Reinforcement Learning",
        "Software Engineering",
        "Object-Oriented Programming",
        "Cyber Security",
        "Mathematics and Statistics",
        "Theory of Computation",
        "Computer Architecture and Concurrency",
        "Logic"
      ],
      achievements: []
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

  <StickyTitleSection title="Projects" id="projects">
    <ProjectList items={projectItems} />
  </StickyTitleSection>
  
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