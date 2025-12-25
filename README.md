🌐 Website Preloader Animation — GSAP + HTML/CSS

A highly-polished website intro animation featuring a GSAP-powered loading screen, dynamic number counter, and bar rotation loader, followed by a smooth reveal of website content.

This project demonstrates a modern preloader flow built using GSAP, custom CSS animations, and clean HTML structure. The loader simulates system-style boot sequences, then transforms fluidly into the main content.

📁 Project Structure
├── index.html
├── style.css
└── /assets (optional)

Key components

Loading Screen (.loading-screen)
Contains the animated counter and the dual-bar loader.

Loader Bar System (.loader, .loader-1, .loader-2)
Two bars animate width, transform, rotate, and scale.

Counter System (.counter, .digit, .num)
Three independent GSAP-driven counters that simulate real loading progress.

Content Reveal (.website-content, .header-revealer)
Main site content is hidden until the preloader is fully finished.

⚙️ How the Preloader Animation Works
1. Number Counter Scroll Animation

Each .digit container contains multiple .num elements representing numbers 0–9 (and extended numbers generated dynamically in JS).
GSAP translates each digit vertically at different speeds, creating a realistic counter progression.

2. Loader Bar Growth

Two bars:

.loader-1

.loader-2

grow in width using GSAP .from() animations. Their durations are staggered for a natural load effect.

3. Bar Rotation & Exit

After the bar fills:

.loader-1 rotates 90°

.loader-2 shifts diagonally

Entire loader scales massively and exits the screen with rotation

This produces a “burst-out transition”.

4. Content Reveal

The .loading-screen fades out, revealing:

Website Header

"Website Content" animated upward with a staggered motion

🧠 Code Explanation (Important Parts Only)
1. Counter Number Generator
for (let i = 0; i < 2; i++) {
    for (let j = 0; j < 10; j++) {
        const div = document.createElement("div");
        div.className = "num";
        div.textContent = j;
        counter3.appendChild(div);
    }
}

What it does

Dynamically extends the number stack for the last counter (counter-3) so that the scroll animation can run continuously.

Why it's used

Instead of hard-coding many numbers, this generates them programmatically.
Impact: cleaner DOM, reusable animation logic, easier scaling.

2. GSAP Number Scroll Animation
function animate(counter, duration, delay = 0){
    const numHeight = counter.querySelector('.num').clientHeight;
    const totalDistance = (counter.querySelectorAll('.num').length - 1) * numHeight;

    gsap.to(counter, {
        y: -totalDistance,
        duration: duration,
        delay: delay,
        ease: "power2.inOut",
    });
}

What it does

Calculates the required vertical distance and scrolls the number stack.

Why it's used

Smooth GSAP-based scroll provides a futuristic loading effect.

Impact:
Creates a professional UI animation sequence that visually simulates progress.

3. Loader Bar Fill Animation
gsap.from(".loader-1", {
    width: 0,
    duration: 6,
    ease: "power2.inOut",
});

What it does

Animates the width of the bar from 0 to full.

Impact

Visually indicates progress without needing actual loading logic.

4. Bar Rotation (the signature effect)
gsap.to(".loader-1", {
    rotate: 90,
    y: -50,
    duration: 0.5,
    delay: 6,
});

Why it's used

Creates a dramatic transition effect that transforms the loader into a motion element before exiting.

Impact

Adds a cinematic, polished look to the preloader.

5. Fade-Out & Reveal
gsap.to(".loading-screen", {
    opacity: 0,
    duration: 0.5,
    delay: 7.5,
});

Impact

Smoothly removes the preloader without abrupt jumps, giving a premium feel.

🎨 Key Styling Techniques Used
1. Clip-path Counter Window
clip-path: polygon(0 0, 100% 0, 100% 100px, 0 100px);


Ensures only part of the number column is visible.
Impact: clean digital counter effect.

2. Rotation Hairline Fix (Chrome-specific)
backface-visibility: hidden;


Impact: prevents Chrome from showing thin anti-alias lines during rotation.

3. Layout and Positioning

Absolute positioning keeps the loader centered

Flexbox for horizontal bar alignment

transform: translate(-50%, -50%) to perfectly center the loader

These combined ensure consistent cross-browser visuals.

🚀 Features

Smooth GSAP-powered animations

Clean typography using Satoshi

Future-proof structure (easy to reuse on real websites)

Chrome anti-aliasing fixes

Expandable counter system

Elegant entry animation for website header

📦 Tech Stack

HTML5

CSS3

GSAP 3.12.2

Satoshi Font (Fontshare)
