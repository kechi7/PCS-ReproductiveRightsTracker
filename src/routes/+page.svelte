
<script>
//  let welcomeMessage = "Welcome to PCS Reproductive Rights Tracker!";
</script>

<!-- Navigation -->
<!-- This is all the information for the nav bar. In HTML so this is where you can change the text in the navBar, add images, etc. -->
<nav class="navbar">
  <div class="nav-container">
    <a href="/" class="logo">PCS Tracker</a>
    <div class="nav-links">
      <a href="/about">About</a>
      <a href="/contact">Contact</a>
    </div>
  </div>
</nav>

<!-- Hero Section (Title and GIF ) -->
<section class="hero">
  <img src="https://media.giphy.com/media/HzMfJIkTZgx8s/giphy.gif" alt="Background GIF" class="hero-gif" />
  <div class="hero-text">
    <h1>Welcome to PCS Reproductive Rights Tracker!</h1>
    <p>Track reproductive rights data and resources effectively.</p>
  </div>
</section>

<!-- In the style section this is where all the CSS for this page is stored  -->
 <!-- This is where you can change the appearance for the webpage if it isnt hard coded in the HTML section -->
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
}

.nav-links a:hover {
  text-decoration: underline;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
}

/* Hero Section */
.hero {
  position: relative;
  margin-top: 70px; /* space below navbar */
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
  max-width: 80%;       /* prevents text from stretching too wide */
  padding: 0 20px;      /* adds horizontal breathing room */
}

.hero-text h1 {
  font-size: 3rem;
  line-height: 1.2;     /* adds spacing between lines */
  margin-bottom: 20px;
}

.hero-text p {
  font-size: 1.5rem;
  line-height: 1.5;     /* more readable paragraph spacing */
}

</style>

