<script lang="ts">
  import Navbar from '$lib/components/Navbar.svelte';
  import Hero from '$lib/components/Hero.svelte';
  import About from '$lib/components/About.svelte';
  import Skills from '$lib/components/Skills.svelte';
  import Projects from '$lib/components/Projects.svelte';
  import Experience from '$lib/components/Experience.svelte';
  import Contact from '$lib/components/Contact.svelte';
  import Footer from '$lib/components/Footer.svelte';
</script>

<svelte:head>
  <title>Ryan Juska | Engineer & Developer Portfolio</title>
  <meta name="description" content="Ryan Juska — Full-Stack Engineer & Robotics Specialist. Frontend, Backend, IoT, Server Infrastructure, and Robotics." />
</svelte:head>

<Navbar />
<main>
  <Hero />
  <About />
  <Skills />
  <Projects />
  <Experience />
  <Contact />
</main>
<Footer />

<style>
  main {
    overflow-x: hidden;
  }
</style>
