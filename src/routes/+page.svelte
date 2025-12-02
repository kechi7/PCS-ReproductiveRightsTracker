<script>
  import ClinicMap from '../ClinicMap.svelte';
</script>

<!-- Navigation -->
<nav class="navbar">
  <div class="nav-container">
    <a href="/" class="logo">PCS Tracker</a>
    <div class="nav-links">
      <a href="#map">Clinic Map</a>
      <a href="src/routes/about/+page.svelte">About</a>
      <a href="src/routes/policy/+page.svelte">Policy</a>
    </div>
  </div>
</nav>

<!-- Hero Section (Title and GIF) -->
<section class="hero">
  <img src="https://media.giphy.com/media/HzMfJIkTZgx8s/giphy.gif" alt="Background GIF" class="hero-gif" />
  <div class="hero-text">
    <h1>Welcome to PCS Reproductive Rights Tracker!</h1>
    <p>Track reproductive rights data and resources effectively.</p>
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

<style> 
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background-color: rgba(30, 64, 175, 0.9);
  color: white;
  z-index: 1000;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 20px;
}

.nav-links a {
  margin-left: 20px;
  color: white;
  text-decoration: none;
  font-weight: bold;
  transition: all 0.3s ease;
}

.nav-links a:hover {
  text-decoration: underline;
  color: #ddd;
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
  filter: brightness(50%);
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
  font-size: 3rem;
  line-height: 1.2;
  margin-bottom: 20px;
}

.hero-text p {
  font-size: 1.5rem;
  line-height: 1.5;
}

/* Map Section */
.map-section {
  padding: 60px 20px;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  min-height: 100vh;
}

.map-container {
  max-width: 1400px;
  margin: 0 auto;
}

.map-container h2 {
  font-size: 2.5rem;
  color: #1e40af;
  margin-bottom: 15px;
  text-align: center;
}

.map-description {
  font-size: 1.1rem;
  color: #4b5563;
  text-align: center;
  margin-bottom: 30px;
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.6;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}
</style>