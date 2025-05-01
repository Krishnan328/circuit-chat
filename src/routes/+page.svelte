<script lang="ts">
    import { onMount } from 'svelte';
    import { goto } from '$app/navigation';
  
    onMount(() => {
      const shapes = document.querySelectorAll('.shape');
      
      shapes.forEach(shape => {
        let posX = Math.random() * window.innerWidth;
        let posY = Math.random() * window.innerHeight;
        let speedX = (Math.random() - 0.5) * 3.5;
        let speedY = (Math.random() - 0.5) * 3.5;
        
        setInterval(() => {
          posX += speedX;
          posY += speedY;
          
          // Bounce off edges
          if (posX <= 0 || posX >= window.innerWidth - 200) {
            speedX *= -1;
          }
          if (posY <= 0 || posY >= window.innerHeight - 200) {
            speedY *= -1;
          }
          
          // Fix TypeScript error with type assertion
          (shape as HTMLElement).style.left = posX + 'px';
          (shape as HTMLElement).style.top = posY + 'px';
        }, 30);
      });
    });

    function handleGetStarted() {
      goto('/signup');
    }
  </script>
  
  <div class="background">
    <div class="shape"></div>
    <div class="shape"></div>
    <div class="shape"></div>
    <div class="shape"></div>
    <div class="shape"></div>
  </div>
  
  <header>
    <div class="logo-container">
      <img src="circuit_chat_icon.svg" alt="Circuit Chat Logo" class="logo">
      <h1 class="app-name">Circuit Chat</h1>
    </div>
    <a href="/login" class="login-button">Log In</a>
  </header>
  
  <main>
    <section class="hero">
      <h2>Professional Communication Reimagined</h2>
      <p class="tagline">Secure. Efficient. Professional.</p>
      <p class="description">
        Circuit Chat provides a streamlined communication platform designed exclusively for business and education professionals.
        Connect with teams, share resources, and collaborate in real-time in a distraction-free environment.
      </p>
      <div class="cta-buttons">
        <button onclick={() => handleGetStarted()} class="primary-button">Get Started</button>
        <button class="secondary-button">Learn More</button>
      </div>
    </section>
    
    <section class="features">
      <div class="feature-card">
        <div class="feature-icon">🔒</div>
        <h3>Enterprise-Grade Security</h3>
        <p>End-to-end encryption and compliance with industry standards</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🚀</div>
        <h3>Seamless Integration</h3>
        <p>Connect with your existing tools and workflows</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🔍</div>
        <h3>Advanced Search</h3>
        <p>Find messages and resources in seconds</p>
      </div>
    </section>
  </main>
  
  <style>
    *,
    *:before,
    *:after {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
    }
    
    :global(body) {
      background-color: #1e1e2e; /* Catppuccin Mocha base */
      font-family: 'Poppins', sans-serif;
      color: #cdd6f4; /* Catppuccin Text */
    }
    
    .background {
      width: 100%;
      height: 100vh;
      position: fixed;
      z-index: -1;
    }
    
    .background .shape {
      height: 200px;
      width: 200px;
      position: absolute;
      border-radius: 50%;
      filter: blur(15px);
      opacity: 0.8;
      transition: all 0.5s ease;
    }
    
    .shape:nth-child(1) {
      background: linear-gradient(
        #f5c2e7, /* Catppuccin Pink */
        #cba6f7  /* Catppuccin Mauve */
      );
    }
    
    .shape:nth-child(2) {
      background: linear-gradient(
        #89dceb, /* Catppuccin Sky */
        #74c7ec  /* Catppuccin Sapphire */
      );
    }
    
    .shape:nth-child(3) {
      background: linear-gradient(
        #a6e3a1, /* Catppuccin Green */
        #94e2d5  /* Catppuccin Teal */
      );
      height: 150px;
      width: 150px;
    }
    
    .shape:nth-child(4) {
      background: linear-gradient(
        #fab387, /* Catppuccin Peach */
        #f9e2af  /* Catppuccin Yellow */
      );
      height: 180px;
      width: 180px;
    }
    
    .shape:nth-child(5) {
      background: linear-gradient(
        #b4befe, /* Catppuccin Lavender */
        #f5c2e7  /* Catppuccin Pink */
      );
      height: 170px;
      width: 170px;
    }
    
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.5rem 2rem;
      backdrop-filter: blur(10px);
      background-color: rgba(30, 30, 46, 0.5);
      border-bottom: 1px solid rgba(205, 214, 244, 0.1);
      position: relative;
      z-index: 10;
    }
    
    .logo-container {
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }
    
    .logo {
      height: 40px;
      width: 40px;
    }
    
    .app-name {
      font-family: 'JetBrains Mono', monospace;
      color: #cba6f7; /* Catppuccin Mauve */
      font-size: 1.8rem;
      font-weight: 600;
    }
    
    .login-button {
      padding: 0.6rem 1.5rem;
      background-color: #cba6f7; /* Catppuccin Mauve */
      color: #1e1e2e; /* Catppuccin Base */
      font-weight: 600;
      border-radius: 8px;
      text-decoration: none;
      transition: all 0.3s ease;
      cursor: pointer;
      border: none;
      font-size: 1rem;
    }
    
    .login-button:hover {
      background-color: #f5c2e7; /* Catppuccin Pink */
    }
    
    main {
      padding: 0 2rem;
      max-width: 1200px;
      margin: 0 auto;
      position: relative;
      z-index: 5;
    }
    
    .hero {
      text-align: center;
      padding: 6rem 1rem 4rem;
      backdrop-filter: blur(5px);
    }
    
    .hero h2 {
      font-size: 2.5rem;
      color: #f5c2e7; /* Catppuccin Pink */
      margin-bottom: 1rem;
    }
    
    .tagline {
      font-size: 1.5rem;
      color: #b4befe; /* Catppuccin Lavender */
      margin-bottom: 1.5rem;
    }
    
    .description {
      max-width: 800px;
      margin: 0 auto 2.5rem;
      line-height: 1.6;
      font-size: 1.1rem;
      color: #a6adc8; /* Catppuccin Subtext0 */
    }
    
    .cta-buttons {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 4rem;
    }
    
    .primary-button {
      padding: 0.8rem 2rem;
      background-color: #cba6f7; /* Catppuccin Mauve */
      color: #1e1e2e; /* Catppuccin Base */
      font-weight: 600;
      border-radius: 8px;
      border: none;
      font-size: 1rem;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    
    .primary-button:hover {
      background-color: #f5c2e7; /* Catppuccin Pink */
    }
    
    .secondary-button {
      padding: 0.8rem 2rem;
      background-color: rgba(49, 50, 68, 0.7); /* Catppuccin Surface0 */
      color: #cdd6f4; /* Catppuccin Text */
      font-weight: 600;
      border-radius: 8px;
      border: 1px solid rgba(108, 112, 134, 0.3); /* Catppuccin overlay0 */
      font-size: 1rem;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    
    .secondary-button:hover {
      background-color: rgba(69, 71, 90, 0.7); /* Catppuccin Surface1 */
      border-color: #b4befe; /* Catppuccin Lavender */
    }
    
    .features {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      padding: 2rem 0 4rem;
    }
    
    .feature-card {
      background-color: rgba(30, 30, 46, 0.75);
      border-radius: 10px;
      backdrop-filter: blur(15px);
      border: 2px solid rgba(205, 214, 244, 0.1);
      box-shadow: 0 0 40px rgba(17, 17, 27, 0.6);
      padding: 2rem;
      text-align: center;
      transition: transform 0.3s ease;
    }
    
    .feature-card:hover {
      transform: translateY(-5px);
    }
    
    .feature-icon {
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }
    
    .feature-card h3 {
      color: #b4befe; /* Catppuccin Lavender */
      margin-bottom: 1rem;
    }
    
    .feature-card p {
      color: #a6adc8; /* Catppuccin Subtext0 */
      line-height: 1.5;
    }
    
    @media (max-width: 768px) {
      header {
        padding: 1rem;
      }
      
      .app-name {
        font-size: 1.5rem;
      }
      
      .hero h2 {
        font-size: 2rem;
      }
      
      .tagline {
        font-size: 1.2rem;
      }
      
      .cta-buttons {
        flex-direction: column;
        align-items: center;
        gap: 1rem;
      }
      
      .primary-button, .secondary-button {
        width: 100%;
        max-width: 300px;
      }
    }
  </style>