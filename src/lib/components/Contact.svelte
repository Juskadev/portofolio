<script lang="ts">
  let sectionRef: HTMLElement;
  let visible = $state(false);
  let formStatus = $state<'idle' | 'sending' | 'sent'>('idle');

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

  function handleSubmit(e: SubmitEvent) {
    e.preventDefault();
    formStatus = 'sending';
    // Simulate form submission
    setTimeout(() => {
      formStatus = 'sent';
      setTimeout(() => { formStatus = 'idle'; }, 3000);
    }, 1500);
  }

  const socials = [
    { name: 'GitHub', url: 'https://github.com/Juskadev', icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>` },
    { name: 'LinkedIn', url: 'https://linkedin.com/in/ryan-juska-68984b2b1', icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>` },
    { name: 'Email', url: 'mailto:Juskapratama1@gmail.com', icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>` },
    { name: 'WhatsApp', url: 'https://wa.me/6285215645649', icon: `<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>` }
  ];
</script>

<section id="contact" class="section contact-section" class:visible bind:this={sectionRef}>
  <div class="container">
    <div class="contact-grid">
      <div class="contact-info">
        <span class="section-label">Get In Touch</span>
        <h2 class="section-title">Let's Connect &<br/>Work Together</h2>
        <p class="contact-text">
          Looking for an Information Technology specialist, Full-Stack developer, or IT operations engineer? 
          Feel free to reach out directly via email, WhatsApp, or connect on LinkedIn and GitHub.
        </p>

        <div class="contact-details">
          <div class="contact-item">
            <div class="contact-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
            </div>
            <div>
              <span class="contact-label">Email</span>
              <a href="mailto:Juskapratama1@gmail.com" class="contact-value">Juskapratama1@gmail.com</a>
            </div>
          </div>

          <div class="contact-item">
            <div class="contact-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
            </div>
            <div>
              <span class="contact-label">Phone / WhatsApp</span>
              <a href="https://wa.me/6285215645649" target="_blank" rel="noopener noreferrer" class="contact-value">0852-1564-5649</a>
            </div>
          </div>

          <div class="contact-item">
            <div class="contact-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/><circle cx="12" cy="10" r="3"/></svg>
            </div>
            <div>
              <span class="contact-label">Location</span>
              <span class="contact-value">Jakarta, Indonesia 🇮🇩</span>
            </div>
          </div>
        </div>

        <div class="social-links">
          {#each socials as social}
            <a href={social.url} class="social-link" aria-label={social.name} target="_blank" rel="noopener noreferrer">
              {@html social.icon}
            </a>
          {/each}
        </div>
      </div>

      <div class="contact-form-wrapper">
        <form class="contact-form glass-card" onsubmit={handleSubmit}>
          <div class="form-group">
            <label for="name" class="form-label">Your Name</label>
            <input type="text" id="name" class="form-input" placeholder="John Doe" required />
          </div>

          <div class="form-group">
            <label for="email" class="form-label">Email Address</label>
            <input type="email" id="email" class="form-input" placeholder="john@example.com" required />
          </div>

          <div class="form-group">
            <label for="subject" class="form-label">Subject</label>
            <input type="text" id="subject" class="form-input" placeholder="Project collaboration" />
          </div>

          <div class="form-group">
            <label for="message" class="form-label">Message</label>
            <textarea id="message" class="form-input form-textarea" placeholder="Tell me about your project..." rows="5" required></textarea>
          </div>

          <button type="submit" class="btn btn-primary submit-btn" disabled={formStatus === 'sending'} id="contact-submit">
            {#if formStatus === 'idle'}
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
              Send Message
            {:else if formStatus === 'sending'}
              <span class="spinner"></span>
              Sending...
            {:else}
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg>
              Message Sent!
            {/if}
          </button>
        </form>
      </div>
    </div>
  </div>
</section>

<style>
  .contact-section {
    background: var(--bg-secondary);
    position: relative;
    overflow: hidden;
  }

  .contact-section::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent-primary), transparent);
  }

  .contact-section::after {
    content: '';
    position: absolute;
    bottom: -200px;
    left: -200px;
    width: 500px;
    height: 500px;
    background: radial-gradient(circle, rgba(124, 58, 237, 0.06), transparent 70%);
    pointer-events: none;
  }

  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: start;
  }

  .contact-info {
    opacity: 0;
    transform: translateY(25px);
  }

  .visible .contact-info {
    animation: fadeInUp 0.6s var(--ease-out-expo) 0.1s forwards;
  }

  .contact-text {
    font-size: 1.05rem;
    color: var(--text-secondary);
    line-height: 1.8;
    margin-bottom: 2rem;
  }

  .contact-details {
    display: flex;
    flex-direction: column;
    gap: 1.2rem;
    margin-bottom: 2rem;
  }

  .contact-item {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .contact-icon {
    width: 44px;
    height: 44px;
    border-radius: var(--radius-sm);
    background: rgba(124, 58, 237, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--accent-primary);
    flex-shrink: 0;
  }

  .contact-label {
    display: block;
    font-size: 0.78rem;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 0.15rem;
  }

  .contact-value {
    font-size: 0.95rem;
    color: var(--text-primary);
    font-weight: 500;
  }

  a.contact-value:hover {
    color: var(--accent-primary);
  }

  .social-links {
    display: flex;
    gap: 0.75rem;
  }

  .social-link {
    width: 44px;
    height: 44px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border-subtle);
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--text-secondary);
    transition: all var(--duration-fast) ease;
  }

  .social-link:hover {
    border-color: var(--accent-primary);
    background: rgba(124, 58, 237, 0.1);
    color: var(--accent-primary);
    transform: translateY(-3px);
    box-shadow: var(--shadow-glow);
  }

  /* Form */
  .contact-form-wrapper {
    opacity: 0;
    transform: translateY(25px);
  }

  .visible .contact-form-wrapper {
    animation: fadeInUp 0.6s var(--ease-out-expo) 0.3s forwards;
  }

  .contact-form {
    padding: 2rem;
  }

  .form-group {
    margin-bottom: 1.3rem;
  }

  .form-label {
    display: block;
    font-size: 0.85rem;
    font-weight: 500;
    color: var(--text-secondary);
    margin-bottom: 0.4rem;
  }

  .form-input {
    width: 100%;
    padding: 0.75rem 1rem;
    background: rgba(10, 10, 20, 0.6);
    border: 1px solid var(--border-subtle);
    border-radius: var(--radius-sm);
    color: var(--text-primary);
    font-family: var(--font-sans);
    font-size: 0.9rem;
    transition: all var(--duration-fast) ease;
    outline: none;
  }

  .form-input::placeholder {
    color: var(--text-muted);
  }

  .form-input:focus {
    border-color: var(--accent-primary);
    box-shadow: 0 0 0 3px rgba(124, 58, 237, 0.1);
  }

  .form-textarea {
    resize: vertical;
    min-height: 120px;
  }

  .submit-btn {
    width: 100%;
    padding: 0.9rem;
    font-size: 1rem;
    margin-top: 0.5rem;
  }

  .submit-btn:disabled {
    opacity: 0.7;
    cursor: not-allowed;
  }

  .spinner {
    width: 18px;
    height: 18px;
    border: 2px solid rgba(255, 255, 255, 0.3);
    border-top-color: white;
    border-radius: 50%;
    animation: spin-slow 0.6s linear infinite;
  }

  @media (max-width: 768px) {
    .contact-grid {
      grid-template-columns: 1fr;
      gap: 3rem;
    }
  }
</style>
