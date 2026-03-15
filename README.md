<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pressure-Driven Membrane Separation Processes in Biotech</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(229, 231, 235, 0.5);
        }
        .tab-active {
            border-bottom: 4px solid #0F766E;
            color: #0F766E;
            font-weight: 600;
        }
        .tab-inactive {
            border-bottom: 4px solid transparent;
            color: #78716C;
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #F5F5F4;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #D6D3D1;
            border-radius: 4px;
        }
    </style>
</head>
<body class="bg-[#F9FAFB] text-stone-800 font-sans antialiased overflow-x-hidden">

    <!-- Chosen Palette: Warm Neutrals with Teal Accents. Background: #F9FAFB (Gray-50), Surface: White/Glass, Text: Stone-800, Accents: Teal-700 (#0F766E) and Sky-600. -->
    
    <!-- Application Structure Plan: 
         1. Hero Section: Sets the context of membrane separation in biotechnology.
         2. Interactive Membrane Explorer: A tabbed interface allowing users to drill down into RO, UF, MF, and Dialysis individually without scrolling through long text blocks.
         3. Comparative Analytics: Side-by-side Chart.js visualizations (Pressure and Pore Size) to allow direct benchmarking of the processes.
         4. Application Matrix: A grid view mapping specific biotech tasks to the appropriate membrane technology.
         This structure ensures a progressive disclosure of information—moving from high-level understanding to specific details, to comparative analysis, and finally practical application. 
    -->

    <!-- Visualization & Content Choices: 
         - Tabbed Explorer: Goal: Isolate and detail each process. Method: HTML/JS Tabs. Justification: Prevents cognitive overload by showing one process at a time.
         - Pressure Chart: Goal: Compare operating requirements. Method: Chart.js Bar Chart. Justification: Bar charts are optimal for comparing discrete numerical values across categories.
         - Pore Size Chart: Goal: Show retention capabilities. Method: Chart.js Horizontal Bar/Range approximation (Logarithmic X-axis). Justification: Effectively maps the physical size constraints of each membrane type.
         - App Matrix: Goal: Practical application lookup. Method: CSS Grid cards. Justification: Easy scanning for specific use cases.
    -->

    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. HTML/CSS entities and Canvas only. -->

    <nav class="sticky top-0 z-50 glass-panel shadow-sm px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <div class="text-2xl font-bold text-teal-700">⚗️ BioMembrane</div>
            <div class="hidden sm:block text-sm text-stone-500 font-medium">Separation Processes Analysis</div>
        </div>
        <div class="text-sm font-semibold px-4 py-2 bg-stone-100 rounded-full text-stone-600">
            Interactive Report
        </div>
    </nav>

    <header class="max-w-5xl mx-auto px-6 pt-16 pb-12 text-center">
        <h1 class="text-4xl md:text-5xl font-extrabold tracking-tight text-stone-900 mb-6">
            Filtration & Separation in <span class="text-teal-700">Biotechnology</span>
        </h1>
        <p class="text-lg md:text-xl text-stone-600 max-w-3xl mx-auto leading-relaxed">
            A comprehensive overview of Reverse Osmosis (RO), Microfiltration (MF), Ultrafiltration (UF), and Dialysis. Explore how pressure-driven and concentration gradients isolate critical biomolecules, purify water, and enable modern bioprocessing.
        </p>
    </header>

    <main class="max-w-6xl mx-auto px-6 pb-24 space-y-20">

        <section id="explorer" class="scroll-mt-24">
            <div class="mb-8 text-center max-w-2xl mx-auto">
                <h2 class="text-2xl font-bold text-stone-800 mb-3">Membrane Technology Explorer</h2>
                <p class="text-stone-600">Select a process below to investigate its operating principles, physical constraints, and primary functions in a biotechnological setting.</p>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-stone-200 overflow-hidden">
                <div class="flex flex-wrap border-b border-stone-200 bg-stone-50" id="tab-container">
                    <button class="flex-1 py-4 px-6 text-center font-medium tab-active transition-colors duration-200 hover:bg-stone-100" data-target="mf">
                        Microfiltration (MF)
                    </button>
                    <button class="flex-1 py-4 px-6 text-center font-medium tab-inactive transition-colors duration-200 hover:bg-stone-100" data-target="uf">
                        Ultrafiltration (UF)
                    </button>
                    <button class="flex-1 py-4 px-6 text-center font-medium tab-inactive transition-colors duration-200 hover:bg-stone-100" data-target="ro">
                        Reverse Osmosis (RO)
                    </button>
                    <button class="flex-1 py-4 px-6 text-center font-medium tab-inactive transition-colors duration-200 hover:bg-stone-100" data-target="dialysis">
                        Dialysis
                    </button>
                </div>

                <div class="p-8 md:p-12 min-h-[400px] flex flex-col md:flex-row gap-8 items-center">
                    <div class="flex-1 space-y-6">
                        <div class="inline-block px-3 py-1 bg-teal-50 text-teal-700 rounded-full text-sm font-bold tracking-wider uppercase" id="panel-badge">
                            Low Pressure
                        </div>
                        <h3 class="text-3xl font-bold text-stone-900" id="panel-title">Microfiltration (MF)</h3>
                        <p class="text-stone-600 text-lg leading-relaxed" id="panel-desc">
                            Microfiltration operates at low pressure to separate suspended particles, large colloids, and cells from dissolved solutes. It acts as a physical sieve, making it the standard for initial clarification steps.
                        </p>
                        <div class="grid grid-cols-2 gap-4 pt-4 border-t border-stone-100">
                            <div>
                                <div class="text-sm text-stone-500 uppercase tracking-wide font-semibold">Pore Size</div>
                                <div class="text-xl font-bold text-stone-800" id="panel-pore">0.1 - 10 µm</div>
                            </div>
                            <div>
                                <div class="text-sm text-stone-500 uppercase tracking-wide font-semibold">Driving Force</div>
                                <div class="text-xl font-bold text-stone-800" id="panel-force">Pressure (0.1 - 2 bar)</div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="w-full md:w-1/3 bg-stone-50 p-6 rounded-xl border border-stone-100">
                        <h4 class="font-bold text-stone-800 mb-4 flex items-center gap-2">
                            <span>🎯</span> Target Retentate
                        </h4>
                        <ul class="space-y-3" id="panel-targets">
                            <li class="flex items-start gap-2 text-stone-600">
                                <span class="text-teal-600 mt-1">✓</span> Intact Cells
                            </li>
                            <li class="flex items-start gap-2 text-stone-600">
                                <span class="text-teal-600 mt-1">✓</span> Bacteria
                            </li>
                            <li class="flex items-start gap-2 text-stone-600">
                                <span class="text-teal-600 mt-1">✓</span> Large Colloids
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section>
            <div class="mb-10 text-center max-w-2xl mx-auto">
                <h2 class="text-2xl font-bold text-stone-800 mb-3">Comparative Analytics</h2>
                <p class="text-stone-600">Interact with the charts below to contrast the operating constraints of each membrane separation technology. Understanding these metrics is crucial for designing bioprocessing pipelines.</p>
            </div>

            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-stone-200">
                    <h3 class="text-lg font-bold text-stone-800 mb-2">Operating Pressure Range</h3>
                    <p class="text-sm text-stone-500 mb-6">Comparing the mechanical force required (in bars) to drive permeation.</p>
                    <div class="chart-container w-full">
                        <canvas id="pressureChart"></canvas>
                    </div>
                </div>

                <div class="bg-white p-6 rounded-2xl shadow-sm border border-stone-200">
                    <h3 class="text-lg font-bold text-stone-800 mb-2">Pore Size Spectrum</h3>
                    <p class="text-sm text-stone-500 mb-6">Logarithmic scale (µm) showing what particles are retained.</p>
                    <div class="chart-container w-full">
                        <canvas id="poreSizeChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <section class="bg-teal-900 text-teal-50 p-8 md:p-12 rounded-3xl relative overflow-hidden">
            <div class="absolute top-0 right-0 p-12 opacity-10 text-9xl pointer-events-none">🔬</div>
            
            <div class="relative z-10">
                <div class="max-w-2xl mb-10">
                    <h2 class="text-2xl font-bold text-white mb-3">Biotechnological Applications Matrix</h2>
                    <p class="text-teal-200">A guide to selecting the correct membrane process based on standard biomanufacturing use cases.</p>
                </div>

                <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="bg-teal-800/50 p-5 rounded-xl border border-teal-700 hover:bg-teal-800 transition-colors">
                        <div class="text-3xl mb-3">🦠</div>
                        <h4 class="font-bold text-white mb-2">Cell Harvesting</h4>
                        <p class="text-sm text-teal-200 mb-4">Removing fermentation broth from intact cells.</p>
                        <div class="inline-block px-2 py-1 bg-teal-950 text-teal-300 text-xs font-bold rounded">Primary: MF</div>
                    </div>

                    <div class="bg-teal-800/50 p-5 rounded-xl border border-teal-700 hover:bg-teal-800 transition-colors">
                        <div class="text-3xl mb-3">🧬</div>
                        <h4 class="font-bold text-white mb-2">Protein Concentration</h4>
                        <p class="text-sm text-teal-200 mb-4">Reducing volume to increase antibody/enzyme titer.</p>
                        <div class="inline-block px-2 py-1 bg-teal-950 text-teal-300 text-xs font-bold rounded">Primary: UF</div>
                    </div>

                    <div class="bg-teal-800/50 p-5 rounded-xl border border-teal-700 hover:bg-teal-800 transition-colors">
                        <div class="text-3xl mb-3">💧</div>
                        <h4 class="font-bold text-white mb-2">WFI Generation</h4>
                        <p class="text-sm text-teal-200 mb-4">Water for Injection production (ultrapure water).</p>
                        <div class="inline-block px-2 py-1 bg-teal-950 text-teal-300 text-xs font-bold rounded">Primary: RO</div>
                    </div>

                    <div class="bg-teal-800/50 p-5 rounded-xl border border-teal-700 hover:bg-teal-800 transition-colors">
                        <div class="text-3xl mb-3">🧪</div>
                        <h4 class="font-bold text-white mb-2">Buffer Exchange</h4>
                        <p class="text-sm text-teal-200 mb-4">Swapping salts without altering protein concentration.</p>
                        <div class="inline-block px-2 py-1 bg-teal-950 text-teal-300 text-xs font-bold rounded">Primary: Dialysis / UF</div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="border-t border-stone-200 bg-white py-8 text-center text-stone-500 text-sm">
        <p>Interactive Architecture & Analysis Model &copy; 2026</p>
        <p class="mt-2 text-stone-400">Data synthesized from standardized biotechnological separation principles.</p>
    </footer>

    <script>
        const membraneData = {
            mf: {
                title: "Microfiltration (MF)",
                badge: "Low Pressure",
                desc: "Microfiltration operates at low pressure to separate suspended particles, large colloids, and cells from dissolved solutes. It acts as a physical sieve, making it the standard for initial clarification steps.",
                pore: "0.1 - 10 µm",
                force: "Pressure (0.1 - 2 bar)",
                targets: ["Intact Cells", "Bacteria", "Large Colloids", "Cell Debris"]
            },
            uf: {
                title: "Ultrafiltration (UF)",
                badge: "Medium Pressure",
                desc: "Ultrafiltration uses highly porous membranes to separate molecules based on weight. It is extensively used for fractionating macromolecules, concentrating proteins, and performing diafiltration.",
                pore: "0.001 - 0.1 µm",
                force: "Pressure (1 - 10 bar)",
                targets: ["Proteins & Enzymes", "Viruses", "Endotoxins", "Macromolecules"]
            },
            ro: {
                title: "Reverse Osmosis (RO)",
                badge: "High Pressure",
                desc: "Reverse Osmosis forces solvent through a semi-permeable membrane against a concentration gradient. It retains almost all dissolved species, making it critical for generating ultrapure pharmaceutical water.",
                pore: "< 0.001 µm",
                force: "Pressure (15 - 80+ bar)",
                targets: ["Monovalent Ions", "Salts", "Sugars", "Small Aqueous Molecules"]
            },
            dialysis: {
                title: "Dialysis",
                badge: "Gradient Driven",
                desc: "Unlike RO/UF/MF, Dialysis is primarily driven by concentration gradients rather than hydrostatic pressure. Solutes diffuse across the membrane from high to low concentration. Used widely for desalting.",
                pore: "0.001 - 0.01 µm",
                force: "Concentration Gradient",
                targets: ["Small Salts (to permeate)", "Buffer Ions (to permeate)", "Retains Proteins"]
            }
        };

        const tabs = document.querySelectorAll('#tab-container button');
        const badge = document.getElementById('panel-badge');
        const title = document.getElementById('panel-title');
        const desc = document.getElementById('panel-desc');
        const pore = document.getElementById('panel-pore');
        const force = document.getElementById('panel-force');
        const targetsList = document.getElementById('panel-targets');

        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                tabs.forEach(t => {
                    t.classList.remove('tab-active');
                    t.classList.add('tab-inactive');
                });
                
                tab.classList.add('tab-active');
                tab.classList.remove('tab-inactive');

                const key = tab.getAttribute('data-target');
                const data = membraneData[key];

                badge.textContent = data.badge;
                title.textContent = data.title;
                desc.textContent = data.desc;
                pore.textContent = data.pore;
                force.textContent = data.force;

                targetsList.innerHTML = '';
                data.targets.forEach(target => {
                    const li = document.createElement('li');
                    li.className = "flex items-start gap-2 text-stone-600";
                    li.innerHTML = `<span class="text-teal-600 mt-1">✓</span> ${target}`;
                    targetsList.appendChild(li);
                });
                
                badge.animate([{opacity: 0, transform: 'translateY(5px)'}, {opacity: 1, transform: 'translateY(0)'}], {duration: 300, fill: 'forwards'});
                title.animate([{opacity: 0}, {opacity: 1}], {duration: 400});
                desc.animate([{opacity: 0}, {opacity: 1}], {duration: 500});
            });
        });

        Chart.defaults.font.family = "ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif";
        Chart.defaults.color = '#78716C';

        const ctxPressure = document.getElementById('pressureChart').getContext('2d');
        new Chart(ctxPressure, {
            type: 'bar',
            data: {
                labels: ['MF', 'UF', 'RO', 'Dialysis'],
                datasets: [
                    {
                        label: 'Min Pressure (bar)',
                        data: [0.1, 1, 15, 0],
                        backgroundColor: '#99F6E4', 
                        borderRadius: 4
                    },
                    {
                        label: 'Max Pressure (bar)',
                        data: [2, 10, 80, 0.5], 
                        backgroundColor: '#0D9488',
                        borderRadius: 4
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { position: 'bottom' },
                    tooltip: { mode: 'index', intersect: false }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        title: { display: true, text: 'Pressure (Bar)' },
                        grid: { color: '#F5F5F4' }
                    },
                    x: {
                        grid: { display: false }
                    }
                }
            }
        });

        const ctxPore = document.getElementById('poreSizeChart').getContext('2d');
        new Chart(ctxPore, {
            type: 'line', 
            data: {
                labels: ['RO', 'UF / Dialysis', 'MF'],
                datasets: [
                    {
                        label: 'Upper Limit (µm)',
                        data: [0.001, 0.1, 10],
                        borderColor: '#0F766E',
                        backgroundColor: 'rgba(15, 118, 110, 0.5)',
                        borderWidth: 2,
                        pointBackgroundColor: '#0F766E',
                        pointRadius: 6,
                        showLine: false 
                    },
                    {
                        label: 'Lower Limit (µm)',
                        data: [0.0001, 0.001, 0.1],
                        borderColor: '#06B6D4',
                        backgroundColor: 'rgba(6, 182, 212, 0.5)',
                        borderWidth: 2,
                        pointBackgroundColor: '#06B6D4',
                        pointRadius: 6,
                        showLine: false
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                indexAxis: 'y', 
                plugins: {
                    legend: { position: 'bottom' },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                return context.dataset.label + ': ' + context.parsed.x + ' µm';
                            }
                        }
                    }
                },
                scales: {
                    x: {
                        type: 'logarithmic',
                        title: { display: true, text: 'Pore Size (µm) - Log Scale' },
                        grid: { color: '#F5F5F4' },
                        min: 0.0001,
                        max: 100
                    },
                    y: {
                        grid: { display: false }
                    }
                }
            }
        });

    </script>
</body>
</html>
