<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);
  let activeCategory = $state('all');

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

  interface Skill {
    name: string;
    level: number;
    category: string;
    icon: string;
    color: string;
  }

  const categories = [
    { id: 'all', label: 'All Skills' },
    { id: 'frontend', label: 'Frontend' },
    { id: 'backend', label: 'Backend & DB' },
    { id: 'iot', label: 'IoT' },
    { id: 'server', label: 'IT & Infrastructure' },
    { id: 'robotics', label: 'Robotics' },
  ];

  const skills: Skill[] = [
    // Frontend
    { name: 'Svelte / SvelteKit', level: 92, category: 'frontend', icon: '🔥', color: '#ff3e00' },
    { name: 'TypeScript / JavaScript', level: 90, category: 'frontend', icon: '📘', color: '#3178c6' },
    { name: 'React / Next.js', level: 88, category: 'frontend', icon: '⚛️', color: '#61dafb' },
    { name: 'CSS / Responsive UI', level: 94, category: 'frontend', icon: '🎨', color: '#06b6d4' },
    { name: 'HTML5 & Semantic Web', level: 95, category: 'frontend', icon: '🌐', color: '#e34f26' },
    // Backend & DB
    { name: 'Python (PCAP Certified)', level: 95, category: 'backend', icon: '🐍', color: '#3776ab' },
    { name: 'SQL & Relational DBs', level: 92, category: 'backend', icon: '🗄️', color: '#336791' },
    { name: 'Node.js / Express', level: 88, category: 'backend', icon: '🟢', color: '#68a063' },
    { name: 'Data Validation & Integrity', level: 94, category: 'backend', icon: '🛡️', color: '#10b981' },
    { name: 'RESTful API Architecture', level: 90, category: 'backend', icon: '🔗', color: '#e535ab' },
    { name: 'Java Basics & OOP', level: 82, category: 'backend', icon: '☕', color: '#f89820' },
    // IoT
    { name: 'Arduino / ESP32', level: 93, category: 'iot', icon: '🔌', color: '#00979d' },
    { name: 'MQTT / IoT Protocols', level: 88, category: 'iot', icon: '📡', color: '#660066' },
    { name: 'Sensor & Actuator I/O', level: 90, category: 'iot', icon: '🌡️', color: '#ff8c00' },
    { name: 'Raspberry Pi / Embedded', level: 89, category: 'iot', icon: '🍓', color: '#c51a4a' },
    { name: 'Microcontroller Programming', level: 86, category: 'iot', icon: '⚙️', color: '#a8b9cc' },
    // IT & Infrastructure
    { name: 'IT Technical Troubleshooting', level: 96, category: 'server', icon: '🛠️', color: '#00bcd4' },
    { name: 'Networking Concepts & TCP/IP', level: 90, category: 'server', icon: '🌐', color: '#2196f3' },
    { name: 'Linux / Command Line / Bash', level: 89, category: 'server', icon: '🐧', color: '#fcc624' },
    { name: 'Cloud Computing Fundamentals', level: 86, category: 'server', icon: '☁️', color: '#ff9900' },
    { name: 'Docker / Containerization', level: 85, category: 'server', icon: '🐳', color: '#2496ed' },
    { name: 'System & Process Documentation', level: 94, category: 'server', icon: '📋', color: '#4caf50' },
    // Robotics
    { name: 'ROS / ROS2', level: 85, category: 'robotics', icon: '🤖', color: '#22314e' },
    { name: 'Computer Vision / OpenCV', level: 82, category: 'robotics', icon: '👁️', color: '#5c3ee8' },
    { name: 'Autonomous Motion Planning', level: 80, category: 'robotics', icon: '🦾', color: '#e74c3c' },
    { name: 'SLAM & Sensor Fusion', level: 78, category: 'robotics', icon: '🗺️', color: '#27ae60' },
  ];

  let filteredSkills = $derived(
    activeCategory === 'all' ? skills : skills.filter(s => s.category === activeCategory)
  );
</script>

<section id="skills" class="section skills-section" class:visible bind:this={sectionRef}>
  <div class="container">
    <div class="skills-header">
      <span class="section-label">Technical Skills</span>
      <h2 class="section-title">My Tech Arsenal</h2>
      <p class="section-subtitle">A comprehensive toolkit spanning across multiple engineering disciplines.</p>
    </div>

    <div class="category-tabs">
      {#each categories as cat}
        <button
          class="tab"
          class:active={activeCategory === cat.id}
          onclick={() => (activeCategory = cat.id)}
          id="skills-tab-{cat.id}"
        >
          {cat.label}
        </button>
      {/each}
    </div>

    <div class="skills-grid">
      {#each filteredSkills as skill, i (skill.name)}
        <div
          class="skill-card glass-card"
          style="animation-delay: {i * 0.05}s; --skill-color: {skill.color}"
        >
          <div class="skill-header">
            <span class="skill-icon">{skill.icon}</span>
            <span class="skill-name">{skill.name}</span>
            <span class="skill-pct">{skill.level}%</span>
          </div>
          <div class="skill-bar-bg">
            <div
              class="skill-bar-fill"
              style="width: {visible ? skill.level : 0}%; background: {skill.color}"
            ></div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .skills-section {
    position: relative;
    overflow: hidden;
  }

  .skills-section::before {
    content: '';
    position: absolute;
    width: 500px;
    height: 500px;
    background: radial-gradient(circle, rgba(6, 182, 212, 0.06), transparent 70%);
    top: -100px;
    right: -100px;
    pointer-events: none;
  }

  .skills-header {
    text-align: center;
    margin-bottom: 3rem;
    opacity: 0;
    transform: translateY(20px);
  }

  .visible .skills-header {
    animation: fadeInUp 0.6s var(--ease-out-expo) 0.1s forwards;
  }

  .skills-header .section-label::before {
    display: none;
  }

  .category-tabs {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 2.5rem;
    opacity: 0;
  }

  .visible .category-tabs {
    animation: fadeInUp 0.6s var(--ease-out-expo) 0.25s forwards;
  }

  .tab {
    padding: 0.55rem 1.3rem;
    border-radius: var(--radius-full);
    border: 1px solid var(--border-subtle);
    background: transparent;
    color: var(--text-secondary);
    font-family: var(--font-sans);
    font-size: 0.85rem;
    font-weight: 500;
    cursor: pointer;
    transition: all var(--duration-fast) ease;
  }

  .tab:hover {
    border-color: var(--border-hover);
    color: var(--text-primary);
  }

  .tab.active {
    background: var(--gradient-primary);
    border-color: transparent;
    color: white;
    box-shadow: 0 4px 15px rgba(124, 58, 237, 0.3);
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1rem;
  }

  .skill-card {
    padding: 1.2rem 1.4rem;
    border-radius: var(--radius-md);
    opacity: 0;
    transform: translateY(15px);
  }

  .visible .skill-card {
    animation: fadeInUp 0.5s var(--ease-out-expo) forwards;
  }

  .skill-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 20px rgba(var(--skill-color), 0.1);
  }

  .skill-header {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    margin-bottom: 0.75rem;
  }

  .skill-icon {
    font-size: 1.2rem;
  }

  .skill-name {
    font-weight: 600;
    font-size: 0.9rem;
    flex: 1;
  }

  .skill-pct {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--text-muted);
  }

  .skill-bar-bg {
    width: 100%;
    height: 4px;
    background: rgba(255, 255, 255, 0.06);
    border-radius: 4px;
    overflow: hidden;
  }

  .skill-bar-fill {
    height: 100%;
    border-radius: 4px;
    transition: width 1.2s var(--ease-out-expo);
    box-shadow: 0 0 8px rgba(124, 58, 237, 0.3);
  }

  @media (max-width: 768px) {
    .skills-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
