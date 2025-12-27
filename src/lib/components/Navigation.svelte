<script lang="ts">
  let scrolled = $state(false);
  let mobileMenuOpen = $state(false);

  const navLinks = [
    { label: 'About', href: '#about' },
    { label: 'Gallery', href: '#gallery' },
    { label: 'Specialties', href: '#specialties' },
    { label: 'Contact', href: '#contact' },
  ];

  function handleScroll() {
    scrolled = window.scrollY > 50;
  }

  function closeMobileMenu() {
    mobileMenuOpen = false;
  }
</script>

<svelte:window onscroll={handleScroll} />

<nav class="nav" class:scrolled>
  <div class="nav-container">
    <a href="#hero" class="nav-logo" onclick={closeMobileMenu}>
      <img src="/images/logo.png" alt="Mia Dessesaure Therapy" />
    </a>

    <div class="nav-links" class:open={mobileMenuOpen}>
      {#each navLinks as link}
        <a href={link.href} class="nav-link" onclick={closeMobileMenu}>
          {link.label}
        </a>
      {/each}
      <a href="#contact" class="btn btn-primary nav-cta" onclick={closeMobileMenu}>
        Schedule Consultation
      </a>
    </div>

    <button
      class="mobile-toggle"
      onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
      aria-label="Toggle menu"
      aria-expanded={mobileMenuOpen}
    >
      <span class="hamburger" class:open={mobileMenuOpen}></span>
    </button>
  </div>
</nav>

<style>
  .nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    padding: var(--space-md) 0;
    transition: all 0.4s var(--ease-out-expo);
    background: transparent;
  }

  .nav.scrolled {
    background: rgba(250, 249, 247, 0.95);
    backdrop-filter: blur(10px);
    box-shadow: 0 2px 20px rgba(45, 45, 45, 0.05);
    padding: var(--space-sm) 0;
  }

  .nav-container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 var(--space-lg);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .nav-logo {
    display: flex;
    align-items: center;
  }

  .nav-logo img {
    height: 60px;
    width: auto;
    transition: height 0.3s var(--ease-out-soft);
  }

  .nav.scrolled .nav-logo img {
    height: 45px;
  }

  .nav-links {
    display: flex;
    align-items: center;
    gap: var(--space-xl);
  }

  .nav-link {
    font-size: 0.95rem;
    font-weight: 500;
    color: var(--charcoal);
    position: relative;
    padding: var(--space-xs) 0;
  }

  .nav-link::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 2px;
    background: var(--sage);
    transition: width 0.3s var(--ease-out-expo);
  }

  .nav-link:hover {
    color: var(--terracotta);
  }

  .nav-link:hover::after {
    width: 100%;
  }

  .nav-cta {
    padding: var(--space-sm) var(--space-lg);
    font-size: 0.875rem;
  }

  .mobile-toggle {
    display: none;
    background: none;
    border: none;
    cursor: pointer;
    padding: var(--space-sm);
    z-index: 1001;
  }

  .hamburger {
    display: block;
    width: 24px;
    height: 2px;
    background: var(--charcoal);
    position: relative;
    transition: all 0.3s var(--ease-out-soft);
  }

  .hamburger::before,
  .hamburger::after {
    content: '';
    position: absolute;
    left: 0;
    width: 24px;
    height: 2px;
    background: var(--charcoal);
    transition: all 0.3s var(--ease-out-soft);
  }

  .hamburger::before {
    top: -7px;
  }

  .hamburger::after {
    bottom: -7px;
  }

  .hamburger.open {
    background: transparent;
  }

  .hamburger.open::before {
    transform: rotate(45deg);
    top: 0;
  }

  .hamburger.open::after {
    transform: rotate(-45deg);
    bottom: 0;
  }

  @media (max-width: 900px) {
    .mobile-toggle {
      display: block;
    }

    .nav-links {
      position: fixed;
      top: 0;
      right: 0;
      bottom: 0;
      width: 280px;
      flex-direction: column;
      justify-content: center;
      gap: var(--space-lg);
      padding: var(--space-xl);
      background: var(--off-white);
      box-shadow: -10px 0 30px rgba(45, 45, 45, 0.1);
      transform: translateX(100%);
      transition: transform 0.4s var(--ease-out-expo);
    }

    .nav-links.open {
      transform: translateX(0);
    }

    .nav-link {
      font-size: 1.25rem;
    }

    .nav-cta {
      width: 100%;
      text-align: center;
    }
  }
</style>
