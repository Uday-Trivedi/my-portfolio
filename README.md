# Cybernetic Portfolio — Uday Trivedi

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
  <img src="https://img.shields.io/badge/GSAP-3.12.5-88CE02?style=for-the-badge&logo=greensock&logoColor=white" alt="GSAP" />
  <img src="https://img.shields.io/badge/Canvas-Physics%20Engine-00f2fe?style=for-the-badge" alt="HTML5 Canvas" />
</p>

<p align="center">
  This repository contains the source code for the personal portfolio website of <strong>Uday Trivedi</strong>.<br>
  Built from scratch using pure vanilla web technologies and an interactive canvas physics engine to create an immersive, cybernetic web experience.
</p>

<p align="center">
  <a href="https://github.com/Uday-Trivedi"><img src="https://img.shields.io/badge/GitHub-Profile-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
  <a href="https://www.linkedin.com/in/uday-trivedi-2b62a7293"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:udaytrivedi0012@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
</p>

---

## ⚡ Overview & Design Philosophy

The objective behind this portfolio was to move away from conventional, static templates and create an engineered web interface that feels alive, responsive, and futuristic. 

### Key Highlights
- **Zero Heavy Frameworks:** Built with pure vanilla HTML5, CSS3, and ES6+ JavaScript — delivering lightweight performance, 60fps animations, and zero bundle or hydration overhead.
- **Horizontal Spatial Track:** A continuous 7-panel sliding architecture that translates along the X-axis (`700vw` total width) rather than standard vertical document flow.
- **Interactive Living Neural Network:** A high-performance canvas engine simulating interconnected neural nodes, signal transmission pulses, and pointer attraction.
- **Tactile Cybernetic Aesthetic:** Dark-mode deep-space palette (`#030712`), glassmorphism with backdrop filters, kinetic navigation underlines, and cursor-following spotlight glows.

---

## 🛠️ Technology Stack

| Layer | Technologies | Purpose |
|:---|:---|:---|
| **Structure** | Semantic HTML5 | Clean DOM hierarchy, accessible landmarks, modal dialogs, and ARIA labels. |
| **Styling** | Vanilla CSS3 | Custom CSS properties (design tokens), flexbox & grid layouts, glassmorphic filters, and hardware-accelerated transitions. |
| **Logic** | Vanilla JavaScript (ES6+) | Spatial navigation state machine, event listeners, touch gesture recognition, and scroll-jacking logic. |
| **Animation** | [GSAP 3.12.5](https://greensock.com/gsap/) | High-precision timeline translation with smooth cubic easing and nav indicator transitions. |
| **Simulation** | HTML5 Canvas API | Mathematical physics engine rendering the interactive neural network background. |
| **Typography** | Google Fonts | `Outfit` (Headings & Display), `Inter` (Body Text), `JetBrains Mono` (Badges & Code Accents). |
| **Icons** | FontAwesome 6.5.1 | Cybernetic iconography for interactive UI controls and tech categories. |

---

## 🔬 How It Was Built: Engineering & Features

### 1. The Living Neural Network Simulation (`NeuralEngine`)
The background is an autonomous canvas physics engine written in object-oriented ES6 JavaScript:

- **Deterministic Node Distribution:** Uses a custom Mulberry32 pseudo-random number generator (`mulberry32`) to create a consistent network of floating synaptic nodes across screen dimensions.
- **Dynamic Proximity Graph:** Nodes evaluate pairwise Euclidean distances on every tick; connections closer than dynamic threshold distance form glowing synaptic links with opacity scaled to distance.
- **Signal Packet Transmission:** Packets travel along active connection vertices with simulated hops, trail decay, and probabilistic directional routing toward the cursor.
- **Pointer Attraction & Magnetics:** Mouse and touch positions project a magnetic field that dynamically biases nearby node positions and accelerates packet traffic toward the user's focus.
- **Performance Optimization:** 
  - Dynamic pixel ratio (`dpr`) scaling respecting device resolution up to 3×.
  - Automatic loop pausing when the tab is inactive via the `visibilitychange` API.
  - Respects accessibility settings via the `prefers-reduced-motion` media query.

```javascript
// Sample configuration of the Neural Engine
const engine = new NeuralEngine(canvas, {
  density: 1.3,        // Node density relative to screen area
  greenAmount: 1.9,    // Proportion of emerald vs cyan packets
  interaction: 2.0,    // Pointer magnetic attraction radius
  packets: 1.0,        // Active packet generation rate
  firingRate: 1.0      // Synaptic pulse frequency
});
```

---

### 2. Spatial Horizontal Slider & Viewport Track
Instead of conventional vertical scrolling, the application uses a horizontal rail coordinate system:

- **700vw Viewport Track:** All 7 panels reside within a horizontal flex container `#viewport-track` with `width: 700vw`.
- **Exact Pixel Translation:** Transitions compute `-currentPanelIndex * window.innerWidth` in pixels to eliminate fractional-viewport rendering artifacts across different browser zooms.
- **Hardware Acceleration:** Transitions leverage GPU-accelerated CSS `transform: translateX(...)` driven by GSAP's power2 easing curve for stutter-free 60fps motion.
- **Dynamic Window Resize Synchronization:** Window resize listeners re-calculate and anchor the active panel offset in real time without animation lag.

---

### 3. Intelligent Hybrid Scroll-Jacking
One common problem with horizontal websites is breaking natural scroll behavior. This implementation solves it through **panel-overflow-aware wheel interception**:

1. **Inner Content Awareness:** When a mouse wheel event fires, the script queries whether the current panel contains scrollable content:
   - If content remains above or below the current scroll position, the event executes standard vertical scrolling inside the panel.
   - If the user reaches the vertical boundary (top/bottom) and continues scrolling, the event transitions to the adjacent horizontal panel.
2. **Debounce & Animation Locks:** Prevents multi-panel skips from trackpad inertia gestures using timestamp-based debounce flags (`isScrollLocked`, `isAnimating`).

---

### 4. Multi-Modal Navigation & Accessibility
The site supports 4 independent navigation schemes:
- **Top Header Bar:** Clickable nav links with kinetic GSAP underline bars that track and expand to the active tab.
- **Keyboard Hotkeys:**
  - `→` or `PageDown`: Move to next panel
  - `←` or `PageUp`: Move to previous panel
  - `Home`: Jump directly to Home (Panel 0)
  - `End`: Jump directly to Contact (Panel 6)
- **Touch Gestures:** Touch start/end delta analysis calculates gesture angle (`|deltaX| > |deltaY|`) and threshold distance (`> 50px`) for natural mobile swiping.
- **Mobile Responsive Drawer:** Collapsible slide-in menu overlay for narrow screens and mobile viewports.

---

### 5. Cybernetic Glassmorphic UI & Micro-Interactions
- **Interactive Spotlight Hover Effect:** Every card (`.data-card`) tracks cursor coordinates locally and renders a dynamic `radial-gradient` highlight on hover:
  ```javascript
  glowLayer.style.background = `radial-gradient(320px circle at ${x}px ${y}px, rgba(56, 189, 248, 0.12), transparent 75%)`;
  ```
- **Kinetic Badge Scaling:** Interactive tech badges feature spring-like hover transforms with subtle text-shadow glowing accents.
- **Custom Cyber Toast Notifications:** Non-intrusive floating toast notifications for copy-to-clipboard actions and form submissions.

---

## 📁 Project Architecture

```
Portfolio/
├── index.html        # Main semantic markup & layout structure
├── style.css         # Complete design system, color tokens & responsive rules
├── app.js            # NeuralEngine canvas simulation & spatial slider logic
├── udayimage.jpeg    # Profile visual asset
└── README.md         # Technical documentation
```

---

## 🚀 Running Locally

Because this project relies exclusively on native web standards, it requires no build pipelines, compilers, or package installations.

### 1. Using VS Code Live Server
1. Open the repository in Visual Studio Code.
2. Install the **Live Server** extension.
3. Right-click `index.html` and choose **"Open with Live Server"**.

### 2. Using Python
```bash
# Start a local static server on port 8000
python -m http.server 8000
```
Open `http://localhost:8000` in your web browser.

### 3. Using Node.js
```bash
npx serve .
```

---

## 🎨 Theme Customization

Core colors and theme tokens are centralized at the top of [`style.css`](style.css) via CSS Custom Properties:

```css
:root {
  --bg-space: #030712;                    /* Deep canvas backdrop */
  --bg-card: rgba(15, 23, 42, 0.7);       /* Glassmorphic card surface */
  --accent-cyan: #38bdf8;                 /* Primary cybernetic glow */
  --accent-emerald: #10b981;              /* Secondary accent */
  --accent-purple: #a855f7;               /* Tertiary accent */
  --border-glass: rgba(56, 189, 248, 0.15); /* Glass border reflection */
}
```

---

## 👤 Author & Contact

**Uday Trivedi**  
- **GitHub:** [@Uday-Trivedi](https://github.com/Uday-Trivedi)
- **LinkedIn:** [Uday Trivedi](https://www.linkedin.com/in/uday-trivedi-2b62a7293)
- **Email:** [udaytrivedi0012@gmail.com](mailto:udaytrivedi0012@gmail.com)

---

<p align="center">
  Crafted with Vanilla Web Technologies &bull; &copy; 2025–2026 Uday Trivedi
</p>
