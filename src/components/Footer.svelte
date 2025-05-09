<script>
  import UnderLineLink from './UnderLineLink.svelte';
</script>

<footer class="w-full mt-24"
        style="padding-left: var(--spacing-header-footer-x); 
               padding-right: var(--spacing-header-footer-x);"
>
<div class="mx-auto border-t border-neutral-300"
     style="max-width: var(--max-container-width);
            padding-top: var(--spacing-header-footer-y); 
            padding-bottom: var(--spacing-header-footer-y);">
    <!-- Main Footer Content -->
    <div class="flex flex-col sm:flex-row justify-between items-center gap-4">
      <!-- Email (Left) -->
      <div class="flex items-center gap-2">
        <i class="fa-regular fa-envelope text-[var(--color-accent)] w-5"></i>
        <UnderLineLink 
          href="mailto:wei.cheong24@imperial.ac.uk"
          text="wei.cheong24@imperial.ac.uk"
        />
      </div>
      
      <!-- Social Links (Right) -->
      <div class="flex items-center gap-4">
        <!-- LinkedIn -->
        <a href="https://linkedin.com/in/bryancwx" target="_blank" class="hover:text-[var(--color-accent)]" aria-label="LinkedIn">
          <i class="fa-brands fa-linkedin text-lg"></i>
        </a>
        
        <!-- GitHub -->
        <a href="https://github.com/Bryan-Cheong" target="_blank" class="hover:text-[var(--color-accent)]" aria-label="GitHub">
          <i class="fa-brands fa-github text-lg"></i>
        </a>
      </div>
    </div>

    <!-- Copyright and Legal -->
    <div class="flex flex-col sm:flex-row justify-between mt-10 pt-6">
      <small class="text-muted">© {new Date().getFullYear()} Bryan Cheong. All rights reserved.</small>
      <div class="flex gap-4 mt-2 sm:mt-0">
        <small><a href="/assets/privacy.pdf" class="text-muted hover:text-[var(--color-accent)]">Privacy Policy</a></small>
        <small><a href="/assets/terms.pdf" class="text-muted hover:text-[var(--color-accent)]">Terms of Use</a></small>
      </div>
    </div>
  </div>
</footer>