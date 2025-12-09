<script>
  import ClinicMap from '../ClinicMap.svelte';
</script>

<!-- Navigation -->
<nav class="navbar">
  <div class="nav-container">
    <a href="/" class="logo">
      <img src="src/lib/assets/pcsLogo.png" alt="PCS Logo" class="nav-logo" />
    </a>
    <div class="nav-links">
      <a href="#map">Clinic Map</a>
      <a href="src/routes/about/+page.svelte">About</a>
      <a href="src/routes/policy/+page.svelte">Policy</a>
    </div>
  </div>
</nav>

<!-- Hero Section (Title and GIF) -->
<section class="hero">
  <div class = "heroGif1">
    <img src="https://datax.berkeley.edu/wp-content/uploads/2021/04/recording1.gif" alt="Background GIF" class="hero-gif" />
  </div>
  
  <div class="hero-text">
    <!-- <img src= "src/lib/assets/pcsLogo.png" /> -->
    <h1 class = "headerTitle">Welcome to PCS Reproductive Rights Tracker!</h1>
    <!-- <p>Track reproductive rights data and resources effectively.</p> -->
  </div>
</section>

<!-- Map Section -->
<section id="map" class="map-section">
  <div class="map-container">
    <h2>Find Reproductive Health Clinics</h2>
    <p class="map-description">Explore clinics offering reproductive health services in your area. Click on markers to view services, payment information, and contact details.</p>
    <ClinicMap />
  </div>
</section>

  <!-- Footer -->
  <footer>
    <div class="footer-content">
      <div class="footer-grid">
        <!-- Brand Section -->
        <div class="footer-brand">
          <h3>Your Organization</h3>
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
            <li><a href="/about/team">Team</a></li>
            <li><a href="/careers">Careers</a></li>
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

        <!-- Legal Links -->
    
      </div>

      <!-- Bottom Bar -->
      <div class="footer-bottom">
        <p>&copy; <span id="year"></span> Berkeley Political Computer Science. All rights reserved.</p>
        <p class="tagline">Empowering informed choices through education and advocacy.</p>
      </div>
    </div>
  </footer>

<style> 

@import url('https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

.heroGif1{
   background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5));

}
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  /* background: rgba(20, 10, 35, 0.7); Darker purple */
  backdrop-filter: blur(10px);
  z-index: 10;
  /* border-bottom: 1px solid rgba(124, 95, 160, 0.2) */
}

.nav-container {
  max-width: 1200px;
  /* margin: 0 auto; */
  /* padding: 16px 20px; */
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
  height: 70px; /* Adjust this to your desired size */
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

.logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
  text-decoration: none;
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
  color : white;
  font-size: 50px;
}


.hero-text p {
  font-size: 1.5rem;
  line-height: 1.5;
}

/* .headerTitle{
  color : white;
  font-size: 12px;

} */

/* Map Section */
.map-section {
  padding: 60px 20px;
  background: #1c0333;
  min-height: 100vh;
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
}

.map-container {
  max-width: 1400px;
  margin: 0 auto;
}

.map-container h2 {
  font-size: 2.5rem;
  color: white;
  margin-bottom: 15px;
  text-align: center;
}

.map-description {
  font-size: 1.1rem;
  color: white;
  text-align: center;
  margin-bottom: 30px;
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.6;
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
      grid-template-columns: 2fr 1fr 1fr 1fr;
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

    @media (max-width: 968px) {
      .footer-grid {
        grid-template-columns: 1fr 1fr;
        gap: 30px;
      }

      .footer-brand {
        grid-column: 1 / -1;
      }
    }

    @media (max-width: 640px) {
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



/* Smooth scrolling */
/* html {
  scroll-behavior: smooth;
} */
</style>

