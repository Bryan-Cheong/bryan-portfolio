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
      logo: '/assets/tecno.png',
      company: 'Tecno International (Capstone Project) - London',
      title: 'LLM Agent Engineer',
      dates: 'June 2025 → August 2025',
      responsibilities: [
        "Designed multi-agent pipeline (Self-Assessment, Research, Strategy) using GPT-4.1 to automate SME ESG consulting",
        "Prototyped Weaviate RAG with hybrid BM25 + embeddings + Reciprocal Rank Fusion to retrieve and contextualise ESG insights",
        "Auto-generated ESG reports and enabled live in-chat edits, cutting analysis time 75% and freeing consultants for higher-order work",
        "Optimised token usage via context compression and caching, reducing API costs by 20% without quality loss",
        "Developed PDF ingestion pipeline using PyMuPDF + LLM extraction to auto-populate client profiles, cutting onboarding by 70%"
      ]
    },
    {
      logo: '/assets/anavio.avif',
      company: 'Anavio Capital Partners LLP - London',
      title: 'Equity Analytics Intern - Long/Short Strategy',
      dates: 'July 2023 → September 2023',
      responsibilities: [
        "Built a Python dashboard to uncover patterns in firm-level efficiency across 15+ metrics, identifying outliers for investment decisions",
        "Scaled coverage from 10 to 200 tickers and automated 80% of manual analysis, accelerating idea generation for the portfolio manager",
        "Enhanced pipeline robustness with 100+ Pytest tests and six error-handling decorators, minimising production risk and downtime",
        "Translated business rules into flowcharts to clarify logic and align tool design with non-technical stakeholders, halving delivery time"
      ]
    },
    {
      logo: '/assets/gse.png',
      company: 'GSE-M Technology - Malaysia',
      title: 'Enterprise Resource Planning (ERP) Assistant',
      dates: 'May 2023 → July 2023',
      responsibilities: [
        "Partnered with five departments to gather 30+ requirements, resolve critical bugs, and address operational pain points",
        "Streamlined ERP with consultants and co-led training for 90 staff, improving process efficiency by 25%"
      ]
    },
    {
      logo: 'assets/britishredcross.png',
      company: 'British Red Cross - London',
      title: 'Data Analyst',
      dates: 'September 2022 → April 2023',
      responsibilities: [
        "Developed 20+ Power BI dashboards to visualise behavioural trends in complaints across the UK for operational and senior teams",
        "Defined resolution KPIs and identified delay drivers, reducing resolution time by 50% and improving service outcomes for customers",
        "Built an ETL pipeline from four sources and used DAX for geographical drill-downs, enabling scalable and customised reporting",
        "Secured future development by presenting a streamlined issue resolution system along with a deployment manual to the Head of Data"
      ]
    },
    {
      logo: 'assets/subplace.png',
      company: 'Subplace - Malaysia',
      title: 'Software Reliability Intern',
      dates: 'June 2022 → August 2022',
      responsibilities: [
        "Cut maintenance time by 60% via modular and systematic test case templates, improving stability for a SQL-backed platform",
        "Resolved 200+ issues and introduced agile, test-driven development practices to enhance reliability and support continuous delivery"
      ]
    }
  ];

  const projectItems = [
    {
      title: "Multi-Channel Attribution",
      description: "Analysed 3.3M contacts and 240K orders to compare catalogue vs. email campaign effectiveness with PostgreSQL. Computed attribution models (first-, last-, linear-click), revealing catalogue's six times higher conversion. Segmented customers into 125 RFM cells, estimated CLV, and recommended targeting strategies based on breakeven cost and ROI.",
      tools: ["PostgreSQL", "Multi-Channel Attribution Modelling", "ROI and Breakeven Cost Analysis", "RFM Segmentation", "CLV Estimation"],
      image: "/assets/projects/attribution.png",
      pdf: "/assets/projects/attribution.zip",
    },
    {
      title: "Portfolio A/B Testing & Analytics.",
      description: "Ran A/B tests with VWO to measure impact of clickbait vs professional phrasing on my portfolio website's “Download CV” CTA; the professional version saw a statistically significant 70.3% higher CTR. Drove traffic via social media, Selenium bots, and a targeted Google Ads campaign; tracked conversions and bounce rate using event-based analytics.",
      tools: ["A/B Testing", "VWO", "Google Analytics", "Google Ads", "Selenium", "Two-sided z-test"],
      image: "/assets/projects/abtest.png",
      pdf: "/assets/projects/abtest.pdf",
      website: "/"
    },
    {
      title: "Text Analytics Project on Song Lyrics",
      description: "Modelled 40,000+ lyrics through LASSO regression with n-grams and FastText embeddings to explore song popularity drivers. Discovered eight genre-level trends in explicitness and thematic content. Leveraged PCA-filtering and cosine similarity on word vectors to quantify semantic shifts between artists' first albums and subsequent works.",
      tools: ["R", "tidyverse", "quanteda", "textclean", "glmnet", "FastText word embeddings", "sentimentr", "stm",],
      image: "/assets/projects/song.png",
      pdf: "/assets/projects/song.pdf"
    },
    {
      title: "RecSys Purchase Prediction",
      description: "Built a two-stage pipeline on 33M clicks and 1.1M purchases to predict purchasing sessions with XGBoost and forecast items bought via heuristic ranking. Engineered 21 features with temporal encodings and rarity filters. Tuned thresholds to optimise a Jaccard-based score and used SHAP to interpret key drivers like session duration and item popularity.",
      tools: ["Python", "Pandas", "XGBoost", "SHAP", "PostgreSQL", "Feature Engineering", "Heuristic Ranking"],
      image: "/assets/projects/recsys.png",
      pdf: "/assets/projects/recsys.pdf"
    },
    {
      title: "Beat the Bookies",
      description: "Engineered a Premier League match predictor using 18 features across five seasons (older data degraded performance), achieving 51% validation and ~40% test accuracy with CatBoost. Feature-engineered Pi-rating variants with tuned hyperparameters and selected key variables using SHAP. Explored pre-game sentiment as a predictive signal using LLMs and Nitter API.",
      tools: ["Python", "Pandas", "CatBoost", "Random Forest", "SHAP", "Nitter API", "Pi-rating", "VADER"],
      image: "/assets/projects/bookies.png",
      pdf: "/assets/projects/bookies.pdf"
    },
    {
      title: "RIE Cleaning of Lagged Covariance Matrices",
      description: "Developed a spectral cleaning algorithm using Rotationally Invariant Estimators, shrinking noise in high-dimensional lagged covariance matrices. Achieved 100% noise reduction in AR(0) and ~20% signal-to-noise improvement in AR(1), with more gains as dimensionality increased. Applicable to portfolio risk modelling, time series forecasting, and signal processing.",
      tools: ["Python", "NumPy", "Pandas", "Matplotlib", "SciPy", "scikit-learn", "Statsmodels", "Marchenko-Pastur law", "SVD", "Rotationally Invariant Estimators", ],
      image: "/assets/projects/rie.png",
      pdf: "assets/projects/rie.pdf",
      github: "https://github.com/Bryan-Cheong/RIE-Singular-Value-Cleaning-of-Lagged-Covariance-Matrices"
    },
    {
      title: "Logistics and Supply Chain Optimisation",
      description: "Simulated a multi-region supply chain implementing hybrid demand forecasting (SARIMA, Croston's method) and cost-benefit analysis to guide factory and warehouse expansion. Applied adjusted reorder points and Silver-Meal heuristics to manage seasonal inventory, securing 2nd place in Imperial's cohort.",
      tools: ["Python", "R", "Excel", "SARIMA", "Croston's method", "Silver-Meal heuristic", "Linear regression"],
      image: "/assets/projects/logistics.png",
      pdf: "/assets/projects/logistics.pdf"
    },
    {
      title: "Energy Demand Forecasting",
      description: "Developed and tuned XGBoost model to forecast UK electricity demand, engineering features like Heating Degree Days, holiday dummies, and temporal lags. Achieved 96.3% R²; generalises well with low residual autocorrelation.",
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
    }
  ];

  const educationItems = [
    {
      logo: '/assets/imperial.png',
      institution: 'Imperial College London',
      degree: 'MSc in Business Analytics (Distinction, 78%)',
      dates: '2024 → 2025',
      courses: [
        "Generative AI and Large Language Models",
        "Machine Learning",
        "Statistics and Econometrics",
        "Optimisation and Decision Models",
        "Digital Marketing Analytics",
        "Financial Analytics",
        "Text Analytics",
        "Network Analytics",
        "Energy Analytics",
        "Logistics and Supply Chain Analytics",
        "Data Visualisation",
        "Data Management and Ethics"
      ],
      achievements: []
    },
    {
      logo: '/assets/ucl.png',
      institution: 'University College London',
      degree: 'BSc in Computer Science (Upper Second-Class Honours, 68%)',
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