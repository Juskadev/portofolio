<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);

  $effect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) visible = true;
      },
      { threshold: 0.1 }
    );
    if (sectionRef) observer.observe(sectionRef);
    return () => observer.disconnect();
  });

  const experiences = [
    {
      role: 'IT & Data Systems Intern',
      company: 'Komisi Yudisial RI (Judicial Commission of Indonesia) | Jakarta',
      period: 'June 2023 — December 2023',
      description: 'Managed and secured sensitive institutional databases (judicial records, verdicts, and complaints) with rigorous data accuracy, integrity, and confidentiality. Resolved data discrepancies through systematic troubleshooting and produced analytical intelligence reports for leadership.',
      highlights: ['Database Security & Integrity', 'System Troubleshooting', 'Analytical Reports for Commissioners', 'Data Operations Center'],
      color: '#06b6d4'
    },
    {
      role: 'Bachelor of Computer Science (S.Kom)',
      company: 'Universitas Bina Sarana Informatika | Central Jakarta',
      period: 'August 2020 — August 2024',
      description: 'Graduated with high honors (GPA 3.70 / 4.00) majoring in Information Technology. Authored a national scientific publication in JNKTI (SINTA 5) in 2024. Completed Cisco Networking Academy PCAP certification in Python and Software Developer certification.',
      highlights: ['GPA 3.70 / 4.00', 'Author JNKTI SINTA 5', 'PCAP Cisco Certified', 'Software Developer Certified'],
      color: '#10b981'
    },
    {
      role: 'Head of Administration (Kepala Tata Usaha)',
      company: 'SMA Muhammadiyah 16 Jakarta | Central Jakarta',
      period: 'September 2019 — December 2020',
      description: 'Led administrative and operational support functions, including document control, correspondence, budgeting, and inter-departmental coordination. Strengthened digital record-keeping systems and facilities management with high attention to detail.',
      highlights: ['Operations & Admin Leadership', 'Digital Record Systems', 'Budget & Resource Management', 'Staff Coordination'],
      color: '#7c3aed'
    },
    {
      role: 'Data Operations Staff (Completions Operator)',
      company: 'PT Sigma Cipta Utama (Subsidiary of Telkom Indonesia) | Jakarta',
      period: 'May 2019 — August 2019',
      description: 'Executed high-volume data entry and system updates from physical documents, digital files, and voice sources. Performed rigorous verification and quality checks to eliminate data errors while upholding Telkom Group confidentiality standards.',
      highlights: ['High-Volume Data Operations', 'Quality Assurance & Audit', 'Telkom Indonesia Subsidiary', 'Confidentiality Standards'],
      color: '#f43f5e'
    }
  ];
</script>

<section id="experience" class="section experience-section" class:visible bind:this={sectionRef}>
  <div class="container">
    <div class="experience-header">
      <span class="section-label">Experience</span>
      <h2 class="section-title">Career Journey</h2>
      <p class="section-subtitle">From frontend pixels to robotic systems — here's my professional timeline.</p>
    </div>

    <div class="timeline">
      <div class="timeline-line"></div>

      {#each experiences as exp, i}
        <div
          class="timeline-item"
          class:right={i % 2 !== 0}
          style="animation-delay: {0.2 + i * 0.2}s"
        >
          <div class="timeline-dot" style="background: {exp.color}; box-shadow: 0 0 15px {exp.color}40"></div>
          <div class="timeline-card glass-card">
            <div class="timeline-period" style="color: {exp.color}">{exp.period}</div>
            <h3 class="timeline-role">{exp.role}</h3>
            <span class="timeline-company">{exp.company}</span>
            <p class="timeline-desc">{exp.description}</p>
            <div class="timeline-highlights">
              {#each exp.highlights as h}
                <span class="timeline-tag" style="border-color: {exp.color}30; color: {exp.color}">
                  {h}
                </span>
              {/each}
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .experience-section {
    position: relative;
    overflow: hidden;
  }

  .experience-header {
    text-align: center;
    margin-bottom: 4rem;
    opacity: 0;
    transform: translateY(20px);
  }

  .visible .experience-header {
    animation: fadeInUp 0.6s var(--ease-out-expo) 0.1s forwards;
  }

  .experience-header .section-label::before {
    display: none;
  }

  .timeline {
    position: relative;
    max-width: 900px;
    margin: 0 auto;
  }

  .timeline-line {
    position: absolute;
    left: 50%;
    top: 0;
    bottom: 0;
    width: 2px;
    background: linear-gradient(to bottom, var(--accent-primary), var(--accent-secondary), var(--accent-success));
    transform: translateX(-50%);
    opacity: 0;
  }

  .visible .timeline-line {
    animation: growDown 1s var(--ease-out-expo) 0.3s forwards;
  }

  @keyframes growDown {
    from { opacity: 0; height: 0; }
    to { opacity: 1; height: 100%; }
  }

  .timeline-item {
    position: relative;
    width: 50%;
    padding: 0 2.5rem 3rem 0;
    opacity: 0;
    transform: translateX(-30px);
  }

  .visible .timeline-item {
    animation: slideInLeft 0.6s var(--ease-out-expo) forwards;
  }

  .timeline-item.right {
    margin-left: 50%;
    padding: 0 0 3rem 2.5rem;
    transform: translateX(30px);
  }

  .visible .timeline-item.right {
    animation: slideInRight 0.6s var(--ease-out-expo) forwards;
  }

  @keyframes slideInRight {
    from { opacity: 0; transform: translateX(30px); }
    to { opacity: 1; transform: translateX(0); }
  }

  .timeline-dot {
    position: absolute;
    right: -8px;
    top: 0.5rem;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    z-index: 2;
    border: 3px solid var(--bg-primary);
  }

  .timeline-item.right .timeline-dot {
    left: -8px;
    right: auto;
  }

  .timeline-card {
    padding: 1.5rem;
    border-radius: var(--radius-md);
  }

  .timeline-card:hover {
    transform: translateY(-4px) !important;
  }

  .timeline-period {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
    letter-spacing: 0.05em;
  }

  .timeline-role {
    font-family: var(--font-display);
    font-size: 1.15rem;
    font-weight: 700;
    color: var(--text-primary);
    margin-bottom: 0.25rem;
  }

  .timeline-company {
    font-size: 0.9rem;
    color: var(--text-muted);
    display: block;
    margin-bottom: 0.75rem;
  }

  .timeline-desc {
    font-size: 0.88rem;
    color: var(--text-secondary);
    line-height: 1.7;
    margin-bottom: 1rem;
  }

  .timeline-highlights {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }

  .timeline-tag {
    padding: 0.2rem 0.65rem;
    border-radius: var(--radius-full);
    font-size: 0.72rem;
    font-weight: 500;
    border: 1px solid;
    background: rgba(255, 255, 255, 0.02);
  }

  @media (max-width: 768px) {
    .timeline-line {
      left: 20px;
    }

    .timeline-item,
    .timeline-item.right {
      width: 100%;
      margin-left: 0;
      padding: 0 0 2.5rem 3.5rem;
    }

    .timeline-dot,
    .timeline-item.right .timeline-dot {
      left: 12px;
      right: auto;
    }

    .timeline-item,
    .visible .timeline-item,
    .timeline-item.right,
    .visible .timeline-item.right {
      transform: none;
      animation: fadeInUp 0.6s var(--ease-out-expo) forwards;
    }
  }
</style>
