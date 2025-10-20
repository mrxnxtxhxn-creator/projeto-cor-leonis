<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Scanner de ID com Módulo de Inventário</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/html5-qrcode@2.3.8/html5-qrcode.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.2/dist/chart.umd.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #0f172a; }
        #reader__scan_region { border: 4px solid rgba(255, 255, 255, 0.5) !important; border-radius: 1.5rem; background: none !important; box-shadow: 0 0 20px rgba(0, 255, 255, 0.3); }
        .scan-line { position: absolute; left: 5%; top: 10px; width: 90%; height: 4px; background: linear-gradient(to right, transparent, #06b6d4, transparent); box-shadow: 0 0 15px #06b6d4, 0 0 5px #fff; border-radius: 4px; animation: scan-animation 2.5s infinite ease-in-out; }
        @keyframes scan-animation { 0% { transform: translateY(0); } 50% { transform: translateY(calc(100% - 20px)); } 100% { transform: translateY(0); } }
        #controls-panel { 
            background: rgba(30, 41, 59, 0.8); 
            backdrop-filter: blur(16px); 
            border-top: 1px solid rgba(71, 85, 105, 0.5);
            transform: translateY(calc(100% - 70px));
            transition: transform 0.3s ease-in-out;
        }
        #controls-panel.open { transform: translateY(0); }
        .feedback-pulse { animation: pulse-feedback 0.8s ease-out; }
        @keyframes pulse-feedback { from { transform: scale(0.9); opacity: 0.7; } to { transform: scale(1); opacity: 1; } }
        /* Animação para "Hunt Success" */
        .hunt-success-pulse { animation: hunt-pulse 0.5s ease-out 3; }
        @keyframes hunt-pulse { 0%, 100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.2); opacity: 0.8; } }
        
        .tab-btn { border-bottom: 3px solid transparent; transition: all 0.2s; white-space: nowrap; }
        .tab-active { border-color: #06b6d4; color: white; }
        .tab-inactive { color: #94a3b8; }
        .toggle-bg:after { content: ''; position: absolute; top: 2px; left: 2px; background: white; border-radius: 9999px; width: 1.25rem; height: 1.25rem; transition: all 0.2s ease; }
        input:checked + .toggle-bg:after { transform: translateX(100%); left: auto; right: 2px; }
        input:checked + .toggle-bg { background-color: #06b6d4; }
    </style>
</head>
<body class="text-slate-200">
    <div id="global-status-bar" class="fixed top-0 left-0 right-0 z-20 p-2 text-center text-sm transition-all duration-300"></div>

    <div id="reader" class="fixed top-0 left-0 w-full h-full z-1"><div class="scan-line"></div></div>
    <div id="feedback-overlay" class="fixed inset-0 z-50 flex items-center justify-center p-4 text-white font-black opacity-0 pointer-events-none transition-opacity duration-200"></div>

    <div id="controls-panel" class="fixed bottom-0 left-0 right-0 z-10 rounded-t-2xl">
        <div id="panel-handle" class="w-full h-10 flex justify-center items-center cursor-pointer">
              <div class="w-10 h-1.5 bg-slate-500 rounded-full"></div>
        </div>
        <div class="w-full max-w-lg mx-auto px-4 pb-4">
            <div class="w-full overflow-x-auto pb-2">
                <div class="flex justify-start mb-4 space-x-2 sm:space-x-4">
                    <button data-view="procurar" class="tab-btn tab-active py-2 px-4 font-semibold text-sm sm:text-base">Procurar</button>
                    <button data-view="encontrados" class="tab-btn tab-inactive py-2 px-4 font-semibold text-sm sm:text-base">Encontrados (<span id="found-count">0</span>)</button>
                    <button data-view="dashboard" class="tab-btn tab-inactive py-2 px-4 font-semibold text-sm sm:text-base">Dashboard</button>
                    <button data-view="inventario" class="tab-btn tab-inactive py-2 px-4 font-semibold text-sm sm:text-base">Inventário</button>
                    <button data-view="excecoes" class="tab-btn tab-inactive py-2 px-4 font-semibold text-sm sm:text-base">Exceções (<span id="exceptions-count">0</span>)</button>
                    <button data-view="log" class="tab-btn tab-inactive py-2 px-4 font-semibold text-sm sm:text-base">Log</button>
                </div>
            </div>
            
            <div data-view-content="procurar" class="text-center">
                <button id="load-file-btn" class="w-full bg-cyan-600 hover:bg-cyan-700 text-white font-bold py-3 px-5 rounded-lg shadow-lg text-lg">Carregar Ficheiro Principal</button>
                <input type="file" id="file-input" class="hidden" accept=".txt,.csv,.xlsx">
                <p id="file-info" class="text-xs text-green-400 mt-2 h-4"></p>
                 <div class="mt-4 text-left border-t border-slate-700 pt-4 space-y-4">
                    
                    <div class="p-3 bg-slate-800 rounded-lg">
                        <label class="text-sm text-slate-300 font-medium">Modo Caça ao Tesouro</label>
                        <p id="hunt-status" class="text-xs text-cyan-400 h-4 mb-2"></p>
                        <div class="flex gap-2">
                            <input type="text" id="hunt-target-id" class="w-full bg-slate-700 p-2 rounded-lg font-mono text-white" placeholder="ID para caçar...">
                            <button id="hunt-toggle-btn" class="bg-blue-600 hover:bg-blue-700 font-bold px-4 rounded-lg whitespace-nowrap">Caçar</button>
                        </div>
                    </div>
                    
                    <div class="flex justify-between items-center">
                        <label for="fast-mode-toggle" class="text-sm text-slate-300 font-medium">Modo Rápido (Sem pausa)</label>
                        <div class="relative inline-block w-10 align-middle select-none transition duration-200 ease-in">
                            <input type="checkbox" name="fast-mode-toggle" id="fast-mode-toggle" class="toggle-checkbox absolute block w-5 h-5 rounded-full bg-white border-4 appearance-none cursor-pointer"/>
                            <label for="fast-mode-toggle" class="toggle-bg block overflow-hidden h-6 w-11 rounded-full bg-slate-600 cursor-pointer"></label>
                        </div>
                    </div>
                    <button id="clear-session-btn" class="w-full bg-red-800 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg text-sm">Limpar Sessão (Apagar Dados)</button>
                    
                    <div>
                        <label for="manual-input" class="text-xs text-slate-400">Ou digite o ID manualmente:</label>
                        <div class="flex gap-2 mt-1">
                            <input type="text" id="manual-input" class="w-full bg-slate-700 p-2 rounded-lg font-mono text-white" placeholder="ID do pacote...">
                            <button id="manual-check-btn" class="bg-blue-600 hover:bg-blue-700 font-bold px-4 rounded-lg">Verificar</button>
                        </div>
                    </div>
                </div>
            </div>

            <div data-view-content="encontrados" class="hidden">
                <button id="export-btn" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-5 rounded-lg mb-4">Exportar Encontrados (.csv)</button>
                <div class="max-h-48 overflow-y-auto pr-2"><ul id="found-list" class="space-y-2 text-center font-mono text-sm"></ul></div>
            </div>

            <div data-view-content="dashboard" class="hidden">
                <h3 class="text-lg font-bold text-center text-white mb-4">Performance da Sessão</h3>
                <div class="grid grid-cols-3 gap-4 mb-4">
                    <div class="flex flex-col items-center justify-center p-4 bg-slate-800 rounded-lg">
                          <h4 class="text-sm font-semibold text-slate-400 mb-2">Progresso</h4>
                          <div class="relative w-24 h-24"><canvas id="progressChart"></canvas><div id="progress-text" class="absolute inset-0 flex items-center justify-center text-2xl font-bold">0%</div></div>
                    </div>
                    <div class="p-4 bg-slate-800 rounded-lg text-center"><h4 class="text-sm font-semibold text-slate-400">Tempo Médio / Bip</h4><p id="kpi-avg-time" class="text-4xl font-black text-white mt-2">-- s</p></div>
                    <div class="p-4 bg-slate-800 rounded-lg text-center"><h4 class="text-sm font-semibold text-slate-400">Bips por Minuto</h4><p id="kpi-bpm" class="text-4xl font-black text-white mt-2">--</p></div>
                </div>
                <div class="border-t border-slate-700 pt-4">
                     <h3 class="text-lg font-bold text-center text-white mb-2">Contagem por Zona</h3>
                     <div id="zone-finds-container" class="space-y-2 max-h-32 overflow-y-auto pr-2">
                         <p class="text-slate-500 text-center">Nenhum item de inventário escaneado ainda.</p>
                     </div>
                </div>
            </div>

            <div data-view-content="inventario" class="hidden">
                <h3 class="text-lg font-bold text-center text-white mb-4">Carregar Listas de Inventário por Zona</h3>
                <div id="inventory-zones-container" class="space-y-4 max-h-64 overflow-y-auto pr-2">
                    </div>
            </div>
            
            <div data-view-content="excecoes" class="hidden">
                <button id="export-exceptions-btn" class="w-full bg-amber-600 hover:bg-amber-700 text-white font-bold py-3 px-5 rounded-lg mb-4">Exportar Exceções (.csv)</button>
                <div class="max-h-48 overflow-y-auto pr-2"><ul id="exceptions-list" class="space-y-2 text-center font-mono text-sm"></ul></div>
            </div>
            
            <div data-view-content="log" class="hidden">
                 <h3 class="text-lg font-bold text-center text-white mb-4">Log de Atividade</h3>
                <div class="max-h-48 overflow-y-auto pr-2"><ul id="scan-log-list" class="space-y-2 text-center font-mono text-xs"></ul></div>
            </div>
            
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const SCAN_DELAY = 1200; 
            const STORAGE_KEY = 'scannerAppState'; 

            let appState = {
                currentView: 'procurar',
                idsToFind: new Set(),
                inventoryZones: [
                    { id: 'buffered', name: 'Buffered' }, { id: 'sorting', name: 'Sorting' },
                    { id: 'fraude', name: 'Fraude' }, { id: 'missort', name: 'Missort' },
                    { id: 'returns', name: 'Returns' }, { id: 'bulky', name: 'Bulky' },
                    { id: 'problemsolver', name: 'Problem Solver' }
                ],
                inventoryZoneData: new Map(),
                foundIds: [], 
                isPaused: false,
                audioContext: null,
                html5QrCode: null,
                scanHistory: [], 
                charts: {},
                notFoundIds: [], 
                scanLog: [], 
                zoneFinds: new Map(), 
                isFastMode: false, 
                lastScanTime: 0,
                // NOVOS ESTADOS (Ideia A & B)
                activeZoneId: null,
                huntMode: { isActive: false, targetId: null }
            };
            
            const controlsPanel = document.getElementById('controls-panel');
            const panelHandle = document.getElementById('panel-handle');
            const togglePanel = () => controlsPanel.classList.toggle('open');
            panelHandle.addEventListener('click', togglePanel);
            
            let touchStartY = 0;
            document.addEventListener('touchstart', e => { if (e.target === panelHandle || controlsPanel.contains(e.target)) touchStartY = e.touches[0].clientY; });
            document.addEventListener('touchend', e => {
                if (touchStartY === 0) return;
                const touchEndY = e.changedTouches[0].clientY;
                if (touchStartY - touchEndY > 50) controlsPanel.classList.add('open');
                else if (touchEndY - touchStartY > 50) controlsPanel.classList.remove('open');
                touchStartY = 0;
            });
            
            // --- FUNÇÕES DE PERSISTÊNCIA ATUALIZADAS ---
            function saveToLocalStorage() {
                try {
                    const dataToSave = {
                        idsToFind: Array.from(appState.idsToFind),
                        inventoryZoneData: Array.from(appState.inventoryZoneData.entries()).map(([key, valueSet]) => [key, Array.from(valueSet)]),
                        foundIds: appState.foundIds,
                        notFoundIds: appState.notFoundIds,
                        zoneFinds: Array.from(appState.zoneFinds.entries()),
                        scanHistory: appState.scanHistory,
                        scanLog: appState.scanLog,
                        // Salva os novos estados
                        activeZoneId: appState.activeZoneId,
                        huntMode: appState.huntMode
                    };
                    localStorage.setItem(STORAGE_KEY, JSON.stringify(dataToSave));
                } catch (e) {
                    console.error("Erro ao salvar no localStorage:", e);
                    alert("Erro: Não foi possível salvar a sessão. O armazenamento pode estar cheio.");
                }
            }

            function loadFromLocalStorage() {
                const savedData = localStorage.getItem(STORAGE_KEY);
                if (!savedData) return;
                
                try {
                    const data = JSON.parse(savedData);
                    appState.idsToFind = new Set(data.idsToFind || []);
                    appState.inventoryZoneData = new Map((data.inventoryZoneData || []).map(([key, valueArray]) => [key, new Set(valueArray)]));
                    appState.foundIds = (data.foundIds || []).map(item => ({...item, timestamp: new Date(item.timestamp)}));
                    appState.notFoundIds = data.notFoundIds || [];
                    appState.zoneFinds = new Map(data.zoneFinds || []);
                    appState.scanHistory = (data.scanHistory || []).map(ts => new Date(ts));
                    appState.scanLog = (data.scanLog || []).map(item => ({...item, time: new Date(item.time)}));
                    // Carrega os novos estados
                    appState.activeZoneId = data.activeZoneId || null;
                    appState.huntMode = data.huntMode || { isActive: false, targetId: null };
                    
                    const totalLoaded = appState.idsToFind.size + appState.foundIds.length;
                    if (totalLoaded > 0) {
                         document.getElementById('file-info').textContent = `Sessão carregada (${totalLoaded} IDs)`;
                    }

                } catch (e) {
                    console.error("Erro ao carregar dados do localStorage:", e);
                    localStorage.removeItem(STORAGE_KEY); 
                }
            }

            function clearSession() {
                if (confirm("Tem certeza que deseja limpar todos os dados da sessão? (Listas carregadas e itens encontrados serão perdidos)")) {
                    localStorage.removeItem(STORAGE_KEY);
                    window.location.reload();
                }
            }
            
            function toggleFastMode() {
                appState.isFastMode = document.getElementById('fast-mode-toggle').checked;
            }

            function initialize() {
                loadFromLocalStorage(); 
                buildInventoryZoneUI(); 
                
                document.getElementById('load-file-btn').addEventListener('click', () => document.getElementById('file-input').click());
                document.getElementById('file-input').addEventListener('change', (e) => handleFileSelect(e, 'main'));
                document.getElementById('export-btn').addEventListener('click', exportFoundIds);
                document.getElementById('export-exceptions-btn').addEventListener('click', exportExceptions);
                document.getElementById('clear-session-btn').addEventListener('click', clearSession); 
                document.getElementById('fast-mode-toggle').addEventListener('change', toggleFastMode); 
                // NOVO: Listeners para Ideia B
                document.getElementById('hunt-toggle-btn').addEventListener('click', toggleHuntMode);
                
                document.body.addEventListener('click', initAudio, { once: true });
                setupTabs();
                startScanner();
                const manualInput = document.getElementById('manual-input');
                const manualCheckBtn = document.getElementById('manual-check-btn');
                manualCheckBtn.addEventListener('click', () => {
                    const manualId = manualInput.value.trim();
                    if (manualId) { processScan(manualId); manualInput.value = ''; }
                });
                manualInput.addEventListener('keydown', (e) => {
                    if (e.key === 'Enter') {
                        e.preventDefault();
                        const manualId = manualInput.value.trim();
                        if (manualId) { processScan(manualId); manualInput.value = ''; }
                    }
                });
                createCharts();
                
                updateFoundListUI();
                updateExceptionsListUI();
                updateScanLogUI();
                updateDashboard();

                // NOVO: Aplica estados carregados à UI
                updateActiveZoneUI(appState.activeZoneId);
                updateHuntModeUI();
            }

            // --- FUNÇÕES DA IDEIA A (Zona Ativa) ---
            function buildInventoryZoneUI() {
                const container = document.getElementById('inventory-zones-container');
                container.innerHTML = `
                    <button id="clear-active-zone-btn" class="w-full bg-slate-600 hover:bg-slate-500 text-white font-bold py-2 px-4 rounded-lg text-sm ${appState.activeZoneId ? '' : 'hidden'}">Limpar Zona Ativa</button>
                `;
                
                appState.inventoryZones.forEach(zone => {
                    if (!appState.inventoryZoneData.has(zone.id)) {
                         appState.inventoryZoneData.set(zone.id, new Set());
                    }
                   
                    const div = document.createElement('div');
                    div.className = "p-3 bg-slate-800 rounded-lg";
                    div.innerHTML = `
                        <div class="flex items-center justify-between mb-3">
                            <div>
                                <p class="font-semibold text-white">${zone.name}</p>
                                <p id="file-info-${zone.id}" class="text-xs text-slate-400">Nenhum ficheiro carregado.</p>
                            </div>
                            <button data-zone-id="${zone.id}" class="set-active-zone-btn bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-3 rounded-lg text-sm whitespace-nowrap">Ativar</button>
                        </div>
                        <div class="flex gap-2">
                             <button data-zone-id="${zone.id}" class="load-zone-file-btn bg-cyan-700 hover:bg-cyan-600 text-white font-bold py-2 px-3 rounded-lg text-sm w-full">Carregar Lista</button>
                             <input type="file" id="file-input-${zone.id}" class="hidden" accept=".txt,.csv,.xlsx">
                        </div>
                    `;
                    
                    const existingData = appState.inventoryZoneData.get(zone.id);
                    if (existingData && existingData.size > 0) {
                        const infoP = div.querySelector(`#file-info-${zone.id}`);
                        infoP.textContent = `${existingData.size} IDs carregados.`;
                        infoP.classList.add('text-green-400');
                    }
                    container.appendChild(div);
                });

                document.getElementById('clear-active-zone-btn').addEventListener('click', () => setActiveZone(null));

                document.querySelectorAll('.load-zone-file-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        document.getElementById(`file-input-${e.currentTarget.dataset.zoneId}`).click();
                    });
                });
                
                document.querySelectorAll('.set-active-zone-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        const zoneId = e.currentTarget.dataset.zoneId;
                        // Alternar: se clicar no mesmo, desativa.
                        const newActiveId = (appState.activeZoneId === zoneId) ? null : zoneId;
                        setActiveZone(newActiveId);
                    });
                });
                
                 document.querySelectorAll('input[type="file"]').forEach(input => {
                    if (input.id.startsWith('file-input-')) {
                        input.addEventListener('change', (e) => handleFileSelect(e, e.target.id.replace('file-input-', '')));
                    }
                });

                // Aplica o estado visual da zona ativa
                updateActiveZoneUI(appState.activeZoneId);
            }
            
            function setActiveZone(zoneId) {
                appState.activeZoneId = zoneId;
                updateActiveZoneUI(zoneId);
                saveToLocalStorage();
            }

            function updateActiveZoneUI(activeId) {
                // Atualiza barra de status global
                const statusBar = document.getElementById('global-status-bar');
                if (activeId) {
                    const zone = appState.inventoryZones.find(z => z.id === activeId);
                    statusBar.textContent = `ZONA ATIVA: ${zone ? zone.name.toUpperCase() : activeId}`;
                    statusBar.className = 'fixed top-0 left-0 right-0 z-20 p-2 text-center text-sm transition-all duration-300 bg-green-700 text-white font-bold';
                } else {
                    statusBar.textContent = '';
                    statusBar.className = 'fixed top-0 left-0 right-0 z-20 p-2 text-center text-sm transition-all duration-300';
                }

                // Atualiza botões
                document.querySelectorAll('.set-active-zone-btn').forEach(btn => {
                    if (btn.dataset.zoneId === activeId) {
                        btn.textContent = 'ATIVA';
                        btn.classList.replace('bg-blue-600', 'bg-green-600');
                        btn.classList.replace('hover:bg-blue-700', 'hover:bg-green-700');
                    } else {
                        btn.textContent = 'Ativar';
                        btn.classList.replace('bg-green-600', 'bg-blue-600');
                        btn.classList.replace('hover:bg-green-700', 'hover:bg-blue-700');
                    }
                });

                // Mostra/Esconde botão de limpar
                const clearBtn = document.getElementById('clear-active-zone-btn');
                if (clearBtn) {
                    clearBtn.classList.toggle('hidden', !activeId);
                }
            }
            
            // --- FUNÇÕES DA IDEIA B (Caça ao Tesouro) ---
            function toggleHuntMode() {
                const targetIdInput = document.getElementById('hunt-target-id');
                const targetId = targetIdInput.value.trim();
                
                if (appState.huntMode.isActive) {
                    // Desativar modo caça
                    appState.huntMode = { isActive: false, targetId: null };
                } else {
                    // Ativar modo caça
                    if (!targetId) {
                        alert("Por favor, digite um ID para caçar.");
                        return;
                    }
                    appState.huntMode = { isActive: true, targetId: targetId };
                    // Pausa o scanner se estiver no meio de um bip
                    appState.isPaused = false; 
                    if(appState.html5QrCode) appState.html5QrCode.pause(false);
                }
                updateHuntModeUI();
                saveToLocalStorage();
            }

            function updateHuntModeUI() {
                const targetIdInput = document.getElementById('hunt-target-id');
                const toggleBtn = document.getElementById('hunt-toggle-btn');
                const statusP = document.getElementById('hunt-status');

                if (appState.huntMode.isActive) {
                    targetIdInput.value = appState.huntMode.targetId;
                    targetIdInput.disabled = true;
                    toggleBtn.textContent = 'Cancelar';
                    toggleBtn.classList.replace('bg-blue-600', 'bg-red-600');
                    toggleBtn.classList.replace('hover:bg-blue-700', 'hover:bg-red-700');
                    statusP.textContent = `CAÇANDO: ${appState.huntMode.targetId}`;
                } else {
                    targetIdInput.value = '';
                    targetIdInput.disabled = false;
                    toggleBtn.textContent = 'Caçar';
                    toggleBtn.classList.replace('bg-red-600', 'bg-blue-600');
                    toggleBtn.classList.replace('hover:bg-red-700', 'hover:bg-blue-700');
                    statusP.textContent = '';
                }
            }


            function handleFileSelect(event, zoneId) {
                const file = event.target.files[0]; if (!file) return;
                const isMainSearch = zoneId === 'main';
                
                const reader = new FileReader();
                const processIds = (ids, fileName) => {
                    const idSet = new Set(ids);
                    if (isMainSearch) {
                        appState.idsToFind = idSet;
                        appState.foundIds = []; 
                        appState.scanHistory = [];
                        appState.scanLog = []; 
                        appState.notFoundIds = [];
                        document.getElementById('file-info').textContent = `"${fileName}" (${ids.length} IDs)`;
                        updateFoundListUI();
                        updateExceptionsListUI();
                        updateScanLogUI();
                        updateDashboard();
                    } else {
                        appState.inventoryZoneData.set(zoneId, idSet);
                         document.getElementById(`file-info-${zoneId}`).textContent = `${ids.length} IDs carregados.`;
                         document.getElementById(`file-info-${zoneId}`).classList.add('text-green-400');
                    }
                    saveToLocalStorage(); 
                };

                if (file.name.endsWith('.xlsx')) {
                    reader.onload = (e) => {
                        const data = new Uint8Array(e.target.result);
                        const workbook = XLSX.read(data, {type: 'array'});
                        const firstSheetName = workbook.SheetNames[0];
                        const worksheet = workbook.Sheets[firstSheetName];
                        const json = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
                        const ids = json.map(row => String(row[0])).filter(id => id && id.trim() !== '' && id !== 'undefined');
                        processIds(ids, file.name);
                    };
                    reader.readAsArrayBuffer(file);
                } else {
                    reader.onload = (e) => {
                        const text = e.target.result;
                        const ids = text.trim().split(/[\n\r,]+/).map(id => id.trim()).filter(id => id);
                        processIds(ids, file.name);
                    };
                    reader.readAsText(file);
                }
            }
            
            // --- FUNÇÃO PROCESSSCAN SUPER ATUALIZADA ---
            function processScan(scannedId) {
                // 1. MODO CAÇA AO TESOURO (Ideia B)
                // Se o modo caça está ativo, ele tem prioridade MÁXIMA.
                if (appState.huntMode.isActive) {
                    if (scannedId === appState.huntMode.targetId) {
                        // ENCONTROU O ALVO!
                        showFeedback('hunt_success', scannedId, "ITEM-ALVO ENCONTRADO!");
                        toggleHuntMode(); // Desativa o modo caça
                    }
                    // Se não for o item caçado, ignora TOTALMENTE o bip.
                    return; 
                }

                // Se não está no modo caça, continua o fluxo normal...
                if (appState.isPaused) return;

                if (appState.isFastMode) {
                    const now = Date.now();
                    if (now - appState.lastScanTime < 350) return; 
                    appState.lastScanTime = now;
                } else {
                    appState.isPaused = true; 
                }
                
                const logEntry = { id: scannedId, time: new Date() };

                // 2. MODO ZONA ATIVA (Ideia A - Detecção de Missort)
                const activeZoneId = appState.activeZoneId;
                if (activeZoneId) {
                    const activeZone = appState.inventoryZones.find(z => z.id === activeZoneId);
                    const activeZoneName = activeZone ? activeZone.name.toUpperCase() : 'ATIVA';

                    // Verifica se o item pertence a QUALQUER *OUTRA* zona
                    for (const [zoneId, idSet] of appState.inventoryZoneData.entries()) {
                        if (zoneId !== activeZoneId && idSet.has(scannedId)) {
                            // É UM MISSORT!
                            const foundZone = appState.inventoryZones.find(z => z.id === zoneId);
                            const foundZoneName = foundZone ? foundZone.name.toUpperCase() : 'OUTRA ZONA';
                            
                            logEntry.status = `Missort (Item de ${foundZoneName} em ${activeZoneName})`;
                            appState.scanLog.unshift(logEntry);
                            updateScanLogUI();
                            
                            showFeedback('warning_missort', scannedId, `ALERTA: ITEM DE ${foundZoneName}`);
                            saveToLocalStorage();
                            return; // Para o processamento aqui
                        }
                    }
                }
                
                // --- FLUXO NORMAL DE VERIFICAÇÃO ---
                // (Só chega aqui se NÃO for um missort e NÃO estiver em modo caça)

                // 3. Verifica se já foi encontrado (na lista principal)
                if (appState.foundIds.some(item => item.id === scannedId)) {
                    logEntry.status = 'Duplicado';
                    appState.scanLog.unshift(logEntry);
                    updateScanLogUI();
                    showFeedback('warning', scannedId, 'JÁ ENCONTRADO');
                    return;
                }
                
                // 4. Verifica a lista principal
                if (appState.idsToFind.has(scannedId)) {
                    logEntry.status = 'Encontrado (Principal)';
                    appState.scanLog.unshift(logEntry);
                    updateScanLogUI();
                    
                    showFeedback('success', scannedId);
                    appState.idsToFind.delete(scannedId);
                    appState.foundIds.unshift({ id: scannedId, timestamp: new Date() });
                    appState.scanHistory.push(new Date());
                    updateFoundListUI();
                    updateDashboard();
                    saveToLocalStorage(); 
                    return;
                }

                // 5. Verifica as Zonas de Inventário (para fins de log/contagem)
                for (const [zoneId, idSet] of appState.inventoryZoneData.entries()) {
                    if (idSet.has(scannedId)) {
                        // Nota: Se a Zona Ativa (Ideia A) estiver ligada, este código só
                        // será executado se o item pertencer à zona ativa (pois o missort
                        // já foi tratado acima).
                        const zone = appState.inventoryZones.find(z => z.id === zoneId);
                        const zoneName = zone ? zone.name.toUpperCase() : 'ZONA';
                        
                        logEntry.status = `Encontrado (${zoneName})`;
                        appState.scanLog.unshift(logEntry);
                        updateScanLogUI();
                        
                        showFeedback('success', scannedId, `ENCONTRADO (EM ${zoneName})`);
                        
                        const currentCount = appState.zoneFinds.get(zoneId) || 0;
                        appState.zoneFinds.set(zoneId, currentCount + 1);
                        updateDashboard();
                        saveToLocalStorage(); 
                        return;
                    }
                }
                
                // 6. Se não encontrou em lugar nenhum (Exceção)
                logEntry.status = 'Não Encontrado';
                appState.scanLog.unshift(logEntry);
                updateScanLogUI();
                
                appState.notFoundIds.unshift({ id: scannedId, timestamp: new Date() });
                updateExceptionsListUI();
                showFeedback('error', scannedId);
                saveToLocalStorage(); 
            }
            
            function setupTabs() {
                const tabButtons = document.querySelectorAll('.tab-btn');
                tabButtons.forEach(button => {
                    button.addEventListener('click', () => {
                        const viewId = button.dataset.view;
                        appState.currentView = viewId;
                        
                        tabButtons.forEach(btn => btn.classList.replace('tab-active', 'tab-inactive'));
                        button.classList.replace('tab-inactive', 'tab-active');
                        
                        document.querySelectorAll('[data-view-content]').forEach(view => {
                            view.classList.toggle('hidden', view.dataset.viewContent !== viewId);
                        });
                    });
                });
            }

            function exportFoundIds() {
                if (appState.foundIds.length === 0) { alert("Nenhum ID foi encontrado para exportar."); return; }
                let csvContent = "data:text/csv;charset=utf-8,ID_Encontrado,Data_Verificacao,Hora_Verificacao\n";
                appState.foundIds.forEach(item => {
                    const row = [item.id, item.timestamp.toLocaleDateString('pt-BR'), item.timestamp.toLocaleTimeString('pt-BR')].join(',');
                    csvContent += row + "\n";
                });
                const encodedUri = encodeURI(csvContent);
                const link = document.createElement("a");
                link.setAttribute("href", encodedUri);
                const date = new Date().toLocaleDateString('pt-BR').replace(/\//g, '-');
                link.setAttribute("download", `sessao_scanner_encontrados_${date}.csv`);
                document.body.appendChild(link); link.click(); document.body.removeChild(link);
            }
            
            function exportExceptions() {
                 if (appState.notFoundIds.length === 0) { alert("Nenhuma exceção foi encontrada para exportar."); return; }
                let csvContent = "data:text/csv;charset=utf-8,ID_Nao_Encontrado,Data_Verificacao,Hora_Verificacao\n";
                appState.notFoundIds.forEach(item => {
                    const row = [item.id, item.timestamp.toLocaleDateString('pt-BR'), item.timestamp.toLocaleTimeString('pt-BR')].join(',');
                    csvContent += row + "\n";
                });
                const encodedUri = encodeURI(csvContent);
                const link = document.createElement("a");
                link.setAttribute("href", encodedUri);
                const date = new Date().toLocaleDateString('pt-BR').replace(/\//g, '-');
                link.setAttribute("download", `sessao_scanner_excecoes_${date}.csv`);
                document.body.appendChild(link); link.click(); document.body.removeChild(link);
            }

            function startScanner() {
                appState.html5QrCode = new Html5Qrcode("reader");
                const config = { fps: 15, qrbox: (w, h) => { const s = Math.min(w, h) * 0.8; return { width: s, height: s }; } };
                appState.html5QrCode.start({ facingMode: "environment" }, config, (decodedText) => processScan(decodedText))
                    .catch(err => alert("ERRO AO INICIAR A CÂMARA: Por favor, verifique se deu permissão de acesso à câmara."));
            }
            
            function updateFoundListUI() {
                document.getElementById('found-count').textContent = appState.foundIds.length;
                const foundList = document.getElementById('found-list');
                if (appState.foundIds.length === 0) {
                    foundList.innerHTML = '<li class="text-slate-500">Nenhum item encontrado ainda.</li>';
                } else {
                    foundList.innerHTML = appState.foundIds.map(item => `<li class="p-2 bg-slate-700 rounded-md text-white flex justify-between"><span>${item.id}</span><span class="text-xs text-slate-400">${item.timestamp.toLocaleTimeString('pt-BR')}</span></li>`).join('');
                }
            }
            
            function updateExceptionsListUI() {
                 document.getElementById('exceptions-count').textContent = appState.notFoundIds.length;
                const exceptionsList = document.getElementById('exceptions-list');
                if (appState.notFoundIds.length === 0) {
                    exceptionsList.innerHTML = '<li class="text-slate-500">Nenhuma exceção registrada.</li>';
                } else {
                    exceptionsList.innerHTML = appState.notFoundIds.map(item => `<li class="p-2 bg-slate-700 rounded-md text-white flex justify-between"><span>${item.id}</span><span class="text-xs text-slate-400">${item.timestamp.toLocaleTimeString('pt-BR')}</span></li>`).join('');
                }
            }
            
            function updateScanLogUI() {
                const logList = document.getElementById('scan-log-list');
                if (appState.scanLog.length === 0) {
                    logList.innerHTML = '<li class="text-slate-500">Nenhuma atividade registrada.</li>';
                } else {
                    logList.innerHTML = appState.scanLog.slice(0, 50).map(item => { 
                        let statusColor = 'text-white';
                        if (item.status === 'Duplicado') statusColor = 'text-amber-400';
                        else if (item.status === 'Não Encontrado') statusColor = 'text-red-400';
                        else if (item.status.includes('Encontrado')) statusColor = 'text-green-400';
                        else if (item.status.includes('Missort')) statusColor = 'text-orange-400 font-bold';
                        
                        return `<li class="p-2 bg-slate-800 rounded-md flex justify-between items-center">
                            <div>
                                <span class="font-bold text-white">${item.id}</span>
                                <span class="block ${statusColor} text-xs">${item.status}</span>
                            </div>
                            <span class="text-xs text-slate-400">${item.time.toLocaleTimeString('pt-BR')}</span>
                        </li>`;
                    }).join('');
                }
            }

            function updateDashboard() {
                const totalItems = appState.idsToFind.size + appState.foundIds.length;
                const foundCount = appState.foundIds.length;
                const progress = totalItems > 0 ? (foundCount / totalItems) * 100 : 0;
                document.getElementById('progress-text').textContent = `${Math.round(progress)}%`;
                appState.charts.progress.data.datasets[0].data = [progress, 100 - progress];
                appState.charts.progress.update();

                if (appState.scanHistory.length > 1) {
                    const lastScans = appState.scanHistory.slice(-10);
                    let totalDiff = 0;
                    for (let i = 1; i < lastScans.length; i++) totalDiff += (lastScans[i] - lastScans[i-1]);
                    const avgTime = (totalDiff / (lastScans.length - 1)) / 1000;
                    if (!isNaN(avgTime) && avgTime > 0) {
                        document.getElementById('kpi-avg-time').textContent = `${avgTime.toFixed(1)} s`;
                        const bpm = avgTime > 0 ? Math.round(60 / avgTime) : '--';
                        document.getElementById('kpi-bpm').textContent = bpm;
                    } else {
                         document.getElementById('kpi-avg-time').textContent = '-- s';
                         document.getElementById('kpi-bpm').textContent = '--';
                    }
                } else {
                     document.getElementById('kpi-avg-time').textContent = '-- s';
                     document.getElementById('kpi-bpm').textContent = '--';
                }
                
                const zoneFindsContainer = document.getElementById('zone-finds-container');
                if (appState.zoneFinds.size === 0) {
                     zoneFindsContainer.innerHTML = '<p class="text-slate-500 text-center">Nenhum item de inventário escaneado ainda.</p>';
                } else {
                    zoneFindsContainer.innerHTML = '';
                    appState.zoneFinds.forEach((count, zoneId) => {
                        const zone = appState.inventoryZones.find(z => z.id === zoneId);
                        const zoneName = zone ? zone.name : zoneId;
                        const div = document.createElement('div');
                        div.className = "flex justify-between items-center bg-slate-800 p-2 rounded-lg";
                        div.innerHTML = `
                            <span class="font-medium text-slate-300">${zoneName}</span>
                            <span class="font-bold text-white text-lg">${count}</span>
                        `;
                        zoneFindsContainer.appendChild(div);
                    });
                }
            }

            function createCharts() {
                const progressCtx = document.getElementById('progressChart').getContext('2d');
                appState.charts.progress = new Chart(progressCtx, {
                    type: 'doughnut',
                    data: { datasets: [{ data: [0, 100], backgroundColor: ['#0ea5e9', '#334155'], borderColor: '#1e293b', borderWidth: 4, cutout: '75%' }] },
                    options: { responsive: true, maintainAspectRatio: false, plugins: { tooltip: { enabled: false } } }
                });
            }

            // --- FUNÇÃO SHOWFEEDBACK ATUALIZADA (Ideia A & B) ---
            function showFeedback(status, scannedId, messageOverride) {
                const message = messageOverride || (status === 'success' ? 'ENCONTRADO' : 'NÃO ENCONTRADO');
                const feedbackOverlay = document.getElementById('feedback-overlay');
                let pulseClass = "feedback-pulse";
                let bgColor = '';
                
                if (status === 'success') {
                    bgColor = 'radial-gradient(circle, rgba(34, 197, 94, 0.8) 0%, rgba(30, 41, 59, 0) 70%)';
                } else if (status === 'warning') {
                    bgColor = 'radial-gradient(circle, rgba(245, 158, 11, 0.8) 0%, rgba(30, 41, 59, 0) 70%)';
                } else if (status === 'warning_missort') {
                    bgColor = 'radial-gradient(circle, rgba(249, 115, 22, 0.8) 0%, rgba(30, 41, 59, 0) 70%)'; // Laranja
                } else if (status === 'hunt_success') {
                    bgColor = 'radial-gradient(circle, rgba(134, 239, 172, 0.9) 0%, rgba(30, 41, 59, 0) 70%)'; // Verde claro
                    pulseClass = "hunt-success-pulse"; // Animação especial
                } else { // error
                    bgColor = 'radial-gradient(circle, rgba(239, 68, 68, 0.8) 0%, rgba(30, 41, 59, 0) 70%)';
                }
                
                feedbackOverlay.style.background = bgColor;
                feedbackOverlay.innerHTML = `<div class="${pulseClass} text-center"><div class="text-6xl">${message}</div><div class="text-2xl mt-4 font-mono p-2 bg-black/30 rounded-lg">${scannedId}</div></div>`;
                feedbackOverlay.style.opacity = '1';
                
                playSound(status); // Toca o som correspondente
                
                if (navigator.vibrate) {
                    if (status === 'success') navigator.vibrate(200);
                    else if (status === 'error') navigator.vibrate([100, 50, 100]);
                    else if (status === 'warning') navigator.vibrate([80, 80]);
                    else if (status === 'warning_missort') navigator.vibrate([120, 60, 120]); // Vibração de alerta
                    else if (status === 'hunt_success') navigator.vibrate([500, 100, 500]); // Vibração longa
                }
                
                // Modo caça SEMPRE pausa e usa delay longo
                const isHunt = (status === 'hunt_success');
                const currentDelay = (appState.isFastMode && !isHunt) ? 250 : SCAN_DELAY;
                
                // Se for caça, o delay é ainda maior para celebrar
                const finalDelay = isHunt ? 2500 : currentDelay;
                
                setTimeout(() => {
                    feedbackOverlay.style.opacity = '0';
                    // Só des-pausa se não estiver no modo rápido
                    // E se não for o modo caça (que já foi desativado em toggleHuntMode)
                    if (!appState.isFastMode && !isHunt) { 
                        appState.isPaused = false;
                    }
                }, finalDelay);
            }
            
            function initAudio() { if (!appState.audioContext) appState.audioContext = new (window.AudioContext || window.webkitAudioContext)(); }
            
            // --- FUNÇÃO PLAYSOUND ATUALIZADA (Ideia A & B) ---
            function playSound(type) {
                if (!appState.audioContext) return;
                const osc = appState.audioContext.createOscillator();
                const gain = appState.audioContext.createGain();
                osc.connect(gain); gain.connect(appState.audioContext.destination);
                gain.gain.setValueAtTime(0.3, appState.audioContext.currentTime);
                
                if (type === 'success') { 
                    osc.frequency.setValueAtTime(1200, osc.context.currentTime); 
                } else if (type === 'error') { 
                    osc.frequency.setValueAtTime(180, osc.context.currentTime); osc.type = 'square'; 
                } else if (type === 'warning') { 
                    osc.frequency.setValueAtTime(600, osc.context.currentTime); osc.type = 'triangle'; 
                } else if (type === 'warning_missort') {
                    // Som de alerta (ex: dois tons)
                    osc.frequency.setValueAtTime(800, osc.context.currentTime);
                    osc.frequency.setValueAtTime(400, osc.context.currentTime + 0.07);
                    osc.type = 'sawtooth';
                } else if (type === 'hunt_success') {
                    // Som de sucesso! (ex: subindo)
                    osc.frequency.setValueAtTime(1000, osc.context.currentTime);
                    osc.frequency.linearRampToValueAtTime(2000, osc.context.currentTime + 0.3);
                }
                
                osc.start(); 
                osc.stop(osc.context.currentTime + (type === 'hunt_success' ? 0.4 : 0.15));
            }
            
            initialize();
        });
    </script>
</body>
</html>
