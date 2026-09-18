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

  // Parallax tilt & mouse coordinates
  let mouseX = $state(0);
  let mouseY = $state(0);
  let tiltX = $state(0);
  let tiltY = $state(0);
  let canvasRef: HTMLCanvasElement;

  function handleMouseMove(e: MouseEvent) {
    const { clientX, clientY } = e;
    mouseX = clientX;
    mouseY = clientY;
    const nx = (clientX / window.innerWidth - 0.5) * 2;
    const ny = (clientY / window.innerHeight - 0.5) * 2;
    tiltX = -ny * 14;
    tiltY = nx * 14;
  }

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

  // Particle system for background
  const particles = Array.from({ length: 45 }, (_, i) => ({
    id: i,
    x: Math.random() * 100,
    y: Math.random() * 100,
    size: Math.random() * 3 + 1,
    duration: Math.random() * 20 + 10,
    delay: Math.random() * 5
  }));

  // Futuristic 3D Cyber Reactor Canvas Animation
  $effect(() => {
    if (!canvasRef) return;
    const ctx = canvasRef.getContext('2d');
    if (!ctx) return;

    let animId: number;
    const width = (canvasRef.width = 380);
    const height = (canvasRef.height = 380);
    const cx = width / 2;
    const cy = height / 2;
    const radius = 118;

    // 3D sphere quantum node constellation
    const pointCount = 70;
    const points: Array<{ x: number; y: number; z: number; baseR: number }> = [];
    for (let i = 0; i < pointCount; i++) {
      const theta = Math.acos(2 * Math.random() - 1);
      const phi = Math.random() * Math.PI * 2;
      points.push({
        x: radius * Math.sin(theta) * Math.cos(phi),
        y: radius * Math.sin(theta) * Math.sin(phi),
        z: radius * Math.cos(theta),
        baseR: Math.random() * 2.2 + 1.2
      });
    }

    let angleX = 0;
    let angleY = 0;
    let scanAngle = 0;

    const render = () => {
      ctx.clearRect(0, 0, width, height);

      angleX += 0.005 + (tiltX * 0.0002);
      angleY += 0.008 + (tiltY * 0.0002);
      scanAngle += 0.03;

      const cosX = Math.cos(angleX);
      const sinX = Math.sin(angleX);
      const cosY = Math.cos(angleY);
      const sinY = Math.sin(angleY);

      // Central glowing plasma reactor core
      const coreGrad = ctx.createRadialGradient(cx, cy, 2, cx, cy, radius * 0.9);
      coreGrad.addColorStop(0, 'rgba(124, 58, 237, 0.4)');
      coreGrad.addColorStop(0.45, 'rgba(6, 182, 212, 0.22)');
      coreGrad.addColorStop(0.85, 'rgba(14, 165, 233, 0.08)');
      coreGrad.addColorStop(1, 'rgba(0, 0, 0, 0)');
      ctx.fillStyle = coreGrad;
      ctx.beginPath();
      ctx.arc(cx, cy, radius * 0.9, 0, Math.PI * 2);
      ctx.fill();

      // Sweeping radar scan beam
      ctx.save();
      ctx.translate(cx, cy);
      ctx.rotate(scanAngle);
      const radarGrad = ctx.createLinearGradient(0, 0, radius * 0.95, 0);
      radarGrad.addColorStop(0, 'rgba(6, 182, 212, 0.7)');
      radarGrad.addColorStop(1, 'rgba(6, 182, 212, 0)');
      ctx.strokeStyle = radarGrad;
      ctx.lineWidth = 1.8;
      ctx.beginPath();
      ctx.moveTo(0, 0);
      ctx.lineTo(radius * 0.95, 0);
      ctx.stroke();
      ctx.restore();

      // Project 3D nodes to 2D
      const projected: Array<{ px: number; py: number; pz: number; size: number }> = [];

      for (let i = 0; i < points.length; i++) {
        const pt = points[i];
        const x1 = pt.x * cosY - pt.z * sinY;
        const z1 = pt.z * cosY + pt.x * sinY;
        const y1 = pt.y * cosX - z1 * sinX;
        const z2 = z1 * cosX + pt.y * sinX;

        const fov = 320;
        const scale = fov / (fov + z2);
        const px = cx + x1 * scale;
        const py = cy + y1 * scale;
        const size = Math.max(0.6, pt.baseR * scale);

        projected.push({ px, py, pz: z2, size });
      }

      // Connecting laser network
      for (let i = 0; i < projected.length; i++) {
        for (let j = i + 1; j < projected.length; j++) {
          const dx = projected[i].px - projected[j].px;
          const dy = projected[i].py - projected[j].py;
          const dist = Math.sqrt(dx * dx + dy * dy);
          if (dist < 48) {
            const alpha = (1 - dist / 48) * 0.3 * (projected[i].pz > 0 || projected[j].pz > 0 ? 1 : 0.35);
            ctx.strokeStyle = `rgba(6, 182, 212, ${alpha})`;
            ctx.lineWidth = 0.8;
            ctx.beginPath();
            ctx.moveTo(projected[i].px, projected[i].py);
            ctx.lineTo(projected[j].px, projected[j].py);
            ctx.stroke();
          }
        }
      }

      // Render glowing nodes
      for (let i = 0; i < projected.length; i++) {
        const { px, py, pz, size } = projected[i];
        const depthAlpha = ((pz + radius) / (radius * 2)) * 0.7 + 0.3;

        ctx.save();
        ctx.beginPath();
        ctx.arc(px, py, size, 0, Math.PI * 2);
        if (i % 3 === 0) {
          ctx.fillStyle = `rgba(6, 182, 212, ${depthAlpha})`;
          ctx.shadowColor = '#06b6d4';
          ctx.shadowBlur = 9;
        } else if (i % 3 === 1) {
          ctx.fillStyle = `rgba(168, 85, 247, ${depthAlpha})`;
          ctx.shadowColor = '#a855f7';
          ctx.shadowBlur = 9;
        } else {
          ctx.fillStyle = `rgba(244, 63, 94, ${depthAlpha * 0.8})`;
          ctx.shadowColor = '#f43f5e';
          ctx.shadowBlur = 6;
        }
        ctx.fill();
        ctx.restore();
      }

      animId = requestAnimationFrame(render);
    };

    render();
    return () => cancelAnimationFrame(animId);
  });
</script>

<svelte:window onmousemove={handleMouseMove} />

<section id="hero" class="hero" class:visible>
  <!-- Animated ambient cursor glow -->
  <div
    class="cursor-glow"
    style="transform: translate({mouseX - 250}px, {mouseY - 250}px);"
  ></div>

  <!-- Background particles -->
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

  <!-- Ambient gradient orbs -->
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>

  <!-- Cyber grid overlay -->
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

    <!-- Interactive 3D Cyber Reactor Visual (Zero Text in Circle) -->
    <div
      class="hero-visual"
      style="transform: perspective(1000px) rotateX({tiltX}deg) rotateY({tiltY}deg);"
    >
      <div class="reactor-wrapper">
        <!-- Outer Sci-Fi HUD Compass Ring -->
        <svg class="hud-ring ring-outer" viewBox="0 0 400 400" aria-hidden="true">
          <circle cx="200" cy="200" r="192" fill="none" stroke="rgba(124, 58, 237, 0.28)" stroke-width="1.5" stroke-dasharray="10 15" />
          <circle cx="200" cy="200" r="180" fill="none" stroke="rgba(6, 182, 212, 0.32)" stroke-width="2" stroke-dasharray="80 30 15 30" />
          <circle cx="200" cy="200" r="168" fill="none" stroke="rgba(244, 63, 94, 0.2)" stroke-width="1" stroke-dasharray="4 8" />
          <!-- Orbiting Satellite Beacons -->
          <circle cx="200" cy="8" r="4.5" fill="#06b6d4" />
          <circle cx="392" cy="200" r="4" fill="#a855f7" />
          <circle cx="200" cy="392" r="3.5" fill="#06b6d4" />
          <circle cx="8" cy="200" r="4" fill="#f43f5e" />
        </svg>

        <!-- Inner Counter-Rotating HUD Ticks Ring -->
        <svg class="hud-ring ring-inner" viewBox="0 0 340 340" aria-hidden="true">
          <circle cx="170" cy="170" r="162" fill="none" stroke="rgba(6, 182, 212, 0.25)" stroke-width="1.5" stroke-dasharray="6 12 25 12" />
          <circle cx="170" cy="170" r="148" fill="none" stroke="rgba(168, 85, 247, 0.3)" stroke-width="1.5" stroke-dasharray="120 40" />
          <!-- Crosshair Compass Ticks -->
          <line x1="170" y1="4" x2="170" y2="18" stroke="#06b6d4" stroke-width="2.5" />
          <line x1="170" y1="322" x2="170" y2="336" stroke="#06b6d4" stroke-width="2.5" />
          <line x1="4" y1="170" x2="18" y2="170" stroke="#a855f7" stroke-width="2.5" />
          <line x1="322" y1="170" x2="336" y2="170" stroke="#a855f7" stroke-width="2.5" />
        </svg>

        <!-- Central 3D Quantum Reactor Core with Ryan's Portrait (No white text) -->
        <div class="core-viewport">
          <img src="/profile-square.png" alt="" class="profile-photo" aria-hidden="true" />
          <canvas bind:this={canvasRef} class="quantum-canvas" aria-hidden="true"></canvas>
          <div class="core-hologram-overlay" aria-hidden="true"></div>
          <div class="core-scanline" aria-hidden="true"></div>
          <div class="core-vignette" aria-hidden="true"></div>
        </div>

        <div class="reactor-glow" aria-hidden="true"></div>

        <!-- Floating Live Telemetry Status Chips -->
        <div class="floating-badge badge-1">
          <span class="telemetry-dot green"></span>
          SYS: ONLINE
        </div>
        <div class="floating-badge badge-2">
          <span class="telemetry-dot cyan"></span>
          FULL-STACK // IOT
        </div>
        <div class="floating-badge badge-3">
          <span class="telemetry-dot purple"></span>
          S.Kom // GPA 3.70
        </div>
        <div class="floating-badge badge-4">
          <span class="telemetry-dot rose"></span>
          ROBOTICS // ROS
        </div>
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

  /* Interactive cursor neon spotlight */
  .cursor-glow {
    position: fixed;
    width: 500px;
    height: 500px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(124, 58, 237, 0.12) 0%, rgba(6, 182, 212, 0.06) 45%, transparent 70%);
    pointer-events: none;
    z-index: 0;
    transition: transform 0.15s ease-out;
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
    0% {
      opacity: 0;
      transform: translateY(100vh) scale(0);
    }
    10% {
      opacity: 0.6;
    }
    90% {
      opacity: 0.6;
    }
    100% {
      opacity: 0;
      transform: translateY(-10vh) scale(1);
    }
  }

  /* Gradient Orbs */
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
    z-index: 0;
  }

  .orb-1 {
    width: 500px;
    height: 500px;
    background: rgba(124, 58, 237, 0.18);
    top: 10%;
    left: -10%;
    animation: orbFloat1 20s ease-in-out infinite;
  }

  .orb-2 {
    width: 450px;
    height: 450px;
    background: rgba(6, 182, 212, 0.15);
    bottom: 5%;
    right: -5%;
    animation: orbFloat2 25s ease-in-out infinite;
  }

  .orb-3 {
    width: 350px;
    height: 350px;
    background: rgba(244, 63, 94, 0.1);
    top: 50%;
    left: 45%;
    animation: orbFloat3 18s ease-in-out infinite;
  }

  @keyframes orbFloat1 {
    0%, 100% { transform: translate(0, 0) scale(1); }
    50% { transform: translate(60px, 40px) scale(1.15); }
  }

  @keyframes orbFloat2 {
    0%, 100% { transform: translate(0, 0) scale(1); }
    50% { transform: translate(-50px, -60px) scale(1.1); }
  }

  @keyframes orbFloat3 {
    0%, 100% { transform: translate(0, 0) scale(1); }
    50% { transform: translate(40px, -30px) scale(0.9); }
  }

  /* Grid Overlay */
  .grid-overlay {
    position: absolute;
    inset: 0;
    background-image: 
      linear-gradient(rgba(255, 255, 255, 0.02) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse at center, black 40%, transparent 80%);
    -webkit-mask-image: radial-gradient(ellipse at center, black 40%, transparent 80%);
    pointer-events: none;
    z-index: 0;
  }

  /* Container & Content */
  .hero-container {
    display: grid;
    grid-template-columns: 1.15fr 0.85fr;
    align-items: center;
    gap: 4rem;
    position: relative;
    z-index: 1;
    padding: 3rem 0;
  }

  .hero-content {
    opacity: 0;
    transform: translateY(30px);
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.2s forwards;
  }

  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.4rem 1rem;
    border-radius: var(--radius-full);
    background: var(--bg-glass);
    border: 1px solid var(--border-subtle);
    font-size: 0.85rem;
    color: var(--text-secondary);
    margin-bottom: 1.5rem;
    backdrop-filter: blur(10px);
  }

  .badge-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--accent-success);
    box-shadow: 0 0 10px var(--accent-success);
    animation: pulse 2s infinite;
  }

  .hero-title {
    margin-bottom: 1rem;
  }

  .hero-greeting {
    display: block;
    font-size: clamp(1.2rem, 2.5vw, 1.6rem);
    font-weight: 400;
    color: var(--text-secondary);
    font-family: var(--font-body);
    letter-spacing: 0.05em;
  }

  .hero-name {
    display: block;
    font-size: clamp(2.5rem, 5.5vw, 4.2rem);
    font-weight: 800;
    line-height: 1.1;
    letter-spacing: -0.03em;
    background: linear-gradient(135deg, #ffffff 0%, #cbd5e1 50%, var(--accent-primary) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-role {
    font-size: clamp(1.1rem, 2.2vw, 1.5rem);
    font-family: var(--font-mono);
    color: var(--text-secondary);
    margin-bottom: 1.5rem;
    min-height: 2.2rem;
    display: flex;
    align-items: center;
  }

  .role-prefix {
    color: var(--text-muted);
  }

  .role-typed {
    color: var(--accent-secondary);
    font-weight: 600;
    margin-left: 0.3rem;
  }

  .role-cursor {
    color: var(--accent-primary);
    animation: blink 0.8s infinite;
    font-weight: 300;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  .hero-description {
    font-size: 1.05rem;
    line-height: 1.7;
    color: var(--text-secondary);
    max-width: 540px;
    margin-bottom: 2rem;
  }

  .hero-actions {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin-bottom: 2.5rem;
  }

  .cv-btn {
    border-color: rgba(6, 182, 212, 0.4);
    color: var(--accent-secondary);
  }

  .cv-btn:hover {
    border-color: var(--accent-secondary);
    background: rgba(6, 182, 212, 0.1);
    box-shadow: 0 0 20px rgba(6, 182, 212, 0.3);
  }

  /* Stats */
  .hero-stats {
    display: flex;
    align-items: center;
    gap: 2rem;
    padding-top: 1.5rem;
    border-top: 1px solid var(--border-subtle);
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
    letter-spacing: 0.08em;
  }

  .stat-divider {
    width: 1px;
    height: 40px;
    background: var(--border-subtle);
  }

  /* 3D Visual / Futuristic Cyber Reactor */
  .hero-visual {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    opacity: 0;
    animation: fadeInUp 0.8s var(--ease-out-expo) 0.5s forwards;
    transition: transform 0.12s ease-out;
    transform-style: preserve-3d;
  }

  .reactor-wrapper {
    position: relative;
    width: clamp(300px, 32vw, 400px);
    height: clamp(300px, 32vw, 400px);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  /* Concentric Sci-Fi HUD Rings */
  .hud-ring {
    position: absolute;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 2;
  }

  .ring-outer {
    animation: spinClockwise 36s linear infinite;
  }

  .ring-inner {
    width: 85%;
    height: 85%;
    animation: spinCounterClockwise 24s linear infinite;
  }

  @keyframes spinClockwise {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  @keyframes spinCounterClockwise {
    from { transform: rotate(360deg); }
    to { transform: rotate(0deg); }
  }

  /* Central Quantum Reactor Viewport */
  .core-viewport {
    position: relative;
    width: 72%;
    height: 72%;
    border-radius: 50%;
    background: radial-gradient(circle at 45% 45%, #131127 0%, #080614 70%, #03020a 100%);
    border: 2px solid rgba(6, 182, 212, 0.4);
    box-shadow: 
      0 0 35px rgba(6, 182, 212, 0.25),
      inset 0 0 30px rgba(124, 58, 237, 0.35);
    overflow: hidden;
    z-index: 3;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .profile-photo {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center 25%;
    position: absolute;
    inset: 0;
    z-index: 1;
    filter: contrast(1.06) brightness(1.02);
    transition: transform 0.4s ease-out;
  }

  .core-viewport:hover .profile-photo {
    transform: scale(1.05);
  }

  .quantum-canvas {
    width: 100%;
    height: 100%;
    display: block;
    position: absolute;
    inset: 0;
    z-index: 2;
    pointer-events: none;
    mix-blend-mode: screen;
    opacity: 0.78;
  }

  .core-hologram-overlay {
    position: absolute;
    inset: 0;
    border-radius: 50%;
    background: radial-gradient(circle, transparent 45%, rgba(124, 58, 237, 0.18) 75%, rgba(6, 182, 212, 0.35) 100%);
    pointer-events: none;
    z-index: 3;
  }

  /* Scanline sweep across the core */
  .core-scanline {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 3px;
    background: linear-gradient(90deg, transparent, rgba(6, 182, 212, 0.9), transparent);
    box-shadow: 0 0 12px rgba(6, 182, 212, 0.8);
    animation: scanSweep 3.2s ease-in-out infinite alternate;
    pointer-events: none;
    z-index: 4;
  }

  @keyframes scanSweep {
    0% { top: 2%; opacity: 0.3; }
    50% { opacity: 0.9; }
    100% { top: 96%; opacity: 0.3; }
  }

  .core-vignette {
    position: absolute;
    inset: 0;
    border-radius: 50%;
    box-shadow: inset 0 0 25px rgba(0, 0, 0, 0.85);
    pointer-events: none;
    z-index: 5;
  }

  .reactor-glow {
    position: absolute;
    inset: -25px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(124, 58, 237, 0.25) 0%, rgba(6, 182, 212, 0.15) 50%, transparent 70%);
    filter: blur(25px);
    z-index: 1;
    animation: pulseReactorGlow 4s ease-in-out infinite alternate;
    pointer-events: none;
  }

  @keyframes pulseReactorGlow {
    0% { opacity: 0.5; transform: scale(0.95); }
    100% { opacity: 0.9; transform: scale(1.05); }
  }

  /* Floating Telemetry Badges */
  .floating-badge {
    position: absolute;
    display: flex;
    align-items: center;
    gap: 0.55rem;
    padding: 0.55rem 1.1rem;
    border-radius: var(--radius-full);
    background: rgba(15, 13, 31, 0.82);
    backdrop-filter: blur(16px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    font-family: var(--font-mono);
    font-size: 0.76rem;
    font-weight: 600;
    color: var(--text-primary);
    white-space: nowrap;
    z-index: 6;
    animation: float 4s ease-in-out infinite;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.4);
    letter-spacing: 0.05em;
  }

  .telemetry-dot {
    width: 7px;
    height: 7px;
    border-radius: 50%;
  }

  .telemetry-dot.green {
    background: #10b981;
    box-shadow: 0 0 8px #10b981;
    animation: blinkDot 1.4s infinite;
  }

  .telemetry-dot.cyan {
    background: #06b6d4;
    box-shadow: 0 0 8px #06b6d4;
    animation: blinkDot 1.8s infinite;
  }

  .telemetry-dot.purple {
    background: #a855f7;
    box-shadow: 0 0 8px #a855f7;
    animation: blinkDot 2.2s infinite;
  }

  .telemetry-dot.rose {
    background: #f43f5e;
    box-shadow: 0 0 8px #f43f5e;
    animation: blinkDot 1.6s infinite;
  }

  @keyframes blinkDot {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.85); }
  }

  .badge-1 {
    top: 3%;
    left: -8%;
    animation-delay: 0s;
    border-color: rgba(16, 185, 129, 0.35);
  }

  .badge-2 {
    top: 12%;
    right: -12%;
    animation-delay: 1s;
    border-color: rgba(6, 182, 212, 0.35);
  }

  .badge-3 {
    bottom: 14%;
    left: -12%;
    animation-delay: 2s;
    border-color: rgba(168, 85, 247, 0.35);
  }

  .badge-4 {
    bottom: 4%;
    right: -8%;
    animation-delay: 3s;
    border-color: rgba(244, 63, 94, 0.35);
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

  @media (max-width: 960px) {
    .hero-container {
      grid-template-columns: 1fr;
      text-align: center;
      gap: 3.5rem;
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

    .reactor-wrapper {
      width: 280px;
      height: 280px;
    }

    .floating-badge {
      display: none;
    }

    .scroll-indicator {
      display: none;
    }
  }
</style>
