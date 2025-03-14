<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Magnetized Sand Simulation</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            width: 100%;
            overflow: hidden;
            background-color: #111; /* Dark background for better contrast */
        }

        canvas {
            display: block;
        }

        #resetButton {
            position: absolute;
            top: 20px;
            left: 20px;
            background-color: rgba(194, 178, 128, 0.8);
            color: white;
            font-family: 'Helvetica', sans-serif;
            font-size: 20px;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            z-index: 10;
        }

        #resetButton:hover {
            background-color: rgba(194, 178, 128, 1);
        }
        
        #toggleMode {
            position: absolute;
            top: 20px;
            right: 20px;
            background-color: rgba(194, 178, 128, 0.8);
            color: white;
            font-family: 'Helvetica', sans-serif;
            font-size: 20px;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            z-index: 10;
        }

        #toggleMode:hover {
            background-color: rgba(194, 178, 128, 1);
        }
    </style>
</head>
<body>
    <canvas id="sandCanvas"></canvas>
    <button id="resetButton">Reset Sand</button>
    <button id="toggleMode">Mode: Attract</button>

    <script>
        const canvas = document.getElementById('sandCanvas');
        const ctx = canvas.getContext('2d', { alpha: false }); // Disable alpha for performance
        const resetButton = document.getElementById('resetButton');
        const toggleMode = document.getElementById('toggleMode');
        
        // Set canvas size
        function setCanvasSize() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        setCanvasSize();

        // Performance optimization variables
        const sandParticles = [];
        const particleSize = 1.5; // Smaller particles for better performance
        let particleDensity = 15000; // Adjust based on screen size
        
        // Mouse interaction variables
        let isMousePressed = false;
        let mouseX = 0;
        let mouseY = 0;
        let lastMouseX = 0;
        let lastMouseY = 0;
        let mouseSpeed = 0;
        let attractMode = true; // Default to attract mode
        
        // Sand colors
        const sandColor = 'rgba(214, 198, 148, 0.9)';
        
        // Wind variables
        const baseWindX = 0.1;
        const baseWindY = 0;
        let gustStrengthX = 0;
        let gustStrengthY = 0;
        const gustDuration = 40;
        let gustCounter = 0;
        
        // Grid-based optimization for particle interaction
        const gridCellSize = 50;
        const grid = {};
        
        // Scale particle density based on screen size
        function adjustParticleDensity() {
            const screenArea = canvas.width * canvas.height;
            const baseArea = 1920 * 1080;
            const scaleFactor = Math.min(1.5, Math.max(0.5, screenArea / baseArea));
            return Math.floor(particleDensity * scaleFactor);
        }

        // Generate sand particles
        function generateSand() {
            sandParticles.length = 0;
            const adjustedDensity = adjustParticleDensity();
            
            for (let i = 0; i < adjustedDensity; i++) {
                const x = Math.random() * canvas.width;
                const y = Math.random() * canvas.height;
                sandParticles.push({
                    x,
                    y,
                    vx: 0,
                    vy: 0,
                    mass: Math.random() * 0.5 + 0.5, // Varying mass for more natural movement
                    rotation: Math.random() * Math.PI * 2,
                    color: Math.random() > 0.9 ? 'rgba(255, 240, 200, 0.9)' : sandColor // Occasional highlight particles
                });
            }
        }

        // Update grid system for faster particle lookups
        function updateGrid() {
            // Clear the grid
            for (const key in grid) {
                delete grid[key];
            }
            
            // Assign particles to grid cells
            for (let i = 0; i < sandParticles.length; i++) {
                const particle = sandParticles[i];
                const cellX = Math.floor(particle.x / gridCellSize);
                const cellY = Math.floor(particle.y / gridCellSize);
                const cellKey = `${cellX},${cellY}`;
                
                if (!grid[cellKey]) {
                    grid[cellKey] = [];
                }
                
                grid[cellKey].push(i);
            }
        }

        // Draw sand particles with optimization
        function drawSand() {
            // Clear with solid background instead of clearRect for performance
            ctx.fillStyle = '#111';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw the mouse attraction point when pressed
            if (isMousePressed) {
                ctx.beginPath();
                ctx.arc(mouseX, mouseY, 8, 0, Math.PI * 2);
                ctx.fillStyle = attractMode ? 'rgba(255, 215, 0, 0.6)' : 'rgba(0, 150, 255, 0.6)';
                ctx.fill();
                
                // Add a glow effect
                ctx.beginPath();
                ctx.arc(mouseX, mouseY, 20, 0, Math.PI * 2);
                ctx.fillStyle = attractMode ? 'rgba(255, 215, 0, 0.2)' : 'rgba(0, 150, 255, 0.2)';
                ctx.fill();
            }
            
            // Draw particles with different colors
            for (let i = 0; i < sandParticles.length; i++) {
                const particle = sandParticles[i];
                ctx.beginPath();
                ctx.arc(particle.x, particle.y, particleSize, 0, Math.PI * 2);
                ctx.fillStyle = particle.color;
                ctx.fill();
            }
        }

        // Apply physics to sand particles
        function updateParticles() {
            // Update grid for spatial optimization
            updateGrid();
            
            // Calculate mouse speed for more dynamic interaction
            if (isMousePressed) {
                const dx = mouseX - lastMouseX;
                const dy = mouseY - lastMouseY;
                mouseSpeed = Math.min(15, Math.sqrt(dx*dx + dy*dy));
                lastMouseX = mouseX;
                lastMouseY = mouseY;
            } else {
                mouseSpeed *= 0.95; // Decay when not moving
            }
            
            // Apply physics to each particle
            for (let i = 0; i < sandParticles.length; i++) {
                const particle = sandParticles[i];
                
                // Apply base wind plus any gusts
                particle.vx += (baseWindX + gustStrengthX) * particle.mass;
                particle.vy += (baseWindY + gustStrengthY) * particle.mass;
                
                // Apply mouse interaction if active and close enough
                if (isMousePressed) {
                    const dx = mouseX - particle.x;
                    const dy = mouseY - particle.y;
                    const distanceSquared = dx*dx + dy*dy;
                    const distance = Math.sqrt(distanceSquared);
                    
                    if (distance < 150) {
                        const angle = Math.atan2(dy, dx);
                        const force = (150 - distance) / 10 * (1/particle.mass);
                        
                        if (attractMode) {
                            // Pull particles toward mouse with magnetism effect
                            particle.vx += Math.cos(angle) * force * 0.2;
                            particle.vy += Math.sin(angle) * force * 0.2;
                            
                            // Add small swirl effect for more interesting visual
                            const perpAngle = angle + Math.PI/2;
                            particle.vx += Math.cos(perpAngle) * force * 0.05;
                            particle.vy += Math.sin(perpAngle) * force * 0.05;
                        } else {
                            // Push particles away from mouse
                            particle.vx -= Math.cos(angle) * force * 0.2;
                            particle.vy -= Math.sin(angle) * force * 0.2;
                        }
                    }
                }
                
                // Apply velocity with damping
                particle.x += particle.vx;
                particle.y += particle.vy;
                
                // Apply damping (friction)
                particle.vx *= 0.96;
                particle.vy *= 0.96;
                
                // Wrap around screen edges with momentum preservation
                if (particle.x > canvas.width) {
                    particle.x = 0;
                } else if (particle.x < 0) {
                    particle.x = canvas.width;
                }
                
                if (particle.y > canvas.height) {
                    particle.y = 0;
                } else if (particle.y < 0) {
                    particle.y = canvas.height;
                }
            }
            
            // Update gust counter
            if (gustCounter > 0) {
                gustCounter--;
                // Gradually reduce gust strength
                gustStrengthX *= 0.98;
                gustStrengthY *= 0.98;
            }
        }

        // Create random gusts of wind
        function createGust() {
            if (Math.random() < 0.01 && gustCounter === 0) { // 1% chance per frame
                gustStrengthX = (Math.random() * 2 - 1) * 0.3;
                gustStrengthY = (Math.random() * 2 - 1) * 0.1;
                gustCounter = gustDuration;
            }
        }

        // Animation loop with timing control
        let lastTime = 0;
        const targetFPS = 60;
        const frameTime = 1000 / targetFPS;
        
        function animate(timestamp) {
            // Time-based animation for consistent speed
            const deltaTime = timestamp - lastTime;
            
            if (deltaTime >= frameTime) {
                createGust();
                updateParticles();
                drawSand();
                lastTime = timestamp;
            }
            
            requestAnimationFrame(animate);
        }

        // Handle mouse events
        function handleMouseMove(e) {
            mouseX = e.clientX;
            mouseY = e.clientY;
        }
        
        canvas.addEventListener('mousedown', (e) => {
            isMousePressed = true;
            mouseX = e.clientX;
            mouseY = e.clientY;
            lastMouseX = mouseX;
            lastMouseY = mouseY;
        });
        
        canvas.addEventListener('mouseup', () => {
            isMousePressed = false;
        });
        
        canvas.addEventListener('mouseleave', () => {
            isMousePressed = false;
        });
        
        canvas.addEventListener('mousemove', handleMouseMove);
        
        // Touch events for mobile support
        canvas.addEventListener('touchstart', (e) => {
            e.preventDefault();
            isMousePressed = true;
            mouseX = e.touches[0].clientX;
            mouseY = e.touches[0].clientY;
            lastMouseX = mouseX;
            lastMouseY = mouseY;
        });
        
        canvas.addEventListener('touchend', (e) => {
            e.preventDefault();
            isMousePressed = false;
        });
        
        canvas.addEventListener('touchmove', (e) => {
            e.preventDefault();
            mouseX = e.touches[0].clientX;
            mouseY = e.touches[0].clientY;
        });
        
        // Reset button event
        resetButton.addEventListener('click', generateSand);
        
        // Toggle mode button event
        toggleMode.addEventListener('click', () => {
            attractMode = !attractMode;
            toggleMode.textContent = `Mode: ${attractMode ? 'Attract' : 'Repel'}`;
        });
        
        // Handle window resize
        window.addEventListener('resize', () => {
            setCanvasSize();
            generateSand();
        });
        
        // Initialize and start animation
        generateSand();
        requestAnimationFrame(animate);
    </script>
</body>
</html>