  <template>
    <footer class="footer">
      <!-- Animated background elements -->
      <div class="animated-bg">
        <div class="float-circle blue"></div>
        <div class="float-circle purple delay-2"></div>
        <div class="float-circle green delay-4"></div>
      </div>

      <div class="footer-container">
        <!-- Main footer -->
        <div class="footer-main">
          <!-- Brand -->
          <div class="brand">
            <div class="brand-icon">
              <i class="fab fa-github"></i>
              <span class="glow"></span>
            </div>
            <span class="brand-title"><a href="https://www.deepseek.com/">Download Source Code</a></span>
            <p class="brand-text">
              Discover and explore GitHub users and their repositories. Built with Vue.js.
            </p>
          </div>

          <!-- Links -->
          <div class="footer-links">
            <!-- Product -->
            <div class="link-group">
              <h4>Product</h4>
              <a href="#">Features</a>
              <a href="#">API</a>
              <a href="#">Integrations</a>
            </div>

            <!-- Support -->
            <div class="link-group">
              <h4>Support</h4>
              <a href="#">Documentation</a>
              <a href="#">Guides</a>
              <a href="#">Help Center</a>
            </div>

            <!-- Company -->
            <div class="link-group">
              <h4>Company</h4>
              <a href="#">About</a>
              <a href="#">Blog</a>
              <a href="#">Careers</a>
            </div>
          </div>
        </div>

        <!-- Bottom -->
        <div class="footer-bottom">
          <div class="legal-links">
            <a href="#">Terms of Service</a>
            <a href="#">Privacy Policy</a>
            <a href="#">Security</a>
            <a href="#">Status</a>
          </div>

          <div class="social">
            <i class="bi bi-google"></i>
            <i class="bi bi-twitter-x"></i>
            <i class="bi bi-facebook"></i>
            <i class="bi bi-telegram"></i>
            <i class="bi bi-twitter"></i>
          </div>
        </div>

        <div class="copyright">&copy; Copyright 2025 (SAKY Unfake) ❤️ </div>
      </div>
    </footer>
  </template>


  <style scoped>
  :root[data-theme="light"] {
    --bg-gradient: radial-gradient(circle, #da4d40 0%, #7a2828 100%);
    --text-color: white;
  }
  :root[data-theme="dark"] {
    --bg-gradient: radial-gradient(circle, #2c313c 0%, 	#343b48 100%);
    --text-color: #f5f5f5;
  }
  .footer {
    position: relative;
    padding-top: 40px;
    border-top: 1px solid #ddd;
    overflow: hidden;
  }

  /* Animated circles */
  .animated-bg {
    position: absolute;
    inset: 0;
    opacity: 0.15;
  }

  .float-circle {
    position: absolute;
    border-radius: 50%;
    filter: blur(20px);
    animation: float 6s ease-in-out infinite;
  }

  .blue { width: 80px; height: 80px; background: #bfdbfe; top: 40px; left: 40px; }
  .purple { width: 60px; height: 60px; background: #e9d5ff; bottom: 40px; right: 40px; }
  .green { width: 50px; height: 50px; background: #bbf7d0; top: 50%; left: 33%; }

  .delay-2 { animation-delay: 2s; }
  .delay-4 { animation-delay: 4s; }

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-12px); }
  }

  /* Layout container */
  .footer-container {
    position: relative;
    padding: 40px 20px;
    max-width: 1200px;
    margin: auto;
    color: white;
    z-index: 2;
  }

  /* Main section flexbox */
  .footer-main {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 40px;
  }

  /* Brand section */
  .brand {
    max-width: 350px;
  }

.brand-icon {
  position: relative;
  font-size: 32px;
  color: white;
  display: inline-block;
  transition: transform 0.45s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              filter 0.45s ease,
              opacity 0.3s ease;
}

.brand-icon:hover {
  transform: scale(1.18) translateY(-4px);
  filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.55));
  color: black;
  opacity: 0.95;
  cursor: pointer;
}

  .glow {
    position: absolute;
    inset: -6px;
    background: #93c5fd;
    border-radius: 50%;
    filter: blur(10px);
    opacity: 0.3;
    color: white;
  }

  .brand-title a {
    text-decoration: none;
    display: inline-block;
    margin-top: 10px;
    font-weight: bold;
    font-size: 22px;
    margin-left: 5px;
    background: linear-gradient(to right, #2563eb, #7c3aed);
    -webkit-background-clip: text;
    color: transparent;
  }
  .brand-title a:hover {
    background: linear-gradient(to right,#a77fec,#0f3c9d) ;
    -webkit-background-clip: text;
    color: transparent;
  }

  .brand-text {
    margin-top: 10px;
    color: white;
    font-size: 14px;
  }

  /* Links grid */
  .footer-links {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 40px;
  }

  .link-group h4 {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 12px;
    background: linear-gradient(to right, #2563eb, #7c3aed);
    -webkit-background-clip: text; /* for Chrome/Safari */
    -webkit-text-fill-color: transparent; /* for Chrome/Safari */
    background-clip: text; /* for Firefox */
    color: transparent; /* fallback */
  }

  .link-group a {
    display: block;
    color: white;
    text-decoration: none;
    margin-bottom: 6px;
    transition: color 0.2s, transform 0.2s;
  }

  .link-group a:hover {
    color: #2563eb;
    transform: translateX(4px);
  }

  /* Bottom section */
  .footer-bottom {
    border-top: 1px solid white;
    padding-top: 20px;
    margin-top: 40px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .legal-links a {
    margin-right: 20px;
    font-size: 14px;
    color: white;
    text-decoration: none;
    transition: 0.2s;
  }

  .legal-links a:hover {
    color:#2563eb;
;
  }

.social i {
  transition: all 0.3s ease; /* Smooth animation */
  color: #ffffff; /* default color */
  cursor: pointer;
  margin-left: 12px;
  color: white;
  font-size: 20px;
  display: inline-flex;
  transition: transform 0.45s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              filter 0.45s ease,
              color 0.25s ease,
              opacity 0.25s ease;
}

/* Hover effects with brand colors */
.social i.bi-google:hover {
  color: #da4d40; /* Google Blue */
  transform: scale(1.5);
}

.social i.bi-twitter-x:hover {
  color: black; /* Twitter X Blue */
  transform: scale(1.5);
}

.social i.bi-facebook:hover {
  color: blue; /* Facebook Blue */
  transform: scale(1.5);
}

.social i.bi-telegram:hover {
  color: #0088cc; /* Telegram Blue */
  transform: scale(1.5);
}

.social i.bi-twitter:hover {
  color: #1DA1F2; /* Twitter Blue */
  transform: scale(1.5);
}

  /* Copyright */
  .copyright {
    margin-top: 30px;
    text-align: center;
    color: white;
    font-size: 14px;
  }


  /* Responsive Footer */
@media (min-width: 600px) {
  .footer-container {
    padding: 10px 20px;
  }
  
} 
/* Mobile */
@media (max-width: 600px) {
  .footer-main {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  .footer-container {
    padding: 10px 10px;
  }
  .footer-links {
    gap: 20px;
  }

  .social{
    display: flex;
    margin-top: 3%;
    justify-content: center; /* Center social icons */
    gap: 15px;
  }
  .footer-bottom{
    display: flex;
    justify-content: center;
  }
 
}

  </style>
