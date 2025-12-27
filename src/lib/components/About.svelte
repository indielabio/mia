<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);

  $effect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            visible = true;
          }
        });
      },
      { threshold: 0.2 }
    );

    if (sectionRef) {
      observer.observe(sectionRef);
    }

    return () => observer.disconnect();
  });
</script>

<section class="about section" id="about" bind:this={sectionRef}>
  <div class="about-container" class:visible>
    <div class="about-image-wrapper">
      <div class="about-image-frame">
        <!-- Placeholder image using a gradient -->
        <div class="about-image-placeholder">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path
              d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
            />
          </svg>
          <span>Secondary Image</span>
        </div>
      </div>
      <!-- Decorative leaf -->
      <div class="about-decoration">
        <svg viewBox="0 0 100 100" fill="none">
          <path
            d="M50 0C50 0 20 30 20 60C20 90 50 100 50 100C50 100 80 90 80 60C80 30 50 0 50 0Z"
            fill="var(--sage)"
            opacity="0.2"
          />
          <path
            d="M50 20V80M35 40Q50 50 65 40M35 60Q50 70 65 60"
            stroke="var(--sage)"
            stroke-width="1.5"
            opacity="0.4"
          />
        </svg>
      </div>
    </div>

    <div class="about-content">
      <div class="section-label">About</div>
      <h2>Mia Dessesaure, LCSW</h2>

      <div class="about-text">
        <p>
          My mission is to provide a safe, nonjudgmental space where you can feel seen and
          supported. Whether you're struggling with anxiety, relationship challenges, or life
          transitions, I help clients uncover their strengths and build tools for lasting change.
          Together, we'll work toward balance, healing, and a more peaceful version of yourself.
        </p>

        <p>
          I help clients of all ages navigate anxiety, depression, ADHD, life transitions, and
          relational challenges. Using evidence-based approaches like CBT, mindfulness, play
          therapy, and strength-based techniques, I guide clients to build skills, draw on their
          strengths, and achieve meaningful, lasting change.
        </p>

        <p>
          I understand that seeking support can feel overwhelming. I meet you where you are,
          honoring your experiences and guiding you toward clarity, growth, and balance. Together,
          we'll create a space where you feel heard, supported, and empowered to take meaningful
          steps forward.
        </p>
      </div>

      <div class="about-credentials">
        <div class="credential">
          <span class="credential-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path
                d="M4.26 10.147a60.436 60.436 0 00-.491 6.347A48.627 48.627 0 0112 20.904a48.627 48.627 0 018.232-4.41 60.46 60.46 0 00-.491-6.347m-15.482 0a50.57 50.57 0 00-2.658-.813A59.905 59.905 0 0112 3.493a59.902 59.902 0 0110.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.697 50.697 0 0112 13.489a50.702 50.702 0 017.74-3.342M6.75 15a.75.75 0 100-1.5.75.75 0 000 1.5zm0 0v-3.675A55.378 55.378 0 0112 8.443m-7.007 11.55A5.981 5.981 0 006.75 15.75v-1.5"
              />
            </svg>
          </span>
          <span>Licensed Clinical Social Worker</span>
        </div>
        <div class="credential">
          <span class="credential-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path
                d="M9 12.75L11.25 15 15 9.75M21 12c0 1.268-.63 2.39-1.593 3.068a3.745 3.745 0 01-1.043 3.296 3.745 3.745 0 01-3.296 1.043A3.745 3.745 0 0112 21c-1.268 0-2.39-.63-3.068-1.593a3.746 3.746 0 01-3.296-1.043 3.745 3.745 0 01-1.043-3.296A3.745 3.745 0 013 12c0-1.268.63-2.39 1.593-3.068a3.745 3.745 0 011.043-3.296 3.746 3.746 0 013.296-1.043A3.746 3.746 0 0112 3c1.268 0 2.39.63 3.068 1.593a3.746 3.746 0 013.296 1.043 3.746 3.746 0 011.043 3.296A3.745 3.745 0 0121 12z"
              />
            </svg>
          </span>
          <span>7+ Years Experience</span>
        </div>
      </div>

      <a href="#contact" class="btn btn-secondary">Get in Touch</a>
    </div>
  </div>
</section>

<style>
  .about {
    background: var(--cream);
    position: relative;
    overflow: hidden;
  }

  .about::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--tan-light), transparent);
  }

  .about-container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 var(--space-lg);
    display: grid;
    grid-template-columns: 1fr 1.2fr;
    gap: var(--space-2xl);
    align-items: center;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s var(--ease-out-expo);
  }

  .about-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .about-image-wrapper {
    position: relative;
  }

  .about-image-frame {
    border-radius: 30px;
    overflow: hidden;
    box-shadow: var(--shadow-medium);
  }

  .about-image-placeholder {
    aspect-ratio: 4/5;
    background: linear-gradient(135deg, var(--warm-gray) 0%, var(--cream) 100%);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: var(--space-md);
    color: var(--charcoal-soft);
  }

  .about-image-placeholder svg {
    width: 48px;
    height: 48px;
    opacity: 0.5;
  }

  .about-image-placeholder span {
    font-size: 0.875rem;
    opacity: 0.6;
  }

  .about-decoration {
    position: absolute;
    bottom: -30px;
    right: -30px;
    width: 120px;
    height: 120px;
    animation: gentleFloat 6s ease-in-out infinite;
  }

  .about-content {
    display: flex;
    flex-direction: column;
    gap: var(--space-lg);
  }

  .section-label {
    font-size: 0.8rem;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--sage);
  }

  .about-content h2 {
    margin-top: calc(var(--space-sm) * -1);
  }

  .about-text {
    display: flex;
    flex-direction: column;
    gap: var(--space-md);
  }

  .about-text p {
    color: var(--charcoal-soft);
    line-height: 1.8;
  }

  .about-credentials {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-lg);
    padding: var(--space-lg) 0;
    border-top: 1px solid var(--warm-gray);
    border-bottom: 1px solid var(--warm-gray);
  }

  .credential {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
    font-size: 0.9rem;
    color: var(--charcoal-soft);
  }

  .credential-icon {
    width: 24px;
    height: 24px;
    color: var(--terracotta);
  }

  .credential-icon svg {
    width: 100%;
    height: 100%;
  }

  @media (max-width: 900px) {
    .about-container {
      grid-template-columns: 1fr;
      gap: var(--space-xl);
    }

    .about-image-wrapper {
      max-width: 400px;
      margin: 0 auto;
    }

    .about-decoration {
      width: 80px;
      height: 80px;
      bottom: -20px;
      right: -20px;
    }

    .about-credentials {
      flex-direction: column;
      gap: var(--space-md);
    }
  }
</style>
