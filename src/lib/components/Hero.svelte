<script lang="ts">
  let visible = $state(false);
  let typedText = $state('');
  const roles = [
    'S1 Teknologi Informasi (S.Kom)',
    'IT & Data Systems Specialist',
    'Full-Stack & Web Developer',
    'IoT & Robotics Engineer',
    'Database & Server Admin'
  ];
  let roleIndex = $state(0);
  let charIndex = $state(0);
  let isDeleting = $state(false);

  $effect(() => {
    visible = true;

    const typeEffect = () => {
      const currentRole = roles[roleIndex];

      if (!isDeleting) {
        typedText = currentRole.substring(0, charIndex + 1);
        charIndex++;

        if (charIndex === currentRole.length) {
          setTimeout(() => {
            isDeleting = true;
          }, 2000);
          return;
        }
      } else {
        typedText = currentRole.substring(0, charIndex - 1);
        charIndex--;

        if (charIndex === 0) {
          isDeleting = false;
          roleIndex = (roleIndex + 1) % roles.length;
        }
      }
    };

    const interval = setInterval(typeEffect, isDeleting ? 50 : 100);
    return () => clearInterval(interval);
  });

  // Particle system
  const particles = Array.from({ length: 40 }, (_, i) => ({
    id: i,
    x: Math.random() * 100,
    y: Math.random() * 100,
    size: Math.random() * 3 + 1,
    duration: Math.random() * 20 + 10,
    delay: Math.random() * 5
  }));
</script>

<section id="hero" class="hero" class:visible>
  <!-- Animated background particles -->
  <div class="particles">
    {#each particles as p}
      <div
        class="particle"
        style="
          left: {p.x}%;
          top: {p.y}%;
          width: {p.size}px;
          height: {p.size}px;
          animation-duration: {p.duration}s;
          animation-delay: {p.delay}s;
        "
      ></div>
    {/each}
  </div>

  <!-- Gradient orbs -->
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>

  <!-- Grid overlay -->
  <div class="grid-overlay"></div>

  <div class="hero-container container">
    <div class="hero-content">
      <div class="hero-badge">
        <span class="badge-dot"></span>
        Available for Full-time & Project Roles
      </div>

      <h1 class="hero-title">
        <span class="hero-greeting">Hello, I'm</span>
        <span class="hero-name">Ryan Juska Pratama</span>
      </h1>

      <div class="hero-role">
        <span class="role-prefix">I'm a </span>
        <span class="role-typed">{typedText}</span>
        <span class="role-cursor">|</span>
      </div>

      <p class="hero-description">
        Bachelor of Computer Science (S.Kom, GPA 3.70/4.00) from Universitas Bina Sarana Informatika. 
        Experienced in IT & Data Systems, web programming, IoT, server administration, and robotics — 
        ready to deliver high data integrity, system stability, and scalable solutions.
      </p>

      <div class="hero-actions">
        <a href="#projects" class="btn btn-primary" onclick={(e) => { e.preventDefault(); document.querySelector('#projects')?.scrollIntoView({ behavior: 'smooth' }) }}>
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
          </svg>
          View Projects
        </a>
        <a href="/Ryan_Juska_Pratama_CV.pdf" target="_blank" download="Ryan_Juska_Pratama_CV.pdf" class="btn btn-outline cv-btn">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/>
          </svg>
          Download CV
        </a>
        <a href="#contact" class="btn btn-outline" onclick={(e) => { e.preventDefault(); document.querySelector('#contact')?.scrollIntoView({ behavior: 'smooth' }) }}>
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
          </svg>
          Contact Me
        </a>
      </div>

      <div class="hero-stats">
        <div class="stat">
          <span class="stat-number">3.70</span>
          <span class="stat-label">IPK / GPA (S.Kom)</span>
        </div>
        <div class="stat-divider"></div>
        <div class="stat">
          <span class="stat-number">SINTA 5</span>
          <span class="stat-label">Published Author</span>
        </div>
        <div class="stat-divider"></div>
        <div class="stat">
          <span class="stat-number">PCAP</span>
          <span class="stat-label">Cisco Certified</span>
        </div>
      </div>
    </div>

    <div class="hero-visual">
      <div class="profile-wrapper">
        <div class="profile-ring"></div>
        <div class="profile-ring ring-2"></div>
        <img src="/profile.jpg" alt="Ryan Juska Pratama" class="profile-img" />
        <div class="profile-glow"></div>
      </div>

      <!-- Floating tech badges -->
      <div class="floating-badge badge-1">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="3" width="20" height="14" rx="2" ry="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>
        Frontend
      </div>
      <div class="floating-badge badge-2">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="2" width="20" height="8" rx="2" ry="2"/><rect x="2" y="14" width="20" height="8" rx="2" ry="2"/><line x1="6" y1="6" x2="6.01" y2="6"/><line x1="6" y1="18" x2="6.01" y2="18"/></svg>
        Server
      </div>
      <div class="floating-badge badge-3">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/></svg>
        IoT
      </div>
      <div class="floating-badge badge-4">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 1v4M12 19v4M4.22 4.22l2.83 2.83M16.95 16.95l2.83 2.83M1 12h4M19 12h4M4.22 19.78l2.83-2.83M16.95 7.05l2.83-2.83"/></svg>
        Robotics
      </div>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="scroll-indicator">
    <div class="scroll-mouse">
      <div class="scroll-wheel"></div>
    </div>
    <span>Scroll to explore</span>
  </div>
</section>

<style>
  .hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    overflow: hidden;
    padding-top: 5rem;
  }

  /* Particles */
  .particles {
    position: absolute;
    inset: 0;
    z-index: 0;
    overflow: hidden;
  }

  .particle {
    position: absolute;
    background: var(--accent-primary);
    border-radius: 50%;
    opacity: 0;
    animation: particleFloat linear infinite;
  }

  @keyframes particleFloat {
    0% { opacity: 0; transform: translateY(0) translateX(0); }
    10% { opacity: 0.6; }
    90% { opacity: 0.6; }
    100% { opacity: 0; transform: translateY(-100vh) translateX(30px); }
  }

  /* Gradient orbs */
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }

  .orb-1 {
    width: 500px;
    height: 500px;
    background: rgba(124, 58, 237, 0.12);
    top: -15%;
    left: -10%;
    animation: float 8s ease-in-out infinite;
  }

  .orb-2 {
    width: 400px;
    height: 400px;
    background: rgba(6, 182, 212, 0.1);
    bottom: -10%;
    right: -5%;
    animation: float 10s ease-in-out infinite reverse;
  }

  .orb-3 {
    width: 300px;
    height: 300px;
    background: rgba(244, 63, 94, 0.08);
    top: 40%;
    right: 20%;
    animation: float 12s ease-in-out infinite;
  }

  /* Grid overlay */
  .grid-overlay {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(124, 58, 237, 0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(124, 58, 237, 0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    z-index: 0;
  }

  /* Container */
  .hero-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: center;
    z-index: 1;
    position: relative;
  }

  /* Content */
  .hero-content {
    opacity: 0;
    transform: translateY(40px);
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.3s forwards;
  }

  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.4rem 1rem 0.4rem 0.6rem;
    border-radius: var(--radius-full);
    background: rgba(16, 185, 129, 0.1);
    border: 1px solid rgba(16, 185, 129, 0.3);
    font-size: 0.8rem;
    font-weight: 500;
    color: var(--accent-success);
    margin-bottom: 1.5rem;
  }

  .badge-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--accent-success);
    animation: pulse-glow 2s ease-in-out infinite;
  }

  .hero-greeting {
    display: block;
    font-family: var(--font-mono);
    font-size: clamp(0.9rem, 2vw, 1.1rem);
    font-weight: 400;
    color: var(--text-secondary);
    margin-bottom: 0.5rem;
    letter-spacing: 0.05em;
  }

  .hero-name {
    display: block;
    font-family: var(--font-display);
    font-size: clamp(2.8rem, 6vw, 4.5rem);
    font-weight: 800;
    line-height: 1.05;
    background: var(--gradient-hero);
    background-size: 200% 200%;
    animation: gradient-shift 4s ease infinite;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.5rem;
  }

  .hero-title {
    margin-bottom: 0.5rem;
  }

  .hero-role {
    font-size: clamp(1.1rem, 2.5vw, 1.5rem);
    font-weight: 500;
    color: var(--text-secondary);
    margin-bottom: 1.5rem;
    min-height: 2rem;
  }

  .role-prefix {
    color: var(--text-muted);
  }

  .role-typed {
    color: var(--accent-secondary);
    font-weight: 600;
  }

  .role-cursor {
    color: var(--accent-secondary);
    animation: blink-caret 0.8s step-end infinite;
    font-weight: 300;
  }

  .hero-description {
    font-size: 1.05rem;
    color: var(--text-secondary);
    line-height: 1.8;
    max-width: 520px;
    margin-bottom: 2rem;
  }

  .hero-actions {
    display: flex;
    gap: 1rem;
    margin-bottom: 2.5rem;
    flex-wrap: wrap;
  }

  .hero-stats {
    display: flex;
    align-items: center;
    gap: 1.5rem;
  }

  .stat {
    display: flex;
    flex-direction: column;
  }

  .stat-number {
    font-family: var(--font-display);
    font-size: 1.8rem;
    font-weight: 700;
    background: var(--gradient-primary);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .stat-label {
    font-size: 0.8rem;
    color: var(--text-muted);
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .stat-divider {
    width: 1px;
    height: 40px;
    background: var(--border-subtle);
  }

  /* Visual / Profile */
  .hero-visual {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    opacity: 0;
    transform: translateY(40px);
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.6s forwards;
  }

  .profile-wrapper {
    position: relative;
    width: clamp(280px, 30vw, 380px);
    height: clamp(280px, 30vw, 380px);
  }

  .profile-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
    position: relative;
    z-index: 2;
    border: 3px solid rgba(124, 58, 237, 0.3);
  }

  .profile-ring {
    position: absolute;
    inset: -15px;
    border-radius: 50%;
    border: 2px dashed rgba(124, 58, 237, 0.2);
    animation: spin-slow 30s linear infinite;
    z-index: 1;
  }

  .profile-ring.ring-2 {
    inset: -30px;
    border-color: rgba(6, 182, 212, 0.15);
    animation-direction: reverse;
    animation-duration: 45s;
  }

  .profile-glow {
    position: absolute;
    inset: -20px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(124, 58, 237, 0.2), transparent 70%);
    z-index: 0;
    animation: pulse-glow 3s ease-in-out infinite;
  }

  /* Floating badges */
  .floating-badge {
    position: absolute;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem 1rem;
    border-radius: var(--radius-full);
    background: var(--bg-glass);
    backdrop-filter: blur(15px);
    border: 1px solid var(--border-subtle);
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--text-primary);
    white-space: nowrap;
    z-index: 3;
    animation: float 4s ease-in-out infinite;
    box-shadow: var(--shadow-md);
  }

  .badge-1 {
    top: 5%;
    left: -5%;
    animation-delay: 0s;
    color: var(--accent-secondary);
  }

  .badge-2 {
    top: 15%;
    right: -10%;
    animation-delay: 1s;
    color: var(--accent-success);
  }

  .badge-3 {
    bottom: 15%;
    left: -10%;
    animation-delay: 2s;
    color: var(--accent-warning);
  }

  .badge-4 {
    bottom: 5%;
    right: -5%;
    animation-delay: 3s;
    color: var(--accent-tertiary);
  }

  /* Scroll indicator */
  .scroll-indicator {
    position: absolute;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    z-index: 2;
    opacity: 0;
    animation: fadeInUp 0.8s var(--ease-out-expo) 1.5s forwards;
  }

  .scroll-indicator span {
    font-size: 0.7rem;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.15em;
  }

  .scroll-mouse {
    width: 24px;
    height: 38px;
    border: 2px solid var(--border-hover);
    border-radius: 12px;
    position: relative;
  }

  .scroll-wheel {
    position: absolute;
    top: 6px;
    left: 50%;
    transform: translateX(-50%);
    width: 3px;
    height: 8px;
    background: var(--accent-primary);
    border-radius: 2px;
    animation: scrollBounce 2s ease-in-out infinite;
  }

  @keyframes scrollBounce {
    0%, 100% { opacity: 1; top: 6px; }
    50% { opacity: 0.3; top: 16px; }
  }

  @media (max-width: 900px) {
    .hero-container {
      grid-template-columns: 1fr;
      text-align: center;
      gap: 3rem;
    }

    .hero-content {
      order: 2;
    }

    .hero-visual {
      order: 1;
    }

    .hero-description {
      margin: 0 auto 2rem;
    }

    .hero-actions {
      justify-content: center;
    }

    .hero-stats {
      justify-content: center;
    }

    .profile-wrapper {
      width: 220px;
      height: 220px;
    }

    .floating-badge {
      display: none;
    }

    .scroll-indicator {
      display: none;
    }
  }
</style>
