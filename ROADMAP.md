# Portfolio Enhancement Roadmap  
_Refining design, ensuring performance, and implementing advanced features for a polished, professional portfolio._

---

## Phase 1: Foundation & Consistency  
*Establish a solid design system and responsive foundation.*

### Typography & Design System
- [x] Standardise font sizes using `clamp()` `[HIGH]`
- [x] Use numeric `font-weight` consistently `[HIGH]`
- [ ] Extract colour palette into CSS variables `[HIGH]`
- [ ] Review spacing (`gap`, `padding`, `margin`) for consistency `[HIGH]`
- [x] Finalise responsive behaviour across all devices `[HIGH]`
- [ ] Explore dynamic colour themes (light/dark/custom themes) `[MEDIUM]`

---

## Phase 2: Component Refinement  
*Polish core components and ensure UI/UX consistency.*

### Navigation & Header
- [x] Refactor `UnderLineLink` component `[HIGH]`
- [x] Refactor `Header` component `[HIGH]`
- [x] Improve active link state styling `[HIGH]`
- [x] Enhance mobile menu accessibility (ARIA roles, focus management) `[MEDIUM]`
- [x] Prevent scrolling when mobile nav bar is open. `[MEDIUM]`
- [x] Improve the scroll progress bar, more responsive `[MEDIUM]`

### Projects Section
- [ ] Polish project card layout, find inspirations `[HIGH]`
- [ ] Insert finalised project content with visuals and descriptions `[HIGH]`
- [ ] Implement filtering by tools/technologies `[LOW]`

### Experience & Education
- [x] Finalise layout (timeline) `[HIGH]`
- [x] Ensure mobile-friendly and consistent design `[HIGH]`

### Footer
- [ ] Standardise spacing and link structure `[MEDIUM]`
- [ ] Add Google Analytics to Privacy Policy and Terms document `[MEDIUM]`
- [ ] Add relevant links or social icons `[LOW]`

### Form
- [ ] Add email form for contact `[LOW]`

---

## Phase 3: Performance & SEO  
*Optimise for visibility, speed, and analytics.*

### SEO Optimisation
- [ ] Implement meta tags using `<svelte:head>` `[HIGH]`
- [ ] Add favicon and social preview images `[MEDIUM]`

### Analytics Integration
- [ ] Set up Google Analytics and Tag Manager `[HIGH]`
- [ ] Ensure GDPR compliance if required `[MEDIUM]`

### Performance Improvements
- [ ] Lazy load images and assets `[HIGH]`
- [ ] Optimise SVGs and other media `[MEDIUM]`
- [ ] Review and improve Lighthouse performance scores `[MEDIUM]`

---

## Phase 4: Advanced Features  
*Enhance interactivity, accessibility, and deployment readiness.*

### UI Enhancements
- [ ] Implement dark mode or theme switcher `[MEDIUM]`
- [ ] Add micro-interactions (hover effects, smooth transitions) `[LOW]`

### Accessibility Improvements
- [ ] Ensure full keyboard navigation support `[MEDIUM]`
- [ ] Verify colour contrast ratios `[MEDIUM]`
- [ ] Add ARIA labels where appropriate `[MEDIUM]`

### Deployment & Optimisation
- [x] Set up deployment pipeline (e.g., Vercel or Netlify) `[HIGH]`
- [ ] Connect custom domain `[HIGH]`
- [ ] Configure basic CI/CD workflow `[LOW]`

---