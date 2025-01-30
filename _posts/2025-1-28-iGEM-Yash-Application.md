---
layout: none
title: Yash Parikh 2025 iGEM Application
---

<div class="intro-text">
    <p>In advance: Yes, this page is very simple. I wanted to keep it that way to show that I can make a simple and clean website. I can make it more complex if needed as I described on the application Google Doc.</p>
    <p>I reviewed the 2023 iGEM wiki for DNHS San Diego. What I liked most about this wiki was its clean and modern design. The color scheme and text was consistent throughout, which gave it a professional look. Our team can implement similar ideas by maintaining a consistent color palette and using engaging visuals. However, I feel that the website wasn't very user friendly, but some people might disagree with that. The reason I say this is because having the nav bar on the side means that every time the viewer scrolls down, they are forced away from the nav bar which makes them have to scroll back up to navigate to a different page. I think that having the nav bar at the top of the page would be more user friendly, or having a small sticky nav bar that follows the user as they scroll on the page.</p>
    <p>Some more improvements that could be made include the use of animations to make the page more interactive and engaging. For example, fade-in effects can be applied to elements as they come into view, creating a smooth and dynamic browsing experience. Additionally, the use of hover effects on links and buttons can provide visual feedback to users, making the site more intuitive to navigate.</p>
    <p>I don't know if this fits in with the iGEM competition ideal, but having maybe small games or quizzes that are related to the team's project could be a fun and interactive way to engage visitors. This could also help educate them about the team's work and the broader field of synthetic biology.</p>
    <p>One idea that I had was that having a small section on the homepage that shows the team's progress in the competition would be a nice touch. This could include a progress bar or a timeline of milestones achieved, giving visitors a quick overview of the team's journey.</p>
    <p>To tailor the design to our team, we can use our colors (102c61, 204f31, 9fa376) and fonts (Becka Script Plain and Collegiate Inside). I got these colors and fonts all from <a href="https://4.files.edl.io/951e/05/26/23/003302-a40f3172-d0ca-4851-a293-64f9f504f691.pdf">Del Norte's official website</a>. Below is an example of HTML, JavaScript, and CSS for a page designed with these elements. I found this tool recently while doing web design and absolutely loved it. <a href="https://coolors.co/">Coolors</a> is a great tool for finding color palettes that work well together. I think that this tool could be very useful for our team when designing the wiki.</p>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/particles.js/2.0.0/particles.min.js"></script>
<style>
    :root {
        --primary-navy-ig: #102c61;
        --primary-navy-light-ig: #1a438f;
        --primary-navy-dark-ig: #0a1d40;
        --primary-green-ig: #204f31;
        --primary-green-light-ig: #2d7246;
        --primary-green-dark-ig: #163521;
        --accent-sage-ig: #9fa376;
        --accent-sage-light-ig: #b5b991;
        --accent-sage-dark-ig: #828759;
        --white-ig: #ffffff;
        --off-white-ig: #f8f9fa;
        --gray-light-ig: #e9ecef;
    }
    *, *::before, *::after {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    body {
        font-family: 'Collegiate Inside', sans-serif;
        background: var(--off-white-ig);
        color: var(--primary-navy-ig);
        line-height: 1.8;
        overflow-x: hidden;
    }
    .intro-text {
        background: var(--gray-light-ig);
        padding: 2rem;
        border-radius: 8px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        margin-bottom: 2rem;
    }
    .intro-text p {
        margin-bottom: 1rem;
    }
    .intro-text a {
        color: var(--primary-green-ig);
        text-decoration: none;
    }
    .intro-text a:hover {
        text-decoration: underline;
    }
    h1, h2 {
        font-family: 'Becka Script Plain', cursive;
        transform: scaleY(1.5);
        transform-origin: top;
        letter-spacing: 0.5px;
        margin-bottom: 1.5rem;
    }
    h1 {
        font-size: 24pt;
        color: var(--white-ig);
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        position: relative;
        z-index: 2;
    }
    h2 {
        font-size: 24pt;
        color: var(--primary-green-ig);
    }
    p {
        font-size: 14pt;
        line-height: 1.8;
        color: var(--primary-navy-ig);
        margin-bottom: 1.5rem;
    }
    header {
        background: linear-gradient(135deg, var(--primary-green-ig) 0%, var(--primary-green-dark-ig) 100%);
        padding: 3rem 2rem;
        text-align: center;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        position: relative;
        overflow: hidden;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    #particles-js-ig {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 1;
    }
    nav {
        position: fixed;
        top: 0;
        width: 100%;
        z-index: 1000;
        background: transparent;
        transition: background 0.3s ease;
        padding: 1rem 0;
    }
    nav.scrolled {
        background: var(--primary-navy-ig);
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
    nav ul {
        list-style: none;
        display: flex;
        justify-content: center;
        gap: 2rem;
    }
    nav ul li a {
        color: var(--white-ig);
        text-decoration: none;
        padding: 0.75rem 1.5rem;
        border-radius: 4px;
        transition: all 0.3s ease;
        position: relative;
        overflow: hidden;
    }
    main {
        max-width: 1200px;
        margin: 0 auto;
        padding: 2rem;
    }
    section {
        min-height: 40vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 4rem 2rem;
        position: relative;
        overflow: hidden;
    }
    .highlight {
        background: linear-gradient(120deg, var(--accent-sage-light-ig) 0%, var(--accent-sage-ig) 100%);
        padding: 1.5rem;
        border-radius: 8px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    }
    .cursor-trail-ig {
        position: fixed;
        width: 10px;
        height: 10px;
        background: var(--accent-sage-ig);
        border-radius: 50%;
        pointer-events: none;
        z-index: 9999;
    }
    @media (max-width: 768px) {
        nav ul {
            flex-direction: column;
            align-items: center;
        }
        section {
            padding: 2rem 1rem;
        }
    }
</style>

<header>
    <div id="particles-js-ig"></div>
    <h1>Yash Parikh 2025 iGEM Application</h1>
</header>

<nav>
    <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#project">Project</a></li>
        <li><a href="#team">Team</a></li>
        <li><a href="#contact">Contact</a></li>
    </ul>
</nav>

<main>
    <section id="home">
        <h2 class="orange">Welcome</h2>
        <p class="highlight">Welcome to our iGEM project page. Here you will find all the information about our project and team.</p>
    </section>
    <section id="about">
        <h2 class="orange">About Us</h2>
        <p>We are a team of dedicated students from Del Norte High School, San Diego, participating in the iGEM competition.</p>
    </section>
    <section id="project">
        <h2 class="orange">Our Project</h2>
        <p>Our project focuses on innovative solutions in synthetic biology to address real-world problems.</p>
    </section>
</main>

<script>
    gsap.registerPlugin(ScrollTrigger);

    particlesJS('particles-js-ig', {
        particles: {
            number: { value: 80 },
            color: { value: '#ffffff' },
            shape: { type: 'circle' },
            opacity: { value: 0.5, random: true },
            size: { value: 3, random: true },
            move: {
                enable: true,
                speed: 2,
                direction: 'none',
                random: true,
                out_mode: 'out'
            }
        }
    });

    const createTrailIg = () => {
        const trail = document.createElement('div');
        trail.className = 'cursor-trail-ig';
        document.body.appendChild(trail);
        setTimeout(() => trail.remove(), 500);
        return trail;
    };

    document.addEventListener('mousemove', (e) => {
        const trail = createTrailIg();
        trail.style.left = e.pageX + 'px';
        trail.style.top = e.pageY + 'px';
        gsap.to(trail, {
            duration: 0.5,
            opacity: 0,
            scale: 0,
            ease: 'power2.out'
        });
    });

    window.addEventListener('scroll', () => {
        const nav = document.querySelector('nav');
        if (window.scrollY > 50) {
            nav.classList.add('scrolled');
        } else {
            nav.classList.remove('scrolled');
        }
    });

    document.querySelectorAll('nav a').forEach(anchor => {
        anchor.addEventListener('click', function(e) {
            e.preventDefault();
            const target = document.querySelector(this.getAttribute('href'));
            gsap.to(window, {
                duration: 1,
                scrollTo: target,
                ease: 'power2.inOut'
            });
        });
    });

    gsap.from('header h1', {
        duration: 1.5,
        y: 100,
        opacity: 0,
        ease: 'power4.out',
        delay: 0.5
    });

    document.querySelectorAll('section').forEach((section, index) => {
        gsap.from(section.querySelector('h2'), {
            scrollTrigger: {
                trigger: section,
                start: 'top center',
                toggleActions: 'play none none reverse'
            },
            duration: 1,
            y: 50,
            opacity: 0,
            ease: 'power2.out'
        });

        gsap.from(section.querySelector('p'), {
            scrollTrigger: {
                trigger: section,
                start: 'top center',
                toggleActions: 'play none none reverse'
            },
            duration: 1,
            y: 50,
            opacity: 0,
            ease: 'power2.out',
            delay: 0.3
        });

        gsap.to(section, {
            scrollTrigger: {
                trigger: section,
                start: 'top bottom',
                end: 'bottom top',
                scrub: true
            },
            backgroundPosition: `50% ${-50 * (index + 1)}px`,
            ease: 'none'
        });
    });

    const createFloatingElementIg = () => {
        const element = document.createElement('div');
        element.style.position = 'fixed';
        element.style.width = '5px';
        element.style.height = '5px';
        element.style.background = 'var(--accent-sage-ig)';
        element.style.borderRadius = '50%';
        element.style.pointerEvents = 'none';
        element.style.opacity = '0.5';
        document.body.appendChild(element);

        gsap.set(element, {
            x: Math.random() * window.innerWidth,
            y: Math.random() * window.innerHeight
        });

        gsap.to(element, {
            duration: 'random(2, 4)',
            x: '+=' + (Math.random() * 200 - 100),
            y: '+=' + (Math.random() * 200 - 100),
            opacity: 0,
            ease: 'none',
            onComplete: () => {
                element.remove();
                createFloatingElementIg();
            }
        });
    };

    for (let i = 0; i < 20; i++) {
        createFloatingElementIg();
    }
</script>

<section id="hero">
    <div class="hero-content">
        <h2 class="hero-title">Welcome to the Future of Synthetic Biology</h2>
        <p class="hero-subtitle">Where Innovation Meets Creativity</p>
        <button class="hero-button">Explore Our Vision</button>
    </div>
    <div class="hero-background"></div>
</section>

<section id="features">
    <h2 class="section-title">Interactive Features</h2>
    <div class="feature-grid">
        <div class="feature-card">
            <div class="feature-icon">✨</div>
            <h3 class="feature-title">Dynamic Animations</h3>
        </div>
        <div class="feature-card">
            <div class="feature-icon">🎮</div>
            <h3 class="feature-title">Mini Games</h3>
        </div>
        <div class="feature-card">
            <div class="feature-icon">📊</div>
            <h3 class="feature-title">Progress Timeline</h3>
        </div>
    </div>
</section>

<section id="timeline">
    <h2 class="section-title">Our Journey</h2>
    <div class="timeline-container">
        <div class="timeline-line"></div>
        <div class="timeline-item">
            <div class="timeline-content">
                <h3 class="timeline-date">January 2024</h3>
                <p class="timeline-description">Team formation and initial brainstorming sessions.</p>
            </div>
        </div>
        <div class="timeline-item">
            <div class="timeline-content">
                <h3 class="timeline-date">March 2024</h3>
                <p class="timeline-description">Project proposal finalized and submitted.</p>
            </div>
        </div>
        <div class="timeline-item">
            <div class="timeline-content">
                <h3 class="timeline-date">June 2024</h3>
                <p class="timeline-description">Lab work begins with great results.</p>
            </div>
        </div>
        <div class="timeline-item">
            <div class="timeline-content">
                <h3 class="timeline-date">October 2024</h3>
                <p class="timeline-description">Final iGEM competition review.</p>
            </div>
        </div>
    </div>
</section>

<section id="team-showcase">
    <h2 class="section-title">Meet the DNHS Dream Team</h2>
    <div class="team-grid">
        <div class="team-member">
            <div class="member-photo" style="background-image: url('https://via.placeholder.com/150');"></div>
            <h3 class="member-name">You</h3>
            <p class="member-role">Team Leader</p>
        </div>
        <div class="team-member">
            <div class="member-photo" style="background-image: url('https://via.placeholder.com/150');"></div>
            <h3 class="member-name">Jane Doe</h3>
            <p class="member-role">Lab Specialist</p>
        </div>
        <div class="team-member">
            <div class="member-photo" style="background-image: url('https://via.placeholder.com/150');"></div>
            <h3 class="member-name">John Smith</h3>
            <p class="member-role">Web Developer</p>
        </div>
        <div class="team-member">
            <div class="member-photo" style="background-image: url('https://via.placeholder.com/150');"></div>
            <h3 class="member-name">Emily Brown</h3>
            <p class="member-role">Data Analyst</p>
        </div>
    </div>
</section>

<section id="contact-fancy">
    <h2 class="section-title">Get in Touch</h2>
    <div class="contact-form">
        <input type="text" placeholder="Your Name" class="form-input">
        <input type="email" placeholder="Your Email" class="form-input">
        <textarea placeholder="Your Message" class="form-textarea"></textarea>
        <button class="form-button">Send Message</button>
    </div>
</section>

<footer>
    <div class="footer-content">
        <p class="footer-text">© 2024 Del Norte iGEM Team. All rights reserved.</p>
        <div class="social-icons">
            <a href="#" class="social-icon">📘</a>
            <a href="#" class="social-icon">🐦</a>
            <a href="#" class="social-icon">📸</a>
        </div>
    </div>
</footer>

<style>
    #hero {
        position: relative;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
        background: linear-gradient(135deg, var(--primary-green-ig) 0%, var(--primary-green-dark-ig) 100%);
    }
    .hero-content {
        text-align: center;
        z-index: 2;
    }
    .hero-title {
        font-size: 4rem;
        color: var(--white-ig);
        margin-bottom: 1rem;
    }
    .hero-subtitle {
        font-size: 1.5rem;
        color: var(--off-white-ig);
        margin-bottom: 2rem;
    }
    .hero-button {
        padding: 1rem 2rem;
        font-size: 1rem;
        color: var(--primary-green-ig);
        background: var(--white-ig);
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    .hero-button:hover {
        background: var(--accent-sage-ig);
        color: var(--white-ig);
    }
    .hero-background {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: url('https://via.placeholder.com/1920x1080') no-repeat center center/cover;
        opacity: 0.2;
        z-index: 1;
    }

    #features {
        padding: 4rem 2rem;
        background: var(--off-white-ig);
    }
    .section-title {
        text-align: center;
        font-size: 2.5rem;
        margin-bottom: 2rem;
        color: var(--primary-green-ig);
    }
    .feature-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 2rem;
    }
    .feature-card {
        background: var(--white-ig);
        padding: 2rem;
        border-radius: 8px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        text-align: center;
        transition: transform 0.3s ease;
    }
    .feature-card:hover {
        transform: translateY(-10px);
    }
    .feature-icon {
        font-size: 3rem;
        margin-bottom: 1rem;
    }
    .feature-title {
        font-size: 1.5rem;
        color: var(--primary-green-ig);
        margin-bottom: 1rem;
    }
    .feature-description {
        font-size: 1rem;
        color: var(--primary-navy-ig);
    }

    #timeline {
        padding: 4rem 2rem;
        background: var(--white-ig);
    }
    .timeline-container {
        position: relative;
        max-width: 800px;
        margin: 0 auto;
    }
    .timeline-line {
        position: absolute;
        top: 0;
        left: 50%;
        width: 2px;
        height: 100%;
        background: var(--primary-green-ig);
        transform: translateX(-50%);
    }
    .timeline-item {
        padding: 2rem;
        position: relative;
        width: 50%;
    }
    .timeline-item:nth-child(odd) {
        left: 0;
    }
    .timeline-item:nth-child(even) {
        left: 50%;
    }
    .timeline-content {
        background: var(--off-white-ig);
        padding: 1.5rem;
        border-radius: 8px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    }
    .timeline-date {
        font-size: 1.25rem;
        color: var(--primary-green-ig);
        margin-bottom: 0.5rem;
    }
    .timeline-description {
        font-size: 1rem;
        color: var(--primary-navy-ig);
    }

    #team-showcase {
        padding: 4rem 2rem;
        background: var(--off-white-ig);
    }
    .team-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 2rem;
    }
    .team-member {
        text-align: center;
    }
    .member-photo {
        width: 150px;
        height: 150px;
        background-size: cover;
        background-position: center;
        border-radius: 50%;
        margin: 0 auto 1rem;
    }
    .member-name {
        font-size: 1.5rem;
        color: var(--primary-green-ig);
        margin-bottom: 0.5rem;
    }
    .member-role {
        font-size: 1rem;
        color: var(--primary-navy-ig);
    }

    #contact-fancy {
        padding: 4rem 2rem;
        background: var(--white-ig);
    }
    .contact-form {
        max-width: 600px;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }
    .form-input, .form-textarea {
        padding: 1rem;
        border: 1px solid var(--gray-light-ig);
        border-radius: 4px;
        font-size: 1rem;
    }
    .form-textarea {
        resize: vertical;
        min-height: 150px;
    }
    .form-button {
        padding: 1rem 2rem;
        font-size: 1rem;
        color: var(--white-ig);
        background: var(--primary-green-ig);
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    .form-button:hover {
        background: var(--primary-green-dark-ig);
    }

    footer {
        padding: 2rem;
        background: var(--primary-navy-ig);
        color: var(--white-ig);
        text-align: center;
    }
    .footer-content {
        max-width: 1200px;
        margin: 0 auto;
    }
    .footer-text {
        margin-bottom: 1rem;
    }
    .social-icons {
        display: flex;
        justify-content: center;
        gap: 1rem;
    }
    .social-icon {
        font-size: 1.5rem;
        color: var(--white-ig);
        text-decoration: none;
    }
</style>

<script>
    gsap.from('.hero-title', {
        duration: 1.5,
        y: 50,
        opacity: 0,
        ease: 'power4.out',
        delay: 0.5
    });
    gsap.from('.hero-subtitle', {
        duration: 1.5,
        y: 50,
        opacity: 0,
        ease: 'power4.out',
        delay: 0.8
    });
    gsap.from('.hero-button', {
        duration: 1.5,
        y: 50,
        opacity: 0,
        ease: 'power4.out',
        delay: 1.1
    });

    gsap.from('.timeline-item', {
        scrollTrigger: {
            trigger: '.timeline-item',
            start: 'top 80%',
            toggleActions: 'play none none none'
        },
        duration: 1,
        y: 50,
        opacity: 0,
        stagger: 0.3,
        ease: 'power2.out'
    });

    gsap.from('.team-member', {
        scrollTrigger: {
            trigger: '.team-member',
            start: 'top 80%',
            toggleActions: 'play none none none'
        },
        duration: 1,
        y: 50,
        opacity: 0,
        stagger: 0.2,
        ease: 'power2.out'
    });

    gsap.from('.contact-form', {
        scrollTrigger: {
            trigger: '.contact-form',
            start: 'top 80%',
            toggleActions: 'play none none none'
        },
        duration: 1,
        y: 50,
        opacity: 0,
        ease: 'power2.out'
    });
</script>