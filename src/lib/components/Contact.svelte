<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);

  const contactInfo = {
    phone: '(929) 684-0752',
    location: 'Bronx, NY 10475',
    websites: [
      { label: 'Psychology Today', url: 'https://www.psychologytoday.com/us/therapists/mia-dessesaure-bronx-ny/1612306' },
      { label: 'ZocDoc', url: 'https://www.zocdoc.com/practice/mia-dessesaure-therapy-148918' },
      { label: 'Headway', url: 'https://care.headway.co/providers/mia-dessesaure' },
    ],
    social: [
      {
        name: 'LinkedIn',
        url: 'https://www.linkedin.com/in/mia-dessesaure-lcsw-89a3b358/',
        icon: `<svg viewBox="0 0 24 24" fill="currentColor"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>`,
      },
    ],
  };

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

<section class="contact section" id="contact" bind:this={sectionRef}>
  <div class="contact-container" class:visible>
    <div class="contact-content">
      <div class="section-label">Contact</div>
      <h2>Begin Your Journey</h2>
      <p class="contact-intro">
        Taking the first step toward therapy is an act of courage. I'm here to support you on your
        path to healing and growth. Reach out today to schedule a consultation.
      </p>

      <div class="contact-cta">
        <a href="https://care.headway.co/providers/mia-dessesaure" class="btn btn-primary btn-large" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path
              d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
            />
          </svg>
          Schedule Consultation
        </a>
      </div>
    </div>

    <div class="contact-info-card">
      <div class="info-section">
        <h3>Get in Touch</h3>

        <a href="tel:{contactInfo.phone.replace(/\D/g, '')}" class="phone-link">
          <span class="phone-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path
                d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 002.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 01-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 00-1.091-.852H4.5A2.25 2.25 0 002.25 4.5v2.25z"
              />
            </svg>
          </span>
          <span class="phone-number">{contactInfo.phone}</span>
        </a>

        <div class="location-info">
          <span class="location-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path
                d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z"
              />
            </svg>
          </span>
          <span class="location-text">{contactInfo.location}</span>
        </div>
      </div>

      <div class="info-section">
        <h4>Find Me On</h4>
        <div class="website-links">
          {#each contactInfo.websites as site}
            <a href={site.url} class="website-link" target="_blank" rel="noopener">
              {site.label}
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path
                  d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25"
                />
              </svg>
            </a>
          {/each}
        </div>
      </div>

      <div class="info-section">
        <h4>Connect</h4>
        <div class="social-links">
          {#each contactInfo.social as social}
            <a
              href={social.url}
              class="social-link"
              target="_blank"
              rel="noopener"
              aria-label={social.name}
            >
              {@html social.icon}
            </a>
          {/each}
        </div>
      </div>

      <!-- Decorative element -->
      <div class="card-decoration">
        <svg viewBox="0 0 100 100" fill="none">
          <path
            d="M50 0C50 0 20 30 20 60C20 90 50 100 50 100C50 100 80 90 80 60C80 30 50 0 50 0Z"
            fill="var(--sage)"
            opacity="0.1"
          />
        </svg>
      </div>
    </div>
  </div>
</section>

<footer class="footer">
  <div class="footer-container">
    <div class="footer-logo">
      <img src="/images/logo.png" alt="Mia Dessesaure Therapy" />
    </div>
    <p class="footer-text">
      &copy; {new Date().getFullYear()} Mia Dessesaure Therapy. All rights reserved.
    </p>
  </div>
</footer>

<style>
  .contact {
    background: linear-gradient(180deg, var(--off-white) 0%, var(--cream) 100%);
    position: relative;
  }

  .contact-container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 var(--space-lg);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--space-2xl);
    align-items: center;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.6s var(--ease-out-expo);
  }

  .contact-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .section-label {
    font-size: 0.8rem;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--sage);
    margin-bottom: var(--space-sm);
  }

  .contact-content h2 {
    margin-bottom: var(--space-md);
  }

  .contact-intro {
    color: var(--charcoal-soft);
    margin-bottom: var(--space-xl);
    line-height: 1.8;
  }

  .contact-cta {
    display: flex;
    gap: var(--space-md);
  }

  .btn-large {
    padding: var(--space-md) var(--space-xl);
    font-size: 1rem;
  }

  .btn-large svg {
    width: 20px;
    height: 20px;
  }

  /* Contact Info Card */
  .contact-info-card {
    background: var(--off-white);
    border-radius: 30px;
    padding: var(--space-xl);
    box-shadow: var(--shadow-medium);
    position: relative;
    overflow: hidden;
  }

  .info-section {
    padding: var(--space-lg) 0;
    border-bottom: 1px solid var(--warm-gray);
  }

  .info-section:first-child {
    padding-top: 0;
  }

  .info-section:last-of-type {
    border-bottom: none;
    padding-bottom: 0;
  }

  .info-section h3 {
    font-size: 1.1rem;
    margin-bottom: var(--space-md);
    color: var(--charcoal);
  }

  .info-section h4 {
    font-family: var(--font-body);
    font-size: 0.85rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--charcoal-soft);
    margin-bottom: var(--space-md);
  }

  .phone-link {
    display: flex;
    align-items: center;
    gap: var(--space-md);
    color: var(--charcoal);
    transition: all 0.3s var(--ease-out-soft);
  }

  .phone-link:hover {
    color: var(--terracotta);
  }

  .phone-icon {
    width: 48px;
    height: 48px;
    background: linear-gradient(135deg, var(--terracotta-light), var(--terracotta));
    border-radius: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    flex-shrink: 0;
  }

  .phone-icon svg {
    width: 24px;
    height: 24px;
  }

  .phone-number {
    font-family: var(--font-display);
    font-size: 1.5rem;
    font-weight: 400;
  }

  .location-info {
    display: flex;
    align-items: center;
    gap: var(--space-md);
    margin-top: var(--space-md);
    color: var(--charcoal-soft);
  }

  .location-icon {
    width: 48px;
    height: 48px;
    background: linear-gradient(135deg, var(--sage-light), var(--sage));
    border-radius: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    flex-shrink: 0;
  }

  .location-icon svg {
    width: 24px;
    height: 24px;
  }

  .location-text {
    font-family: var(--font-display);
    font-size: 1.25rem;
    font-weight: 400;
  }

  .website-links {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
  }

  .website-link {
    display: inline-flex;
    align-items: center;
    gap: var(--space-xs);
    color: var(--charcoal-soft);
    font-size: 0.95rem;
    transition: all 0.3s var(--ease-out-soft);
  }

  .website-link:hover {
    color: var(--terracotta);
    transform: translateX(5px);
  }

  .website-link svg {
    width: 14px;
    height: 14px;
    opacity: 0.5;
  }

  .social-links {
    display: flex;
    gap: var(--space-md);
  }

  .social-link {
    width: 44px;
    height: 44px;
    background: var(--cream);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--charcoal-soft);
    transition: all 0.3s var(--ease-out-expo);
  }

  .social-link:hover {
    background: var(--terracotta);
    color: white;
    transform: translateY(-3px);
  }

  .social-link :global(svg) {
    width: 20px;
    height: 20px;
  }

  .card-decoration {
    position: absolute;
    bottom: -30px;
    right: -30px;
    width: 150px;
    height: 150px;
    opacity: 0.5;
    pointer-events: none;
  }

  /* Footer */
  .footer {
    background: var(--charcoal);
    padding: var(--space-xl) 0;
  }

  .footer-container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 var(--space-lg);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--space-md);
  }

  .footer-logo img {
    height: 50px;
    width: auto;
    filter: brightness(0) invert(1);
    opacity: 0.8;
  }

  .footer-text {
    color: rgba(255, 255, 255, 0.5);
    font-size: 0.85rem;
  }

  @media (max-width: 900px) {
    .contact-container {
      grid-template-columns: 1fr;
      gap: var(--space-xl);
    }

    .contact-content {
      text-align: center;
    }

    .contact-intro {
      max-width: 100%;
    }

    .contact-cta {
      justify-content: center;
    }

    .phone-number {
      font-size: 1.25rem;
    }
  }
</style>
