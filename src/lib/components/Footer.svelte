<script lang="ts">
</script>

<footer class="footer">
  <div class="footer-glow"></div>
  <div class="container">
    <div class="footer-content">
      <div class="footer-brand">
        <a href="#hero" class="footer-logo">
          <span class="logo-bracket">&lt;</span>
          <span class="logo-text">RJ</span>
          <span class="logo-bracket">/&gt;</span>
        </a>
        <p class="footer-tagline">Engineering the digital & physical world.</p>
      </div>

      <div class="footer-links">
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#projects">Projects</a>
        <a href="#experience">Experience</a>
        <a href="#contact">Contact</a>
      </div>
    </div>

    <div class="footer-bottom">
      <p class="footer-copy">&copy; {new Date().getFullYear()} Ryan Juska Pratama, S.Kom. Built with <span class="heart">♥</span> and SvelteKit.</p>
      <p class="footer-stack">
        <span class="tech-badge">Svelte</span>
        <span class="tech-badge">TypeScript</span>
        <span class="tech-badge">CSS</span>
      </p>
    </div>
  </div>
</footer>

<style>
  .footer {
    position: relative;
    padding: 3rem 0 1.5rem;
    background: var(--bg-primary);
    border-top: 1px solid var(--border-subtle);
    overflow: hidden;
  }

  .footer-glow {
    position: absolute;
    top: -150px;
    left: 50%;
    transform: translateX(-50%);
    width: 600px;
    height: 300px;
    background: radial-gradient(ellipse, rgba(124, 58, 237, 0.06), transparent 70%);
    pointer-events: none;
  }

  .footer-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
    position: relative;
    z-index: 1;
  }

  .footer-logo {
    font-family: var(--font-mono);
    font-size: 1.3rem;
    font-weight: 700;
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 2px;
    margin-bottom: 0.5rem;
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

  .footer-tagline {
    font-size: 0.85rem;
    color: var(--text-muted);
  }

  .footer-links {
    display: flex;
    gap: 1.5rem;
  }

  .footer-links a {
    font-size: 0.88rem;
    color: var(--text-secondary);
    text-decoration: none;
    transition: color var(--duration-fast) ease;
  }

  .footer-links a:hover {
    color: var(--accent-primary);
  }

  .footer-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 1.5rem;
    border-top: 1px solid var(--border-subtle);
    position: relative;
    z-index: 1;
  }

  .footer-copy {
    font-size: 0.82rem;
    color: var(--text-muted);
  }

  .heart {
    color: var(--accent-tertiary);
    display: inline-block;
    animation: heartbeat 1.5s ease-in-out infinite;
  }

  @keyframes heartbeat {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.2); }
  }

  .footer-stack {
    display: flex;
    gap: 0.5rem;
  }

  .tech-badge {
    padding: 0.2rem 0.6rem;
    border-radius: var(--radius-full);
    font-size: 0.7rem;
    font-family: var(--font-mono);
    font-weight: 500;
    background: rgba(124, 58, 237, 0.08);
    color: var(--text-muted);
    border: 1px solid var(--border-subtle);
  }

  @media (max-width: 768px) {
    .footer-content {
      flex-direction: column;
      text-align: center;
      gap: 1.5rem;
    }

    .footer-links {
      flex-wrap: wrap;
      justify-content: center;
    }

    .footer-bottom {
      flex-direction: column;
      gap: 1rem;
      text-align: center;
    }
  }
</style>
