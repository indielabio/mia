<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);

  const topSpecialties = [
    {
      name: 'Anxiety',
      description: 'Managing worry, panic, and overwhelming fears',
      icon: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 9v3.75m9-.75a9 9 0 11-18 0 9 9 0 0118 0zm-9 3.75h.008v.008H12v-.008z"/></svg>`,
    },
    {
      name: 'Depression',
      description: 'Finding hope and meaning through darkness',
      icon: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 3v2.25m6.364.386l-1.591 1.591M21 12h-2.25m-.386 6.364l-1.591-1.591M12 18.75V21m-4.773-4.227l-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0z"/></svg>`,
    },
    {
      name: "Women's Issues",
      description: 'Supporting women through life transitions',
      icon: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M21 8.25c0-2.485-2.099-4.5-4.688-4.5-1.935 0-3.597 1.126-4.312 2.733-.715-1.607-2.377-2.733-4.313-2.733C5.1 3.75 3 5.765 3 8.25c0 7.22 9 12 9 12s9-4.78 9-12z"/></svg>`,
    },
  ];

  const expertise = [
    'Bisexual',
    'Coping Skills',
    'Family Conflict',
    'Grief',
    'Lesbian',
    'LGBTQ+',
    'Mood Disorders',
    'Relationship Issues',
    'Stress',
    'Thinking Disorders',
    'Transgender',
    'Trauma and PTSD',
  ];

  $effect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            visible = true;
          }
        });
      },
      { threshold: 0.1 }
    );

    if (sectionRef) {
      observer.observe(sectionRef);
    }

    return () => observer.disconnect();
  });
</script>

<section class="specialties section" id="specialties" bind:this={sectionRef}>
  <div class="specialties-bg">
    <div class="bg-shape bg-shape-1"></div>
    <div class="bg-shape bg-shape-2"></div>
  </div>

  <div class="specialties-container" class:visible>
    <div class="specialties-header">
      <div class="section-label">Specialties & Expertise</div>
      <h2>How I Can Help</h2>
      <p>
        I offer specialized support across a wide range of mental health concerns, creating
        personalized treatment approaches for each individual.
      </p>
    </div>

    <div class="top-specialties">
      {#each topSpecialties as specialty, index}
        <div class="specialty-card featured" style="animation-delay: {0.15 * index}s">
          <div class="specialty-icon">
            {@html specialty.icon}
          </div>
          <h3>{specialty.name}</h3>
          <p>{specialty.description}</p>
        </div>
      {/each}
    </div>

    <div class="expertise-section">
      <h3 class="expertise-title">Additional Areas of Expertise</h3>
      <div class="expertise-grid">
        {#each expertise as item, index}
          <div class="expertise-tag" style="animation-delay: {0.05 * index + 0.4}s">
            <span class="expertise-dot"></span>
            {item}
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  .specialties {
    background: var(--cream);
    position: relative;
    overflow: hidden;
  }

  .specialties-bg {
    position: absolute;
    inset: 0;
    pointer-events: none;
  }

  .bg-shape {
    position: absolute;
    border-radius: 50%;
    opacity: 0.08;
  }

  .bg-shape-1 {
    width: 600px;
    height: 600px;
    background: var(--sage);
    top: -200px;
    right: -200px;
  }

  .bg-shape-2 {
    width: 400px;
    height: 400px;
    background: var(--terracotta);
    bottom: -150px;
    left: -100px;
  }

  .specialties-container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 var(--space-lg);
    position: relative;
    z-index: 1;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.6s var(--ease-out-expo);
  }

  .specialties-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .specialties-header {
    text-align: center;
    margin-bottom: var(--space-2xl);
  }

  .section-label {
    font-size: 0.8rem;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--sage);
    margin-bottom: var(--space-sm);
  }

  .specialties-header h2 {
    margin-bottom: var(--space-md);
  }

  .specialties-header p {
    color: var(--charcoal-soft);
    max-width: 600px;
    margin: 0 auto;
  }

  /* Top Specialties Grid */
  .top-specialties {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--space-lg);
    margin-bottom: var(--space-2xl);
  }

  .specialty-card {
    background: var(--off-white);
    border-radius: 24px;
    padding: var(--space-xl);
    text-align: center;
    box-shadow: var(--shadow-soft);
    transition: all 0.4s var(--ease-out-expo);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.6s var(--ease-out-expo) forwards;
  }

  .specialty-card:hover {
    transform: translateY(-8px);
    box-shadow: var(--shadow-lifted);
  }

  .specialty-icon {
    width: 56px;
    height: 56px;
    margin: 0 auto var(--space-md);
    background: linear-gradient(135deg, var(--sage-light), var(--sage));
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    transition: transform 0.3s var(--ease-out-expo);
  }

  .specialty-card:hover .specialty-icon {
    transform: scale(1.1);
  }

  .specialty-icon :global(svg) {
    width: 28px;
    height: 28px;
  }

  .specialty-card h3 {
    font-size: 1.25rem;
    margin-bottom: var(--space-sm);
    color: var(--charcoal);
  }

  .specialty-card p {
    font-size: 0.9rem;
    color: var(--charcoal-soft);
    line-height: 1.6;
  }

  /* Expertise Section */
  .expertise-section {
    background: var(--off-white);
    border-radius: 30px;
    padding: var(--space-xl);
    box-shadow: var(--shadow-soft);
  }

  .expertise-title {
    font-size: 1.1rem;
    text-align: center;
    margin-bottom: var(--space-lg);
    color: var(--charcoal-soft);
    font-weight: 400;
  }

  .expertise-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: var(--space-sm);
  }

  .expertise-tag {
    display: inline-flex;
    align-items: center;
    gap: var(--space-xs);
    background: var(--cream);
    padding: var(--space-sm) var(--space-md);
    border-radius: 100px;
    font-size: 0.9rem;
    color: var(--charcoal-soft);
    transition: all 0.3s var(--ease-out-soft);
    opacity: 0;
    transform: translateY(10px);
    animation: fadeInUp 0.4s var(--ease-out-expo) forwards;
  }

  .expertise-tag:hover {
    background: var(--sage-light);
    color: var(--charcoal);
    transform: translateY(-2px);
  }

  .expertise-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--terracotta);
    flex-shrink: 0;
  }

  @media (max-width: 900px) {
    .top-specialties {
      grid-template-columns: 1fr;
      gap: var(--space-md);
    }

    .specialty-card {
      padding: var(--space-lg);
    }

    .expertise-section {
      padding: var(--space-lg);
    }

    .expertise-tag {
      font-size: 0.85rem;
      padding: var(--space-xs) var(--space-md);
    }
  }

  @media (min-width: 600px) and (max-width: 900px) {
    .top-specialties {
      grid-template-columns: repeat(2, 1fr);
    }

    .top-specialties .specialty-card:last-child {
      grid-column: span 2;
      max-width: 400px;
      margin: 0 auto;
    }
  }
</style>
