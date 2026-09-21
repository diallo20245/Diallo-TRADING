# Diallo-TRADING
Journal de trading interactif et gestionnaire de capital avec simulateur 90 jours et statistiques de performance.


<!DOCTYPE html>
<html lang="fr" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diallo TRADING - Journal de Trading & Suivi de Capital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkBg: '#0b0f19',
                        cardBg: '#111827',
                        cardBorder: '#1f2937',
                        brandGreen: '#10b981',
                        brandRed: '#ef4444',
                        accentBlue: '#3b82f6'
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background-color: #0b0f19;
            color: #f3f4f6;
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #111827;
        }
        ::-webkit-scrollbar-thumb {
            background: #374151;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #4b5563;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-darkBg text-gray-100">

    <!-- Header -->
    <header class="bg-cardBg border-b border-cardBorder sticky top-0 z-50 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <div class="bg-gradient-to-tr from-blue-600 to-emerald-500 p-2.5 rounded-xl shadow-md">
                    <i class="fa-solid me-1 fa-chart-line text-2xl text-white"></i>
                </div>
                <div>
                    <h1 class="text-2xl font-black tracking-wider text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 via-teal-300 to-blue-500">
                        Diallo TRADING
                    </h1>
                    <p class="text-xs text-gray-400 font-medium">
                        Bienvenue, <span class="text-emerald-400 font-semibold">Diallo AMADOU</span> | Suivi & Performance
                    </p>
                </div>
            </div>

            <!-- Navigation Tabs -->
            <nav class="flex bg-gray-900/80 p-1.5 rounded-xl border border-gray-800 text-sm font-medium">
                <button onclick="switchTab('dashboard')" id="tab-dashboard" class="tab-btn px-4 py-2 rounded-lg transition-all duration-200 text-emerald-400 bg-gray-800 shadow">
                    <i class="fa-solid fa-gauge-high mr-2"></i>Tableau de Bord
                </button>
                <button onclick="switchTab('journal')" id="tab-journal" class="tab-btn px-4 py-2 rounded-lg text-gray-400 hover:text-gray-200 transition-all duration-200">
                    <i class="fa-solid fa-book-bookmark mr-2"></i>Journal
                </button>
                <button onclick="switchTab('plan90')" id="tab-plan90" class="tab-btn px-4 py-2 rounded-lg text-gray-400 hover:text-gray-200 transition-all duration-200">
                    <i class="fa-solid fa-calendar-days mr-2"></i>Plan 90 Jours
                </button>
            </nav>

            <!-- Actions Bar -->
            <div class="flex items-center gap-2">
                <button onclick="exportData()" title="Exporter mes données" class="px-3 py-2 bg-gray-800 hover:bg-gray-700 text-gray-300 rounded-lg text-xs font-semibold flex items-center gap-1.5 border border-gray-700 transition">
                    <i class="fa-solid fa-download text-emerald-400"></i> Exporter
                </button>
                <label title="Importer des données" class="px-3 py-2 bg-gray-800 hover:bg-gray-700 text-gray-300 rounded-lg text-xs font-semibold flex items-center gap-1.5 border border-gray-700 cursor-pointer transition">
                    <i class="fa-solid fa-upload text-blue-400"></i> Importer
                    <input type="file" id="importFile" accept=".json" class="hidden" onchange="importData(event)">
                </label>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">

        <!-- Dashboard Overview Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <div class="bg-cardBg p-5 rounded-2xl border border-cardBorder shadow-sm relative overflow-hidden">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs font-bold uppercase tracking-wider text-gray-400">Capital Actuel</span>
                    <span class="p-2 bg-blue-500/10 text-blue-400 rounded-lg"><i class="fa-solid fa-wallet"></i></span>
                </div>
                <div class="text-3xl font-extrabold text-white" id="stat-capital">$0.00</div>
                <p class="text-xs text-gray-400 mt-2">Départ initial: <span id="stat-initial-cap" class="text-gray-300">$0.00</span></p>
            </div>

            <div class="bg-cardBg p-5 rounded-2xl border border-cardBorder shadow-sm relative overflow-hidden">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs font-bold uppercase tracking-wider text-gray-400">Profit / Perte Total</span>
                    <span id="stat-pnl-icon" class="p-2 bg-emerald-500/10 text-emerald-400 rounded-lg"><i class="fa-solid fa-chart-line"></i></span>
                </div>
                <div class="text-3xl font-extrabold" id="stat-total-pnl">$0.00</div>
                <p class="text-xs text-gray-400 mt-2">Rendement: <span id="stat-roi" class="font-bold">0%</span></p>
            </div>

            <div class="bg-cardBg p-5 rounded-2xl border border-cardBorder shadow-sm relative overflow-hidden">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs font-bold uppercase tracking-wider text-gray-400">Taux de Réussite</span>
                    <span class="p-2 bg-amber-500/10 text-amber-400 rounded-lg"><i class="fa-solid fa-bullseye"></i></span>
                </div>
                <div class="text-3xl font-extrabold text-white" id="stat-winrate">0%</div>
                <p class="text-xs text-gray-400 mt-2"><span id="stat-wins" class="text-emerald-400 font-semibold">0G</span> / <span id="stat-losses" class="text-red-400 font-semibold">0P</span> / <span id="stat-neutrals" class="text-gray-400 font-semibold">0N</span></p>
            </div>

            <div class="bg-cardBg p-5 rounded-2xl border border-cardBorder shadow-sm relative overflow-hidden">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs font-bold uppercase tracking-wider text-gray-400">Total Enregistrés</span>
                    <span class="p-2 bg-purple-500/10 text-purple-400 rounded-lg"><i class="fa-solid fa-list-check"></i></span>
                </div>
                <div class="text-3xl font-extrabold text-white" id="stat-count">0</div>
                <p class="text-xs text-gray-400 mt-2">Trades & sessions de trading</p>
            </div>
        </div>

        <!-- SECTION 1: DASHBOARD VIEW -->
        <div id="view-dashboard" class="space-y-6">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Add Trade Form -->
                <div class="bg-cardBg p-6 rounded-2xl border border-cardBorder shadow-md lg:col-span-1">
                    <div class="flex items-center justify-between mb-5">
                        <h2 class="text-lg font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-square-plus text-emerald-400"></i>
                            <span id="form-title">Nouveau Trade / Jour</span>
                        </h2>
                        <button id="cancel-edit-btn" onclick="resetForm()" class="hidden text-xs text-red-400 hover:underline">Annuler modif.</button>
                    </div>

                    <form id="trade-form" onsubmit="handleFormSubmit(event)" class="space-y-4">
                        <input type="hidden" id="edit-id">

                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1">Date</label>
                            <input type="date" id="trade-date" required class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2.5 text-sm text-gray-100 focus:outline-none focus:border-emerald-500 transition">
                        </div>

                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Capital Initial ($)</label>
                                <input type="number" step="0.01" id="trade-capital" required placeholder="10.00" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2.5 text-sm text-gray-100 focus:outline-none focus:border-emerald-500 transition">
                            </div>

                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Profit / Perte ($)</label>
                                <input type="number" step="0.01" id="trade-pnl" required placeholder="Ex: 0.60 ou -0.50" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2.5 text-sm text-gray-100 focus:outline-none focus:border-emerald-500 transition">
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Statut</label>
                                <select id="trade-status" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2.5 text-sm text-gray-100 focus:outline-none focus:border-emerald-500 transition">
                                    <option value="Gagnant">Gagnant (Win)</option>
                                    <option value="Perdu">Perdu (Loss)</option>
                                    <option value="Neutre">Neutre (BE)</option>
                                </select>
                            </div>

                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Stratégie</label>
                                <select id="trade-strategy" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2.5 text-sm text-gray-100 focus:outline-none focus:border-emerald-500 transition">
                                    <option value="Breakout">Breakout</option>
                                    <option value="ICT / SMC">ICT / Smart Money</option>
                                    <option value="Suivi de Tendance">Suivi de Tendance</option>
                                    <option value="Scalping">Scalping</option>
                                    <option value="Rebond / Support">Rebond / Support</option>
                                    <option value="Autre">Autre</option>
                                </select>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1">Notes & Paire (Optionnel)</label>
                            <textarea id="trade-notes" rows="2" placeholder="Ex: EUR/USD, achat après cassure du high..." class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2 text-sm text-gray-100 focus:outline-none focus:border-emerald-500 transition"></textarea>
                        </div>

                        <button type="submit" id="submit-btn" class="w-full bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white font-bold py-3 px-4 rounded-xl shadow-lg transition duration-200 flex items-center justify-center gap-2">
                            <i class="fa-solid fa-plus-circle"></i>
                            <span>Enregistrer le Trade</span>
                        </button>
                    </form>
                </div>

                <!-- Performance Chart -->
                <div class="bg-cardBg p-6 rounded-2xl border border-cardBorder shadow-md lg:col-span-2 flex flex-col justify-between">
                    <div class="flex justify-between items-center mb-4">
                        <h2 class="text-lg font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-chart-area text-blue-400"></i>
                            Évolution du Capital
                        </h2>
                        <span class="text-xs text-gray-400">Progression en temps réel</span>
                    </div>
                    <div class="relative w-full h-72">
                        <canvas id="capitalChart"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- SECTION 2: JOURNAL TABLE VIEW -->
        <div id="view-journal" class="hidden space-y-4">
            <div class="bg-cardBg p-6 rounded-2xl border border-cardBorder shadow-md">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 mb-6">
                    <div>
                        <h2 class="text-xl font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-table-list text-emerald-400"></i>
                            Journal de Trading Détaillé
                        </h2>
                        <p class="text-xs text-gray-400">Historique complet des transactions & performances quotidiennes</p>
                    </div>
                    <div class="flex gap-2">
                        <button onclick="clearAllData()" class="px-3 py-2 bg-red-950/40 hover:bg-red-900/60 text-red-400 border border-red-800/50 rounded-xl text-xs font-semibold transition">
                            <i class="fa-solid fa-trash-can mr-1"></i> Réinitialiser tout
                        </button>
                    </div>
                </div>

                <!-- Interactive Data Table -->
                <div class="overflow-x-auto rounded-xl border border-gray-800">
                    <table class="w-full text-sm text-left text-gray-300">
                        <thead class="text-xs uppercase bg-gray-900/90 text-gray-400 font-semibold border-b border-gray-800">
                            <tr>
                                <th class="px-4 py-3.5"># Jour</th>
                                <th class="px-4 py-3.5">Date</th>
                                <th class="px-4 py-3.5">Capital Initial</th>
                                <th class="px-4 py-3.5">Profit / Perte</th>
                                <th class="px-4 py-3.5">Capital Final</th>
                                <th class="px-4 py-3.5">Stratégie</th>
                                <th class="px-4 py-3.5">Statut</th>
                                <th class="px-4 py-3.5">Notes</th>
                                <th class="px-4 py-3.5 text-center">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="journal-tbody" class="divide-y divide-gray-800/60">
                            <!-- Populated via Javascript -->
                        </tbody>
                    </table>
                </div>
                <div id="empty-journal-msg" class="text-center py-12 text-gray-500 hidden">
                    <i class="fa-solid fa-folder-open text-4xl mb-3 block opacity-50"></i>
                    Aucune transaction enregistrée. Remplissez le formulaire pour commencer votre journal !
                </div>
            </div>
        </div>

        <!-- SECTION 3: PLAN 90 DAYS (SIMULATOR) VIEW -->
        <div id="view-plan90" class="hidden space-y-6">
            <div class="bg-cardBg p-6 rounded-2xl border border-cardBorder shadow-md">
                <div class="flex flex-col lg:flex-row justify-between items-start lg:items-center gap-4 mb-6">
                    <div>
                        <h2 class="text-2xl font-black text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 to-blue-400 flex items-center gap-2">
                            <i class="fa-solid fa-bullseye text-emerald-400"></i>
                            Plan de Croissance 90 Jours
                        </h2>
                        <p class="text-xs text-gray-400 mt-1">
                            Inspiré de la stratégie de composition des intérêts (ex: 10$ de départ à 6% de gain quotidien).
                        </p>
                    </div>

                    <!-- Simulator Controls -->
                    <div class="flex flex-wrap items-center gap-3 bg-gray-900 p-3 rounded-xl border border-gray-800">
                        <div>
                            <label class="block text-[10px] uppercase tracking-wider text-gray-400 font-bold mb-1">Capital Départ ($)</label>
                            <input type="number" id="sim-start" value="10" class="w-24 bg-cardBg border border-gray-700 rounded-lg px-2.5 py-1 text-sm font-semibold text-white focus:outline-none focus:border-emerald-500">
                        </div>
                        <div>
                            <label class="block text-[10px] uppercase tracking-wider text-gray-400 font-bold mb-1">% Gain / Jour</label>
                            <input type="number" id="sim-rate" value="6" step="0.5" class="w-20 bg-cardBg border border-gray-700 rounded-lg px-2.5 py-1 text-sm font-semibold text-white focus:outline-none focus:border-emerald-500">
                        </div>
                        <div class="flex items-end">
                            <button onclick="generatePlan90Table()" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-4 py-1.5 rounded-lg text-xs transition">
                                Re-calculer
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Highlight Badge -->
                <div class="bg-emerald-950/30 border border-emerald-800/40 rounded-xl p-4 mb-6 flex flex-col md:flex-row justify-between items-center gap-4">
                    <div class="flex items-center gap-3">
                        <div class="p-3 bg-emerald-500/10 rounded-full text-emerald-400">
                            <i class="fa-solid fa-rocket text-xl"></i>
                        </div>
                        <div>
                            <div class="text-sm font-bold text-white">Objectif Jour 90 : <span id="sim-final-val" class="text-emerald-400 font-black text-lg">$0.00</span></div>
                            <div class="text-xs text-gray-400">Discipline, gestion du risque et régularité quotidienne sont vos clés.</div>
                        </div>
                    </div>
                    <div class="text-xs text-gray-300 bg-gray-900/80 px-3 py-2 rounded-lg border border-gray-800">
                        Total Multiplicateur: <span id="sim-multiplier" class="font-bold text-emerald-400">0x</span>
                    </div>
                </div>

                <!-- 3 Columns Plan Display matching image style -->
                <div id="plan90-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Populated via Javascript -->
                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="bg-cardBg border-t border-cardBorder py-6 mt-12 text-center text-xs text-gray-500">
        <p>© 2026 <strong class="text-gray-300">Diallo TRADING</strong>. Développé pour Diallo AMADOU. Tous droits réservés.</p>
        <p class="mt-1 text-gray-600">Le trading comporte des risques importants. Gérez votre capital de manière responsable.</p>
    </footer>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-5 right-5 transform translate-y-20 opacity-0 transition-all duration-300 bg-gray-800 text-white border border-gray-700 px-4 py-3 rounded-xl shadow-2xl flex items-center gap-3 z-50">
        <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400 text-lg"></i>
        <span id="toast-msg" class="text-sm font-medium">Action effectuée</span>
    </div>

    <script>
        // State management
        let trades = JSON.parse(localStorage.getItem('diallo_trades')) || [];
        let chartInstance = null;

        // Initialize App
        window.onload = function() {
            // Set default date to today in form
            document.getElementById('trade-date').valueAsDate = new Date();
            
            // Load Demo Data if empty
            if (trades.length === 0) {
                initDemoData();
            }

            renderDashboard();
            generatePlan90Table();
        };

        // Load initial dummy trades matching user pattern if completely clean
        function initDemoData() {
            trades = [
                { id: 1, date: '2026-09-01', capital: 10.00, pnl: 0.60, strategy: 'Breakout', status: 'Gagnant', notes: 'Premier jour - objectif 6%' },
                { id: 2, date: '2026-09-02', capital: 10.60, pnl: 0.64, strategy: 'ICT / SMC', status: 'Gagnant', notes: 'Confirmation FVG' },
                { id: 3, date: '2026-09-03', capital: 11.24, pnl: 0.67, strategy: 'Scalping', status: 'Gagnant', notes: 'Paire EURUSD' },
                { id: 4, date: '2026-09-04', capital: 11.91, pnl: -0.40, strategy: 'Suivi de Tendance', status: 'Perdu', notes: 'Stop loss touché' }
            ];
            saveTrades();
        }

        // Save to LocalStorage
        function saveTrades() {
            localStorage.setItem('diallo_trades', JSON.stringify(trades));
        }

        function switchTab(tab) {
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('text-emerald-400', 'bg-gray-800', 'shadow');
                btn.classList.add('text-gray-400');
            });

            document.getElementById('view-dashboard').classList.add('hidden');
            document.getElementById('view-journal').classList.add('hidden');
            document.getElementById('view-plan90').classList.add('hidden');

            document.getElementById(`tab-${tab}`).classList.add('text-emerald-400', 'bg-gray-800', 'shadow');
            document.getElementById(`tab-${tab}`).classList.remove('text-gray-400');
            
            document.getElementById(`view-${tab}`).classList.remove('hidden');

            if (tab === 'dashboard' || tab === 'journal') {
                renderDashboard();
            }
        }

        function handleFormSubmit(e) {
            e.preventDefault();

            const editId = document.getElementById('edit-id').value;
            const date = document.getElementById('trade-date').value;
            const capital = parseFloat(document.getElementById('trade-capital').value);
            const pnl = parseFloat(document.getElementById('trade-pnl').value);
            const status = document.getElementById('trade-status').value;
            const strategy = document.getElementById('trade-strategy').value;
            const notes = document.getElementById('trade-notes').value;

            if (editId) {
                // Update existing
                const index = trades.findIndex(t => t.id == editId);
                if (index !== -1) {
                    trades[index] = { id: parseInt(editId), date, capital, pnl, status, strategy, notes };
                    showToast("Trade mis à jour avec succès !");
                }
            } else {
                // Create new
                const newTrade = {
                    id: Date.now(),
                    date,
                    capital,
                    pnl,
                    status,
                    strategy,
                    notes
                };
                trades.push(newTrade);
                showToast("Nouveau trade enregistré !");
            }

            // Sort trades chronologically
            trades.sort((a, b) => new Date(a.date) - new Date(b.date));

            saveTrades();
            resetForm();
            renderDashboard();
        }

        function resetForm() {
            document.getElementById('edit-id').value = '';
            document.getElementById('trade-form').reset();
            document.getElementById('trade-date').valueAsDate = new Date();
            document.getElementById('submit-btn').innerHTML = `<i class="fa-solid fa-plus-circle"></i> Enregistrer le Trade`;
            document.getElementById('form-title').innerText = "Nouveau Trade / Jour";
            document.getElementById('cancel-edit-btn').classList.add('hidden');
        }

        function editTrade(id) {
            const trade = trades.find(t => t.id === id);
            if (!trade) return;

            document.getElementById('edit-id').value = trade.id;
            document.getElementById('trade-date').value = trade.date;
            document.getElementById('trade-capital').value = trade.capital;
            document.getElementById('trade-pnl').value = trade.pnl;
            document.getElementById('trade-status').value = trade.status;
            document.getElementById('trade-strategy').value = trade.strategy;
            document.getElementById('trade-notes').value = trade.notes || '';

            document.getElementById('submit-btn').innerHTML = `<i class="fa-solid fa-floppy-disk"></i> Mettre à jour`;
            document.getElementById('form-title').innerText = "Modifier le Trade";
            document.getElementById('cancel-edit-btn').classList.remove('hidden');

            switchTab('dashboard');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function deleteTrade(id) {
            if (confirm("Êtes-vous sûr de vouloir supprimer cette ligne du journal ?")) {
                trades = trades.filter(t => t.id !== id);
                saveTrades();
                renderDashboard();
                showToast("Trade supprimé", "red");
            }
        }

        function clearAllData() {
            if (confirm("ATTENTION: Souhaitez-vous effacer l'intégralité de votre journal de trading ?")) {
                trades = [];
                saveTrades();
                renderDashboard();
                showToast("Toutes les données ont été réinitialisées", "red");
            }
        }

        function renderDashboard() {
            // Populate metrics
            const totalCount = trades.length;
            const wins = trades.filter(t => t.status === 'Gagnant').length;
            const losses = trades.filter(t => t.status === 'Perdu').length;
            const neutrals = trades.filter(t => t.status === 'Neutre').length;

            const winRate = totalCount > 0 ? ((wins / totalCount) * 100).toFixed(1) : 0;
            const initialCapital = trades.length > 0 ? trades[0].capital : 0;
            
            let totalPnl = 0;
            trades.forEach(t => totalPnl += t.pnl);

            const currentCapital = trades.length > 0 ? (trades[trades.length - 1].capital + trades[trades.length - 1].pnl) : 0;
            const roi = initialCapital > 0 ? ((totalPnl / initialCapital) * 100).toFixed(2) : 0;

            // DOM elements
            document.getElementById('stat-capital').innerText = `$${currentCapital.toFixed(2)}`;
            document.getElementById('stat-initial-cap').innerText = `$${initialCapital.toFixed(2)}`;
            
            const pnlElem = document.getElementById('stat-total-pnl');
            pnlElem.innerText = `${totalPnl >= 0 ? '+' : ''}$${totalPnl.toFixed(2)}`;
            pnlElem.className = `text-3xl font-extrabold ${totalPnl >= 0 ? 'text-emerald-400' : 'text-red-400'}`;

            document.getElementById('stat-roi').innerText = `${roi >= 0 ? '+' : ''}${roi}%`;
            document.getElementById('stat-roi').className = `font-bold ${roi >= 0 ? 'text-emerald-400' : 'text-red-400'}`;

            document.getElementById('stat-winrate').innerText = `${winRate}%`;
            document.getElementById('stat-wins').innerText = `${wins}G`;
            document.getElementById('stat-losses').innerText = `${losses}P`;
            document.getElementById('stat-neutrals').innerText = `${neutrals}N`;
            document.getElementById('stat-count').innerText = totalCount;

            // Update Auto-fill for Form Capital if last trade exists
            if (trades.length > 0 && !document.getElementById('edit-id').value) {
                const lastTrade = trades[trades.length - 1];
                document.getElementById('trade-capital').value = (lastTrade.capital + lastTrade.pnl).toFixed(2);
            }

            renderJournalTable();
            renderChart();
        }

        function renderJournalTable() {
            const tbody = document.getElementById('journal-tbody');
            const emptyMsg = document.getElementById('empty-journal-msg');
            tbody.innerHTML = '';

            if (trades.length === 0) {
                emptyMsg.classList.remove('hidden');
                return;
            } else {
                emptyMsg.classList.add('hidden');
            }

            trades.forEach((trade, idx) => {
                const finalCap = trade.capital + trade.pnl;
                const isGain = trade.pnl >= 0;

                let statusBadge = '';
                if (trade.status === 'Gagnant') {
                    statusBadge = `<span class="bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 px-2.5 py-1 rounded-md text-xs font-semibold">Gagnant</span>`;
                } else if (trade.status === 'Perdu') {
                    statusBadge = `<span class="bg-red-500/10 text-red-400 border border-red-500/20 px-2.5 py-1 rounded-md text-xs font-semibold">Perdu</span>`;
                } else {
                    statusBadge = `<span class="bg-gray-500/10 text-gray-400 border border-gray-500/20 px-2.5 py-1 rounded-md text-xs font-semibold">Neutre</span>`;
                }

                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/40 transition duration-150";
                tr.innerHTML = `
                    <td class="px-4 py-3 font-bold text-gray-400">Jour ${idx + 1}</td>
                    <td class="px-4 py-3 text-gray-300 font-medium whitespace-nowrap">${trade.date}</td>
                    <td class="px-4 py-3 font-medium text-gray-200">$${trade.capital.toFixed(2)}</td>
                    <td class="px-4 py-3 font-bold ${isGain ? 'text-emerald-400' : 'text-red-400'} whitespace-nowrap">
                        ${isGain ? '+' : ''}$${trade.pnl.toFixed(2)}
                    </td>
                    <td class="px-4 py-3 font-extrabold text-white">$${finalCap.toFixed(2)}</td>
                    <td class="px-4 py-3 text-gray-300"><span class="bg-gray-800 px-2 py-0.5 rounded text-xs border border-gray-700">${trade.strategy}</span></td>
                    <td class="px-4 py-3">${statusBadge}</td>
                    <td class="px-4 py-3 text-xs text-gray-400 max-w-xs truncate">${trade.notes || '-'}</td>
                    <td class="px-4 py-3 text-center">
                        <div class="flex items-center justify-center gap-2">
                            <button onclick="editTrade(${trade.id})" title="Modifier" class="p-1.5 text-blue-400 hover:bg-blue-500/10 rounded transition">
                                <i class="fa-solid fa-pen-to-square"></i>
                            </button>
                            <button onclick="deleteTrade(${trade.id})" title="Supprimer" class="p-1.5 text-red-400 hover:bg-red-500/10 rounded transition">
                                <i class="fa-solid fa-trash"></i>
                            </button>
                        </div>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderChart() {
            const ctx = document.getElementById('capitalChart').getContext('2d');

            const labels = trades.map((t, i) => `Jour ${i + 1} (${t.date})`);
            const dataPoints = trades.map(t => t.capital + t.pnl);

            if (chartInstance) {
                chartInstance.destroy();
            }

            chartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels.length > 0 ? labels : ['Départ'],
                    datasets: [{
                        label: 'Capital Total ($)',
                        data: dataPoints.length > 0 ? dataPoints : [0],
                        borderColor: '#10b981',
                        backgroundColor: 'rgba(16, 185, 129, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.3,
                        pointBackgroundColor: '#10b981',
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
                            callbacks: {
                                label: function(context) {
                                    return `Capital: $${context.raw.toFixed(2)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            grid: { color: 'rgba(255, 255, 255, 0.05)' },
                            ticks: { color: '#9ca3af', font: { size: 11 } }
                        },
                        y: {
                            grid: { color: 'rgba(255, 255, 255, 0.05)' },
                            ticks: { color: '#9ca3af', font: { size: 11 } }
                        }
                    }
                }
            });
        }

        function generatePlan90Table() {
            const container = document.getElementById('plan90-grid');
            container.innerHTML = '';

            let startCap = parseFloat(document.getElementById('sim-start').value) || 10;
            let dailyRate = (parseFloat(document.getElementById('sim-rate').value) || 6) / 100;

            let currentCap = startCap;
            
            // Create 3 columns matching image layout (1-30, 31-60, 61-90)
            const columns = [
                { title: "Jours 1 - 30", startDay: 1, endDay: 30 },
                { title: "Jours 31 - 60", startDay: 31, endDay: 60 },
                { title: "Jours 61 - 90", startDay: 61, endDay: 90 }
            ];

            let dayCounter = 1;

            columns.forEach(col => {
                const colDiv = document.createElement('div');
                colDiv.className = "bg-gray-900 rounded-xl border border-gray-800 overflow-hidden shadow-sm";
                
                let tableHTML = `
                    <div class="bg-gray-800/80 px-4 py-2.5 font-bold text-xs uppercase tracking-wider text-emerald-400 border-b border-gray-700">
                        ${col.title}
                    </div>
                    <table class="w-full text-xs">
                        <thead>
                            <tr class="bg-gray-900/50 text-gray-400 border-b border-gray-800">
                                <th class="px-3 py-2 text-left">Jour</th>
                                <th class="px-3 py-2 text-right">Capital</th>
                                <th class="px-3 py-2 text-right">Profit (${(dailyRate * 100).toFixed(1)}%)</th>
                                <th class="px-3 py-2 text-right">Total</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-gray-800/40">
                `;

                for (let d = col.startDay; d <= col.endDay; d++) {
                    const profit = currentCap * dailyRate;
                    const totalProfit = currentCap + profit;

                    tableHTML += `
                        <tr class="hover:bg-gray-800/30 transition">
                            <td class="px-3 py-1.5 font-bold text-emerald-400">${d}</td>
                            <td class="px-3 py-1.5 text-right text-gray-300 font-mono">$${currentCap.toFixed(2)}</td>
                            <td class="px-3 py-1.5 text-right text-emerald-400 font-mono">+$${profit.toFixed(2)}</td>
                            <td class="px-3 py-1.5 text-right text-white font-extrabold font-mono">$${totalProfit.toFixed(2)}</td>
                        </tr>
                    `;

                    currentCap = totalProfit;
                }

                tableHTML += `</tbody></table>`;
                colDiv.innerHTML = tableHTML;
                container.appendChild(colDiv);
            });

            // Update stats
            document.getElementById('sim-final-val').innerText = `$${currentCap.toFixed(2)}`;
            const multiplier = (currentCap / startCap).toFixed(1);
            document.getElementById('sim-multiplier').innerText = `${multiplier}x`;
        }

        function exportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(trades, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `Diallo_TRADING_Journal_${new Date().toISOString().slice(0, 10)}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast("Journal exporté au format JSON !");
        }

        function importData(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const imported = JSON.parse(e.target.result);
                    if (Array.isArray(imported)) {
                        trades = imported;
                        saveTrades();
                        renderDashboard();
                        showToast("Données importées avec succès !");
                    } else {
                        alert("Format de fichier invalide.");
                    }
                } catch (err) {
                    alert("Erreur lors de la lecture du fichier.");
                }
            };
            reader.readAsText(file);
        }

        function showToast(msg, color = 'emerald') {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toast-msg');
            const toastIcon = document.getElementById('toast-icon');

            toastMsg.innerText = msg;
            toastIcon.className = color === 'red' ? 'fa-solid fa-circle-xmark text-red-400 text-lg' : 'fa-solid fa-circle-check text-emerald-400 text-lg';

            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
