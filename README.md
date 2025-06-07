
body {
    margin: 0;
    padding: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #0f2027;
    /* Dark gradient */
    background: linear-gradient(to right, #2c5364, #203a43, #0f2027);
    color: #ffffff !important;
    overflow-x: hidden;
}

header {
    background: rgba(0, 0, 0, 0.6);
    padding: 1rem;
    text-align: center;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.4);
}

header h1 {
    margin: 0;
    font-size: 2rem;
    color: #00d1b2;
}

main {
    padding: 2rem;
    max-width: 1000px;
    margin: auto;
}

.controls {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: space-between;
    margin-bottom: 2rem;
    background: rgba(255, 255, 255, 0.05);
    padding: 1rem;
    border-radius: 12px;
}

.controls label {
    font-weight: bold;
    margin-right: 0.5rem;
}

.controls select {
    padding: 0.5rem;
    border: none;
    border-radius: 6px;
    background-color: #1f2d3d;
    color: white;
    width: 180px;
}

.chart-container {
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    padding: 1rem;
    height: 400px;
    margin-bottom: 2rem;
}

.chart-container canvas {
    width: 100% !important;
    height: 100% !important;
    color: white !important;
}

section {
    background-color: rgba(255, 255, 255, 0.08);
    padding: 1rem;
    margin-top: 1rem;
    border-radius: 10px;
}

h2 {
    color: #00d1b2;
    margin-bottom: 1rem;
    margin-top: 1rem;
}

#emission-value,
#vehicle-emission-value {
    font-weight: bold;
    color: #ffd700;
}

footer {
    text-align: center;
    padding: 1rem;
    background-color: #1a1a1a;
    color: #888;
    margin-top: 2rem;
}

#particles-js {
    position: fixed;
    width: 100%;
    height: 100%;
    z-index: -1;
    top: 0;
    left: 0;
}

/* Basic styling for the navigation bar */
nav {
    background-color: #1f2d3d;
    padding: 1rem 0;
    position: sticky;
    /* Optional: make it stick to the top */
    top: 0;
    z-index: 100;
    /* Ensure it's above other elements */
}

nav ul {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    justify-content: center;
}

nav ul li {
    margin: 0 1rem;
}

nav ul li a {
    color: #ffffff;
    text-decoration: none;
    font-weight: bold;
    transition: color 0.3s ease;
}

nav ul li a:hover {
    color: #00d1b2;
}

/* Style for active navigation link */
nav ul li a.active-nav {
    color: #00ffbf;
    /* Gold-like color for glow */
    text-shadow: 0 0 8px rgba(82, 218, 199, 0.8);
    /* Subtle glow effect */
}
