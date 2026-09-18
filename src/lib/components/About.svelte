<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);

  $effect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) visible = true;
      },
      { threshold: 0.15 }
    );
    if (sectionRef) observer.observe(sectionRef);
    return () => observer.disconnect();
  });

  const highlights = [
    {
      icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>`,
      title: 'Full-Stack & Systems Mindset',
      description: 'Clean coding across web development, databases, and low-level system integrations.'
    },
    {
      icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>`,
      title: 'Data Integrity & Troubleshooting',
      description: 'Proven track record securing institutional databases and resolving complex technical issues.'
    },
    {
      icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 1v4M12 19v4M4.22 4.22l2.83 2.83M16.95 16.95l2.83 2.83M1 12h4M19 12h4M4.22 19.78l2.83-2.83M16.95 7.05l2.83-2.83"/></svg>`,
      title: 'IoT & Hardware Integration',
      description: 'Bridging physical microcontrollers (ESP32/Arduino/ROS) with cloud services and web dashboards.'
    }
  ];
</script>

<section id="about" class="section about" class:visible bind:this={sectionRef}>
  <div class="container">
    <div class="about-grid">
      <div class="about-content">
        <span class="section-label">About Me</span>
        <h2 class="section-title">Bridging Systems, Data,<br/>& Modern Engineering</h2>
        <p class="about-text">
          I am an Information Technology graduate (S.Kom) from <strong>Universitas Bina Sarana Informatika</strong> with a <strong>GPA of 3.70 / 4.00</strong>. 
          My professional background combines hands-on experience supporting institutional information systems, managing sensitive databases, and architecting end-to-end technology solutions.
        </p>
        <p class="about-text">
          From ensuring data integrity at the <strong>Komisi Yudisial Republik Indonesia</strong> to building web applications, configuring IoT sensor networks, and deploying server infrastructure, 
          I bring analytical rigor, reliability, and clear communication to every technical challenge.
        </p>

        <div class="about-highlights">
          {#each highlights as h, i}
            <div class="highlight-card" style="animation-delay: {0.2 + i * 0.15}s">
              <div class="highlight-icon">{@html h.icon}</div>
              <div>
                <h4 class="highlight-title">{h.title}</h4>
                <p class="highlight-desc">{h.description}</p>
              </div>
            </div>
          {/each}
        </div>
      </div>

      <div class="about-visual">
        <div class="code-window">
          <div class="code-header">
            <div class="code-dots">
              <span class="dot red"></span>
              <span class="dot yellow"></span>
              <span class="dot green"></span>
            </div>
            <span class="code-filename">ryan_profile.ts</span>
          </div>
          <pre class="code-content"><code><span class="kw">interface</span> <span class="type">ITSpecialist</span> {'{'}<br/>  <span class="prop">name</span>: <span class="str">"Ryan Juska Pratama, S.Kom"</span>;<br/>  <span class="prop">degree</span>: <span class="str">"S1 Teknologi Informasi"</span>;<br/>  <span class="prop">gpa</span>: <span class="str">"3.70 / 4.00"</span>;<br/>  <span class="prop">email</span>: <span class="str">"Juskapratama1@gmail.com"</span>;<br/>  <span class="prop">github</span>: <span class="str">"github.com/Juskadev"</span>;<br/>  <span class="prop">skills</span>: <span class="type">string</span>[];<br/>  <span class="prop">publication</span>: <span class="str">"JNKTI SINTA 5 (2024)"</span>;<br/>{'}'}<br/><br/><span class="kw">const</span> <span class="var">ryan</span>: <span class="type">ITSpecialist</span> = {'{'}<br/>  <span class="prop">name</span>: <span class="str">"Ryan Juska Pratama"</span>,<br/>  <span class="prop">degree</span>: <span class="str">"S1 Teknologi Informasi"</span>,<br/>  <span class="prop">gpa</span>: <span class="str">"3.70 / 4.00"</span>,<br/>  <span class="prop">email</span>: <span class="str">"Juskapratama1@gmail.com"</span>,<br/>  <span class="prop">skills</span>: [<br/>    <span class="str">"IT Systems & Support"</span>,<br/>    <span class="str">"Web & Full-Stack"</span>,<br/>    <span class="str">"Database & SQL"</span>,<br/>    <span class="str">"IoT & Robotics"</span>,<br/>    <span class="str">"Python & Networking"</span>,<br/>  ],<br/>  <span class="prop">publication</span>: <span class="str">"JNKTI SINTA 5"</span>,<br/>{'}'};<br/><br/><span class="kw">export default</span> <span class="var">ryan</span>;</code></pre>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .about {
    background: var(--bg-secondary);
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
    background: linear-gradient(90deg, transparent, var(--accent-primary), transparent);
  }

  .about-grid {
    display: grid;
    grid-template-columns: 1.1fr 0.9fr;
    gap: 4rem;
    align-items: start;
  }

  .about-content {
    opacity: 0;
    transform: translateY(30px);
  }

  .visible .about-content {
    animation: fadeInUp 0.7s var(--ease-out-expo) 0.2s forwards;
  }

  .about-text {
    font-size: 1.05rem;
    color: var(--text-secondary);
    line-height: 1.8;
    margin-bottom: 1.2rem;
  }

  .about-highlights {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 2rem;
  }

  .highlight-card {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
    padding: 1.2rem;
    background: var(--bg-glass);
    border: 1px solid var(--border-subtle);
    border-radius: var(--radius-md);
    transition: all var(--duration-normal) var(--ease-out-expo);
    opacity: 0;
    transform: translateX(-20px);
  }

  .visible .highlight-card {
    animation: slideInLeft 0.6s var(--ease-out-expo) forwards;
  }

  .highlight-card:hover {
    border-color: var(--border-hover);
    background: rgba(124, 58, 237, 0.06);
    transform: translateX(5px);
  }

  .highlight-icon {
    flex-shrink: 0;
    width: 44px;
    height: 44px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: var(--radius-sm);
    background: rgba(124, 58, 237, 0.1);
    color: var(--accent-primary);
  }

  .highlight-title {
    font-family: var(--font-display);
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 0.25rem;
    color: var(--text-primary);
  }

  .highlight-desc {
    font-size: 0.85rem;
    color: var(--text-muted);
    line-height: 1.5;
  }

  /* Code Window */
  .about-visual {
    opacity: 0;
    transform: translateY(30px);
  }

  .visible .about-visual {
    animation: fadeInUp 0.7s var(--ease-out-expo) 0.5s forwards;
  }

  .code-window {
    border-radius: var(--radius-lg);
    overflow: hidden;
    border: 1px solid var(--border-subtle);
    background: rgba(10, 10, 20, 0.9);
    box-shadow: var(--shadow-lg);
    position: sticky;
    top: 6rem;
  }

  .code-header {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 0.8rem 1.2rem;
    background: rgba(20, 20, 40, 0.8);
    border-bottom: 1px solid var(--border-subtle);
  }

  .code-dots {
    display: flex;
    gap: 6px;
  }

  .dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
  }

  .dot.red { background: #ff5f57; }
  .dot.yellow { background: #ffbd2e; }
  .dot.green { background: #28c840; }

  .code-filename {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    color: var(--text-muted);
  }

  .code-content {
    padding: 1.5rem;
    font-family: var(--font-mono);
    font-size: 0.82rem;
    line-height: 1.8;
    overflow-x: auto;
    color: var(--text-secondary);
  }

  .code-content :global(.kw) { color: #c678dd; }
  .code-content :global(.type) { color: #e5c07b; }
  .code-content :global(.str) { color: #98c379; }
  .code-content :global(.prop) { color: #61afef; }
  .code-content :global(.var) { color: #e06c75; }

  @media (max-width: 900px) {
    .about-grid {
      grid-template-columns: 1fr;
      gap: 3rem;
    }

    .code-window {
      position: static;
    }
  }
</style>
