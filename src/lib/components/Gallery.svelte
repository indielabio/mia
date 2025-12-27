<script lang="ts">
  let sectionRef: HTMLElement;
  let carouselRef: HTMLElement;
  let visible = $state(false);
  let isDragging = $state(false);
  let startX = $state(0);
  let scrollLeft = $state(0);

  const placeholderImages = [
    { id: 1, alt: 'Therapy office space' },
    { id: 2, alt: 'Comfortable seating area' },
    { id: 3, alt: 'Natural light environment' },
    { id: 4, alt: 'Calming decor' },
    { id: 5, alt: 'Welcoming entrance' },
    { id: 6, alt: 'Private consultation room' },
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

  function handleMouseDown(e: MouseEvent) {
    isDragging = true;
    startX = e.pageX - carouselRef.offsetLeft;
    scrollLeft = carouselRef.scrollLeft;
    carouselRef.style.cursor = 'grabbing';
  }

  function handleMouseUp() {
    isDragging = false;
    carouselRef.style.cursor = 'grab';
  }

  function handleMouseMove(e: MouseEvent) {
    if (!isDragging) return;
    e.preventDefault();
    const x = e.pageX - carouselRef.offsetLeft;
    const walk = (x - startX) * 1.5;
    carouselRef.scrollLeft = scrollLeft - walk;
  }

  function handleMouseLeave() {
    isDragging = false;
    carouselRef.style.cursor = 'grab';
  }

  function handleTouchStart(e: TouchEvent) {
    startX = e.touches[0].pageX - carouselRef.offsetLeft;
    scrollLeft = carouselRef.scrollLeft;
  }

  function handleTouchMove(e: TouchEvent) {
    const x = e.touches[0].pageX - carouselRef.offsetLeft;
    const walk = (x - startX) * 1.5;
    carouselRef.scrollLeft = scrollLeft - walk;
  }
</script>

<section class="gallery section" id="gallery" bind:this={sectionRef}>
  <div class="gallery-header" class:visible>
    <div class="section-label">Gallery</div>
    <h2>A Space for Healing</h2>
    <p>Creating a warm, inviting environment where you can feel comfortable and safe.</p>
  </div>

  <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
  <div
    class="gallery-carousel"
    class:visible
    bind:this={carouselRef}
    onmousedown={handleMouseDown}
    onmouseup={handleMouseUp}
    onmousemove={handleMouseMove}
    onmouseleave={handleMouseLeave}
    ontouchstart={handleTouchStart}
    ontouchmove={handleTouchMove}
    role="region"
    aria-label="Image gallery"
  >
    <div class="gallery-track">
      {#each placeholderImages as image, index}
        <div class="gallery-item" style="animation-delay: {0.1 * index}s">
          <div class="gallery-image-placeholder">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path
                d="M2.25 15.75l5.159-5.159a2.25 2.25 0 013.182 0l5.159 5.159m-1.5-1.5l1.409-1.409a2.25 2.25 0 013.182 0l2.909 2.909m-18 3.75h16.5a1.5 1.5 0 001.5-1.5V6a1.5 1.5 0 00-1.5-1.5H3.75A1.5 1.5 0 002.25 6v12a1.5 1.5 0 001.5 1.5zm10.5-11.25h.008v.008h-.008V8.25zm.375 0a.375.375 0 11-.75 0 .375.375 0 01.75 0z"
              />
            </svg>
            <span>{image.alt}</span>
          </div>
        </div>
      {/each}
    </div>
  </div>

  <div class="gallery-hint" class:visible>
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
      <path d="M7.5 21L3 16.5m0 0L7.5 12M3 16.5h13.5m0-13.5L21 7.5m0 0L16.5 12M21 7.5H7.5" />
    </svg>
    <span>Swipe to explore</span>
  </div>
</section>

<style>
  .gallery {
    position: relative;
    overflow: hidden;
  }

  .gallery-header {
    max-width: 1280px;
    margin: 0 auto var(--space-xl);
    padding: 0 var(--space-lg);
    text-align: center;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s var(--ease-out-expo);
  }

  .gallery-header.visible {
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

  .gallery-header h2 {
    margin-bottom: var(--space-md);
  }

  .gallery-header p {
    color: var(--charcoal-soft);
    max-width: 500px;
    margin: 0 auto;
  }

  .gallery-carousel {
    cursor: grab;
    overflow-x: auto;
    overflow-y: hidden;
    scroll-behavior: smooth;
    scrollbar-width: none;
    -ms-overflow-style: none;
    padding: var(--space-md) 0;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s var(--ease-out-expo) 0.2s;
  }

  .gallery-carousel.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .gallery-carousel::-webkit-scrollbar {
    display: none;
  }

  .gallery-track {
    display: flex;
    gap: var(--space-lg);
    padding: 0 max(var(--space-lg), calc((100vw - 1280px) / 2 + var(--space-lg)));
    width: max-content;
  }

  .gallery-item {
    flex-shrink: 0;
    width: 320px;
    opacity: 0;
    animation: fadeInUp 0.6s var(--ease-out-expo) forwards;
  }

  .gallery-image-placeholder {
    aspect-ratio: 4/3;
    background: linear-gradient(135deg, var(--cream) 0%, var(--warm-gray) 100%);
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: var(--space-sm);
    color: var(--charcoal-soft);
    box-shadow: var(--shadow-soft);
    transition: all 0.4s var(--ease-out-expo);
    user-select: none;
    pointer-events: none;
  }

  .gallery-item:hover .gallery-image-placeholder {
    box-shadow: var(--shadow-medium);
    transform: translateY(-5px);
  }

  .gallery-image-placeholder svg {
    width: 40px;
    height: 40px;
    opacity: 0.4;
  }

  .gallery-image-placeholder span {
    font-size: 0.8rem;
    opacity: 0.5;
    text-align: center;
    padding: 0 var(--space-md);
  }

  .gallery-hint {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: var(--space-sm);
    margin-top: var(--space-lg);
    color: var(--charcoal-soft);
    font-size: 0.85rem;
    opacity: 0;
    transition: opacity 0.6s var(--ease-out-soft) 0.6s;
  }

  .gallery-hint.visible {
    opacity: 0.6;
  }

  .gallery-hint svg {
    width: 20px;
    height: 20px;
  }

  @media (max-width: 768px) {
    .gallery-item {
      width: 280px;
    }

    .gallery-track {
      gap: var(--space-md);
    }
  }
</style>
