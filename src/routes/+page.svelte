
<script>
  let welcomeMessage = "Welcome to PCS Reproductive Rights Tracker!";
</script>

<main class="homepage">
  <h1>{welcomeMessage}</h1>
  <p>This is your homepage. Customize it as you like!</p>

  <nav>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
  </nav>
</main>

<style>
.homepage {
  text-align: center;
  padding: 50px;
  background-color: #e5e7eb; /* light gray */
  min-height: 100vh; /* full viewport height */
}

.homepage h1 {
  font-size: 3rem;
  color: #1e40af; /* dark blue */
  margin-bottom: 20px;
}

.homepage p {
  font-size: 1.2rem;
  color: #374151;
  margin-bottom: 30px;
}

.homepage nav a {
  margin: 0 15px;
  font-weight: bold;
}

.homepage nav a:hover {
  color: #2563eb; /* blue hover */
}
</style>

