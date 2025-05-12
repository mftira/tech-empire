---
layout: default
title: About
permalink: /about/
---

<div class="about-page">
  <!-- Ad space at top -->
  <div class="ad-space">
    <script type="text/javascript">
      aclib.runAutoTag({
          zoneId: 'edujuvxsbw',
      });
    </script>
  </div>

  <div class="about-container">
    <div class="about-header">
      <h1 class="gradient-text">About Tech Empire</h1>
      <p class="about-subtitle">Your Gateway to the Future of Technology</p>
    </div>

    <div class="about-content">
      <section class="about-section">
        <h2>Our Mission</h2>
        <p>Tech Empire is your trusted source for the latest in technology, AI, gadgets, apps, and innovation. 
        We empower readers with clear, actionable tutorials, insightful guides, and up-to-date news from the 
        ever-evolving world of technology.</p>
      </section>

      <section class="about-section">
        <h2>What We Cover</h2>
        <div class="features-grid">
          <div class="feature-card">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"></path>
            </svg>
            <h3>AI & Machine Learning</h3>
            <p>Latest developments in artificial intelligence and machine learning technologies</p>
          </div>
          <div class="feature-card">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <rect x="4" y="4" width="16" height="16" rx="2" ry="2"></rect>
              <line x1="12" y1="6" x2="12" y2="18"></line>
            </svg>
            <h3>Gadget Reviews</h3>
            <p>In-depth reviews and comparisons of the latest tech gadgets</p>
          </div>
          <div class="feature-card">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"></path>
            </svg>
            <h3>Tutorials & Guides</h3>
            <p>Step-by-step tutorials and comprehensive guides for all skill levels</p>
          </div>
          <div class="feature-card">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="10"></circle>
              <line x1="12" y1="16" x2="12" y2="12"></line>
              <line x1="12" y1="8" x2="12.01" y2="8"></line>
            </svg>
            <h3>Tech News</h3>
            <p>Breaking news and analysis from the tech industry</p>
          </div>
        </div>
      </section>

      <section class="about-section">
        <h2>Why Choose Us</h2>
        <ul class="benefits-list">
          <li>✓ Clean, distraction-free reading experience</li>
          <li>✓ SEO-optimized, fast, and mobile-friendly</li>
          <li>✓ Regular updates from tech experts</li>
          <li>✓ In-depth analysis and comprehensive coverage</li>
        </ul>
      </section>

      <section class="about-section contact-section">
        <h2>Get in Touch</h2>
        <p>For inquiries, collaborations, or feedback, reach out to us at:</p>
        <a href="mailto:{{ site.email }}" class="contact-button">{{ site.email }}</a>
      </section>
    </div>
  </div>

  <!-- Ad space at bottom -->
  <div class="ad-space">
    <script type="text/javascript">
      aclib.runAutoTag({
          zoneId: 'edujuvxsbw',
      });
    </script>
  </div>
</div>

<style>
.about-page {
  background: var(--bg-primary);
}

.about-header {
  text-align: center;
  margin-bottom: 4rem;
}

.about-subtitle {
  font-size: 1.25rem;
  color: var(--text-secondary);
  margin-top: 1rem;
}

.about-section {
  margin-bottom: 4rem;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.feature-card {
  background: var(--card-bg);
  padding: 2rem;
  border-radius: 1rem;
  border: 1px solid var(--border-color);
  text-align: center;
  transition: all 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.feature-card svg {
  color: var(--accent-color);
  margin-bottom: 1rem;
  width: 40px;
  height: 40px;
}

.benefits-list {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 2rem;
}

.benefits-list li {
  padding: 1rem;
  background: var(--card-bg);
  border-radius: 0.5rem;
  border: 1px solid var(--border-color);
}

.contact-section {
  text-align: center;
}

.contact-button {
  display: inline-block;
  padding: 1rem 2rem;
  background: var(--accent-color);
  color: white;
  border-radius: 9999px;
  margin-top: 1rem;
  transition: all 0.3s ease;
}

.contact-button:hover {
  background: var(--accent-hover);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .features-grid {
    grid-template-columns: 1fr;
  }
  
  .benefits-list {
    grid-template-columns: 1fr;
  }
}
</style>
