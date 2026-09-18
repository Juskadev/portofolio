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

  const projects = [
    {
      title: 'Smart Home IoT Dashboard',
      description: 'A comprehensive IoT platform connecting 50+ sensors and actuators via MQTT. Real-time data visualization, automated routines, and mobile-first responsive design with live energy monitoring.',
      image: '/project-iot.jpg',
      tags: ['ESP32', 'MQTT', 'React', 'Node.js', 'InfluxDB'],
      category: 'IoT',
      color: '#06b6d4',
      github: 'https://github.com/Juskadev',
      demo: '#'
    },
    {
      title: 'Autonomous Navigation Robot',
      description: 'Built a self-navigating robot using SLAM algorithms, LiDAR, and computer vision. Capable of mapping unknown environments and path-planning in real-time with obstacle avoidance.',
      image: '/project-robotics.jpg',
      tags: ['ROS2', 'Python', 'OpenCV', 'LiDAR', 'C++'],
      category: 'Robotics',
      color: '#f43f5e',
      github: 'https://github.com/Juskadev',
      demo: '#'
    },
    {
      title: 'Enterprise Analytics Platform',
      description: 'A full-stack SaaS analytics dashboard featuring real-time data pipelines, interactive charts, role-based access control, and multi-tenant architecture serving 10K+ daily active users.',
      image: '/project-webapp.jpg',
      tags: ['Next.js', 'TypeScript', 'PostgreSQL', 'GraphQL', 'Docker'],
      category: 'Full-Stack',
      color: '#7c3aed',
      github: 'https://github.com/Juskadev',
      demo: '#'
    },
    {
      title: 'Cloud Infrastructure Platform',
      description: 'Designed and deployed a highly available microservices architecture on AWS. Auto-scaling, blue-green deployments, centralized logging, and 99.99% uptime SLA across multiple regions.',
      image: '/project-server.jpg',
      tags: ['AWS', 'Kubernetes', 'Terraform', 'Prometheus', 'Grafana'],
      category: 'Server',
      color: '#10b981',
      github: 'https://github.com/Juskadev',
      demo: '#'
    }
  ];
</script>

<section id="projects" class="section projects-section" class:visible bind:this={sectionRef}>
  <div class="container">
    <div class="projects-header">
      <span class="section-label">Featured Work</span>
      <h2 class="section-title">Projects That Define Me</h2>
      <p class="section-subtitle">A showcase of projects spanning IoT, robotics, web development, and cloud infrastructure.</p>
    </div>

    <div class="projects-grid">
      {#each projects as project, i}
        <div
          class="project-card"
          style="animation-delay: {0.1 + i * 0.15}s; --project-color: {project.color}"
        >
          <div class="project-image-wrapper">
            <img src={project.image} alt={project.title} class="project-image" />
            <div class="project-overlay">
              <div class="project-links">
                <a href={project.github} class="project-link" aria-label="View source code">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
                </a>
                <a href={project.demo} class="project-link" aria-label="View live demo">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
                </a>
              </div>
            </div>
            <span class="project-category" style="color: {project.color}">{project.category}</span>
          </div>

          <div class="project-info">
            <h3 class="project-title">{project.title}</h3>
            <p class="project-description">{project.description}</p>
            <div class="project-tags">
              {#each project.tags as tag}
                <span class="tag">{tag}</span>
              {/each}
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .projects-section {
    background: var(--bg-secondary);
    position: relative;
    overflow: hidden;
  }

  .projects-section::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent-secondary), transparent);
  }

  .projects-header {
    text-align: center;
    margin-bottom: 3.5rem;
    opacity: 0;
    transform: translateY(20px);
  }

  .visible .projects-header {
    animation: fadeInUp 0.6s var(--ease-out-expo) 0.1s forwards;
  }

  .projects-header .section-label::before {
    display: none;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }

  .project-card {
    background: var(--bg-glass);
    border: 1px solid var(--border-subtle);
    border-radius: var(--radius-lg);
    overflow: hidden;
    transition: all var(--duration-normal) var(--ease-out-expo);
    opacity: 0;
    transform: translateY(25px);
  }

  .visible .project-card {
    animation: fadeInUp 0.6s var(--ease-out-expo) forwards;
  }

  .project-card:hover {
    border-color: var(--project-color, var(--border-hover));
    box-shadow: 0 8px 40px rgba(0, 0, 0, 0.3), 0 0 30px color-mix(in srgb, var(--project-color, var(--accent-primary)) 20%, transparent);
    transform: translateY(-6px);
  }

  .project-image-wrapper {
    position: relative;
    overflow: hidden;
    aspect-ratio: 16 / 9;
  }

  .project-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform var(--duration-slow) var(--ease-out-expo);
  }

  .project-card:hover .project-image {
    transform: scale(1.05);
  }

  .project-overlay {
    position: absolute;
    inset: 0;
    background: rgba(10, 10, 15, 0.7);
    backdrop-filter: blur(4px);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity var(--duration-normal) ease;
  }

  .project-card:hover .project-overlay {
    opacity: 1;
  }

  .project-links {
    display: flex;
    gap: 1rem;
  }

  .project-link {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(255, 255, 255, 0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    transition: all var(--duration-fast) ease;
    transform: translateY(10px);
  }

  .project-card:hover .project-link {
    transform: translateY(0);
  }

  .project-link:hover {
    background: var(--accent-primary);
    border-color: var(--accent-primary);
    transform: scale(1.1) !important;
  }

  .project-category {
    position: absolute;
    top: 1rem;
    left: 1rem;
    padding: 0.3rem 0.8rem;
    border-radius: var(--radius-full);
    background: rgba(10, 10, 15, 0.7);
    backdrop-filter: blur(10px);
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    border: 1px solid rgba(255, 255, 255, 0.1);
  }

  .project-info {
    padding: 1.5rem;
  }

  .project-title {
    font-family: var(--font-display);
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 0.6rem;
    color: var(--text-primary);
  }

  .project-description {
    font-size: 0.9rem;
    color: var(--text-secondary);
    line-height: 1.7;
    margin-bottom: 1.2rem;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }

  .tag {
    padding: 0.25rem 0.7rem;
    border-radius: var(--radius-full);
    font-size: 0.72rem;
    font-weight: 500;
    font-family: var(--font-mono);
    background: rgba(124, 58, 237, 0.1);
    color: var(--accent-primary);
    border: 1px solid rgba(124, 58, 237, 0.15);
  }

  @media (max-width: 768px) {
    .projects-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
