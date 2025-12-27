<script lang="ts">
  let visible = $state(false);

  $effect(() => {
    const timer = setTimeout(() => {
      visible = true;
    }, 100);
    return () => clearTimeout(timer);
  });
</script>

<section class="hero" id="hero">
  <!-- Decorative organic shapes -->
  <div class="hero-shapes">
    <div class="shape shape-1"></div>
    <div class="shape shape-2"></div>
    <div class="shape shape-3"></div>
  </div>

  <div class="hero-container" class:visible>
    <div class="hero-content">
      <img src="/images/logo.png" alt="Mia Dessesaure Therapy" class="hero-logo" />

      <p class="hero-tagline">
        My mission is to provide a safe, nonjudgmental space where you can feel seen and supported
      </p>

      <div class="hero-cta">
        <a href="#contact" class="btn btn-primary">Schedule Consultation</a>
        <a href="#about" class="btn btn-secondary">Learn More</a>
      </div>
    </div>

    <div class="hero-image-wrapper">
      <div class="hero-image-frame">
        <img src="/images/headshot.jpg" alt="Mia Dessesaure, LCSW" class="hero-image" />
      </div>
      <!-- Decorative accent -->
      <div class="hero-image-accent"></div>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="scroll-indicator" class:visible>
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<style>
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: calc(var(--space-3xl) + 60px) 0 var(--space-2xl);
    position: relative;
    overflow: hidden;
  }

  /* Decorative Shapes */
  .hero-shapes {
    position: absolute;
    inset: 0;
    pointer-events: none;
    overflow: hidden;
  }

  .shape {
    position: absolute;
    border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
    opacity: 0;
    animation: shapeAppear 1.5s var(--ease-out-expo) forwards;
  }

  .shape-1 {
    width: 500px;
    height: 500px;
    background: linear-gradient(135deg, var(--sage-light) 0%, transparent 70%);
    top: -150px;
    right: -100px;
    animation-delay: 0.3s;
  }

  .shape-2 {
    width: 300px;
    height: 300px;
    background: linear-gradient(45deg, var(--tan-light) 0%, transparent 70%);
    bottom: 10%;
    left: -50px;
    animation-delay: 0.5s;
  }

  .shape-3 {
    width: 200px;
    height: 200px;
    background: linear-gradient(180deg, var(--terracotta-light) 0%, transparent 80%);
    top: 40%;
    right: 15%;
    opacity: 0.1;
    animation-delay: 0.7s;
  }

  @keyframes shapeAppear {
    from {
      opacity: 0;
      transform: scale(0.8);
    }
    to {
      opacity: 0.15;
      transform: scale(1);
    }
  }

  .hero-container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 var(--space-lg);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--space-2xl);
    align-items: center;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.8s var(--ease-out-expo);
  }

  .hero-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .hero-content {
    display: flex;
    flex-direction: column;
    gap: var(--space-lg);
  }

  .hero-logo {
    width: 280px;
    height: auto;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.2s forwards;
  }

  .hero-tagline {
    font-family: var(--font-display);
    font-size: clamp(1.25rem, 2.5vw, 1.75rem);
    font-weight: 300;
    font-style: italic;
    line-height: 1.5;
    color: var(--charcoal-soft);
    max-width: 500px;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.4s forwards;
  }

  .hero-cta {
    display: flex;
    gap: var(--space-md);
    flex-wrap: wrap;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.6s forwards;
  }

  /* Hero Image */
  .hero-image-wrapper {
    position: relative;
    display: flex;
    justify-content: center;
    opacity: 0;
    transform: translateX(30px);
    animation: slideInRight 1s var(--ease-out-expo) 0.3s forwards;
  }

  @keyframes slideInRight {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .hero-image-frame {
    position: relative;
    width: 100%;
    max-width: 420px;
    border-radius: 200px 200px 40px 40px;
    overflow: hidden;
    box-shadow: var(--shadow-lifted);
  }

  .hero-image {
    width: 100%;
    height: auto;
    display: block;
    object-fit: cover;
    aspect-ratio: 3/4;
  }

  .hero-image-accent {
    position: absolute;
    width: 100%;
    height: 100%;
    max-width: 420px;
    border-radius: 200px 200px 40px 40px;
    border: 2px solid var(--sage);
    top: 15px;
    left: -15px;
    z-index: -1;
    opacity: 0;
    animation: accentAppear 0.8s var(--ease-out-expo) 0.8s forwards;
  }

  @keyframes accentAppear {
    to {
      opacity: 0.5;
    }
  }

  /* Scroll Indicator */
  .scroll-indicator {
    position: absolute;
    bottom: var(--space-lg);
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--space-sm);
    opacity: 0;
    transition: opacity 0.5s var(--ease-out-soft) 1.2s;
  }

  .scroll-indicator.visible {
    opacity: 1;
  }

  .scroll-indicator span {
    font-size: 0.75rem;
    font-weight: 500;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--charcoal-soft);
  }

  .scroll-line {
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--tan), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }

  @keyframes scrollPulse {
    0%,
    100% {
      transform: scaleY(1);
      opacity: 1;
    }
    50% {
      transform: scaleY(0.6);
      opacity: 0.5;
    }
  }

  /* Mobile */
  @media (max-width: 900px) {
    .hero {
      padding: calc(var(--space-2xl) + 80px) 0 var(--space-xl);
      min-height: auto;
    }

    .hero-container {
      grid-template-columns: 1fr;
      gap: var(--space-xl);
      text-align: center;
    }

    .hero-content {
      order: 2;
      align-items: center;
    }

    .hero-logo {
      width: 220px;
    }

    .hero-tagline {
      max-width: 100%;
    }

    .hero-cta {
      justify-content: center;
    }

    .hero-image-wrapper {
      order: 1;
    }

    .hero-image-frame {
      max-width: 300px;
    }

    .hero-image-accent {
      max-width: 300px;
    }

    .shape-1 {
      width: 300px;
      height: 300px;
      top: -100px;
      right: -80px;
    }

    .shape-2 {
      width: 200px;
      height: 200px;
    }

    .shape-3 {
      display: none;
    }

    .scroll-indicator {
      display: none;
    }
  }
</style>
