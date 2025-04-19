<script>
  import { onMount } from 'svelte';
  
  // Technical skills with proficiency levels
  const technicalSkills = [
    { name: "Python", level: 90 },
    { name: "R", level: 85 },
    { name: "SQL", level: 80 },
    { name: "Machine Learning", level: 85 },
    { name: "Data Visualization", level: 90 },
    { name: "Statistical Analysis", level: 85 },
    { name: "JavaScript", level: 70 },
    { name: "Power BI", level: 75 }
  ];
  
  // Soft skills
  const softSkills = [
    "Data Storytelling",
    "Problem Solving",
    "Communication",
    "Project Management",
    "Critical Thinking",
    "Team Collaboration"
  ];
  
  // Animation states
  let isReady = $state(false);
  let runText = $state(true);
  let visibleSkills = $state([]);
  let visibleSoftSkills = $state(false);
  let bioVisible = $state(false);
  let sectionRef;
  
  onMount(() => {
    if (typeof IntersectionObserver !== 'undefined') {
      const observer = new IntersectionObserver((entries) => {
        const [entry] = entries;
        
        if (entry.isIntersecting) {
          // Start the animation sequence when section is visible
          setTimeout(() => {
            isReady = true;
            
            setTimeout(() => {
              runText = false;
              bioVisible = true;
              
              setTimeout(() => {
                visibleSoftSkills = true;
              }, 300);
              
              technicalSkills.forEach((_, index) => {
                setTimeout(() => {
                  visibleSkills = [...visibleSkills, index];
                }, 150 * index);
              });
            }, 1000);
          }, 300);
          
          // Unobserve after triggering the animation
          observer.unobserve(entry.target);
        }
      }, {
        threshold: 0.1 // Trigger when 10% of the section is visible
      });
      
      // Start observing the section
      observer.observe(sectionRef);
    }
  });
</script>

<div class="grid grid-cols-1 lg:grid-cols-3 gap-12" bind:this={sectionRef}>
  <!-- Bio Section -->
  <div class="lg:col-span-2">
    <h3 class="text-xl font-medium mb-6">My Story</h3>
    <div class="prose prose-neutral max-w-none">
      {#if isReady}
        {#if runText}
          <!-- Loading placeholder for bio -->
          <div class="space-y-4">
            <div class="w-full h-4 bg-neutral-300 animate-pulse rounded"></div>
            <div class="w-full h-4 bg-neutral-300 animate-pulse rounded"></div>
            <div class="w-full h-4 bg-neutral-300 animate-pulse rounded"></div>
            <div class="w-3/4 h-4 bg-neutral-300 animate-pulse rounded"></div>
          </div>
        {:else}
          <!-- Actual bio text with fade-in animation -->
          <div class="transition-all duration-500" 
               class:opacity-0={!bioVisible} 
               class:opacity-100={bioVisible}
               class:transform={true}
               class:translate-y-4={!bioVisible}
               class:translate-y-0={bioVisible}>
            <p>
              With a background in Computer Science from University College London and currently pursuing a Master's in Business Analytics at Imperial College London, I bring a unique blend of technical expertise and business acumen to data analysis.
            </p>
            <p>
              My experience spans quantitative finance, data visualization, and software reliability, giving me a comprehensive understanding of how data drives decision-making across industries. I'm passionate about transforming complex data into actionable insights that help organizations thrive.
            </p>
            <p>
              Throughout my career, I've worked with diverse teams to develop analytical solutions that address real-world challenges. Whether it's predicting market trends, optimizing business processes, or enhancing customer experiences, I approach each project with curiosity and rigor.
            </p>
          </div>
        {/if}
      {/if}
    </div>
    
    <!-- Soft Skills -->
    <h3 class="text-xl font-medium mt-10 mb-6">Soft Skills</h3>
    <div class="flex flex-wrap gap-3">
      {#each softSkills as skill, i}
        <span 
          class="px-4 py-2 bg-blue-100 text-blue-900 rounded-full text-sm font-medium transition-all duration-500"
          style="transition-delay: {i * 100}ms;"
          class:opacity-0={!visibleSoftSkills}
          class:opacity-100={visibleSoftSkills}
          class:transform={true}
          class:scale-90={!visibleSoftSkills}
          class:scale-100={visibleSoftSkills}
        >
          {skill}
        </span>
      {/each}
    </div>
  </div>
  
  <!-- Rest of your component remains the same -->
  <!-- Technical Skills with Progress Bars -->
  <div>
    <h3 class="text-xl font-medium mb-6">Technical Skills</h3>
    <div class="flex flex-col gap-5">
      {#each technicalSkills as { name, level }, i}
        <div class="transition-all duration-300" 
             style="transition-delay: {i * 150}ms;"
             class:opacity-0={!visibleSkills.includes(i) && !runText}
             class:opacity-100={visibleSkills.includes(i) || runText}
             class:transform={true}
             class:translate-y-4={!visibleSkills.includes(i) && !runText}
             class:translate-y-0={visibleSkills.includes(i) || runText}>
          <div class="flex justify-between mb-1">
            <span class="font-medium">{name}</span>
            <span class="text-neutral-500 text-sm">{visibleSkills.includes(i) ? level + '%' : ''}</span>
          </div>
          <div class="h-2 w-full bg-neutral-200 rounded-full overflow-hidden">
            {#if isReady}
              {#if runText}
                <div class="h-full bg-neutral-300 animate-pulse rounded-full" style="width: 100%"></div>
              {:else}
                <div 
                  class="h-full bg-blue-900 rounded-full transition-all duration-1000 ease-out" 
                  style="width: {visibleSkills.includes(i) ? level + '%' : '0%'}"
                ></div>
              {/if}
            {/if}
          </div>
        </div>
      {/each}
    </div>
  </div>
</div>