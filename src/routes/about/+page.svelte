<script>
  let activeSection = 'about';
</script>

<!-- Navigation - Matches your main page -->
<nav class="navbar">
  <div class="nav-container">
    <a href="/" class="logo">
      <img src="/src/lib/assets/pcsLogo.png" alt="PCS Logo" class="nav-logo" />
    </a>
    <div class="nav-links">
      <a href="/">Home</a>
      <a href="/about">About</a>
      <a href="/policy">Policy</a>
    </div>
  </div>
</nav>

<!-- Hero Section with Image - Matches Figma -->
<section class="hero-about">
  <div class="hero-content-wrapper">
    <div class="hero-left">
      <p class="hero-label">Built to Provide</p>
      <h1 class="hero-heading">Simple Accessibility</h1>
      
      <div class="hero-description">
        <p>The Reproductive HeatMap Project aims to provide a clear resource page for various Reproductive Health needs within the Bay Area.</p>
        <p>We hope to provide a one-site solution to finding the best clinic for every need; from std testing to abortions.</p>
      </div>

      <a href="/#map" class="find-resources-btn">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
          <circle cx="12" cy="10" r="3"></circle>
        </svg>
        Find Resources Near You
      </a>
    </div>

    <div class="hero-right">
      <div class="hero-image-container">
        <img src="https://images.unsplash.com/photo-1576091160399-112ba8d25d1d?w=800&auto=format&fit=crop&q=80" alt="Reproductive Health" />
      </div>
    </div>
  </div>
</section>

<!-- Section Navigation Tabs - Sticky like Figma -->
<div class="section-tabs-wrapper">
  <nav class="section-tabs">
    <button 
      class="tab-btn {activeSection === 'about' ? 'active' : ''}"
      on:click={() => activeSection = 'about'}
    >
      About
    </button>
    <button 
      class="tab-btn {activeSection === 'sources' ? 'active' : ''}"
      on:click={() => activeSection = 'sources'}
    >
      Sources
    </button>
    <button 
      class="tab-btn {activeSection === 'history' ? 'active' : ''}"
      on:click={() => activeSection = 'history'}
    >
      History
    </button>
  </nav>
</div>

<!-- Content Sections -->
<div class="content-wrapper">
  
  <!-- About Section (Team) -->
  {#if activeSection === 'about'}
  <section class="about-section">
    <div class="section-header">
      <h2>Our Team</h2>
      <p>Meet the dedicated professionals working to combat food insecurity through innovative technology and data-driven solutions.</p>
    </div>

    <div class="team-grid">
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Smrithi</h3>
        <p>Project Lead</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Abby Kaufman</h3>
        <p>Tech Team</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Asher Lee Nguyen</h3>
        <p>Policy Team</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Charley Gallardo</h3>
        <p>Tech Team</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Haeun Lee</h3>
        <p>Policy Team</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Nkechi Onyejekwe</h3>
        <p>Tech Team</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Sadie Muller</h3>
        <p>Policy Team</p>
      </div>
    </div>
  </section>
  {/if}

  <!-- Sources Section -->
  {#if activeSection === 'sources'}
  <section class="sources-section">
    <div class="section-header">
      <h2>Our Sources</h2>
      <p>We compile data from trusted organizations and institutions to provide accurate and comprehensive reproductive health information.</p>
    </div>

    <div class="sources-grid">
      <div class="source-card">
        <div class="source-header">
          <h3>CDC - Reproductive Health</h3>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
            <polyline points="15 3 21 3 21 9"></polyline>
            <line x1="10" y1="14" x2="21" y2="3"></line>
          </svg>
        </div>
        <p class="source-desc">Centers for Disease Control and Prevention data on reproductive health services and statistics.</p>
        <a href="https://www.cdc.gov/reproductivehealth/" target="_blank" rel="noopener noreferrer" class="source-link">
          Visit source <span>→</span>
        </a>
      </div>

      <div class="source-card">
        <div class="source-header">
          <h3>Planned Parenthood</h3>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
            <polyline points="15 3 21 3 21 9"></polyline>
            <line x1="10" y1="14" x2="21" y2="3"></line>
          </svg>
        </div>
        <p class="source-desc">Comprehensive reproductive health care services and educational resources.</p>
        <a href="https://www.plannedparenthood.org/" target="_blank" rel="noopener noreferrer" class="source-link">
          Visit source <span>→</span>
        </a>
      </div>

      <div class="source-card">
        <div class="source-header">
          <h3>ACOG</h3>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
            <polyline points="15 3 21 3 21 9"></polyline>
            <line x1="10" y1="14" x2="21" y2="3"></line>
          </svg>
        </div>
        <p class="source-desc">American College of Obstetricians and Gynecologists clinical guidelines and resources.</p>
        <a href="https://www.acog.org/" target="_blank" rel="noopener noreferrer" class="source-link">
          Visit source <span>→</span>
        </a>
      </div>

      <div class="source-card">
        <div class="source-header">
          <h3>Bay Area Health Facilities</h3>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
            <polyline points="15 3 21 3 21 9"></polyline>
            <line x1="10" y1="14" x2="21" y2="3"></line>
          </svg>
        </div>
        <p class="source-desc">Local health department directory of reproductive health clinics and services.</p>
        <a href="#" class="source-link">
          Visit source <span>→</span>
        </a>
      </div>

      <div class="source-card">
        <div class="source-header">
          <h3>Title X Family Planning</h3>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
            <polyline points="15 3 21 3 21 9"></polyline>
            <line x1="10" y1="14" x2="21" y2="3"></line>
          </svg>
        </div>
        <p class="source-desc">Federal program providing family planning services to low-income individuals.</p>
        <a href="https://opa.hhs.gov/grant-programs/title-x-service-grants" target="_blank" rel="noopener noreferrer" class="source-link">
          Visit source <span>→</span>
        </a>
      </div>

      <div class="source-card">
        <div class="source-header">
          <h3>National Women's Health Network</h3>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
            <polyline points="15 3 21 3 21 9"></polyline>
            <line x1="10" y1="14" x2="21" y2="3"></line>
          </svg>
        </div>
        <p class="source-desc">Independent health information and advocacy for reproductive health rights.</p>
        <a href="https://nwhn.org/" target="_blank" rel="noopener noreferrer" class="source-link">
          Visit source <span>→</span>
        </a>
      </div>
    </div>
  </section>
  {/if}

  <!-- History Section (Timeline) -->
  {#if activeSection === 'history'}
  <section class="history-section">
    <div class="section-header">
      <h2>History of Reproductive Rights</h2>
      <p>Understanding the evolution of reproductive healthcare and rights in the United States.</p>
    </div>

    <div class="timeline">
      <!-- Timeline Item 1 -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Griswold v. Connecticut</h3>
            <p>Supreme Court rules that married couples have the right to use contraception, establishing privacy rights.</p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">1965</div>
        </div>
      </div>

      <!-- Timeline Item 2 -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-year">1916</div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-card">
            <h3>First Birth Control Clinic</h3>
            <p>Margaret Sanger opens the first birth control clinic in the United States in Brooklyn, New York.</p>
          </div>
        </div>
      </div>

      <!-- Timeline Item 3 -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Title X Established</h3>
            <p>Federal program providing family planning services to low-income individuals.</p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">1970</div>
        </div>
      </div>

      <!-- Timeline Item 4 -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-year">1973</div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-card">
            <h3>Roe v. Wade</h3>
            <p>Supreme Court establishes constitutional right to abortion, legalizing it nationwide.</p>
          </div>
        </div>
      </div>

      <!-- Timeline Item 5 -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Planned Parenthood v. Casey</h3>
            <p>Supreme Court reaffirms abortion rights while allowing some state restrictions.</p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">1992</div>
        </div>
      </div>

      <!-- Timeline Item 6 -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-year">2022</div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-card">
            <h3>Dobbs v. Jackson</h3>
            <p>Supreme Court overturns Roe v. Wade, returning abortion regulation to individual states.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
  {/if}
</div>

<!-- Footer - Exactly matches your main page -->
<footer>
  <div class="footer-content">
    <div class="footer-grid">
      <div class="footer-brand">
        <h3>Berkeley Political Computer Science</h3>
        <p>Dedicated to advancing reproductive rights and healthcare access for all.</p>
        <div class="social-links">
          <a href="https://pcs.studentorg.berkeley.edu/about" aria-label="Instagram" class="social-link">📷</a>
          <a href="#" aria-label="LinkedIn" class="social-link">in</a>
        </div>
      </div>

      <div class="footer-section">
        <h4>About</h4>
        <ul>
          <li><a href="/about">Our Mission</a></li>
          <li><a href="/about">Team</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </div>

      <div class="footer-section">
        <h4>Resources</h4>
        <ul>
          <li><a href="/policy">Policy Information</a></li>
          <li><a href="#">Educational Resources</a></li>
          <li><a href="#">News & Updates</a></li>
        </ul>
      </div>
    </div>

    <div class="footer-bottom">
      <p>&copy; 2024 Berkeley Political Computer Science. All rights reserved.</p>
      <p class="tagline">Empowering informed choices through education and advocacy.</p>
    </div>
  </div>
</footer>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

  * {
    box-sizing: border-box;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: "Montserrat", sans-serif;
    background: #1c0333;
  }

  /* Navbar */
  .navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    backdrop-filter: blur(10px);
    z-index: 100;
    background: transparent;
  }

  .nav-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0;
  }

  .logo {
    display: flex;
    align-items: center;
    text-decoration: none;
  }

  .nav-logo {
    height: 70px;
    width: auto;
  }

  .nav-links {
    display: flex;
    gap: 30px;
    padding-right: 40px;
  }

  .nav-links a {
    color: #e0d5f0;
    text-decoration: none;
    font-weight: 500;
    font-size: 16px;
  }

  .nav-links a:hover {
    color: #b39ddb;
  }

  /* Hero Section */
  .hero-about {
    padding: 120px 60px 80px;
    background: #1c0333;
  }

  .hero-content-wrapper {
    max-width: 1300px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 100px;
    align-items: center;
  }

  .hero-label {
    font-size: 18px;
    color: #e0d5f0;
    margin: 0 0 8px 0;
    font-weight: 300;
  }

  .hero-heading {
    font-family: "Montserrat", sans-serif;
    font-size: 28px;
    color: #e0d5f0;
    margin: 0 0 40px 0;
    font-weight: 300;
  }

  .hero-description p {
    color: white;
    font-size: 16px;
    line-height: 1.8;
    margin: 0 0 20px 0;
    font-weight: 300;
  }

  .find-resources-btn {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    background: #c5b3e6;
    color: #1c0333;
    padding: 14px 28px;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 500;
    font-size: 15px;
    margin-top: 20px;
  }

  .hero-image-container {
    border-radius: 24px;
    overflow: hidden;
    background: linear-gradient(135deg, #ffd95a 0%, #ffb84d 40%, #ff9a76 70%, #f48fb1 100%);
    padding: 32px;
  }

  .hero-image-container img {
    width: 100%;
    border-radius: 16px;
  }

  /* Tab Navigation */
  .section-tabs-wrapper {
    position: sticky;
    top: 70px;
    background: rgba(28, 3, 51, 0.98);
    backdrop-filter: blur(10px);
    z-index: 90;
    border-top: 1px solid rgba(197, 179, 230, 0.15);
    border-bottom: 1px solid rgba(197, 179, 230, 0.15);
  }

  .section-tabs {
    max-width: 600px;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    gap: 50px;
    padding: 24px 20px;
  }

  .tab-btn {
    background: none;
    border: none;
    color: #9585a9;
    font-size: 17px;
    font-family: "Montserrat", sans-serif;
    font-weight: 400;
    cursor: pointer;
    padding: 8px 4px;
    position: relative;
  }

  .tab-btn.active {
    color: white;
  }

  .tab-btn.active::after {
    content: '';
    position: absolute;
    bottom: -24px;
    left: 0;
    right: 0;
    height: 2px;
    background: white;
  }

  /* Content */
  .content-wrapper {
    background: #1c0333;
    min-height: 60vh;
    padding: 80px 60px;
  }

  .section-header {
    text-align: center;
    max-width: 900px;
    margin: 0 auto 70px;
  }

  .section-header h2 {
    font-family: "Montserrat", sans-serif;
    font-size: 36px;
    color: white;
    margin: 0 0 16px 0;
    font-weight: 400;
  }

  .section-header p {
    color: white;
    font-size: 16px;
    line-height: 1.7;
    font-weight: 300;
  }

  /* Team Grid */
  .team-grid {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
  }

  .team-member {
    background: rgba(45, 27, 78, 0.4);
    border: 1px solid rgba(197, 179, 230, 0.2);
    border-radius: 12px;
    padding: 40px 24px;
    text-align: center;
  }

  .member-avatar {
    width: 90px;
    height: 90px;
    border-radius: 50%;
    background: rgba(197, 179, 230, 0.5);
    margin: 0 auto 16px;
  }

  .team-member h3 {
    font-family: "Montserrat", sans-serif;
    font-size: 18px;
    color: white;
    margin: 0 0 6px 0;
    font-weight: 500;
  }

  .team-member p {
    color: #e0d5f0;
    font-size: 13px;
    font-weight: 300;
  }

  /* Sources Grid */
  .sources-grid {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
  }

  .source-card {
    background: rgba(45, 27, 78, 0.4);
    border: 1px solid rgba(197, 179, 230, 0.2);
    border-radius: 12px;
    padding: 28px;
  }

  .source-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 14px;
  }

  .source-header h3 {
    font-family: "Montserrat", sans-serif;
    font-size: 18px;
    color: white;
    margin: 0;
    font-weight: 600;
  }

  .source-header svg {
    color: #e0d5f0;
  }

  .source-desc {
    color: white;
    line-height: 1.6;
    margin: 0 0 18px 0;
    font-size: 14px;
    font-weight: 300;
  }

  .source-link {
    color: #e0d5f0;
    text-decoration: none;
    font-size: 14px;
  }

  /* Timeline */
  .timeline {
    max-width: 900px;
    margin: 0 auto;
  }

  .timeline-row {
    display: grid;
    grid-template-columns: 1fr 80px 1fr;
    gap: 30px;
    margin-bottom: 50px;
    align-items: center;
  }

  .timeline-center {
    display: flex;
    justify-content: center;
    position: relative;
    height: 100%;
  }

  .timeline-center::before {
    content: '';
    position: absolute;
    top: 0;
    bottom: -50px;
    left: 50%;
    transform: translateX(-50%);
    width: 2px;
    background: rgba(197, 179, 230, 0.3);
  }

  .timeline-dot {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: #b39ddb;
    border: 3px solid #1c0333;
    z-index: 1;
  }

  .timeline-left {
    display: flex;
    justify-content: flex-end;
  }

  .timeline-right {
    display: flex;
    justify-content: flex-start;
  }

  .timeline-card {
    background: rgba(45, 27, 78, 0.4);
    border: 1px solid rgba(197, 179, 230, 0.2);
    border-radius: 12px;
    padding: 20px;
    max-width: 380px;
  }

  .timeline-card h3 {
    font-family: "Montserrat", sans-serif;
    font-size: 20px;
    color: white;
    margin: 0 0 10px 0;
    font-weight: 600;
  }

  .timeline-card p {
    color: white;
    line-height: 1.6;
    margin: 0;
    font-size: 14px;
    font-weight: 300;
  }

  .timeline-year {
    background: rgba(124, 95, 160, 0.3);
    border: 1px solid rgba(197, 179, 230, 0.3);
    border-radius: 10px;
    padding: 10px 20px;
    color: #e0d5f0;
    font-size: 20px;
    font-family: "Montserrat", sans-serif;
    font-weight: 400;
    text-align: center;
  }

  /* Footer */
  footer {
    background: linear-gradient(135deg, #2d1b4e 0%, #1a0f2e 100%);
    color: #e0d5f0;
    padding: 60px 20px 30px;
  }

  .footer-content {
    max-width: 1200px;
    margin: 0 auto;
  }

  .footer-grid {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    gap: 40px;
    margin-bottom: 40px;
  }

  .footer-brand h3 {
    color: #ffffff;
    font-size: 1.5rem;
    margin: 0 0 16px 0;
    font-weight: 700;
  }

  .footer-brand p {
    color: #d0c4e5;
    line-height: 1.6;
    margin: 0 0 24px 0;
    max-width: 300px;
  }

  .social-links {
    display: flex;
    gap: 12px;
  }

  .social-link {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    background: rgba(124, 95, 160, 0.3);
    border: 1px solid rgba(124, 95, 160, 0.5);
    border-radius: 8px;
    color: #e0d5f0;
    text-decoration: none;
    font-size: 1.2rem;
    transition: all 0.3s ease;
  }

  .social-link:hover {
    background: rgba(149, 117, 205, 0.4);
    border-color: #9575cd;
    transform: translateY(-2px);
  }

  .footer-section h4 {
    color: #ffffff;
    font-size: 1.1rem;
    margin: 0 0 20px 0;
    font-weight: 600;
  }

  .footer-section ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .footer-section li {
    margin-bottom: 12px;
  }

  .footer-section a {
    color: #d0c4e5;
    text-decoration: none;
    transition: color 0.3s ease;
    font-size: 0.95rem;
  }

  .footer-section a:hover {
    color: #b39ddb;
  }

  .footer-bottom {
    padding-top: 30px;
    border-top: 1px solid rgba(124, 95, 160, 0.3);
    text-align: center;
  }

  .footer-bottom p {
    margin: 8px 0;
    color: #b5a5c9;
    font-size: 0.9rem;
  }

  .tagline {
    font-style: italic;
    color: #9585a9;
  }

  /* Responsive */
  @media (max-width: 1024px) {
    .hero-content-wrapper {
      grid-template-columns: 1fr;
      gap: 50px;
    }

    .team-grid {
      grid-template-columns: repeat(3, 1fr);
    }

    .sources-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 768px) {
    .hero-about {
      padding: 100px 30px 60px;
    }

    .content-wrapper {
      padding: 60px 30px;
    }

    .section-tabs {
      gap: 30px;
    }

    .team-grid {
      grid-template-columns: repeat(2, 1fr);
    }

    .sources-grid {
      grid-template-columns: 1fr;
    }

    .timeline-row {
      grid-template-columns: 1fr;
      gap: 15px;
    }

    .timeline-center {
      display: none;
    }

    .timeline-left,
    .timeline-right {
      justify-content: flex-start !important;
    }

    .footer-grid {
      grid-template-columns: 1fr;
    }
  }
</style>