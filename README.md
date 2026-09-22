Diallo-TRADING
Journal de trading interactif et gestionnaire de capital avec simulateur 90 jours et statistiques de performance.


<!DOCTYPE html>
<html lang="fr" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diallo TRADING - Dashboard & Journal Modern</title>
    
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        obsidian: '#0A0D14',
                        cardBg: 'rgba(15, 23, 42, 0.65)',
                        borderGlass: 'rgba(255, 255, 255, 0.08)',
                        neonEmerald: '#00F59B',
                        neonCyan: '#00E5FF',
                        neonRose: '#FF3B6B',
                        neonGold: '#FFB800'
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        mono: ['JetBrains Mono', 'Fira Code', 'monospace']
                    },
                    boxShadow: {
                        'neon-glow': '0 0 25px -5px rgba(0, 245, 155, 0.25)',
                        'cyan-glow': '0 0 25px -5px rgba(0, 229, 255, 0.25)',
                        'rose-glow': '0 0 25px -5px rgba(255, 59, 107, 0.25)'
                    }
                }
            }
        }
    </script>
    
    <!-- Google Fonts & Font Awesome Icons -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <style>
        body {
            background-color: #06080E;
            background-image: 
                radial-gradient(at 0% 0%, rgba(0, 245, 155, 0.08) 0px, transparent 50%),
                radial-gradient(at 100% 0%, rgba(0, 229, 255, 0.06) 0px, transparent 50%),
                radial-gradient(at 50% 100%, rgba(15, 23, 42, 0.8) 0px, transparent 100%);
            background-attachment: fixed;
            font-family: 'Inter', sans-serif;
            color: #E2E8F0;
        }

        /* Glassmorphism Styles */
        .glass-card {
            background: rgba(13, 19, 33, 0.7);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .glass-card-hover {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .glass-card-hover:hover {
            border-color: rgba(0, 245, 155, 0.3);
            transform: translateY(-2px);
            box-shadow: 0 10px 30px -10px rgba(0, 245, 155, 0.15);
        }

        .glass-input {
            background: rgba(8, 13, 23, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: #F8FAFC;
            transition: all 0.2s ease;
        }

        .glass-input:focus {
            outline: none;
            border-color: #00F59B;
            box-shadow: 0 0 12px rgba(0, 245, 155, 0.25);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(6, 8, 14, 0.8);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.15);
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00F59B;
        }

        /* Custom Animations */
        @keyframes pulseGlow {
            0%, 100% { opacity: 0.4; }
            50% { opacity: 0.8; }
        }

        .pulse-glow {
            animation: pulseGlow 4s infinite ease-in-out;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between antialiased selection:bg-emerald-500 selection:text-black">

    <!-- MAIN WRAPPER -->
    <div id="app" class="w-full max-w-[1600px] mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-8">
        
        <!-- HEADER -->
        <header class="glass-card rounded-2xl p-4 md:p-6 relative overflow-hidden">
            <div class="absolute -top-24 -right-24 w-60 h-60 bg-emerald-500/10 rounded-full blur-3xl pointer-events-none pulse-glow"></div>
            <div class="absolute -bottom-24 -left-24 w-60 h-60 bg-cyan-500/10 rounded-full blur-3xl pointer-events-none pulse-glow"></div>
            
            <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-6 relative z-10">
                <!-- Brand Title & Tagline -->
                <div class="flex items-center gap-4">
                    <div class="w-12 h-12 rounded-xl bg-gradient-to-tr from-emerald-500 to-cyan-400 p-[1px] shadow-neon-glow">
                        <div class="w-full h-full bg-slate-950 rounded-[11px] flex items-center justify-center">
                            <i class="fa-solid me-0.5 fa-chart-line text-xl text-emerald-400"></i>
                        </div>
                    </div>
                    <div>
                        <div class="flex items-center gap-3">
                            <h1 class="text-2xl sm:text-3xl font-extrabold tracking-tight bg-gradient-to-r from-white via-slate-200 to-emerald-400 bg-clip-text text-transparent">
                                Diallo <span class="text-emerald-400 font-mono">TRADING</span>
                            </h1>
                            <span class="px-2.5 py-0.5 text-xs font-semibold uppercase tracking-wider rounded-full bg-emerald-500/10 text-emerald-400 border border-emerald-500/30">
                                PRO v2.5
                            </span>
                        </div>
                        <p class="text-xs sm:text-sm text-slate-400 mt-0.5 flex items-center gap-2">
                            <span>Bienvenue, <strong class="text-slate-200 font-medium">Diallo AMADOU</strong></span>
                            <span class="inline-block w-1.5 h-1.5 rounded-full bg-emerald-400 animate-ping"></span>
                            <span class="text-xs text-slate-500">Suivi & Performance en temps réel</span>
                        </p>
                    </div>
                </div>

                <!-- Navigation Tabs & Actions -->
                <div class="flex flex-wrap items-center justify-between lg:justify-end gap-3">
                    <nav class="flex p-1 bg-slate-950/80 rounded-xl border border-white/10 gap-1">
                        <button id="nav-dashboard" onclick="switchTab('dashboard')" class="nav-tab px-4 py-2 text-xs sm:text-sm font-medium rounded-lg transition-all text-emerald-400 bg-emerald-500/15 border border-emerald-500/30 flex items-center gap-2">
                            <i class="fa-solid fa-gauge-high"></i> Tableau de Bord
                        </button>
                        <button id="nav-journal" onclick="switchTab('journal')" class="nav-tab px-4 py-2 text-xs sm:text-sm font-medium text-slate-400 hover:text-white rounded-lg transition-all flex items-center gap-2">
                            <i class="fa-solid fa-book-bookmark"></i> Journal
                        </button>
                        <button id="nav-plan90" onclick="switchTab('plan90')" class="nav-tab px-4 py-2 text-xs sm:text-sm font-medium text-slate-400 hover:text-white rounded-lg transition-all flex items-center gap-2">
                            <i class="fa-solid fa-bullseye"></i> Plan 90 Jours
                        </button>
                    </nav>

                    <div class="flex items-center gap-2">
                        <button onclick="exportData()" title="Exporter en JSON" class="px-3 py-2 bg-slate-900/90 hover:bg-slate-800 text-slate-300 hover:text-white text-xs font-medium rounded-xl border border-white/10 transition-all flex items-center gap-1.5 shadow-sm">
                            <i class="fa-solid fa-download text-emerald-400"></i> <span class="hidden sm:inline">Exporter</span>
                        </button>
                        <label title="Importer un fichier JSON" class="px-3 py-2 bg-slate-900/90 hover:bg-slate-800 text-slate-300 hover:text-white text-xs font-medium rounded-xl border border-white/10 transition-all flex items-center gap-1.5 cursor-pointer shadow-sm">
                            <i class="fa-solid fa-upload text-cyan-400"></i> <span class="hidden sm:inline">Importer</span>
                            <input type="file" id="import-file" accept=".json" class="hidden" onchange="importData(event)">
                        </label>
                    </div>
                </div>
            </div>
        </header>

        <!-- METRICS / STAT CARDS GRID -->
        <section class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <!-- Stat 1: Capital Actuel -->
            <div class="glass-card glass-card-hover p-5 rounded-2xl relative overflow-hidden group">
                <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Capital Actuel</span>
                    <div class="w-9 h-9 rounded-xl bg-emerald-500/10 text-emerald-400 flex items-center justify-center border border-emerald-500/20">
                        <i class="fa-solid fa-wallet"></i>
                    </div>
                </div>
                <div class="mt-3">
                    <div id="stat-capital" class="text-2xl sm:text-3xl font-extrabold font-mono text-white tracking-tight">$10,000.00</div>
                    <p class="text-xs text-slate-400 mt-1 flex items-center gap-1">
                        Initial: <span id="stat-initial-cap" class="text-slate-300 font-mono">$10,000.00</span>
                    </p>
                </div>
                <div class="absolute bottom-0 left-0 right-0 h-1 bg-gradient-to-r from-emerald-500 to-teal-400 opacity-80"></div>
            </div>

            <!-- Stat 2: Profit / Perte Total -->
            <div class="glass-card glass-card-hover p-5 rounded-2xl relative overflow-hidden group">
                <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Profit / Perte Total</span>
                    <div id="stat-pnl-icon-bg" class="w-9 h-9 rounded-xl bg-emerald-500/10 text-emerald-400 flex items-center justify-center border border-emerald-500/20">
                        <i id="stat-pnl-icon" class="fa-solid fa-chart-line"></i>
                    </div>
                </div>
                <div class="mt-3">
                    <div id="stat-pnl" class="text-2xl sm:text-3xl font-extrabold font-mono text-emerald-400 tracking-tight">+$0.00</div>
                    <p id="stat-pnl-percent" class="text-xs text-emerald-400 font-medium mt-1 flex items-center gap-1">
                        +0.00%
                    </p>
                </div>
                <div id="stat-pnl-bar" class="absolute bottom-0 left-0 right-0 h-1 bg-emerald-500 opacity-80"></div>
            </div>

            <!-- Stat 3: Win Rate -->
            <div class="glass-card glass-card-hover p-5 rounded-2xl relative overflow-hidden group">
                <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Taux de Réussite</span>
                    <div class="w-9 h-9 rounded-xl bg-cyan-500/10 text-cyan-400 flex items-center justify-center border border-cyan-500/20">
                        <i class="fa-solid fa-trophy"></i>
                    </div>
                </div>
                <div class="mt-3">
                    <div id="stat-winrate" class="text-2xl sm:text-3xl font-extrabold font-mono text-white tracking-tight">0.0%</div>
                    <div class="flex items-center gap-2 mt-1 text-xs font-mono">
                        <span id="stat-wins" class="text-emerald-400">0W</span>
                        <span class="text-slate-600">/</span>
                        <span id="stat-losses" class="text-rose-400">0L</span>
                        <span class="text-slate-600">/</span>
                        <span id="stat-neutrals" class="text-slate-400">0N</span>
                    </div>
                </div>
                <div class="absolute bottom-0 left-0 right-0 h-1 bg-gradient-to-r from-cyan-500 to-blue-500 opacity-80"></div>
            </div>

            <!-- Stat 4: Total Trades -->
            <div class="glass-card glass-card-hover p-5 rounded-2xl relative overflow-hidden group">
                <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Total Enregistrés</span>
                    <div class="w-9 h-9 rounded-xl bg-purple-500/10 text-purple-400 flex items-center justify-center border border-purple-500/20">
                        <i class="fa-solid fa-list-check"></i>
                    </div>
                </div>
                <div class="mt-3">
                    <div id="stat-total-trades" class="text-2xl sm:text-3xl font-extrabold font-mono text-white tracking-tight">0</div>
                    <p class="text-xs text-slate-400 mt-1 flex items-center gap-1">
                        Jours tradés: <span id="stat-days-traded" class="text-slate-200 font-mono">0</span>
                    </p>
                </div>
                <div class="absolute bottom-0 left-0 right-0 h-1 bg-gradient-to-r from-purple-500 to-indigo-500 opacity-80"></div>
            </div>
        </section>

        <!-- VIEW SECTION 1: DASHBOARD (Default) -->
        <div id="tab-dashboard" class="tab-content space-y-6">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                
                <!-- Trade Logging Form (5 Cols) -->
                <div class="lg:col-span-5 glass-card rounded-2xl p-6 relative">
                    <div class="flex items-center justify-between pb-4 mb-5 border-b border-white/10">
                        <h2 class="text-lg font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-pen-to-square text-emerald-400"></i>
                            <span id="form-title">Enregistrer un Trade</span>
                        </h2>
                        <button id="cancel-edit-btn" onclick="resetForm()" class="hidden text-xs text-slate-400 hover:text-rose-400 transition-colors">
                            <i class="fa-solid fa-xmark"></i> Annuler Modif
                        </button>
                    </div>

                    <form id="trade-form" onsubmit="handleTradeSubmit(event)" class="space-y-4">
                        <input type="hidden" id="trade-edit-id" value="">
                        
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">Date</label>
                                <input type="date" id="trade-date" required class="w-[#100%] glass-input rounded-xl px-3.5 py-2.5 text-xs text-slate-200 focus:outline-none">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">Stratégie</label>
                                <select id="trade-strategy" required class="w-full glass-input rounded-xl px-3.5 py-2.5 text-xs text-slate-200 focus:outline-none">
                                    <option value="SMC / ICT" class="bg-slate-900">SMC / ICT</option>
                                    <option value="Breakout" class="bg-slate-900">Breakout</option>
                                    <option value="Pullback Trend" class="bg-slate-900">Pullback Trend</option>
                                    <option value="Scalping" class="bg-slate-900">Scalping</option>
                                    <option value="Reversal" class="bg-slate-900">Reversal</option>
                                    <option value="Autre" class="bg-slate-900">Autre</option>
                                </select>
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">Capital Départ ($)</label>
                                <input type="number" step="0.01" id="trade-initial-cap" required readonly class="w-full glass-input rounded-xl px-3.5 py-2.5 text-xs font-mono text-slate-400 bg-slate-950/50 cursor-not-allowed">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">Résultat PnL ($)</label>
                                <input type="number" step="0.01" id="trade-pnl" placeholder="ex: +250 ou -100" required oninput="calculateFinalCapital()" class="w-full glass-input rounded-xl px-3.5 py-2.5 text-xs font-mono text-slate-200">
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">Capital Final ($)</label>
                                <input type="number" step="0.01" id="trade-final-cap" readonly class="w-full glass-input rounded-xl px-3.5 py-2.5 text-xs font-mono text-emerald-400 bg-slate-950/50 font-bold">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-300 mb-1.5">Statut</label>
                                <select id="trade-status" required class="w-full glass-input rounded-xl px-3.5 py-2.5 text-xs text-slate-200 focus:outline-none">
                                    <option value="GAIN" class="bg-slate-900 text-emerald-400">GAIN (WIN)</option>
                                    <option value="PERTE" class="bg-slate-900 text-rose-400">PERTE (LOSS)</option>
                                    <option value="NEUTRE" class="bg-slate-900 text-slate-400">NEUTRE (BE)</option>
                                </select>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1.5">Notes & Remarques (Optionnel)</label>
                            <textarea id="trade-notes" rows="3" placeholder="Configuration, émotions, paire de devises, risque RR..." class="w-full glass-input rounded-xl px-3.5 py-2.5 text-xs text-slate-200 resize-none"></textarea>
                        </div>

                        <button type="submit" id="submit-trade-btn" class="w-full py-3 bg-gradient-to-r from-emerald-500 to-teal-500 hover:from-emerald-400 hover:to-teal-400 text-slate-950 font-bold text-xs uppercase tracking-wider rounded-xl shadow-neon-glow transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-plus"></i> Ajouter au Journal
                        </button>
                    </form>
                </div>

                <!-- Dynamic Evolution Chart (7 Cols) -->
                <div class="lg:col-span-7 glass-card rounded-2xl p-6 flex flex-col justify-between">
                    <div class="flex items-center justify-between pb-4 mb-4 border-b border-white/10">
                        <div class="flex items-center gap-2">
                            <i class="fa-solid fa-chart-area text-cyan-400"></i>
                            <h2 class="text-lg font-bold text-white">Évolution du Capital</h2>
                        </div>
                        <span class="text-xs text-slate-400 bg-slate-900 px-3 py-1 rounded-full border border-white/5 font-mono">
                            Temps réel
                        </span>
                    </div>

                    <div class="relative w-full h-[320px] sm:h-[360px] flex-1">
                        <canvas id="capitalChart"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- VIEW SECTION 2: DETAILED JOURNAL TABLE (Hidden by default) -->
        <div id="tab-journal" class="tab-content hidden space-y-4">
            <div class="glass-card rounded-2xl p-6">
                
                <!-- Table Controls Header -->
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-6 pb-4 border-b border-white/10">
                    <div>
                        <h2 class="text-lg font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-table-list text-emerald-400"></i>
                            Historique Complet des Trades
                        </h2>
                        <p class="text-xs text-slate-400 mt-0.5">Consultez, filtrez et gérez vos transactions passées.</p>
                    </div>

                    <div class="flex flex-wrap items-center gap-3">
                        <!-- Search input -->
                        <div class="relative">
                            <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-xs text-slate-400"></i>
                            <input type="text" id="journal-search" placeholder="Rechercher par note, date..." oninput="filterJournalTable()" class="glass-input rounded-xl pl-9 pr-3 py-2 text-xs text-slate-200 w-48 sm:w-64">
                        </div>

                        <!-- Filter Status -->
                        <select id="journal-filter-status" onchange="filterJournalTable()" class="glass-input rounded-xl px-3 py-2 text-xs text-slate-200">
                            <option value="ALL" class="bg-slate-900">Tous les résultats</option>
                            <option value="GAIN" class="bg-slate-900">Gains uniquement</option>
                            <option value="PERTE" class="bg-slate-900">Pertes uniquement</option>
                            <option value="NEUTRE" class="bg-slate-900">Neutres uniquement</option>
                        </select>

                        <!-- Clear All -->
                        <button onclick="confirmClearAllTrades()" class="px-3 py-2 bg-rose-500/10 hover:bg-rose-500/20 text-rose-400 text-xs font-semibold rounded-xl border border-rose-500/20 transition-all flex items-center gap-1.5">
                            <i class="fa-solid fa-trash-can"></i> Réinitialiser
                        </button>
                    </div>
                </div>

                <!-- Trades Table -->
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="border-b border-white/10 text-[11px] font-semibold uppercase tracking-wider text-slate-400 bg-slate-950/40">
                                <th class="py-3 px-4 rounded-l-xl"># Jour</th>
                                <th class="py-3 px-4">Date</th>
                                <th class="py-3 px-4 font-mono">Cap. Initial</th>
                                <th class="py-3 px-4 font-mono">PnL ($)</th>
                                <th class="py-3 px-4 font-mono">Cap. Final</th>
                                <th class="py-3 px-4">Stratégie</th>
                                <th class="py-3 px-4">Statut</th>
                                <th class="py-3 px-4">Notes</th>
                                <th class="py-3 px-4 text-right rounded-r-xl">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="journal-table-body" class="divide-y divide-white/5 text-xs text-slate-300">
                            <!-- Dynamic Content Rendered Here -->
                        </tbody>
                    </table>
                </div>

                <!-- Empty State Indicator -->
                <div id="journal-empty-state" class="py-12 text-center text-slate-500 hidden">
                    <i class="fa-solid fa-folder-open text-4xl mb-3 opacity-40"></i>
                    <p class="text-sm font-medium">Aucun trade n'a encore été enregistré.</p>
                    <p class="text-xs mt-1">Utilisez le Tableau de bord pour commencer votre suivi.</p>
                </div>
            </div>
        </div>

        <!-- VIEW SECTION 3: 90-DAY PLAN SIMULATOR (Hidden by default) -->
        <div id="tab-plan90" class="tab-content hidden space-y-6">
            <!-- Simulator Controls -->
            <div class="glass-card rounded-2xl p-6">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-6 pb-6 border-b border-white/10">
                    <div>
                        <h2 class="text-lg font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-calculator text-cyan-400"></i>
                            Simulateur de Croissance Composée (90 Jours)
                        </h2>
                        <p class="text-xs text-slate-400 mt-0.5">Projetez l'évolution théorique de votre capital grâce aux intérêts composés.</p>
                    </div>

                    <!-- Simulator Inputs -->
                    <div class="flex flex-wrap items-center gap-4">
                        <div>
                            <label class="block text-[11px] font-semibold uppercase text-slate-400 mb-1">Capital Initial ($)</label>
                            <input type="number" id="sim-start-cap" value="10000" class="glass-input rounded-xl px-3.5 py-2 text-xs font-mono text-emerald-400 font-bold w-32">
                        </div>
                        <div>
                            <label class="block text-[11px] font-semibold uppercase text-slate-400 mb-1">Objectif/Jour (%)</label>
                            <input type="number" step="0.1" id="sim-daily-rate" value="2.0" class="glass-input rounded-xl px-3.5 py-2 text-xs font-mono text-cyan-400 font-bold w-24">
                        </div>
                        <div class="self-end">
                            <button onclick="calculate90DayPlan()" class="px-5 py-2.5 bg-gradient-to-r from-cyan-500 to-blue-500 hover:from-cyan-400 hover:to-blue-400 text-slate-950 font-bold text-xs uppercase tracking-wider rounded-xl shadow-cyan-glow transition-all flex items-center gap-2">
                                <i class="fa-solid fa-rotate"></i> Recalculer
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Simulation Summary Header -->
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mt-6">
                    <div class="p-4 rounded-xl bg-slate-950/60 border border-white/5">
                        <span class="text-xs text-slate-400">Capital Cible au Jour 90</span>
                        <div id="sim-final-target" class="text-2xl font-extrabold font-mono text-emerald-400 mt-1">$59,431.33</div>
                    </div>
                    <div class="p-4 rounded-xl bg-slate-950/60 border border-white/5">
                        <span class="text-xs text-slate-400">Profit Théorique Total</span>
                        <div id="sim-total-profit" class="text-2xl font-extrabold font-mono text-cyan-400 mt-1">+$49,431.33</div>
                    </div>
                    <div class="p-4 rounded-xl bg-slate-950/60 border border-white/5">
                        <span class="text-xs text-slate-400">Multiplicateur de Capital</span>
                        <div id="sim-multiplier" class="text-2xl font-extrabold font-mono text-purple-400 mt-1">5.94x</div>
                    </div>
                </div>
            </div>

            <!-- 90 Days Grid -->
            <div id="plan-90-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-3">
                <!-- Dynamic Day Cards Generated Here -->
            </div>
        </div>

    </div>

    <!-- TOAST NOTIFICATION SYSTEM CONTAINER -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- FOOTER -->
    <footer class="w-full border-t border-white/10 mt-12 py-6 bg-slate-950/80 backdrop-blur-md">
        <div class="max-w-[1600px] mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs text-slate-500">
            <div class="flex items-center gap-2">
                <span class="font-bold text-slate-400">Diallo TRADING</span>
                <span>© 2026 Tous droits réservés.</span>
            </div>
            <p class="text-center sm:text-right text-[11px] max-w-xl text-slate-600">
                Avertissement: Le trading comporte des risques financiers élevés. Ce journal est un outil de suivi personnel et de simulation à but éducatif.
            </p>
        </div>
    </footer>

    <!-- JAVASCRIPT LOGIC & STATE MANAGEMENT -->
    <script>
        // ==========================================
        // STATE MANAGEMENT & LOCAL STORAGE
        // ==========================================
        const INITIAL_CAPITAL = 10000.00;

        let appState = {
            trades: [],
            simStartCap: 10000,
            simDailyRate: 2.0
        };

        let capitalChart = null;

        // Initialize App on DOM Load
        window.addEventListener('DOMContentLoaded', () => {
            loadState();
            setDefaultDate();
            initChart();
            updateAllViews();
        });

        // Load data from LocalStorage
        function loadState() {
            const savedData = localStorage.getItem('diallo_trading_data');
            if (savedData) {
                try {
                    appState = JSON.parse(savedData);
                } catch(e) {
                    console.error("Erreur de chargement LocalStorage:", e);
                }
            }
        }

        // Save state to LocalStorage
        function saveState() {
            localStorage.setItem('diallo_trading_data', JSON.stringify(appState));
        }

        // Default Date Picker to Today
        function setDefaultDate() {
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('trade-date').value = today;
        }

        // ==========================================
        // NAVIGATION TABS
        // ==========================================
        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.add('hidden'));
            document.querySelectorAll('.nav-tab').forEach(btn => {
                btn.classList.remove('text-emerald-400', 'bg-emerald-500/15', 'border', 'border-emerald-500/30');
                btn.classList.add('text-slate-400');
            });

            const selectedContent = document.getElementById(`tab-${tabName}`);
            const selectedBtn = document.getElementById(`nav-${tabName}`);

            if (selectedContent && selectedBtn) {
                selectedContent.classList.remove('hidden');
                selectedBtn.classList.remove('text-slate-400');
                selectedBtn.classList.add('text-emerald-400', 'bg-emerald-500/15', 'border', 'border-emerald-500/30');
            }

            if (tabName === 'plan90') {
                calculate90DayPlan();
            }
        }

        // ==========================================
        // DYNAMIC CALCULATIONS & METRICS
        // ==========================================
        function getCurrentCapital() {
            if (appState.trades.length === 0) return INITIAL_CAPITAL;
            return appState.trades[appState.trades.length - 1].finalCap;
        }

        function calculateFinalCapital() {
            const currentCap = getCurrentCapital();
            const editId = document.getElementById('trade-edit-id').value;
            
            let baseCap = currentCap;
            if (editId) {
                const index = appState.trades.findIndex(t => t.id === editId);
                if (index !== -1) {
                    baseCap = appState.trades[index].initialCap;
                }
            } else {
                document.getElementById('trade-initial-cap').value = currentCap.toFixed(2);
            }

            const pnlVal = parseFloat(document.getElementById('trade-pnl').value) || 0;
            const finalCap = baseCap + pnlVal;
            document.getElementById('trade-final-cap').value = finalCap.toFixed(2);

            // Auto status suggestion
            const statusSelect = document.getElementById('trade-status');
            if (pnlVal > 0) statusSelect.value = 'GAIN';
            else if (pnlVal < 0) statusSelect.value = 'PERTE';
            else statusSelect.value = 'NEUTRE';
        }

        function updateMetrics() {
            const currentCap = getCurrentCapital();
            const totalPnL = currentCap - INITIAL_CAPITAL;
            const pnlPercent = (totalPnL / INITIAL_CAPITAL) * 100;

            const wins = appState.trades.filter(t => t.status === 'GAIN').length;
            const losses = appState.trades.filter(t => t.status === 'PERTE').length;
            const neutrals = appState.trades.filter(t => t.status === 'NEUTRE').length;
            const total = appState.trades.length;

            const winrate = total > 0 ? ((wins / (wins + losses || 1)) * 100).toFixed(1) : "0.0";

            // Unique days count
            const uniqueDays = new Set(appState.trades.map(t => t.date)).size;

            // DOM Updates
            document.getElementById('stat-capital').innerText = `$${currentCap.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
            document.getElementById('stat-initial-cap').innerText = `$${INITIAL_CAPITAL.toLocaleString('en-US', {minimumFractionDigits: 2})}`;

            const pnlElem = document.getElementById('stat-pnl');
            const pnlPercentElem = document.getElementById('stat-pnl-percent');
            const pnlBar = document.getElementById('stat-pnl-bar');

            if (totalPnL >= 0) {
                pnlElem.innerText = `+$${totalPnL.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                pnlElem.className = "text-2xl sm:text-3xl font-extrabold font-mono text-emerald-400 tracking-tight";
                pnlPercentElem.innerText = `+${pnlPercent.toFixed(2)}% de croissance`;
                pnlPercentElem.className = "text-xs text-emerald-400 font-medium mt-1 flex items-center gap-1";
                pnlBar.className = "absolute bottom-0 left-0 right-0 h-1 bg-emerald-500 opacity-80";
            } else {
                pnlElem.innerText = `-$${Math.abs(totalPnL).toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                pnlElem.className = "text-2xl sm:text-3xl font-extrabold font-mono text-rose-400 tracking-tight";
                pnlPercentElem.innerText = `${pnlPercent.toFixed(2)}% de baisse`;
                pnlPercentElem.className = "text-xs text-rose-400 font-medium mt-1 flex items-center gap-1";
                pnlBar.className = "absolute bottom-0 left-0 right-0 h-1 bg-rose-500 opacity-80";
            }

            document.getElementById('stat-winrate').innerText = `${winrate}%`;
            document.getElementById('stat-wins').innerText = `${wins}W`;
            document.getElementById('stat-losses').innerText = `${losses}L`;
            document.getElementById('stat-neutrals').innerText = `${neutrals}N`;

            document.getElementById('stat-total-trades').innerText = total;
            document.getElementById('stat-days-traded').innerText = uniqueDays;

            // Update Initial Cap input in form
            document.getElementById('trade-initial-cap').value = currentCap.toFixed(2);
            document.getElementById('trade-final-cap').value = currentCap.toFixed(2);
        }

        // ==========================================
        // TRADE CRUD OPERATIONS
        // ==========================================
        function handleTradeSubmit(e) {
            e.preventDefault();

            const editId = document.getElementById('trade-edit-id').value;
            const date = document.getElementById('trade-date').value;
            const strategy = document.getElementById('trade-strategy').value;
            const initialCap = parseFloat(document.getElementById('trade-initial-cap').value);
            const pnl = parseFloat(document.getElementById('trade-pnl').value);
            const finalCap = parseFloat(document.getElementById('trade-final-cap').value);
            const status = document.getElementById('trade-status').value;
            const notes = document.getElementById('trade-notes').value;

            if (editId) {
                // Edit existing
                const index = appState.trades.findIndex(t => t.id === editId);
                if (index !== -1) {
                    appState.trades[index] = { id: editId, date, strategy, initialCap, pnl, finalCap, status, notes };
                    showToast('Trade mis à jour avec succès!', 'success');
                }
            } else {
                // Add new trade
                const dayNumber = appState.trades.length + 1;
                const newTrade = {
                    id: 'trade_' + Date.now(),
                    dayNumber,
                    date,
                    strategy,
                    initialCap,
                    pnl,
                    finalCap,
                    status,
                    notes
                };
                appState.trades.push(newTrade);
                showToast('Nouveau trade enregistré!', 'success');
            }

            // Recalculate subsequent trades if edited
            recalculateAllTradesChain();
            saveState();
            resetForm();
            updateAllViews();
        }

        function recalculateAllTradesChain() {
            let runningCap = INITIAL_CAPITAL;
            appState.trades.forEach((trade, idx) => {
                trade.dayNumber = idx + 1;
                trade.initialCap = runningCap;
                trade.finalCap = runningCap + trade.pnl;
                runningCap = trade.finalCap;
            });
        }

        function editTrade(id) {
            const trade = appState.trades.find(t => t.id === id);
            if (!trade) return;

            document.getElementById('trade-edit-id').value = trade.id;
            document.getElementById('trade-date').value = trade.date;
            document.getElementById('trade-strategy').value = trade.strategy;
            document.getElementById('trade-initial-cap').value = trade.initialCap.toFixed(2);
            document.getElementById('trade-pnl').value = trade.pnl;
            document.getElementById('trade-final-cap').value = trade.finalCap.toFixed(2);
            document.getElementById('trade-status').value = trade.status;
            document.getElementById('trade-notes').value = trade.notes || '';

            document.getElementById('form-title').innerText = "Modifier le Trade #" + trade.dayNumber;
            document.getElementById('submit-trade-btn').innerHTML = '<i class="fa-solid fa-floppy-disk"></i> Enregistrer Modifs';
            document.getElementById('cancel-edit-btn').classList.remove('hidden');

            switchTab('dashboard');
        }

        function deleteTrade(id) {
            if (confirm("Voulez-vous vraiment supprimer ce trade ?")) {
                appState.trades = appState.trades.filter(t => t.id !== id);
                recalculateAllTradesChain();
                saveState();
                updateAllViews();
                showToast('Trade supprimé.', 'warning');
            }
        }

        function resetForm() {
            document.getElementById('trade-edit-id').value = '';
            document.getElementById('trade-form').reset();
            setDefaultDate();
            
            document.getElementById('form-title').innerText = "Enregistrer un Trade";
            document.getElementById('submit-trade-btn').innerHTML = '<i class="fa-solid fa-plus"></i> Ajouter au Journal';
            document.getElementById('cancel-edit-btn').classList.add('hidden');

            const currentCap = getCurrentCapital();
            document.getElementById('trade-initial-cap').value = currentCap.toFixed(2);
            document.getElementById('trade-final-cap').value = currentCap.toFixed(2);
        }

        function confirmClearAllTrades() {
            if (confirm("ATTENTION: Êtes-vous sûr de vouloir supprimer TOUT le journal de trading ?")) {
                appState.trades = [];
                saveState();
                updateAllViews();
                showToast('Journal réinitialisé à zéro.', 'danger');
            }
        }

        // ==========================================
        // RENDER JOURNAL TABLE
        // ==========================================
        function renderJournalTable(tradesToRender = appState.trades) {
            const tbody = document.getElementById('journal-table-body');
            const emptyState = document.getElementById('journal-empty-state');
            tbody.innerHTML = '';

            if (tradesToRender.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            tradesToRender.forEach((trade) => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-900/60 transition-colors";

                let statusBadge = '';
                if (trade.status === 'GAIN') {
                    statusBadge = `<span class="px-2.5 py-1 text-[10px] font-bold rounded-md bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">GAIN</span>`;
                } else if (trade.status === 'PERTE') {
                    statusBadge = `<span class="px-2.5 py-1 text-[10px] font-bold rounded-md bg-rose-500/10 text-rose-400 border border-rose-500/20">PERTE</span>`;
                } else {
                    statusBadge = `<span class="px-2.5 py-1 text-[10px] font-bold rounded-md bg-slate-500/10 text-slate-400 border border-slate-500/20">NEUTRE</span>`;
                }

                const pnlClass = trade.pnl > 0 ? 'text-emerald-400 font-bold' : (trade.pnl < 0 ? 'text-rose-400 font-bold' : 'text-slate-400');
                const pnlPrefix = trade.pnl > 0 ? '+' : '';

                tr.innerHTML = `
                    <td class="py-3 px-4 font-mono font-medium text-slate-400">#${trade.dayNumber}</td>
                    <td class="py-3 px-4 text-slate-200">${trade.date}</td>
                    <td class="py-3 px-4 font-mono text-slate-400">$${trade.initialCap.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td class="py-3 px-4 font-mono ${pnlClass}">${pnlPrefix}$${trade.pnl.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td class="py-3 px-4 font-mono font-semibold text-slate-200">$${trade.finalCap.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td class="py-3 px-4">
                        <span class="px-2 py-0.5 text-[10px] rounded bg-slate-800 text-slate-300 border border-white/5 font-mono">
                            ${trade.strategy}
                        </span>
                    </td>
                    <td class="py-3 px-4">${statusBadge}</td>
                    <td class="py-3 px-4 text-slate-400 max-w-xs truncate" title="${trade.notes || '-'}">${trade.notes || '-'}</td>
                    <td class="py-3 px-4 text-right space-x-1">
                        <button onclick="editTrade('${trade.id}')" class="p-1.5 text-slate-400 hover:text-emerald-400 rounded-lg hover:bg-slate-800 transition-all" title="Modifier">
                            <i class="fa-solid fa-pen-to-square"></i>
                        </button>
                        <button onclick="deleteTrade('${trade.id}')" class="p-1.5 text-slate-400 hover:text-rose-400 rounded-lg hover:bg-slate-800 transition-all" title="Supprimer">
                            <i class="fa-solid fa-trash"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function filterJournalTable() {
            const query = document.getElementById('journal-search').value.toLowerCase();
            const statusFilter = document.getElementById('journal-filter-status').value;

            const filtered = appState.trades.filter(trade => {
                const matchesQuery = (trade.notes && trade.notes.toLowerCase().includes(query)) ||
                                     trade.date.includes(query) ||
                                     trade.strategy.toLowerCase().includes(query);

                const matchesStatus = statusFilter === 'ALL' || trade.status === statusFilter;

                return matchesQuery && matchesStatus;
            });

            renderJournalTable(filtered);
        }

        // ==========================================
        // CHART.JS INTEGRATION
        // ==========================================
        function initChart() {
            const ctx = document.getElementById('capitalChart').getContext('2d');
            
            // Gradient fill
            const gradient = ctx.createLinearGradient(0, 0, 0, 300);
            gradient.addColorStop(0, 'rgba(0, 245, 155, 0.35)');
            gradient.addColorStop(1, 'rgba(0, 245, 155, 0.0)');

            capitalChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Départ'],
                    datasets: [{
                        label: 'Capital ($)',
                        data: [INITIAL_CAPITAL],
                        borderColor: '#00F59B',
                        borderWidth: 2.5,
                        backgroundColor: gradient,
                        fill: true,
                        tension: 0.3,
                        pointBackgroundColor: '#00F59B',
                        pointBorderColor: '#0A0D14',
                        pointBorderWidth: 2,
                        pointRadius: 4,
                        pointHoverRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            backgroundColor: 'rgba(10, 13, 20, 0.9)',
                            titleFont: { family: 'Inter', size: 12 },
                            bodyFont: { family: 'JetBrains Mono', size: 13 },
                            borderColor: 'rgba(0, 245, 155, 0.3)',
                            borderWidth: 1,
                            padding: 10,
                            displayColors: false,
                            callbacks: {
                                label: (context) => ` Capital: $${context.parsed.y.toLocaleString('en-US', {minimumFractionDigits: 2})}`
                            }
                        }
                    },
                    scales: {
                        x: {
                            grid: { color: 'rgba(255, 255, 255, 0.05)' },
                            ticks: { color: '#64748B', font: { family: 'Inter', size: 10 } }
                        },
                        y: {
                            grid: { color: 'rgba(255, 255, 255, 0.05)' },
                            ticks: { 
                                color: '#64748B', 
                                font: { family: 'JetBrains Mono', size: 10 },
                                callback: (val) => '$' + val.toLocaleString()
                            }
                        }
                    }
                }
            });
        }

        function updateChart() {
            if (!capitalChart) return;

            const labels = ['Départ', ...appState.trades.map(t => `J${t.dayNumber} (${t.date})`)];
            const data = [INITIAL_CAPITAL, ...appState.trades.map(t => t.finalCap)];

            capitalChart.data.labels = labels;
            capitalChart.data.datasets[0].data = data;
            capitalChart.update();
        }

        // ==========================================
        // 90-DAY COMPOUND SIMULATOR
        // ==========================================
        function calculate90DayPlan() {
            const startCap = parseFloat(document.getElementById('sim-start-cap').value) || INITIAL_CAPITAL;
            const dailyRate = parseFloat(document.getElementById('sim-daily-rate').value) || 2.0;

            const grid = document.getElementById('plan-90-grid');
            grid.innerHTML = '';

            let currentCap = startCap;

            for (let day = 1; day <= 90; day++) {
                const targetProfit = currentCap * (dailyRate / 100);
                const endCap = currentCap + targetProfit;

                // Check if trade for this day exists
                const actualTrade = appState.trades[day - 1];
                let cardBorder = "border-white/5";
                let statusBadge = '';

                if (actualTrade) {
                    if (actualTrade.pnl >= targetProfit) {
                        cardBorder = "border-emerald-500/50 bg-emerald-500/5";
                        statusBadge = `<span class="text-[9px] px-1.5 py-0.5 rounded bg-emerald-500/20 text-emerald-400 font-bold">ATTEINT</span>`;
                    } else if (actualTrade.pnl > 0) {
                        cardBorder = "border-cyan-500/50 bg-cyan-500/5";
                        statusBadge = `<span class="text-[9px] px-1.5 py-0.5 rounded bg-cyan-500/20 text-cyan-400 font-bold">PARTIEL</span>`;
                    } else {
                        cardBorder = "border-rose-500/50 bg-rose-500/5";
                        statusBadge = `<span class="text-[9px] px-1.5 py-0.5 rounded bg-rose-500/20 text-rose-400 font-bold">RATIÉ</span>`;
                    }
                }

                const dayCard = document.createElement('div');
                dayCard.className = `glass-card p-3.5 rounded-xl border ${cardBorder} flex flex-col justify-between hover:border-white/20 transition-all`;
                dayCard.innerHTML = `
                    <div class="flex items-center justify-between mb-2">
                        <span class="text-xs font-bold text-slate-300 font-mono">Jour ${day}</span>
                        ${statusBadge}
                    </div>
                    <div class="space-y-1 font-mono text-[11px]">
                        <div class="flex justify-between text-slate-400">
                            <span>Objectif:</span>
                            <span class="text-cyan-400 font-semibold">+$${targetProfit.toFixed(2)}</span>
                        </div>
                        <div class="flex justify-between text-slate-200 border-t border-white/5 pt-1">
                            <span>Solde Cible:</span>
                            <span class="font-bold text-emerald-400">$${endCap.toFixed(2)}</span>
                        </div>
                    </div>
                `;
                grid.appendChild(dayCard);

                currentCap = endCap;
            }

            // Summary metrics update
            const totalProfit = currentCap - startCap;
            const multiplier = currentCap / startCap;

            document.getElementById('sim-final-target').innerText = `$${currentCap.toLocaleString('en-US', {maximumFractionDigits: 2})}`;
            document.getElementById('sim-total-profit').innerText = `+$${totalProfit.toLocaleString('en-US', {maximumFractionDigits: 2})}`;
            document.getElementById('sim-multiplier').innerText = `${multiplier.toFixed(2)}x`;
        }

        // ==========================================
        // IMPORT / EXPORT DATA
        // ==========================================
        function exportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(appState, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `diallo_trading_backup_${new Date().toISOString().split('T')[0]}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast('Données exportées avec succès.', 'info');
        }

        function importData(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedState = JSON.parse(e.target.result);
                    if (importedState && Array.isArray(importedState.trades)) {
                        appState = importedState;
                        recalculateAllTradesChain();
                        saveState();
                        updateAllViews();
                        showToast('Sauvegarde importée avec succès !', 'success');
                    } else {
                        showToast('Format de fichier JSON invalide.', 'danger');
                    }
                } catch(err) {
                    showToast('Erreur lors de la lecture du fichier.', 'danger');
                }
            };
            reader.readAsText(file);
        }

        // Helper to Refresh Everything
        function updateAllViews() {
            updateMetrics();
            renderJournalTable();
            updateChart();
            if (!document.getElementById('tab-plan90').classList.contains('hidden')) {
                calculate90DayPlan();
            }
        }

        // ==========================================
        // TOAST NOTIFICATIONS
        // ==========================================
        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            
            let bgClass = "bg-slate-900 border-slate-700 text-slate-200";
            let icon = "fa-circle-info text-cyan-400";

            if (type === 'success') {
                bgClass = "bg-slate-950 border-emerald-500/40 text-emerald-300 shadow-neon-glow";
                icon = "fa-circle-check text-emerald-400";
            } else if (type === 'warning') {
                bgClass = "bg-slate-950 border-amber-500/40 text-amber-300";
                icon = "fa-triangle-exclamation text-amber-400";
            } else if (type === 'danger') {
                bgClass = "bg-slate-950 border-rose-500/40 text-rose-300 shadow-rose-glow";
                icon = "fa-circle-xmark text-rose-400";
            }

            toast.className = `pointer-events-auto px-4 py-3 rounded-xl border ${bgClass} text-xs font-medium flex items-center gap-2.5 shadow-2xl transition-all duration-300 transform translate-y-2 opacity-0`;
            toast.innerHTML = `<i class="fa-solid ${icon} text-sm"></i> <span>${message}</span>`;

            container.appendChild(toast);

            // Animate In
            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 10);

            // Auto Remove
            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }
    </script>
</body>
</html>
