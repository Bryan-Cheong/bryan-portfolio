<script>
  // Technical skills with proficiency levels
  const technicalSkills = {
    proficient: ["Python", "R", "Data Visualization", "Statistical Analysis"],
    intermediate: ["SQL", "Machine Learning", "Power BI"],
    basic: ["JavaScript", "TensorFlow", "Docker"]
  };
  
  // Soft skills
  const softSkills = [
    "Data Storytelling",
    "Problem Solving",
    "Communication",
    "Project Management",
    "Critical Thinking",
    "Team Collaboration"
  ];
</script>

<div class="grid grid-cols-1 lg:grid-cols-3 gap-12">
  <!-- Bio Section -->
  <div class="lg:col-span-2">
    <h3 class="text-xl font-medium mb-6">My Story</h3>
    <div class="prose prose-neutral max-w-none">
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
    
    <!-- Soft Skills -->
    <h3 class="text-xl font-medium mt-10 mb-6">Soft Skills</h3>
    <div class="flex flex-wrap gap-3">
      {#each softSkills as skill}
        <span class="px-4 py-2 bg-blue-100 text-blue-900 rounded-full text-sm font-medium">
          {skill}
        </span>
      {/each}
    </div>
  </div>
  
  <!-- Technical Skills by Proficiency Level -->
  <div>
    <h3 class="text-xl font-medium mb-6">Technical Skills</h3>
    
    <!-- Proficient Skills -->
    <div class="mb-6">
      <h4 class="text-lg font-medium text-blue-900 mb-3">Proficient</h4>
      <div class="flex flex-wrap gap-2">
        {#each technicalSkills.proficient as skill}
          <span class="px-3 py-1.5 bg-blue-100 text-blue-900 rounded text-sm font-medium">
            {skill}
          </span>
        {/each}
      </div>
    </div>
    
    <!-- Intermediate Skills -->
    <div class="mb-6">
      <h4 class="text-lg font-medium text-blue-800 mb-3">Intermediate</h4>
      <div class="flex flex-wrap gap-2">
        {#each technicalSkills.intermediate as skill}
          <span class="px-3 py-1.5 bg-blue-50 text-blue-800 rounded text-sm font-medium">
            {skill}
          </span>
        {/each}
      </div>
    </div>
    
    <!-- Basic Skills -->
    <div>
      <h4 class="text-lg font-medium text-blue-700 mb-3">Basic</h4>
      <div class="flex flex-wrap gap-2">
        {#each technicalSkills.basic as skill}
          <span class="px-3 py-1.5 bg-stone-100 text-blue-700 rounded text-sm font-medium">
            {skill}
          </span>
        {/each}
      </div>
    </div>
  </div>
</div>