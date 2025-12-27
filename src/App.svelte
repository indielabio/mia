<script lang="ts">
  import Navigation from './lib/components/Navigation.svelte';
  import Hero from './lib/components/Hero.svelte';
  import About from './lib/components/About.svelte';
  import Gallery from './lib/components/Gallery.svelte';
  import Specialties from './lib/components/Specialties.svelte';
  import Contact from './lib/components/Contact.svelte';
</script>

<div class="grain-overlay" aria-hidden="true"></div>

<Navigation />

<main>
  <Hero />
  <About />
  <Gallery />
  <Specialties />
  <Contact />
</main>

<style>
  main {
    position: relative;
  }
</style>
