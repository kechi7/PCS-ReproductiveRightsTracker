<script>
  import { onMount } from 'svelte';
  
  onMount(() => {
    document.getElementById('year').textContent = new Date().getFullYear();
  });
</script>

<!-- Navigation -->
<nav class="navbar">
  <div class="nav-container">
    <a href="/" class="logo">
      <img src="/src/lib/assets/pcsLogo.png" alt="PCS Logo" class="nav-logo" />
    </a>
    <div class="nav-links">
      <a href="/#map">Clinic Map</a>
      <a href="/about">About</a>
      <a href="/policy">Policy</a>
    </div>
  </div>
</nav>

<!-- Hero Section -->
<section class="hero">
  <div class="heroGif1">
    <img src="https://images.unsplash.com/photo-1576091160399-112ba8d25d1d?w=1200&auto=format&fit=crop&q=80" alt="Background" class="hero-gif" />
  </div>
  
  <div class="hero-text">
    <h1 class="headerTitle">About Our Mission</h1>
    <p>Dedicated to advancing reproductive rights and healthcare access for all.</p>
  </div>
</section>

<!-- Mission Section -->
<section class="mission-section">
  <div class="mission-container">
    <div class="mission-content">
      <p class="mission-label">Built to Provide</p>
      <h2>Simple Accessibility</h2>
      
      <div class="mission-description">
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
  </div>
</section>

<!-- Team Section -->
<section id="team" class="team-section">
  <div class="team-container">
    <h2>Our Team</h2>
    <p class="team-description">Meet the dedicated professionals working to advance reproductive rights through innovative technology and data-driven solutions.</p>
    
    <div class="team-grid">
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Smrithi Senthilnathan</h3>
        <p>Project Lead</p>
      </div>
      <div class="team-member">
        <div class="member-avatar"></div>
        <h3>Abby Kaufman</h3>
        <p>Project Lead</p>
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
        <p>Tech Team</p>
      </div>
    </div>
  </div>
</section>

<!-- Footer -->
<footer>
  <div class="footer-content">
    <div class="footer-grid">
      <!-- Brand Section -->
      <div class="footer-brand">
        <h3>Reproductive Rights Tracker</h3>
        <p>Dedicated to advancing reproductive rights and healthcare access for all.</p>
        <div class="social-links">
          <a href="https://pcs.studentorg.berkeley.edu/about" aria-label="Instagram" class="social-link">📷</a>
          <a href="#" aria-label="LinkedIn" class="social-link">in</a>
        </div>
      </div>

      <!-- About Links -->
      <div class="footer-section">
        <h4>About</h4>
        <ul>
          <li><a href="/about">Our Mission</a></li>
          <li><a href="/about#team">Team</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </div>

      <!-- Resources Links -->
      <div class="footer-section">
        <h4>Resources</h4>
        <ul>
          <li><a href="/policy">Policy Information</a></li>
          <li><a href="/resources">Educational Resources</a></li>
          <li><a href="/news">News & Updates</a></li>
          <li><a href="/faq">FAQ</a></li>
        </ul>
      </div>
    </div>

    <!-- Bottom Bar -->
    <div class="footer-bottom">
      <p>&copy; <span id="year"></span> Political Computer Science @ Berkeley. All rights reserved.</p>
      <p class="tagline">Empowering informed choices through education and advocacy.</p>
    </div>
  </div>
</footer>

<style>
@import url('https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:global(body) {
  margin: 0;
  padding: 0;
  font-family: "Montserrat", sans-serif;
  background: #1c0333;
}


.heroGif1 {
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5));
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  backdrop-filter: blur(10px);
  z-index: 10;
}

.nav-container {
  max-width: 1200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  text-decoration: none;
}

.nav-logo {
  height: 70px;
  width: auto;
  display: block;
}

.nav-links {
  display: flex;
  gap: 30px;
  align-items: center;
}

.nav-links a {
  color: #e0d5f0;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: #b39ddb;
}

/* Hero Section */
.hero {
  position: relative;
  text-align: center;
  color: white;
  overflow: hidden;
}

.hero-gif {
  width: 100%;
  height: 80vh;
  object-fit: cover;
  filter: brightness(35%);
}

.hero-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 80%;
  padding: 0 20px;
}

.hero-text h1 {
  line-height: 1.2;
  margin-bottom: 20px;
  color: white;
  font-size: 50px;
}

.hero-text p {
  font-size: 1.5rem;
  line-height: 1.5;
}

/* Mission Section */
.mission-section {
  padding: 80px 60px;
  background: #1c0333;
}

.mission-container {
  max-width: 1200px;
  margin: 0 auto;
}

.mission-content {
  max-width: 700px;
  margin: 0 auto;
  text-align: center;
}

.mission-label {
  font-size: 18px;
  color: #e0d5f0;
  margin: 0 0 8px 0;
  font-weight: 300;
}

.mission-content h2 {
  font-size: 2.5rem;
  color: white;
  margin-bottom: 30px;
  font-weight: 400;
}

.mission-description p {
  color: white;
  font-size: 1.1rem;
  line-height: 1.8;
  margin-bottom: 20px;
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
  transition: all 0.3s ease;
}

.find-resources-btn:hover {
  background: #b39ddb;
  transform: translateY(-2px);
}

/* Team Section */
.team-section {
  padding: 80px 60px;
  background: #1c0333;
  min-height: 60vh;
}

.team-container {
  max-width: 1200px;
  margin: 0 auto;
}

.team-container h2 {
  font-size: 2.5rem;
  color: white;
  margin-bottom: 15px;
  text-align: center;
}

.team-description {
  font-size: 1.1rem;
  color: white;
  text-align: center;
  margin-bottom: 50px;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.6;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 30px;
  margin-top: 50px;
}

.team-member {
  background: rgba(45, 27, 78, 0.4);
  border: 1px solid rgba(197, 179, 230, 0.2);
  border-radius: 12px;
  padding: 40px 24px;
  text-align: center;
  transition: all 0.3s ease;
}

.team-member:hover {
  background: rgba(45, 27, 78, 0.6);
  border-color: rgba(197, 179, 230, 0.4);
  transform: translateY(-5px);
}

.member-avatar {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  background: rgba(197, 179, 230, 0.5);
  margin: 0 auto 16px;
}

.team-member h3 {
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

/* Footer Styles */
footer {
  background: linear-gradient(135deg, #2d1b4e 0%, #1a0f2e 100%);
  color: #e0d5f0;
  padding: 60px 20px 30px;
  margin-top: auto;
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

/* Responsive Design */
@media (max-width: 968px) {
  .team-grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .footer-grid {
    grid-template-columns: 1fr 1fr;
    gap: 30px;
  }

  .footer-brand {
    grid-column: 1 / -1;
  }
}

@media (max-width: 640px) {
  .hero-text h1 {
    font-size: 36px;
  }

  .mission-section,
  .team-section {
    padding: 60px 20px;
  }

  .team-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  footer {
    padding: 40px 20px 20px;
  }

  .footer-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .footer-brand p {
    max-width: 100%;
  }
}
</style>