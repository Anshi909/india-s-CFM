
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


// js/active-nav.js
document.addEventListener('DOMContentLoaded', () => {
    const currentPath = window.location.pathname.split('/').pop();
    const navLinks = document.querySelectorAll('nav ul li a');

    navLinks.forEach(link => {
        const linkPath = link.href.split('/').pop();
        if (linkPath === currentPath) {
            link.classList.add('active-nav');
        }
    });
});


document.addEventListener('DOMContentLoaded', () => {
    // Sample data - replace with your actual data
    const stateEmissions = {
        "Delhi": 2500,
        "Maharashtra": 5200,
        "Tamil Nadu": 3100,
        "Uttar Pradesh": 4800,
        "Karnataka": 3600,
        "Gujarat": 4300,
        "West Bengal": 3900,
        "Rajasthan": 3000,
        "Bihar": 2700,
        "Kerala": 2200,
        "Punjab": 2500,
        "Andhra Pradesh": 3300,
        "Odisha": 3800
    };

    const districtEmissions = {
        "Delhi": {
            "New Delhi": 800,
            "East Delhi": 600,
            "North Delhi": 700
        },
        "Maharashtra": {
            "Mumbai": 2200,
            "Pune": 1800,
            "Nagpur": 1200
        },
        "Tamil Nadu": {
            "Chennai": 1300,
            "Coimbatore": 1100,
            "Madurai": 700
        },
        "Uttar Pradesh": {
            "Lucknow": 1600,
            "Kanpur": 1500,
            "Varanasi": 1700
        },
        "Karnataka": {
            "Bengaluru": 2000,
            "Mysuru": 800,
            "Hubli": 800
        },
        "Gujarat": {
            "Ahmedabad": 1800,
            "Surat": 1500,
            "Vadodara": 1000
        },
        "West Bengal": {
            "Kolkata": 1700,
            "Howrah": 1200,
            "Durgapur": 1000
        },
        "Rajasthan": {
            "Jaipur": 1200,
            "Jodhpur": 1000,
            "Udaipur": 800
        },
        "Bihar": {
            "Patna": 1000,
            "Gaya": 900,
            "Muzaffarpur": 800
        },
        "Kerala": {
            "Thiruvananthapuram": 900,
            "Kochi": 800,
            "Kozhikode": 500
        },
        "Punjab": {
            "Ludhiana": 900,
            "Amritsar": 800,
            "Jalandhar": 800
        },
        "Andhra Pradesh": {
            "Visakhapatnam": 1300,
            "Vijayawada": 1100,
            "Tirupati": 900
        },
        "Odisha": {
        "Bhubaneswar": 1500,
        "Cuttack": 1200,
        "Puri": 900,
        "Rourkela": 1100,
        "Sambalpur": 800
        }
    };

    const vehicleEmissions = {
        "bike": 0.12,
        "car": 0.27,
        "truck": 0.8,
        "bus": 0.3,
        "cycle": 0,
        "walking": 0
    };

    // Initialize chart - creates a chart using Chart.js library
    const ctx = document.getElementById('emissionChart').getContext('2d');
    let emissionChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: [],
            datasets: [{
                label: 'CO2 Emissions (tons/year)',
                data: [],
                backgroundColor: 'rgba(54, 162, 235, 0.7)',
                borderColor: 'rgb(231, 24, 24)',
                borderWidth: 1
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    labels: {
                        color: '#ffffff' // White font for legend
                    }
                }
            },
            scales: {
                x: {
                    ticks: {
                        color: '#ffffff' // White font for x-axis
                    },
                    title: {
                        display: true,
                        text: 'Category',
                        color: '#ffffff'
                    }
                },
                y: {
                    beginAtZero: true,
                    ticks: {
                        color: '#ffffff' // White font for y-axis
                    },
                    title: {
                        display: true,
                        text: 'CO2 Emissions (tons/year)',
                        color: '#ffffff'
                    }
                }
            }
        }
    });

    // Function to update the chart data based on selections
    function updateChart() {
        const state = document.getElementById('state').value;
        const district = document.getElementById('district').value;
        const emissionValue = document.getElementById('emission-value');
        const chartContainer = document.querySelector('.chart-container');

        let labels = [];
        let data = [];

        if (state) {
            chartContainer.classList.add('visible'); // Show chart when state is selected

            if (!district) {
                // Show all states for comparison
                labels = Object.keys(stateEmissions);
                data = labels.map(label => stateEmissions[label]);
                emissionValue.textContent = stateEmissions[state];
            } else {
                // Show districts within selected state
                labels = Object.keys(districtEmissions[state]);
                data = labels.map(label => districtEmissions[state][label]);
                emissionValue.textContent = districtEmissions[state][district];
            }
        } else {
            // No state selected - hide chart
            chartContainer.classList.remove('visible');
            emissionValue.textContent = '0';
            return; // Exit without updating chart data
        }

        emissionChart.data.labels = labels;
        emissionChart.data.datasets[0].data = data;
        emissionChart.update();
    }

    // Function to populate the district dropdown based on the selected state
    function populateDistricts() {
        const stateSelect = document.getElementById('state');
        const districtSelect = document.getElementById('district');
        districtSelect.innerHTML = '<option value="">--Select a District--</option>';

        if (stateSelect.value && districtEmissions[stateSelect.value]) {
            Object.keys(districtEmissions[stateSelect.value]).forEach(district => {
                const option = document.createElement('option');
                option.value = district;
                option.textContent = district;
                districtSelect.appendChild(option);
            });
        }
    }

    // Add event listeners
    document.getElementById('vehicle').addEventListener('change', function () {
        const vehicleEmissionValue = document.getElementById('vehicle-emission-value');
        if (this.value && vehicleEmissions[this.value] !== undefined) {
            vehicleEmissionValue.textContent = vehicleEmissions[this.value];
        } else {
            vehicleEmissionValue.textContent = '0';
        }
    });

    // Get the state select element
    const stateSelect = document.getElementById('state');

    // Update districts when state changes
    stateSelect.addEventListener('change', function () {
        populateDistricts();
        updateChart();
    });

    document.getElementById('district').addEventListener('change', updateChart);

    // Populate state dropdown - Initial population of state options
    Object.keys(stateEmissions).forEach(state => {
        const option = document.createElement('option');
        option.value = state;
        option.textContent = state;
        document.getElementById('state').appendChild(option);
    });

    // Initialize with all states data
    updateChart();
});

// Function to load login history from localStorage
function loadLoginHistory() {
    const historyJSON = localStorage.getItem('login_history');
    return historyJSON ? JSON.parse(historyJSON) : [];
}

// Function to display login history in the table
document.addEventListener('DOMContentLoaded', () => {
    const historyTableBody = document.querySelector('.history-table tbody');
    if (historyTableBody) {
        const loginHistory = loadLoginHistory();
        historyTableBody.innerHTML = ''; // Clear existing rows

        if (loginHistory.length === 0) {
            // Changed colspan from 3 to 2 because we now have 2 columns
            const noHistoryRow = document.createElement('tr');
            noHistoryRow.innerHTML = `<td colspan="2" style="text-align: center; color: #aaa;">No login history available.</td>`;
            historyTableBody.appendChild(noHistoryRow);
        } else {
            loginHistory.forEach(entry => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${entry.timestamp}</td>
                    <td>${entry.username}</td>
                    `;
                historyTableBody.appendChild(row);
            });
        }
    }
});
