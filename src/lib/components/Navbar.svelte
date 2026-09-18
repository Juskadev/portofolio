<script lang="ts">
  let scrolled = $state(false);
  let menuOpen = $state(false);

  const navLinks = [
    { label: 'Home', href: '#hero' },
    { label: 'About', href: '#about' },
    { label: 'Skills', href: '#skills' },
    { label: 'Projects', href: '#projects' },
    { label: 'Experience', href: '#experience' },
    { label: 'Contact', href: '#contact' }
  ];

  function handleScroll() {
    scrolled = window.scrollY > 50;
  }

  function closeMenu() {
    menuOpen = false;
  }

  function handleNavClick(e: MouseEvent, href: string) {
    e.preventDefault();
    closeMenu();
    const el = document.querySelector(href);
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' });
    }
  }
</script>

<svelte:window onscroll={handleScroll} />

<nav class="navbar" class:scrolled>
  <div class="nav-container">
    <a href="#hero" class="logo" onclick={(e) => handleNavClick(e, '#hero')}>
      <span class="logo-bracket">&lt;</span>
      <span class="logo-text">RJ</span>
      <span class="logo-bracket">/&gt;</span>
    </a>

    <div class="nav-links" class:open={menuOpen}>
      {#each navLinks as link}
        <a
          href={link.href}
          class="nav-link"
          onclick={(e) => handleNavClick(e, link.href)}
        >
          {link.label}
        </a>
      {/each}
      <a href="#contact" class="btn btn-primary nav-cta" onclick={(e) => handleNavClick(e, '#contact')}>
        Let's Talk
      </a>
    </div>

    <button
      class="hamburger"
      class:active={menuOpen}
      onclick={() => (menuOpen = !menuOpen)}
      aria-label="Toggle menu"
      id="nav-hamburger"
    >
      <span></span>
      <span></span>
      <span></span>
    </button>
  </div>
</nav>

{#if menuOpen}
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div class="nav-overlay" onclick={closeMenu} onkeydown={() => {}}></div>
{/if}

<style>
  .navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    padding: 1.2rem 0;
    transition: all var(--duration-normal) var(--ease-out-expo);
  }

  .navbar.scrolled {
    padding: 0.7rem 0;
    background: rgba(10, 10, 15, 0.85);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border-subtle);
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.3);
  }

  .nav-container {
    max-width: var(--container-max);
    margin: 0 auto;
    padding: 0 clamp(1.5rem, 4vw, 3rem);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .logo {
    font-family: var(--font-mono);
    font-size: 1.4rem;
    font-weight: 700;
    text-decoration: none;
    color: var(--text-primary);
    display: flex;
    align-items: center;
    gap: 2px;
    transition: all var(--duration-fast) ease;
  }

  .logo:hover {
    transform: scale(1.05);
  }

  .logo-bracket {
    color: var(--accent-primary);
    font-weight: 400;
  }

  .logo-text {
    background: var(--gradient-primary);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .nav-links {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .nav-link {
    font-size: 0.9rem;
    font-weight: 500;
    color: var(--text-secondary);
    text-decoration: none;
    padding: 0.5rem 1rem;
    border-radius: var(--radius-sm);
    transition: all var(--duration-fast) ease;
    position: relative;
  }

  .nav-link::after {
    content: '';
    position: absolute;
    bottom: 2px;
    left: 50%;
    transform: translateX(-50%) scaleX(0);
    width: 60%;
    height: 2px;
    background: var(--gradient-primary);
    border-radius: 2px;
    transition: transform var(--duration-normal) var(--ease-out-expo);
  }

  .nav-link:hover {
    color: var(--text-primary);
  }

  .nav-link:hover::after {
    transform: translateX(-50%) scaleX(1);
  }

  .nav-cta {
    margin-left: 1rem;
    padding: 0.6rem 1.4rem;
    font-size: 0.85rem;
  }

  .hamburger {
    display: none;
    flex-direction: column;
    gap: 5px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 8px;
    z-index: 1001;
  }

  .hamburger span {
    display: block;
    width: 24px;
    height: 2px;
    background: var(--text-primary);
    border-radius: 2px;
    transition: all var(--duration-normal) var(--ease-out-expo);
  }

  .hamburger.active span:nth-child(1) {
    transform: rotate(45deg) translate(5px, 5px);
  }

  .hamburger.active span:nth-child(2) {
    opacity: 0;
    transform: scaleX(0);
  }

  .hamburger.active span:nth-child(3) {
    transform: rotate(-45deg) translate(5px, -5px);
  }

  .nav-overlay {
    display: none;
  }

  @media (max-width: 768px) {
    .hamburger {
      display: flex;
    }

    .nav-links {
      position: fixed;
      top: 0;
      right: -100%;
      width: 280px;
      height: 100vh;
      background: rgba(10, 10, 20, 0.97);
      backdrop-filter: blur(30px);
      flex-direction: column;
      justify-content: center;
      gap: 0.5rem;
      padding: 2rem;
      transition: right var(--duration-normal) var(--ease-out-expo);
      border-left: 1px solid var(--border-subtle);
      z-index: 1000;
    }

    .nav-links.open {
      right: 0;
    }

    .nav-link {
      font-size: 1.1rem;
      padding: 0.8rem 1rem;
    }

    .nav-cta {
      margin-left: 0;
      margin-top: 1rem;
      width: 100%;
      text-align: center;
    }

    .nav-overlay {
      display: block;
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      z-index: 999;
    }
  }
</style>
