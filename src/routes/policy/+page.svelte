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
    <img src="https://images.unsplash.com/photo-1589829545856-d10d557cf95f?w=1200&auto=format&fit=crop&q=80" alt="Policy Background" class="hero-gif" />
  </div>
  
  <div class="hero-text">
    <h1 class="headerTitle">Policy & Legal Information</h1>
    <p>Understanding reproductive rights through landmark cases and current legislation.</p>
  </div>
</section>

<!-- Court Cases Timeline Section -->
<section class="timeline-section">
  <div class="timeline-container">
    <h2>Landmark Supreme Court Cases</h2>
    <p class="section-description">Key federal court decisions that have shaped reproductive rights in America.</p>
    
    <div class="timeline">
      <!-- Griswold v. Connecticut -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Griswold v. Connecticut</h3>
            <p class="case-date">Argued: March 29, 1965 | Decided: June 7, 1965</p>
            <p>The Court ruled that a Connecticut law banning the use of contraceptives, even by married couples, was unconstitutional. The Court held that the law violated the right to marital privacy, which is implied by the “penumbras” and “emanations” of several guarantees in the Bill of Rights—specifically the First, Third, Fourth, Fifth, and Ninth Amendments. This case established the constitutional right to privacy in marital relations and laid the groundwork for later decisions involving reproductive freedom, including <i>Roe v. Wade.</i></p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">1965</div>
        </div>
      </div>

      <!-- Eisenstadt v. Baird -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-year">1972</div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-card">
            <h3>Eisenstadt v. Baird</h3>
            <p class="case-date">Argued: November 17, 1971 | Decided: March 22, 1972</p>
            <p>The Court ruled that a Massachusetts law prohibiting the distribution of contraceptives to unmarried individuals was unconstitutional. Extending Griswold, the Court recognized that the right to privacy includes an individual's decision whether to bear or beget a child, regardless of marital status.</p>
          </div>
        </div>
      </div>

      <!-- Roe v. Wade -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Roe v. Wade</h3>
            <p class="case-date">Argued: December 13, 1971 | Decided: January 22, 1973</p>
            <p>The court ruled that a person may choose to have an abortion until a fetus becomes viable, based on the right to privacy contained in the Due Process Clause of the Fourteenth Amendment. Viability means the ability to live outside the womb, which usually happens between 24 and 28 weeks after conception. This case recognized a constitutionally protected right to abortion. </p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot highlight"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">1973</div>
        </div>
      </div>

      <!-- Doe v. Bolton -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-year">1973</div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-card">
            <h3>Doe v. Bolton</h3>
            <p class="case-date">Argued: December 13, 1971 | Decided: January 22, 1973</p>
            <p>The Court ruled that Georgia’s restrictive abortion law was unconstitutional because it placed undue procedural barriers on a woman’s right to obtain an abortion. The Court held that the right to privacy, protected by the Due Process Clause of the Fourteenth Amendment, extends to a woman’s decision to have an abortion. It struck down requirements such as the need for approval from multiple physicians and a hospital committee, as well as residency restrictions, finding that these imposed unnecessary burdens and infringed upon the physician–patient relationship. This was a companion case of Roe v. Wade. </p>
          </div>
        </div>
      </div>

      <!-- Planned Parenthood v. Casey -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Planned Parenthood v. Casey</h3>
            <p class="case-date">Argued: April 22, 1992 | Decided: June 29, 1992</p>
            <p>The Court reaffirmed the essential holding of Roe v. Wade but replaced the trimester framework with the "undue burden standard," holding that states may regulate abortions before viability as long as regulations don't place substantial obstacles in a woman's path.</p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">1992</div>
        </div>
      </div>

      <!-- Gonzalez v. Carhart -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-year">2007</div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-card">
            <h3>Gonzalez v. Carhart</h3>
            <p class="case-date">Argued: November 8, 2006 | Decided: April 18, 2007</p>
            <p>The Court ruled that the federal Partial-Birth Abortion Ban Act of 2003 was constitutional, marking the first time since Roe v. Wade that the Court upheld a federal restriction on abortion procedures.</p>
          </div>
        </div>
      </div>

      <!-- Dobbs v. Jackson -->
      <div class="timeline-row">
        <div class="timeline-left">
          <div class="timeline-card">
            <h3>Dobbs v. Jackson Women's Health Organization</h3>
            <p class="case-date">Argued: December 1, 2021 | Decided: June 24, 2022</p>
            <p>The Court ruled that the Constitution does not confer a right to abortion, overturning Roe v. Wade and Planned Parenthood v. Casey. The Court held that the authority to regulate abortion belongs to the states and their elected representatives.</p>
          </div>
        </div>
        <div class="timeline-center">
          <div class="timeline-dot highlight"></div>
        </div>
        <div class="timeline-right">
          <div class="timeline-year">2022</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- California Policies Section -->
<section class="policies-section">
  <div class="policies-container">
    <h2>California Legislation</h2>
    <p class="section-description">Current and proposed laws protecting reproductive rights in California.</p>
    
    <div class="policies-grid">
      <!-- AB 260 -->
      <div class="policy-card">
        <div class="policy-header">
          <h3>AB 260: Sexual and Reproductive Health Care</h3>
          <span class="policy-badge">2025-2026 Session</span>
        </div>
        <div class="policy-body">
          <p>This bill protects against unconstitutional criminal punishment for receiving an abortion without parental consent, assisting in, or advertising for abortion. Key provisions include:</p>
          <ul>
            <li>Authorizes pharmacists to prescribe abortion medications without disclosing patient information</li>
            <li>Requires pharmacists to keep confidential logs not subject to law enforcement inspection without subpoena</li>
            <li>Prohibits criminal, civil, or professional discipline against licensed clinics for transporting or engaging in acts relating to mifepristone or medication abortion drugs lawful in California</li>
          </ul>
          <a href="https://calmatters.digitaldemocracy.org/bills/ca_202520260ab260" target="_blank" rel="noopener noreferrer" class="policy-link">
            Read Full Bill <span>→</span>
          </a>
        </div>
      </div>

      <!-- AB 1525 -->
      <div class="policy-card">
        <div class="policy-header">
          <h3>AB 1525: Attorneys: Discipline: Sensitive Services</h3>
          <span class="policy-badge">2025 Session</span>
        </div>
        <div class="policy-body">
          <p>This bill protects attorneys from disciplinary action for providing legal services related to reproductive healthcare. Key provisions include:</p>
          <ul>
            <li>Defines "excluded events" that cannot be grounds for disciplinary action</li>
            <li>Protects attorneys who provide, recommend, or advocate for sensitive services lawful in California</li>
            <li>Prevents State Bar from requiring reporting of excluded events</li>
            <li>Ensures actions based on another state's law that interferes with reproductive rights don't affect California licensure</li>
          </ul>
        </div>
      </div>

      <!-- Family PACT -->
      <div class="policy-card">
        <div class="policy-header">
          <h3>Family PACT Program</h3>
          <span class="policy-badge active">Active Program</span>
        </div>
        <div class="policy-body">
          <p>California's Family Planning, Access, Care, and Treatment (Family PACT) program provides comprehensive family planning services to eligible individuals.</p>
          <ul>
            <li>Provides free or low-cost family planning services</li>
            <li>Covers contraception, counseling, and reproductive health screenings</li>
            <li>Available to eligible California residents</li>
            <li>No immigration status requirements</li>
          </ul>
          <a href="https://familypact.org" target="_blank" rel="noopener noreferrer" class="policy-link">
            Visit Program Website <span>→</span>
          </a>
        </div>
      </div>

      <!-- Equity in Birth Control Act -->
      <div class="policy-card">
        <div class="policy-header">
          <h3>Equity in Birth Control Act</h3>
          <span class="policy-badge active">Active Legislation</span>
        </div>
        <div class="policy-body">
          <p>Legislation aimed at improving access to contraception and ensuring equity in birth control availability across California.</p>
          <ul>
            <li>Expands access to over-the-counter contraception</li>
            <li>Addresses barriers to contraceptive access</li>
            <li>Focuses on equity for underserved communities</li>
            <li>Supports insurance coverage for comprehensive contraceptive care</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Resources Section -->
<section class="resources-section">
  <div class="resources-container">
    <h2>Resources & Services</h2>
    <p class="section-description">Organizations and services providing reproductive healthcare and support in California.</p>
    
    <!-- Abortion Care -->
    <div class="resource-category">
      <h3 class="category-title">Abortion Care Services</h3>
      <div class="resources-grid">
        <div class="resource-card">
          <h4>UCSF Center for Pregnancy Options</h4>
          <p>Comprehensive abortion care and family planning services</p>
          <a href="https://www.ucsfhealth.org/clinics/center-for-pregnancy-options" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>AbortionFinder</h4>
          <p>Abortion provider search, funding assistance, and support resources</p>
          <a href="https://www.abortionfinder.org" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>Carafem</h4>
          <p>Abortion care, abortion pill delivery, missed period pill services</p>
          <a href="https://carafem.org" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>Abortion on Demand</h4>
          <p>Telehealth abortion care services</p>
          <a href="https://abortionondemand.org" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>HeyJane</h4>
          <p>Telehealth care and discreet abortion pill delivery</p>
          <a href="https://www.heyjane.com" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
      </div>
    </div>

    <!-- Mental Health Support -->
    <div class="resource-category">
      <h3 class="category-title">Mental Health Support</h3>
      <div class="resources-grid">
        <div class="resource-card">
          <h4>Exhale Pro-Voice</h4>
          <p>Confidential text line for emotional support after abortion</p>
          <a href="https://exhaleprovoice.org" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>All-Options Talkline</h4>
          <p>Free, confidential talkline for pregnancy, parenting, abortion, and adoption support</p>
          <a href="https://www.all-options.org/find-support/talkline/" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
      </div>
    </div>

    <!-- Additional Resources -->
    <div class="resource-category">
      <h3 class="category-title">Additional Resources</h3>
      <div class="resources-grid">
        <div class="resource-card">
          <h4>California Abortion Finder</h4>
          <p>Official State of California abortion provider finder tool</p>
          <a href="https://www.cdph.ca.gov/Programs/OHE/abortion/Pages/find-a-provider.aspx" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>HER Smart Choice</h4>
          <p>Discreet abortion pill delivery and online care</p>
          <a href="https://hersmartchoice.com" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
        
        <div class="resource-card">
          <h4>PLAN C</h4>
          <p>Information resource for abortion pills and surgical abortion</p>
          <a href="https://www.plancpills.org" target="_blank" rel="noopener noreferrer">Visit Website →</a>
        </div>
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

/* Timeline Section */
.timeline-section {
  padding: 80px 60px;
  background: #1c0333;
  min-height: 60vh;
}

.timeline-container {
  max-width: 1100px;
  margin: 0 auto;
}

.timeline-container h2 {
  font-size: 2.5rem;
  color: white;
  margin-bottom: 15px;
  text-align: center;
}

.section-description {
  font-size: 1.1rem;
  color: white;
  text-align: center;
  margin-bottom: 60px;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.6;
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

.timeline-row:last-child .timeline-center::before {
  display: none;
}

.timeline-dot {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: #b39ddb;
  border: 3px solid #1c0333;
  z-index: 1;
}

.timeline-dot.highlight {
  width: 18px;
  height: 18px;
  background: #c5b3e6;
  box-shadow: 0 0 15px rgba(197, 179, 230, 0.5);
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
  padding: 24px;
  max-width: 380px;
  transition: all 0.3s ease;
}

.timeline-card:hover {
  background: rgba(45, 27, 78, 0.6);
  border-color: rgba(197, 179, 230, 0.4);
  transform: translateY(-3px);
}

.timeline-card h3 {
  font-size: 20px;
  color: white;
  margin: 0 0 8px 0;
  font-weight: 600;
}

.case-date {
  color: #e0d5f0;
  font-size: 12px;
  margin-bottom: 12px;
  font-style: italic;
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
  font-weight: 400;
  text-align: center;
}

/* Policies Section */
.policies-section {
  padding: 80px 60px;
  background: #1c0333;
}

.policies-container {
  max-width: 1200px;
  margin: 0 auto;
}

.policies-container h2 {
  font-size: 2.5rem;
  color: white;
  margin-bottom: 15px;
  text-align: center;
}

.policies-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
  margin-top: 50px;
}

.policy-card {
  background: rgba(45, 27, 78, 0.4);
  border: 1px solid rgba(197, 179, 230, 0.2);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.3s ease;
}

.policy-card:hover {
  background: rgba(45, 27, 78, 0.6);
  border-color: rgba(197, 179, 230, 0.4);
  transform: translateY(-3px);
}

.policy-header {
  padding: 24px 24px 16px;
  border-bottom: 1px solid rgba(197, 179, 230, 0.15);
}

.policy-header h3 {
  font-size: 20px;
  color: white;
  margin: 0 0 12px 0;
  font-weight: 600;
}

.policy-badge {
  display: inline-block;
  padding: 4px 12px;
  background: rgba(197, 179, 230, 0.2);
  border: 1px solid rgba(197, 179, 230, 0.3);
  border-radius: 12px;
  color: #e0d5f0;
  font-size: 12px;
  font-weight: 500;
}

.policy-badge.active {
  background: rgba(139, 195, 74, 0.2);
  border-color: rgba(139, 195, 74, 0.4);
  color: #a5d6a7;
}

.policy-body {
  padding: 24px;
}

.policy-body p {
  color: white;
  line-height: 1.7;
  margin-bottom: 16px;
  font-size: 14px;
  font-weight: 300;
}

.policy-body ul {
  margin: 16px 0;
  padding-left: 20px;
}

.policy-body li {
  color: white;
  line-height: 1.7;
  margin-bottom: 10px;
  font-size: 14px;
  font-weight: 300;
}

.policy-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  color: #c5b3e6;
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  margin-top: 12px;
  transition: color 0.3s ease;
}

.policy-link:hover {
  color: #b39ddb;
}

/* Resources Section */
.resources-section {
  padding: 80px 60px;
  background: #1c0333;
}

.resources-container {
  max-width: 1200px;
  margin: 0 auto;
}

.resources-container h2 {
  font-size: 2.5rem;
  color: white;
  margin-bottom: 15px;
  text-align: center;
}

.resource-category {
  margin-top: 60px;
}

.category-title {
  font-size: 1.8rem;
  color: #e0d5f0;
  margin-bottom: 30px;
  padding-bottom: 12px;
  border-bottom: 2px solid rgba(197, 179, 230, 0.2);
}

.resources-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.resource-card {
  background: rgba(45, 27, 78, 0.4);
  border: 1px solid rgba(197, 179, 230, 0.2);
  border-radius: 12px;
  padding: 24px;
  transition: all 0.3s ease;
}

.resource-card:hover {
  background: rgba(45, 27, 78, 0.6);
  border-color: rgba(197, 179, 230, 0.4);
  transform: translateY(-3px);
}

.resource-card h4 {
  font-size: 18px;
  color: white;
  margin: 0 0 12px 0;
  font-weight: 600;
}

.resource-card p {
  color: white;
  line-height: 1.6;
  margin-bottom: 16px;
  font-size: 14px;
  font-weight: 300;
}

.resource-card a {
  color: #c5b3e6;
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  transition: color 0.3s ease;
}

.resource-card a:hover {
  color: #b39ddb;
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
@media (max-width: 1024px) {
  .timeline-row {
    grid-template-columns: 1fr 60px 1fr;
    gap: 20px;
  }

  .policies-grid {
    grid-template-columns: 1fr;
  }

  .resources-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .hero-text h1 {
    font-size: 36px;
  }

  .timeline-section,
  .policies-section,
  .resources-section {
    padding: 60px 30px;
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

  .resources-grid {
    grid-template-columns: 1fr;
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