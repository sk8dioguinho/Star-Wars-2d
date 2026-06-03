html
<!DOCTYPE html>
<html lang="pt-PT">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Star Wars: Rogue Starfighter</title>
    <!-- Tailwind CSS para estilização moderna -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons para os ícones do HUD e Loja -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap');
        
        body {
            font-family: 'Orbitron', sans-serif;
            user-select: none;
            -webkit-user-select: none;
            touch-action: none;
            background-color: #030712;
            overflow: hidden;
        }

        /* Estilo para simular efeito de monitor holográfico */
        .holo-text {
            text-shadow: 0 0 8px rgba(56, 189, 248, 0.8), 0 0 20px rgba(56, 189, 248, 0.4);
        }
        
        .holo-border {
            box-shadow: inset 0 0 15px rgba(56, 189, 248, 0.3), 0 0 15px rgba(56, 189, 248, 0.2);
            border: 1px solid rgba(56, 189, 248, 0.4);
        }

        /* Rolagem elegante para dispositivos móveis */
        .custom-scroll::-webkit-scrollbar {
            width: 4px;
        }
        .custom-scroll::-webkit-scrollbar-track {
            background: rgba(15, 23, 42, 0.5);
        }
        .custom-scroll::-webkit-scrollbar-thumb {
            background: rgba(56, 189, 248, 0.5);
            border-radius: 2px;
        }

        @keyframes pulse-red {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }
        .alert-pulse {
            animation: pulse-red 1s infinite;
        }
    </style>
</head>
<body class="w-full h-screen relative flex items-center justify-center text-white">

    <!-- CONTAINER PRINCIPAL DO JOGO -->
    <div id="game-container" class="relative w-full max-w-md h-full bg-black overflow-hidden flex flex-col justify-between">
        
        <!-- TELA DE MENU INICIAL -->
        <div id="screen-menu" class="absolute inset-0 z-50 flex flex-col justify-between p-5 bg-gradient-to-b from-slate-950 via-black to-slate-950 transition-opacity duration-300">
            <!-- Cabeçalho -->
            <div class="text-center mt-6">
                <span class="text-[9px] text-yellow-400 tracking-[0.4em] uppercase font-bold block mb-1">Galaxy Defender</span>
                <h1 class="text-3xl font-black text-transparent bg-clip-text bg-gradient-to-r from-yellow-400 via-amber-200 to-yellow-500 tracking-wider mb-0.5">STAR WARS</h1>
                <h2 class="text-sky-400 text-sm tracking-[0.2em] font-bold uppercase holo-text">ROGUE STARFIGHTER</h2>
            </div>

            <!-- Nave Selecionada Atualmente -->
            <div class="bg-slate-950/80 border border-slate-800/80 rounded-2xl p-4 flex flex-col items-center my-2">
                <span class="text-[10px] text-slate-500 uppercase tracking-widest mb-2">O teu caça ativo</span>
                <div id="menu-ship-preview" class="w-24 h-24 flex items-center justify-center">
                    <!-- SVG renderizado dinamicamente via JS -->
                </div>
                <h3 id="menu-ship-name" class="font-bold text-base mt-2 text-white">X-Wing T-65</h3>
                <span id="menu-ship-desc" class="text-xs text-sky-400 font-bold uppercase tracking-wider">Equilibrado</span>
            </div>

            <!-- Caixa de Recurso Permanente -->
            <div class="flex justify-center mb-2">
                <div class="inline-flex items-center gap-2 bg-slate-900/90 border border-amber-500/30 px-4 py-1.5 rounded-full">
                    <i data-lucide="nut" class="w-4 h-4 text-amber-400"></i>
                    <span class="text-amber-400 font-bold text-sm" id="menu-scrap-display">0</span>
                    <span class="text-[9px] text-slate-500 uppercase tracking-wider">Sucatas</span>
                </div>
            </div>

            <!-- Botões de Ação do Menu -->
            <div class="space-y-3 mb-4">
                <button onclick="startGame()" class="w-full py-3.5 bg-gradient-to-r from-sky-600 to-blue-700 hover:from-sky-500 hover:to-blue-600 text-white rounded-xl font-bold tracking-widest text-base uppercase transition-all duration-200 shadow-[0_0_20px_rgba(56,189,248,0.3)]">
                    Iniciar Missão
                </button>
                
                <button onclick="openStore()" class="w-full py-3 bg-slate-900 border border-amber-500/40 hover:border-amber-400 hover:bg-slate-850 text-amber-400 rounded-xl font-bold tracking-widest text-sm uppercase transition-all duration-200 flex items-center justify-center gap-2">
                    <i data-lucide="shopping-bag" class="w-4 h-4"></i> Loja de Caças
                </button>

                <div class="flex justify-between text-[11px] text-slate-500 px-2 pt-1">
                    <span id="high-score-label">Recorde: 0</span>
                    <button onclick="toggleAudio()" class="flex items-center gap-1 focus:outline-none">
                        <i id="audio-icon" data-lucide="volume-2" class="w-3.5 h-3.5"></i>
                        <span id="audio-status">Som Ligado</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- TELA DA LOJA DE NAVES -->
        <div id="screen-store" class="absolute inset-0 z-50 hidden flex flex-col justify-between p-5 bg-gradient-to-b from-slate-950 via-slate-900 to-black transition-opacity duration-300">
            <!-- Cabeçalho da Loja -->
            <div class="flex justify-between items-center mt-4 pb-2 border-b border-slate-800">
                <div>
                    <h2 class="text-amber-400 text-lg font-black uppercase tracking-wider holo-text flex items-center gap-2">
                        <i data-lucide="shopping-bag" class="w-5 h-5"></i> Hangar de Compra
                    </h2>
                    <p class="text-[10px] text-slate-400">Adquire novos caças estelares rebeldes ou imperiais</p>
                </div>
                <div class="flex items-center gap-1.5 bg-slate-950 px-3 py-1 rounded-full border border-amber-500/30">
                    <i data-lucide="nut" class="w-3.5 h-3.5 text-amber-400"></i>
                    <span class="text-amber-400 font-bold text-xs" id="store-scrap-display">0</span>
                </div>
            </div>

            <!-- Lista de Naves (Scrollable) -->
            <div id="store-list" class="my-3 flex-1 overflow-y-auto space-y-3 pr-1 custom-scroll">
                <!-- Injetado dinamicamente via JS -->
            </div>

            <!-- Botão de Voltar da Loja -->
            <div class="mb-4">
                <button onclick="closeStore()" class="w-full py-3 bg-slate-900 hover:bg-slate-850 text-slate-300 rounded-xl font-bold tracking-widest text-xs uppercase transition-all duration-200 border border-slate-800">
                    Voltar ao Menu
                </button>
            </div>
        </div>

        <!-- TELA DE UPGRADES / COMPRA EM PARTIDA -->
        <div id="screen-upgrades" class="absolute inset-0 z-40 hidden flex flex-col justify-between p-5 bg-slate-950/95 transition-opacity duration-300">
            <div class="text-center mt-6">
                <h2 class="text-sky-400 text-lg font-bold uppercase tracking-wider holo-text">Base Rebelde: Upgrades</h2>
                <p class="text-[10px] text-slate-400 mt-0.5">Melhora o teu caça ativo para esta partida</p>
                
                <div class="inline-flex items-center gap-2 bg-slate-900 border border-amber-500/30 px-3 py-1.5 rounded-full mt-3">
                    <i data-lucide="nut" class="w-4 h-4 text-amber-400"></i>
                    <span class="text-amber-400 font-bold text-xs" id="upgrade-scrap-display">0</span>
                    <span class="text-[9px] text-slate-500 uppercase">Sucatas</span>
                </div>
            </div>

            <!-- Lista de Upgrades -->
            <div class="my-auto space-y-3.5">
                <!-- Upgrade 1: Laser -->
                <div class="bg-slate-900/90 p-3.5 rounded-xl border border-slate-800 flex justify-between items-center">
                    <div class="space-y-0.5">
                        <span class="font-bold text-xs block text-white">Canhões Laser Avançados</span>
                        <span class="text-[10px] text-slate-400 block" id="laser-desc">Disparos paralelos ou adicionais</span>
                    </div>
                    <button id="btn-up-laser" onclick="buyUpgrade('laser')" class="px-3 py-2 bg-sky-600 hover:bg-sky-500 disabled:bg-slate-800 disabled:text-slate-500 rounded-lg text-xs font-bold transition-all flex items-center gap-1">
                        <span id="btn-up-laser-cost">50</span> <i data-lucide="nut" class="w-3.5 h-3.5"></i>
                    </button>
                </div>

                <!-- Upgrade 2: Escudo Máximo -->
                <div class="bg-slate-900/90 p-3.5 rounded-xl border border-slate-800 flex justify-between items-center">
                    <div class="space-y-0.5">
                        <span class="font-bold text-xs block text-white">Defletores de Força</span>
                        <span class="text-[10px] text-slate-400 block" id="shield-desc">Amplia o teto do escudo em +25%</span>
                    </div>
                    <button id="btn-up-shield" onclick="buyUpgrade('shield')" class="px-3 py-2 bg-sky-600 hover:bg-sky-500 disabled:bg-slate-800 disabled:text-slate-500 rounded-lg text-xs font-bold transition-all flex items-center gap-1">
                        <span id="btn-up-shield-cost">40</span> <i data-lucide="nut" class="w-3.5 h-3.5"></i>
                    </button>
                </div>

                <!-- Upgrade 3: Torpedos -->
                <div class="bg-slate-900/90 p-3.5 rounded-xl border border-slate-800 flex justify-between items-center">
                    <div class="space-y-0.5">
                        <span class="font-bold text-xs block text-white">Torpedos de Prótons</span>
                        <span class="text-[10px] text-slate-400 block">Ataque devastador em área (Máx: 3)</span>
                    </div>
                    <button id="btn-up-torpedo" onclick="buyUpgrade('torpedo')" class="px-3 py-2 bg-sky-600 hover:bg-sky-500 disabled:bg-slate-800 disabled:text-slate-500 rounded-lg text-xs font-bold transition-all flex items-center gap-1">
                        <span id="btn-up-torpedo-cost">30</span> <i data-lucide="nut" class="w-3.5 h-3.5"></i>
                    </button>
                </div>
            </div>

            <!-- Botão de Voltar de Upgrades -->
            <div class="space-y-2 mb-4">
                <button onclick="resumeGameFromUpgrade()" class="w-full py-3 bg-emerald-600 hover:bg-emerald-500 text-white rounded-xl font-bold tracking-widest text-xs uppercase transition-all duration-200">
                    Retornar à Batalha
                </button>
            </div>
        </div>

        <!-- HUD DE COMBATE (TOPO) -->
        <div id="game-hud" class="absolute top-0 inset-x-0 z-30 p-4 flex justify-between items-start pointer-events-none transition-opacity duration-300 opacity-0">
            <!-- Lado Esquerdo: Vida e Escudo -->
            <div class="w-1/2 space-y-1.5">
                <!-- Escudo Defletor -->
                <div class="space-y-0.5">
                    <div class="flex justify-between text-[9px] tracking-wider text-sky-400 font-bold uppercase">
                        <span class="flex items-center gap-1"><i data-lucide="shield" class="w-2.5 h-2.5"></i> Escudo</span>
                        <span id="hud-shield-val">100%</span>
                    </div>
                    <div class="w-full h-1.5 bg-slate-950 rounded-full border border-sky-500/20 p-0.5 overflow-hidden">
                        <div id="hud-shield-bar" class="h-full bg-sky-400 rounded-full transition-all duration-100" style="width: 100%;"></div>
                    </div>
                </div>

                <!-- Integridade do Casco -->
                <div class="space-y-0.5">
                    <div class="flex justify-between text-[9px] tracking-wider text-red-500 font-bold uppercase">
                        <span class="flex items-center gap-1"><i data-lucide="heart" class="w-2.5 h-2.5"></i> Casco</span>
                        <span id="hud-health-val">100%</span>
                    </div>
                    <div class="w-full h-1.5 bg-slate-950 rounded-full border border-red-500/20 p-0.5 overflow-hidden">
                        <div id="hud-health-bar" class="h-full bg-red-500 rounded-full transition-all duration-100" style="width: 100%;"></div>
                    </div>
                </div>
            </div>

            <!-- Lado Direito: Pontuação, Nível e Sucatas -->
            <div class="flex flex-col items-end space-y-1">
                <div class="text-right">
                    <div id="hud-level-tag" class="text-[9px] text-yellow-400 font-bold uppercase tracking-widest bg-yellow-950/40 border border-yellow-500/20 px-1.5 py-0.5 rounded">NÍVEL 1</div>
                </div>
                <div class="text-right">
                    <div id="hud-score" class="text-base font-black text-amber-400 tracking-wider leading-none">0</div>
                </div>
                <div class="flex items-center gap-1 bg-slate-900/80 px-2 py-0.5 rounded border border-slate-700/50 text-[10px]">
                    <i data-lucide="nut" class="w-3 h-3 text-amber-400"></i>
                    <span id="hud-scrap" class="text-amber-400 font-bold">0</span>
                </div>
            </div>
        </div>

        <!-- CONTROLES DO JOGO DE SOBREPOSIÇÃO -->
        <div id="game-controls" class="absolute bottom-0 inset-x-0 z-30 p-4 flex justify-between items-end pointer-events-none transition-opacity duration-300 opacity-0">
            <!-- Botão de Pausa -->
            <button id="btn-pause" class="pointer-events-auto p-3 bg-slate-950/85 border border-slate-800 rounded-full flex items-center justify-center active:scale-90 transition-transform text-slate-300">
                <i data-lucide="pause" class="w-4.5 h-4.5"></i>
            </button>

            <!-- Indicador do Chefe / Progresso da Wave -->
            <div id="wave-progress-container" class="flex-1 mx-3 mb-1.5 flex flex-col items-center">
                <span id="wave-title" class="text-[8px] text-slate-400 uppercase tracking-widest mb-1 font-bold">Avanço da Frota Imperial</span>
                <div class="w-full h-1.5 bg-slate-950 rounded-full border border-slate-800/80 overflow-hidden">
                    <div id="wave-progress-bar" class="h-full bg-amber-500 transition-all duration-300" style="width: 0%;"></div>
                </div>
            </div>

            <!-- Botão de Torpedos de Prótons -->
            <button id="btn-torpedo" class="pointer-events-auto relative p-3.5 bg-red-950/90 border-2 border-red-500/80 rounded-full flex items-center justify-center active:scale-95 transition-all text-red-500 shadow-[0_0_15px_rgba(239,68,68,0.3)]">
                <i data-lucide="crosshair" class="w-6 h-6 alert-pulse"></i>
                <span id="torpedo-count" class="absolute -top-1 -right-1 bg-red-500 text-white text-[9px] font-bold w-4.5 h-4.5 rounded-full flex items-center justify-center">0</span>
            </button>
        </div>

        <!-- TELA DE GAME OVER -->
        <div id="screen-gameover" class="absolute inset-0 z-50 hidden flex flex-col justify-between p-5 bg-black/95 transition-opacity duration-300">
            <div class="text-center mt-12 space-y-2">
                <div class="text-red-500 alert-pulse">
                    <i data-lucide="shield-alert" class="w-14 h-14 mx-auto"></i>
                </div>
                <h2 class="text-xl font-black text-red-500 tracking-wider uppercase">CAÇA ABATIDO</h2>
                <p class="text-[11px] text-slate-400 max-w-xs mx-auto">O teu caça foi desintegrado. A Aliança Rebelde ainda conta com as peças recolhidas em combate para manter a frota operacional.</p>
            </div>

            <!-- Resumo dos Resultados -->
            <div class="bg-slate-900/60 p-4 rounded-xl border border-slate-800 space-y-2.5 my-auto max-w-sm mx-auto w-full">
                <div class="flex justify-between items-center text-xs border-b border-slate-800/80 pb-1.5">
                    <span class="text-slate-400">Nível Atingido</span>
                    <span id="go-level" class="font-bold text-yellow-400">Nível 1</span>
                </div>
                <div class="flex justify-between items-center text-xs border-b border-slate-800/80 pb-1.5">
                    <span class="text-slate-400">Pontuação Total</span>
                    <span id="go-score" class="font-bold text-amber-400">0</span>
                </div>
                <div class="flex justify-between items-center text-xs border-b border-slate-800/80 pb-1.5">
                    <span class="text-slate-400">Inimigos Abatidos</span>
                    <span id="go-kills" class="font-bold text-white">0</span>
                </div>
                <div class="flex justify-between items-center text-xs pb-1.5">
                    <span class="text-slate-400">Sucata Coletada</span>
                    <span id="go-scrap" class="font-bold text-yellow-500 flex items-center gap-1"><i data-lucide="nut" class="w-3.5 h-3.5"></i> 0</span>
                </div>
                <div class="flex justify-between items-center text-xs border-t border-slate-800 pt-2 text-sky-400 font-bold">
                    <span>Hangar Atualizado</span>
                    <span id="go-total-scrap" class="flex items-center gap-1"><i data-lucide="nut" class="w-3.5 h-3.5"></i> 0</span>
                </div>
            </div>

            <!-- Botões Finais -->
            <div class="space-y-2.5 mb-4">
                <button onclick="restartGame()" class="w-full py-3.5 bg-gradient-to-r from-red-600 to-red-800 text-white rounded-xl font-bold tracking-widest text-sm uppercase transition-all duration-200">
                    Tentar Novamente
                </button>
                <button onclick="goToMenu()" class="w-full py-2.5 bg-slate-900 text-slate-300 rounded-xl font-bold tracking-widest text-[11px] uppercase transition-all duration-200">
                    Menu Principal
                </button>
            </div>
        </div>

        <!-- TELA DE VITÓRIA DO NÍVEL -->
        <div id="screen-victory" class="absolute inset-0 z-50 hidden flex flex-col justify-between p-5 bg-black/95 transition-opacity duration-300">
            <div class="text-center mt-12 space-y-2">
                <div class="text-yellow-400 animate-bounce">
                    <i data-lucide="trophy" class="w-14 h-14 mx-auto"></i>
                </div>
                <h2 id="victory-headline" class="text-xl font-black text-yellow-400 tracking-wider uppercase">NÍVEL CONCLUÍDO</h2>
                <p id="victory-subline" class="text-[11px] text-slate-400 max-w-xs mx-auto">O Star Destroyer Imperial foi neutralizado e as forças rebeldes conseguiram escapar!</p>
            </div>

            <!-- Estatísticas da Vitória -->
            <div class="bg-slate-900/60 p-4 rounded-xl border border-slate-800 space-y-2.5 my-auto max-w-sm mx-auto w-full">
                <div class="flex justify-between items-center text-xs border-b border-slate-800/80 pb-1.5">
                    <span class="text-slate-400">Nível Concluído</span>
                    <span id="vic-level" class="font-bold text-yellow-400">Nível 1</span>
                </div>
                <div class="flex justify-between items-center text-xs border-b border-slate-800/80 pb-1.5">
                    <span class="text-slate-400">Bónus de Conclusão</span>
                    <span class="font-bold text-emerald-400">+500 pts</span>
                </div>
                <div class="flex justify-between items-center text-xs border-b border-slate-800/80 pb-1.5">
                    <span class="text-slate-400">Prémio de Batalha</span>
                    <span id="vic-bonus-type" class="font-bold text-yellow-400 flex items-center gap-1"><i data-lucide="nut" class="w-3.5 h-3.5"></i> +150</span>
                </div>
                <div class="flex justify-between items-center text-xs">
                    <span class="text-slate-400">Sucata em Missão</span>
                    <span id="vic-scrap" class="font-bold text-amber-500 flex items-center gap-1"><i data-lucide="nut" class="w-3.5 h-3.5"></i> 0</span>
                </div>
                <div class="flex justify-between items-center text-xs border-t border-slate-800 pt-2 text-sky-400 font-bold">
                    <span>Hangar Atualizado</span>
                    <span id="vic-total-scrap" class="flex items-center gap-1"><i data-lucide="nut" class="w-3.5 h-3.5"></i> 0</span>
                </div>
            </div>

            <!-- Botões Finais -->
            <div class="space-y-2.5 mb-4">
                <button onclick="advanceLevel()" class="w-full py-3.5 bg-gradient-to-r from-emerald-600 to-teal-700 text-white rounded-xl font-bold tracking-widest text-sm uppercase transition-all duration-200">
                    Avançar Próximo Nível
                </button>
                <button onclick="goToMenu()" class="w-full py-2.5 bg-slate-900 text-slate-300 rounded-xl font-bold tracking-widest text-[11px] uppercase transition-all duration-200">
                    Menu Principal
                </button>
            </div>
        </div>

        <!-- CANVAS DO JOGO -->
        <canvas id="game-canvas" class="w-full h-full block bg-gray-950"></canvas>

    </div>

    <!-- SISTEMA DE JOGO -->
    <script>
        // Inicializar ícones do Lucide
        lucide.createIcons();

        // Canvas e contexto
        const canvas = document.getElementById('game-canvas');
        const ctx = canvas.getContext('2d');

        // Configurações do jogo e estado
        let gameActive = false;
        let isPaused = false;
        let isLoopRunning = false; // Guardião para prevenir duplicidade de loops gráficos
        let score = 0;
        let kills = 0;
        let scrapCollectedInSession = 0; // Sucatas apanhadas durante a gameplay atual
        let gameLevel = 1; // Nível atual da sessão

        // Economia do Utilizador (Persistida em localStorage)
        let totalScrap = parseInt(localStorage.getItem('starwars_scrap') || '0');
        let unlockedShips = JSON.parse(localStorage.getItem('starwars_unlocked') || '["xwing", "awing"]');
        let selectedShipType = localStorage.getItem('starwars_selected') || 'xwing';

        // DEFINIÇÃO DETALHADA DE TODAS AS NAVES COMPRÁVEIS
        const SHIP_PRESETS = {
            xwing: {
                id: 'xwing',
                name: 'X-Wing T-65',
                desc: 'Equilibrado / Rebelde',
                price: 0,
                maxShield: 100,
                maxHealth: 100,
                speed: 8,
                laserLevel: 1,
                startingTorpedos: 1,
                bulletStyle: 'double',
                drawFn: drawXwingSVG
            },
            awing: {
                id: 'awing',
                name: 'A-Wing RZ-1',
                desc: 'Veloz / Baixa Blindagem',
                price: 0,
                maxShield: 60,
                maxHealth: 80,
                speed: 11,
                laserLevel: 1,
                startingTorpedos: 1,
                bulletStyle: 'dual-fast',
                drawFn: drawAwingSVG
            },
            ywing: {
                id: 'ywing',
                name: 'Y-Wing BTL-A4',
                desc: 'Tanque / Escudo Pesado',
                price: 100,
                maxShield: 180,
                maxHealth: 150,
                speed: 6.5,
                laserLevel: 1,
                startingTorpedos: 2,
                bulletStyle: 'heavy-double',
                drawFn: drawYwingSVG
            },
            tieinterceptor: {
                id: 'tieinterceptor',
                name: 'TIE Interceptor Imperial',
                desc: 'Ataque Triplo Rápido',
                price: 250,
                maxShield: 80,
                maxHealth: 100,
                speed: 10.5,
                laserLevel: 2,
                startingTorpedos: 1,
                bulletStyle: 'triple',
                drawFn: drawTieIntSVG
            },
            millennium: {
                id: 'millennium',
                name: 'Millennium Falcon',
                desc: 'Lendária / Lasers Quádruplos',
                price: 500,
                maxShield: 220,
                maxHealth: 200,
                speed: 8.5,
                laserLevel: 3,
                startingTorpedos: 3,
                bulletStyle: 'quad',
                drawFn: drawFalconSVG
            }
        };

        // Estado ativo do caça do jogador
        let player = {
            x: 0,
            y: 0,
            width: 50,
            height: 50,
            shield: 100,
            maxShield: 100,
            health: 100,
            maxHealth: 100,
            speed: 8,
            laserLevel: 1,
            torpedos: 1,
            targetX: 0,
            targetY: 0,
            bulletStyle: 'double'
        };

        // Entidades do jogo
        let stars = [];
        let lasers = [];
        let enemies = [];
        let enemyLasers = [];
        let asteroids = [];
        let items = [];
        let explosions = [];
        let boss = null;

        // Controle de Waves e spawning
        let waveProgress = 0;
        let bossActive = false;
        let bossDefeated = false;
        let lastEnemySpawn = 0;
        let lastAsteroidSpawn = 0;
        let nextWaveTarget = 120; // Pontos para invocar o Boss

        // Áudio Sintetizado (Web Audio API)
        let audioEnabled = true;
        let audioCtx = null;

        // Ajuste de tamanho dinâmico do Canvas
        function resizeCanvas() {
            const container = document.getElementById('game-container');
            const rect = container.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            if (player) {
                player.x = canvas.width / 2;
                player.y = canvas.height * 0.8;
                player.targetX = player.x;
                player.targetY = player.y;
            }
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // Criar estrelas ao fundo
        function createStars() {
            stars = [];
            for (let i = 0; i < 70; i++) {
                stars.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    size: Math.random() * 2,
                    speed: Math.random() * 2.5 + 0.5
                });
            }
        }
        createStars();

        // --- SVGs VETORIAIS DE PREVISUALIZAÇÃO (SISTEMA DE UI E LOJA) ---

        function drawXwingSVG() {
            return `<svg class="w-full h-full text-slate-300" viewBox="0 0 100 100" fill="currentColor">
                <path d="M50,12 L54,32 L54,75 L50,85 L46,75 L46,32 Z" fill="#cbd5e1"/>
                <path d="M50,45 L15,48 L15,55 L46,52 Z" fill="#94a3b8"/>
                <path d="M50,45 L85,48 L85,55 L54,52 Z" fill="#94a3b8"/>
                <path d="M11,40 L16,40 L16,58 L11,58 Z" fill="#ef4444"/>
                <path d="M84,40 L89,40 L89,58 L84,58 Z" fill="#ef4444"/>
            </svg>`;
        }

        function drawAwingSVG() {
            return `<svg class="w-full h-full text-red-500" viewBox="0 0 100 100" fill="currentColor">
                <path d="M50,15 L66,73 L58,78 L50,71 L42,78 L34,73 Z" fill="#f1f5f9"/>
                <path d="M34,58 L30,78 M66,58 L70,78" stroke="#ef4444" stroke-width="3"/>
                <path d="M50,26 L56,48 L44,48 Z" fill="#ef4444"/>
            </svg>`;
        }

        function drawYwingSVG() {
            return `<svg class="w-full h-full text-yellow-500" viewBox="0 0 100 100" fill="currentColor">
                <path d="M50,10 L55,30 L55,60 L50,70 L45,60 L45,30 Z" fill="#e2e8f0"/>
                <path d="M30,40 L45,45 L45,55 L30,60 Z" fill="#78716c"/>
                <path d="M70,40 L55,45 L55,55 L70,60 Z" fill="#78716c"/>
                <path d="M25,35 L33,35 L33,80 L25,80 Z" fill="#f59e0b"/>
                <path d="M67,35 L75,35 L75,80 L67,80 Z" fill="#f59e0b"/>
                <circle cx="50" cy="22" r="4" fill="#f59e0b"/>
            </svg>`;
        }

        function drawTieIntSVG() {
            return `<svg class="w-full h-full text-sky-500" viewBox="0 0 100 100" fill="currentColor">
                <circle cx="50" cy="50" r="10" fill="#475569" stroke="#000" stroke-width="2"/>
                <circle cx="50" cy="50" r="5" fill="#0f172a"/>
                <path d="M20,25 L40,50 L20,75 L15,50 Z" fill="#1e293b" stroke="#64748b" stroke-width="2"/>
                <path d="M80,25 L60,50 L80,75 L85,50 Z" fill="#1e293b" stroke="#64748b" stroke-width="2"/>
                <line x1="38" y1="50" x2="62" y2="50" stroke="#94a3b8" stroke-width="3"/>
            </svg>`;
        }

        function drawFalconSVG() {
            return `<svg class="w-full h-full text-amber-500" viewBox="0 0 100 100" fill="currentColor">
                <circle cx="50" cy="52" r="30" fill="#cbd5e1" stroke="#94a3b8" stroke-width="2"/>
                <path d="M38,35 L38,15 L45,15 L45,30 Z" fill="#cbd5e1" stroke="#94a3b8" stroke-width="1.5"/>
                <path d="M62,35 L62,15 L55,15 L55,30 Z" fill="#cbd5e1" stroke="#94a3b8" stroke-width="1.5"/>
                <rect x="74" y="38" width="10" height="15" rx="3" fill="#64748b"/>
                <line x1="68" y1="45" x2="74" y2="45" stroke="#cbd5e1" stroke-width="4"/>
                <path d="M28,72 Q50,85 72,72" fill="none" stroke="#06b6d4" stroke-width="4" stroke-linecap="round"/>
            </svg>`;
        }

        // --- SISTEMA DE ÁUDIO SINTETIZADO ---
        function initAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        }

        function toggleAudio() {
            audioEnabled = !audioEnabled;
            const statusText = document.getElementById('audio-status');
            const icon = document.getElementById('audio-icon');
            
            if (audioEnabled) {
                statusText.innerText = "Som Ligado";
                icon.setAttribute('data-lucide', 'volume-2');
                initAudio();
            } else {
                statusText.innerText = "Som Mudo";
                icon.setAttribute('data-lucide', 'volume-x');
            }
            lucide.createIcons();
        }

        function playLaserSound(isPlayer = true) {
            if (!audioEnabled) return;
            initAudio();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            
            if (isPlayer) {
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(850, audioCtx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(160, audioCtx.currentTime + 0.15);
                gain.gain.setValueAtTime(0.12, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.15);
                osc.start();
                osc.stop(audioCtx.currentTime + 0.15);
            } else {
                osc.type = 'square';
                osc.frequency.setValueAtTime(550, audioCtx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(90, audioCtx.currentTime + 0.18);
                gain.gain.setValueAtTime(0.08, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.18);
                osc.start();
                osc.stop(audioCtx.currentTime + 0.18);
            }
        }

        function playLaserDeathStarSound() {
            if (!audioEnabled) return;
            initAudio();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.type = 'sawtooth';
            osc.frequency.setValueAtTime(120, audioCtx.currentTime);
            osc.frequency.linearRampToValueAtTime(40, audioCtx.currentTime + 0.5);
            gain.gain.setValueAtTime(0.25, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.5);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.5);
        }

        function playExplosionSound(isBig = false) {
            if (!audioEnabled) return;
            initAudio();
            const bufferSize = audioCtx.sampleRate * (isBig ? 0.9 : 0.45);
            const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
            const data = buffer.getChannelData(0);
            
            for (let i = 0; i < bufferSize; i++) {
                data[i] = Math.random() * 2 - 1;
            }
            
            const noise = audioCtx.createBufferSource();
            noise.buffer = buffer;
            const filter = audioCtx.createBiquadFilter();
            filter.type = 'lowpass';
            filter.frequency.setValueAtTime(isBig ? 180 : 350, audioCtx.currentTime);
            filter.frequency.exponentialRampToValueAtTime(10, audioCtx.currentTime + (isBig ? 0.9 : 0.45));
            
            const gain = audioCtx.createGain();
            gain.gain.setValueAtTime(isBig ? 0.35 : 0.18, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + (isBig ? 0.9 : 0.45));
            
            noise.connect(filter);
            filter.connect(gain);
            gain.connect(audioCtx.destination);
            noise.start();
        }

        function playShieldHitSound() {
            if (!audioEnabled) return;
            initAudio();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = 'sine';
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.frequency.setValueAtTime(1100, audioCtx.currentTime);
            osc.frequency.linearRampToValueAtTime(1400, audioCtx.currentTime + 0.08);
            gain.gain.setValueAtTime(0.12, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.08);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.08);
        }

        function playUpgradeSound() {
            if (!audioEnabled) return;
            initAudio();
            const now = audioCtx.currentTime;
            const notes = [440, 554, 659, 880];
            notes.forEach((freq, idx) => {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'triangle';
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.frequency.setValueAtTime(freq, now + idx * 0.07);
                gain.gain.setValueAtTime(0.1, now + idx * 0.07);
                gain.gain.exponentialRampToValueAtTime(0.01, now + idx * 0.07 + 0.12);
                osc.start(now + idx * 0.07);
                osc.stop(now + idx * 0.07 + 0.12);
            });
        }

        // --- SISTEMAS DE NAVEGAÇÃO E TELA DE LOJA ---

        function updateMenuShipPreview() {
            const preset = SHIP_PRESETS[selectedShipType];
            document.getElementById('menu-ship-preview').innerHTML = preset.drawFn();
            document.getElementById('menu-ship-name').innerText = preset.name;
            document.getElementById('menu-ship-desc').innerText = preset.desc;
            document.getElementById('menu-scrap-display').innerText = totalScrap;
        }
        updateMenuShipPreview();

        function openStore() {
            initAudio();
            document.getElementById('store-scrap-display').innerText = totalScrap;
            renderStoreList();
            document.getElementById('screen-store').classList.remove('hidden');
        }

        function closeStore() {
            document.getElementById('screen-store').classList.add('hidden');
            updateMenuShipPreview();
        }

        function renderStoreList() {
            const listContainer = document.getElementById('store-list');
            listContainer.innerHTML = '';

            Object.keys(SHIP_PRESETS).forEach(key => {
                const ship = SHIP_PRESETS[key];
                const isUnlocked = unlockedShips.includes(key);
                const isSelected = selectedShipType === key;

                let actionBtnHTML = '';
                if (isSelected) {
                    actionBtnHTML = `<span class="px-3 py-1.5 bg-emerald-950 text-emerald-400 border border-emerald-500/50 rounded-lg text-xs font-bold uppercase tracking-wider">Ativa</span>`;
                } else if (isUnlocked) {
                    actionBtnHTML = `<button onclick="selectShip('${key}')" class="px-4 py-1.5 bg-sky-600 hover:bg-sky-500 rounded-lg text-xs font-bold uppercase tracking-wider">Equipar</button>`;
                } else {
                    const canAfford = totalScrap >= ship.price;
                    actionBtnHTML = `<button onclick="buyShip('${key}')" ${canAfford ? '' : 'disabled'} class="px-3 py-1.5 bg-amber-600 hover:bg-amber-500 disabled:bg-slate-800 disabled:text-slate-500 rounded-lg text-xs font-bold uppercase tracking-wider flex items-center gap-1">
                        ${ship.price} <i data-lucide="nut" class="w-3.5 h-3.5"></i>
                    </button>`;
                }

                const itemHTML = `
                    <div class="bg-slate-900/90 border ${isSelected ? 'border-sky-500' : 'border-slate-800'} rounded-xl p-3 flex items-center gap-3">
                        <div class="w-16 h-16 flex-shrink-0 bg-black/60 rounded-lg border border-slate-800 p-1">
                            ${ship.drawFn()}
                        </div>
                        <div class="flex-1 min-w-0">
                            <h4 class="font-bold text-xs text-white truncate">${ship.name}</h4>
                            <p class="text-[10px] text-slate-400 truncate">${ship.desc}</p>
                            <div class="flex gap-2.5 mt-1 text-[9px] text-slate-500 font-bold">
                                <span class="flex items-center gap-0.5 text-sky-400"><i data-lucide="shield" class="w-2.5 h-2.5"></i> ${ship.maxShield}</span>
                                <span class="flex items-center gap-0.5 text-red-400"><i data-lucide="heart" class="w-2.5 h-2.5"></i> ${ship.maxHealth}</span>
                                <span class="flex items-center gap-0.5 text-emerald-400"><i data-lucide="zap" class="w-2.5 h-2.5"></i> ${ship.speed}</span>
                            </div>
                        </div>
                        <div class="flex-shrink-0">
                            ${actionBtnHTML}
                        </div>
                    </div>
                `;
                listContainer.insertAdjacentHTML('beforeend', itemHTML);
            });
            lucide.createIcons();
        }

        function buyShip(key) {
            const ship = SHIP_PRESETS[key];
            if (totalScrap >= ship.price && !unlockedShips.includes(key)) {
                totalScrap -= ship.price;
                unlockedShips.push(key);
                selectedShipType = key;

                localStorage.setItem('starwars_scrap', totalScrap);
                localStorage.setItem('starwars_unlocked', JSON.stringify(unlockedShips));
                localStorage.setItem('starwars_selected', selectedShipType);

                playUpgradeSound();
                document.getElementById('store-scrap-display').innerText = totalScrap;
                renderStoreList();
            }
        }

        function selectShip(key) {
            if (unlockedShips.includes(key)) {
                selectedShipType = key;
                localStorage.setItem('starwars_selected', selectedShipType);
                playUpgradeSound();
                renderStoreList();
            }
        }

        // --- FUNCIONAMENTO DO COMBATE ---

        function startGame() {
            initAudio();
            document.getElementById('screen-menu').classList.add('opacity-0');
            setTimeout(() => {
                document.getElementById('screen-menu').classList.add('hidden');
                document.getElementById('game-hud').classList.remove('opacity-0');
                document.getElementById('game-controls').classList.remove('opacity-0');
                
                // Configuração inicial do caça
                const preset = SHIP_PRESETS[selectedShipType];
                player.maxShield = preset.maxShield;
                player.maxHealth = preset.maxHealth;
                player.shield = preset.maxShield;
                player.health = preset.maxHealth;
                player.speed = preset.speed;
                player.laserLevel = preset.laserLevel;
                player.torpedos = preset.startingTorpedos;
                player.bulletStyle = preset.bulletStyle;
                player.x = canvas.width / 2;
                player.y = canvas.height * 0.8;
                player.targetX = player.x;
                player.targetY = player.y;

                score = 0;
                kills = 0;
                scrapCollectedInSession = 0;
                gameLevel = 1; // Inicia no Nível 1
                waveProgress = 0;
                bossActive = false;
                bossDefeated = false;
                boss = null;
                nextWaveTarget = 120; // Alvo do Nível 1
                
                lasers = [];
                enemies = [];
                enemyLasers = [];
                asteroids = [];
                items = [];
                explosions = [];

                updateHUD();
                
                gameActive = true;
                isPaused = false;
                lastEnemySpawn = Date.now();
                lastAsteroidSpawn = Date.now();
                
                // Dispara o loop gráfico prevenindo múltiplas execuções simultâneas
                if (!isLoopRunning) {
                    isLoopRunning = true;
                    gameLoop();
                }
            }, 300);
        }

        function advanceLevel() {
            document.getElementById('screen-victory').classList.add('hidden');
            
            // Subir de nível
            gameLevel++;
            
            // Reajustar gatilho de pontuação do boss baseado no nível
            nextWaveTarget = score + 120 + (gameLevel * 20);
            
            // Limpar entidades do nível anterior para uma transição limpa
            bossActive = false;
            bossDefeated = false;
            boss = null;
            lasers = [];
            enemies = [];
            enemyLasers = [];
            asteroids = [];
            items = [];
            explosions = [];

            // Regenerar 40% do escudo gratuitamente para ajudar o jogador
            player.shield = Math.min(player.maxShield, player.shield + Math.round(player.maxShield * 0.4));

            updateHUD();
            
            isPaused = false;
            gameActive = true;
            lastEnemySpawn = Date.now();
            lastAsteroidSpawn = Date.now();

            // Reinicia o ciclo apenas se já não estiver ativamente em execução
            if (!isLoopRunning) {
                isLoopRunning = true;
                gameLoop();
            }
        }

        function restartGame() {
            document.getElementById('screen-gameover').classList.add('hidden');
            document.getElementById('screen-victory').classList.add('hidden');
            startGame();
        }

        function goToMenu() {
            document.getElementById('screen-gameover').classList.add('hidden');
            document.getElementById('screen-victory').classList.add('hidden');
            document.getElementById('screen-menu').classList.remove('hidden');
            setTimeout(() => {
                document.getElementById('screen-menu').classList.remove('opacity-0');
            }, 50);
            
            document.getElementById('game-hud').classList.add('opacity-0');
            document.getElementById('game-controls').classList.add('opacity-0');
            gameActive = false;
            isLoopRunning = false; // Desliga o loop
            updateMenuShipPreview();
        }

        function gameOver() {
            gameActive = false;
            isLoopRunning = false;
            playExplosionSound(true);

            // Persistir Sucatas Coletadas
            totalScrap += scrapCollectedInSession;
            localStorage.setItem('starwars_scrap', totalScrap);
            
            // Salvar Recorde
            const currentHighScore = localStorage.getItem('starwars_highscore') || 0;
            if (score > currentHighScore) {
                localStorage.setItem('starwars_highscore', score);
                document.getElementById('high-score-label').innerText = `Recorde: ${score}`;
            }

            // Atualizar UI de Fim de Jogo
            document.getElementById('go-level').innerText = `Nível ${gameLevel}`;
            document.getElementById('go-score').innerText = score;
            document.getElementById('go-kills').innerText = kills;
            document.getElementById('go-scrap').innerText = scrapCollectedInSession;
            document.getElementById('go-total-scrap').innerText = totalScrap;

            document.getElementById('screen-gameover').classList.remove('hidden');
        }

        function gameLevelCleared() {
            gameActive = false; // Pausa a lógica de física ativa
            isLoopRunning = false; // Para as requisições de renderização adicionais
            
            // Prémios por derrotar o chefe
            const isDeathStar = (gameLevel % 10 === 0);
            const levelBonusScrap = isDeathStar ? 300 : 150;
            
            // Acumular provisoriamente sucatas para a sessão atual
            scrapCollectedInSession += levelBonusScrap;
            totalScrap += levelBonusScrap;
            localStorage.setItem('starwars_scrap', totalScrap);

            // Ajustar textos de vitória baseados no tipo do Chefe derrotado
            if (isDeathStar) {
                document.getElementById('victory-headline').innerText = "ESTRELA DA MORTE DESTRUÍDA!";
                document.getElementById('victory-subline').innerText = "Um disparo certeiro no reator principal selou o destino da estação militar mais poderosa do Império!";
                document.getElementById('vic-bonus-type').innerHTML = `<i data-lucide="nut" class="w-3.5 h-3.5"></i> +300 (Prémio Estrela)`;
            } else {
                document.getElementById('victory-headline').innerText = `NÍVEL ${gameLevel} COMPLETO`;
                document.getElementById('victory-subline').innerText = "O Star Destroyer Imperial que bloqueava o setor espacial foi completamente desativado!";
                document.getElementById('vic-bonus-type').innerHTML = `<i data-lucide="nut" class="w-3.5 h-3.5"></i> +150 (Prémio Cruiser)`;
            }

            // Atualizar estatísticas na tela de progresso
            document.getElementById('vic-level').innerText = `Nível ${gameLevel}`;
            document.getElementById('vic-scrap').innerText = scrapCollectedInSession;
            document.getElementById('vic-total-scrap').innerText = totalScrap;

            document.getElementById('screen-victory').classList.remove('hidden');
            lucide.createIcons();
        }

        // --- GESTÃO DE CONTROLES DE TOQUE ---

        function handleMove(e) {
            if (!gameActive || isPaused) return;
            const rect = canvas.getBoundingClientRect();
            const clientX = e.touches ? e.touches[0].clientX : e.clientX;
            const clientY = e.touches ? e.touches[0].clientY : e.clientY;
            
            let touchX = clientX - rect.left;
            let touchY = clientY - rect.top;

            const fingerOffset = -55; 
            
            player.targetX = touchX;
            player.targetY = touchY + fingerOffset;
        }

        canvas.addEventListener('touchmove', (e) => {
            e.preventDefault();
            handleMove(e);
        }, { passive: false });

        canvas.addEventListener('touchstart', (e) => {
            e.preventDefault();
            handleMove(e);
        }, { passive: false });

        canvas.addEventListener('mousemove', handleMove);

        // Disparar Torpedo
        document.getElementById('btn-torpedo').addEventListener('click', fireTorpedo);

        // Abrir Hangar de Upgrades durante partida
        function openUpgradeMenu() {
            isPaused = true;
            document.getElementById('upgrade-scrap-display').innerText = scrapCollectedInSession;
            updateUpgradeScreenButtons();
            document.getElementById('screen-upgrades').classList.remove('hidden');
        }

        function resumeGameFromUpgrade() {
            document.getElementById('screen-upgrades').classList.add('hidden');
            isPaused = false;
        }

        document.getElementById('btn-pause').addEventListener('click', openUpgradeMenu);

        // Upgrades de partida
        function updateUpgradeScreenButtons() {
            const upLaserCost = player.laserLevel === 1 ? 40 : player.laserLevel === 2 ? 85 : 150;
            const upShieldCost = 30 + (player.maxShield - SHIP_PRESETS[selectedShipType].maxShield);
            const upTorpedoCost = 25;

            const btnLaser = document.getElementById('btn-up-laser');
            document.getElementById('btn-up-laser-cost').innerText = upLaserCost;
            if (player.laserLevel >= 3) {
                btnLaser.disabled = true;
                document.getElementById('laser-desc').innerText = "Lasers no patamar máximo!";
                btnLaser.innerText = "MAX";
            } else {
                btnLaser.disabled = scrapCollectedInSession < upLaserCost;
            }

            const btnShield = document.getElementById('btn-up-shield');
            document.getElementById('btn-up-shield-cost').innerText = upShieldCost;
            btnShield.disabled = scrapCollectedInSession < upShieldCost;

            const btnTorpedo = document.getElementById('btn-up-torpedo');
            document.getElementById('btn-up-torpedo-cost').innerText = upTorpedoCost;
            btnTorpedo.disabled = scrapCollectedInSession < upTorpedoCost || player.torpedos >= 3;
            if (player.torpedos >= 3) {
                btnTorpedo.innerText = "CHEIO";
            } else {
                btnTorpedo.innerHTML = `${upTorpedoCost} <i data-lucide="nut" class="w-3.5 h-3.5"></i>`;
            }
            lucide.createIcons();
        }

        function buyUpgrade(type) {
            if (type === 'laser') {
                const cost = player.laserLevel === 1 ? 40 : player.laserLevel === 2 ? 85 : 150;
                if (scrapCollectedInSession >= cost && player.laserLevel < 3) {
                    scrapCollectedInSession -= cost;
                    player.laserLevel++;
                    playUpgradeSound();
                }
            } else if (type === 'shield') {
                const cost = 30 + (player.maxShield - SHIP_PRESETS[selectedShipType].maxShield);
                if (scrapCollectedInSession >= cost) {
                    scrapCollectedInSession -= cost;
                    player.maxShield += 25;
                    player.shield = player.maxShield;
                    playUpgradeSound();
                }
            } else if (type === 'torpedo') {
                const cost = 25;
                if (scrapCollectedInSession >= cost && player.torpedos < 3) {
                    scrapCollectedInSession -= cost;
                    player.torpedos++;
                    playUpgradeSound();
                }
            }

            updateHUD();
            document.getElementById('upgrade-scrap-display').innerText = scrapCollectedInSession;
            updateUpgradeScreenButtons();
        }

        // Atirar Torpedo
        function fireTorpedo() {
            if (!gameActive || isPaused || player.torpedos <= 0) return;
            player.torpedos--;
            updateHUD();

            if (audioEnabled) {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sawtooth';
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.frequency.setValueAtTime(180, audioCtx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(1600, audioCtx.currentTime + 0.55);
                gain.gain.setValueAtTime(0.28, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.55);
                osc.start();
                osc.stop(audioCtx.currentTime + 0.55);
            }

            explosions.push({
                x: canvas.width / 2,
                y: canvas.height / 2,
                radius: 10,
                maxRadius: canvas.width * 0.85,
                speed: 16,
                color: 'rgba(239, 68, 68, 0.45)'
            });

            setTimeout(() => {
                enemies.forEach(e => {
                    e.health -= 100;
                    if (e.health <= 0) {
                        spawnScrap(e.x, e.y);
                        score += e.scorePoints;
                        kills++;
                    }
                });
                enemies = enemies.filter(e => e.health > 0);

                asteroids.forEach(a => {
                    a.health = 0;
                    score += 5;
                });
                asteroids = asteroids.filter(a => a.health > 0);

                if (boss) {
                    boss.health -= 180;
                    if (boss.health <= 0) {
                        bossDefeated = true;
                        score += 1000;
                        playExplosionSound(true);
                    }
                }

                playExplosionSound(true);
                updateHUD();
            }, 550);
        }

        function spawnScrap(x, y) {
            const rand = Math.random();
            if (rand < 0.65) {
                items.push({
                    x: x,
                    y: y,
                    type: 'scrap',
                    size: 14,
                    speed: 2.2
                });
            } else if (rand < 0.82) {
                items.push({
                    x: x,
                    y: y,
                    type: 'heal',
                    size: 14,
                    speed: 2.2
                });
            }
        }

        function updateHUD() {
            document.getElementById('hud-shield-val').innerText = `${Math.round((player.shield / player.maxShield) * 100)}%`;
            document.getElementById('hud-shield-bar').style.width = `${Math.max(0, (player.shield / player.maxShield) * 100)}%`;
            
            document.getElementById('hud-health-val').innerText = `${Math.round((player.health / player.maxHealth) * 100)}%`;
            document.getElementById('hud-health-bar').style.width = `${Math.max(0, (player.health / player.maxHealth) * 100)}%`;
            
            document.getElementById('hud-score').innerText = score;
            document.getElementById('hud-scrap').innerText = scrapCollectedInSession;
            document.getElementById('torpedo-count').innerText = player.torpedos;
            document.getElementById('hud-level-tag').innerText = `NIV ${gameLevel}`;

            // Determinar tipo do chefe atual
            const isDeathStar = (gameLevel % 10 === 0);

            // Avanço da Frota
            const baseStartScore = (nextWaveTarget - 120 - (gameLevel * 20));
            const progress = bossActive ? 100 : Math.max(0, Math.min(100, ((score - baseStartScore) / (120 + (gameLevel * 20))) * 100));
            document.getElementById('wave-progress-bar').style.width = `${progress}%`;
            
            if (bossActive) {
                document.getElementById('wave-title').innerText = isDeathStar ? "ESTRELA DA MORTE LOCALIZADA!" : "MIRA TRAVADA: STAR DESTROYER";
                document.getElementById('wave-title').classList.add('text-red-500', 'alert-pulse');
                document.getElementById('wave-progress-bar').classList.remove('bg-amber-500');
                document.getElementById('wave-progress-bar').classList.add('bg-red-500');
            } else {
                document.getElementById('wave-title').innerText = "Avanço da Frota Imperial";
                document.getElementById('wave-title').classList.remove('text-red-500', 'alert-pulse');
                document.getElementById('wave-progress-bar').classList.remove('bg-red-500');
                document.getElementById('wave-progress-bar').classList.add('bg-amber-500');
            }
        }

        // --- SISTEMA DE SPAWN COM ESCALONAMENTO DE DIFICULDADE POR NÍVEL ---
        function spawnEnemy() {
            if (bossActive) return; // Nenhum capanga normal ressurge se um chefe estiver ativo

            const now = Date.now();
            
            // Frequência de respawn acelera suavemente a cada nível
            let baseInterval = 1900 - (gameLevel * 80);
            let spawnInterval = Math.max(500, baseInterval - score / 15);

            if (now - lastEnemySpawn > spawnInterval) {
                const rand = Math.random();
                let enemyType = 'tie';
                
                // Vida base e velocidade escalonam com o nível
                let enemyHp = 10 + Math.floor(gameLevel * 1.5);
                let enemySpeed = 3.2 + (gameLevel * 0.15);
                let scorePoints = 10;

                if (rand > 0.80) {
                    enemyType = 'tie-bomber';
                    enemyHp = 35 + Math.floor(gameLevel * 4);
                    enemySpeed = 2 + (gameLevel * 0.1);
                    scorePoints = 30;
                } else if (rand > 0.60) {
                    enemyType = 'tie-interceptor';
                    enemyHp = 18 + Math.floor(gameLevel * 2.5);
                    enemySpeed = 4.6 + (gameLevel * 0.18);
                    scorePoints = 20;
                }

                enemies.push({
                    x: Math.random() * (canvas.width - 40) + 20,
                    y: -40,
                    width: 36,
                    height: 36,
                    type: enemyType,
                    health: enemyHp,
                    maxHealth: enemyHp,
                    speed: enemySpeed,
                    scorePoints: scorePoints,
                    lastShot: 0,
                    // Intervalo de tiro reduz a cada nível (inimigos atiram mais)
                    shootInterval: Math.max(700, (1300 + Math.random() * 900) - (gameLevel * 40)),
                    directionX: Math.random() > 0.5 ? 1 : -1
                });
                lastEnemySpawn = now;
            }
        }

        function spawnAsteroid() {
            // Asteroides não aparecem durante a luta contra chefes
            if (bossActive) return;

            const now = Date.now();
            if (now - lastAsteroidSpawn > 3200) {
                const size = Math.random() * 26 + 18;
                asteroids.push({
                    x: Math.random() * canvas.width,
                    y: -size,
                    size: size,
                    speed: Math.random() * 1.8 + 1.6 + (gameLevel * 0.1),
                    health: Math.ceil(size / 8) + Math.floor(gameLevel * 0.5),
                    maxHealth: Math.ceil(size / 8) + Math.floor(gameLevel * 0.5),
                    rot: Math.random() * Math.PI,
                    rotSpeed: (Math.random() - 0.5) * 0.04
                });
                lastAsteroidSpawn = now;
            }
        }

        function triggerBoss() {
            bossActive = true;
            
            // É um nível da Estrela da Morte? (A cada 10 níveis)
            const isDeathStar = (gameLevel % 10 === 0);

            if (isDeathStar) {
                // Configuração da lendária Estrela da Morte
                boss = {
                    type: 'deathstar',
                    x: canvas.width / 2,
                    y: -160, // Desce suavemente do topo
                    width: 250,
                    height: 250,
                    // Vida colossal (Cresce com o fator nível)
                    health: 1200 + (gameLevel * 40),
                    maxHealth: 1200 + (gameLevel * 40),
                    speed: 0.8, // Lento, mas de movimento colossal
                    lastShot: 0,
                    shootInterval: 1200,
                    
                    // Ataque Especial de Superlaser
                    lastSuperLaser: Date.now() + 2000, 
                    superLaserActive: false,
                    superLaserTimer: 0,
                    superLaserWarning: false,

                    // Suas defesas
                    turrets: [
                        { xOffset: -60, yOffset: 40 },
                        { xOffset: 60, yOffset: 40 },
                        { xOffset: -100, yOffset: 0 },
                        { xOffset: 100, yOffset: 0 }
                    ]
                };
            } else {
                // Configuração do Star Destroyer com escalonamento de vida/velocidade
                boss = {
                    type: 'destroyer',
                    x: canvas.width / 2,
                    y: -140,
                    width: 190,
                    height: 110,
                    health: 550 + (gameLevel * 75),
                    maxHealth: 550 + (gameLevel * 75),
                    speed: 1.4 + (gameLevel * 0.1),
                    lastShot: 0,
                    shootInterval: Math.max(500, 1000 - (gameLevel * 30)),
                    turrets: [
                        { xOffset: -55, yOffset: 10 },
                        { xOffset: 55, yOffset: 10 },
                        { xOffset: 0, yOffset: 45 }
                    ]
                };
            }
            updateHUD();
        }

        // --- ATIRAR LASERS BASEADO NO MODELO DA NAVE ---
        let lastPlayerShot = 0;
        function autoFire() {
            const now = Date.now();
            let delay = selectedShipType === 'awing' ? 160 : selectedShipType === 'millennium' ? 220 : 230;
            
            if (now - lastPlayerShot > delay) {
                const style = player.bulletStyle;
                const level = player.laserLevel;

                if (style === 'dual-fast' || (style === 'double' && level === 1)) {
                    lasers.push({ x: player.x - 12, y: player.y - 12, speed: 13 });
                    lasers.push({ x: player.x + 12, y: player.y - 12, speed: 13 });
                } 
                else if (style === 'double' && level >= 2) {
                    lasers.push({ x: player.x - 16, y: player.y - 8, speed: 13 });
                    lasers.push({ x: player.x + 16, y: player.y - 8, speed: 13 });
                    if (level >= 3) {
                        lasers.push({ x: player.x, y: player.y - 20, speed: 16, isCharged: true });
                    }
                }
                else if (style === 'heavy-double') {
                    lasers.push({ x: player.x - 14, y: player.y - 10, speed: 11, isCharged: true });
                    lasers.push({ x: player.x + 14, y: player.y - 10, speed: 11, isCharged: true });
                }
                else if (style === 'triple' || (style === 'dual-fast' && level >= 2)) {
                    lasers.push({ x: player.x - 18, y: player.y - 5, speed: 14 });
                    lasers.push({ x: player.x + 18, y: player.y - 5, speed: 14 });
                    lasers.push({ x: player.x, y: player.y - 18, speed: 14 });
                }
                else if (style === 'quad' || level >= 3) {
                    lasers.push({ x: player.x - 22, y: player.y - 2, speed: 14 });
                    lasers.push({ x: player.x - 10, y: player.y - 14, speed: 14 });
                    lasers.push({ x: player.x + 10, y: player.y - 14, speed: 14 });
                    lasers.push({ x: player.x + 22, y: player.y - 2, speed: 14 });
                }
                
                playLaserSound(true);
                lastPlayerShot = now;
            }
        }

        // --- ATUALIZAÇÕES FÍSICAS ---
        function update() {
            if (!gameActive || isPaused) return;

            stars.forEach(star => {
                star.y += star.speed;
                if (star.y > canvas.height) {
                    star.y = 0;
                    star.x = Math.random() * canvas.width;
                }
            });

            // Suavização da movimentação (Lerp)
            const dx = player.targetX - player.x;
            const dy = player.targetY - player.y;
            player.x += dx * 0.16;
            player.y += dy * 0.16;

            player.x = Math.max(25, Math.min(canvas.width - 25, player.x));
            player.y = Math.max(canvas.height * 0.45, Math.min(canvas.height - 40, player.y));

            autoFire();

            // Lasers do Jogador
            lasers.forEach(laser => { laser.y -= laser.speed; });
            lasers = lasers.filter(laser => laser.y > -20);

            // Asteroides (Apenas se chefe não estiver ativo)
            if (!bossActive) {
                asteroids.forEach(asteroid => {
                    asteroid.y += asteroid.speed;
                    asteroid.rot += asteroid.rotSpeed;

                    const distToPlayer = Math.hypot(asteroid.x - player.x, asteroid.y - player.y);
                    if (distToPlayer < (asteroid.size + 15)) {
                        damagePlayer(Math.round(asteroid.size / 1.8));
                        asteroid.health = 0;
                    }
                });
                asteroids = asteroids.filter(a => {
                    if (a.health <= 0) {
                        playExplosionSound(false);
                        createExplosion(a.x, a.y, a.size, '#6b7280');
                        return false;
                    }
                    return a.y < canvas.height + 40;
                });
            } else {
                asteroids = []; // Limpa no momento em que o boss se manifesta
            }

            // Inimigos normais (Apenas se chefe não estiver ativo)
            if (!bossActive) {
                enemies.forEach(enemy => {
                    enemy.y += enemy.speed;

                    if (enemy.type === 'tie-interceptor') {
                        enemy.x += enemy.directionX * 2.2;
                        if (enemy.x < 30 || enemy.x > canvas.width - 30) {
                            enemy.directionX *= -1;
                        }
                    }

                    const now = Date.now();
                    if (now - enemy.lastShot > enemy.shootInterval && enemy.y > 0) {
                        enemyLasers.push({
                            x: enemy.x,
                            y: enemy.y + 12,
                            speed: enemy.type === 'tie-interceptor' ? 7.5 : 5.5
                        });
                        playLaserSound(false);
                        enemy.lastShot = now;
                    }

                    const distToPlayer = Math.hypot(enemy.x - player.x, enemy.y - player.y);
                    if (distToPlayer < 34) {
                        damagePlayer(28);
                        enemy.health = 0;
                    }
                });
                enemies = enemies.filter(enemy => {
                    if (enemy.health <= 0) {
                        playExplosionSound(false);
                        createExplosion(enemy.x, enemy.y, 24, '#22c55e');
                        return false;
                    }
                    return enemy.y < canvas.height + 40;
                });
            } else {
                enemies = []; // Sem capangas no duelo de chefão
            }

            // Lasers Inimigos
            enemyLasers.forEach(laser => {
                laser.y += laser.speed;

                const dist = Math.hypot(laser.x - player.x, laser.y - player.y);
                if (dist < 22) {
                    damagePlayer(11);
                    laser.y = canvas.height + 100;
                }
            });
            enemyLasers = enemyLasers.filter(l => l.y < canvas.height + 15);

            // Colisão Lasers do Jogador vs Alvos
            lasers.forEach(laser => {
                // Contra Boss (se ativo)
                if (bossActive && boss) {
                    // Raio de colisão maior para a gigantesca Estrela da Morte
                    const hitRadius = boss.type === 'deathstar' ? 95 : 75;
                    const dist = Math.hypot(laser.x - boss.x, laser.y - (boss.y + 20));
                    
                    if (dist < hitRadius) {
                        const damage = laser.isCharged ? 22 : 9;
                        boss.health -= damage;
                        laser.y = -100;
                        createExplosion(laser.x, laser.y, 8, '#06b6d4');
                        if (boss.health <= 0) {
                            bossDefeated = true;
                            score += 1000;
                            updateHUD();
                        }
                    }
                }

                // Contra Inimigos normais
                enemies.forEach(enemy => {
                    const dist = Math.hypot(laser.x - enemy.x, laser.y - enemy.y);
                    if (dist < 24) {
                        const damage = laser.isCharged ? 35 : 15;
                        enemy.health -= damage;
                        laser.y = -100;
                        if (enemy.health <= 0) {
                            spawnScrap(enemy.x, enemy.y);
                            score += enemy.scorePoints;
                            kills++;
                            updateHUD();
                        }
                    }
                });

                // Contra Asteroides
                asteroids.forEach(ast => {
                    const dist = Math.hypot(laser.x - ast.x, laser.y - ast.y);
                    if (dist < ast.size + 10) {
                        const damage = laser.isCharged ? 4 : 1;
                        ast.health -= damage;
                        laser.y = -100;
                        if (ast.health <= 0) {
                            score += 5;
                            updateHUD();
                        }
                    }
                });
            });

            // Coletáveis (Atração magnética)
            items.forEach(item => {
                item.y += item.speed;

                const dist = Math.hypot(item.x - player.x, item.y - player.y);
                if (dist < 110) {
                    item.x += (player.x - item.x) * 0.12;
                    item.y += (player.y - item.y) * 0.12;
                }

                if (dist < 28) {
                    if (item.type === 'scrap') {
                        scrapCollectedInSession += Math.floor(Math.random() * 4 + 4);
                        if (audioEnabled) {
                            const osc = audioCtx.createOscillator();
                            const gain = audioCtx.createGain();
                            osc.type = 'sine';
                            osc.connect(gain);
                            gain.connect(audioCtx.destination);
                            osc.frequency.setValueAtTime(950, audioCtx.currentTime);
                            gain.gain.setValueAtTime(0.08, audioCtx.currentTime);
                            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);
                            osc.start();
                            osc.stop(audioCtx.currentTime + 0.1);
                        }
                    } else if (item.type === 'heal') {
                        player.shield = Math.min(player.maxShield, player.shield + 30);
                        playUpgradeSound();
                    }
                    item.y = canvas.height + 200;
                    updateHUD();
                }
            });
            items = items.filter(i => i.y < canvas.height + 40);

            // Explosões
            explosions.forEach(exp => { exp.radius += exp.speed; });
            explosions = explosions.filter(exp => exp.radius < exp.maxRadius);

            // Invocação e controle do Chefe
            if (!bossActive && score >= nextWaveTarget) {
                triggerBoss();
            }

            if (bossActive && boss) {
                if (boss.type === 'deathstar') {
                    // Entrada lenta e assustadora da Estrela da Morte
                    if (boss.y < 95) {
                        boss.y += boss.speed;
                    } else {
                        // Flutuação lateral muito contida por conta do seu tamanho massivo
                        boss.x += boss.speed;
                        if (boss.x > canvas.width - 70 || boss.x < 70) {
                            boss.speed *= -1;
                        }

                        const now = Date.now();

                        // 1. ATAQUE CONVENCIONAL: Baterias secundárias
                        if (now - boss.lastShot > boss.shootInterval) {
                            boss.turrets.forEach(t => {
                                enemyLasers.push({
                                    x: boss.x + t.xOffset,
                                    y: boss.y + t.yOffset,
                                    speed: 5.5 + (gameLevel * 0.1)
                                });
                            });
                            playLaserSound(false);
                            boss.lastShot = now;
                        }

                        // 2. SUPER ATAQUE: Superlaser de foco central verde gigante!
                        if (!boss.superLaserActive && !boss.superLaserWarning) {
                            // Carregar o Superlaser a cada 6 segundos
                            if (now - boss.lastSuperLaser > 6000) {
                                boss.superLaserWarning = true;
                                boss.superLaserTimer = now;
                                playLaserDeathStarSound();
                            }
                        }

                        if (boss.superLaserWarning) {
                            // Fase de mira/aviso: 1.5 segundos emitindo um aviso luminoso
                            if (now - boss.superLaserTimer > 1500) {
                                boss.superLaserWarning = false;
                                boss.superLaserActive = true;
                                boss.superLaserTimer = now;
                                playExplosionSound(true); 
                            }
                        }

                        if (boss.superLaserActive) {
                            // O laser gigante fica ativo infligindo dano massivo contínuo por 1.2 segundos
                            if (now - boss.superLaserTimer < 1200) {
                                // Verificar colisão do laser contínuo (coluna de largura 50 descendo verticalmente da Estrela da Morte)
                                const laserLeft = boss.x - 25;
                                const laserRight = boss.x + 25;
                                if (player.x > laserLeft - 10 && player.x < laserRight + 10 && player.y > boss.y) {
                                    damagePlayer(2.5); 
                                }
                            } else {
                                boss.superLaserActive = false;
                                boss.lastSuperLaser = now;
                            }
                        }
                    }
                } else {
                    // Comportamento do Star Destroyer (Cruiser Convencional)
                    if (boss.y < 85) {
                        boss.y += boss.speed;
                    } else {
                        boss.x += boss.speed;
                        if (boss.x > canvas.width - 90 || boss.x < 90) {
                            boss.speed *= -1;
                        }

                        const now = Date.now();
                        if (now - boss.lastShot > boss.shootInterval) {
                            boss.turrets.forEach(t => {
                                enemyLasers.push({
                                    x: boss.x + t.xOffset,
                                    y: boss.y + t.yOffset,
                                    speed: 6
                                });
                            });
                            playLaserSound(false);
                            boss.lastShot = now;
                        }
                    }
                }

                if (bossDefeated) {
                    playExplosionSound(true);
                    createExplosion(boss.x, boss.y, 110, '#f97316');
                    
                    setTimeout(() => {
                        gameLevelCleared();
                    }, 1200);
                    boss = null;
                }
            }

            spawnEnemy();
            spawnAsteroid();
        }

        function damagePlayer(amount) {
            if (navigator.vibrate) {
                navigator.vibrate(amount * 4);
            }

            if (player.shield > 0) {
                player.shield -= amount;
                playShieldHitSound();
                if (player.shield < 0) {
                    player.health += player.shield;
                    player.shield = 0;
                }
            } else {
                player.health -= amount;
                playExplosionSound(false);
            }

            updateHUD();

            if (player.health <= 0) {
                gameOver();
            }
        }

        function createExplosion(x, y, maxRad, color) {
            explosions.push({
                x: x,
                y: y,
                radius: 2,
                maxRadius: maxRad,
                speed: 5.5,
                color: color || 'rgba(239, 68, 68, 0.4)'
            });
        }

        // --- MÉTODOS DE DESENHO VETORIAL PARA O PLAYER EM COMBATE ---

        function drawPlayer() {
            ctx.save();
            ctx.translate(player.x, player.y);

            // Escudo holográfico ativo
            if (player.shield > 0) {
                ctx.beginPath();
                ctx.arc(0, -4, 38, 0, Math.PI * 2);
                ctx.strokeStyle = `rgba(56, 189, 248, ${0.12 + (player.shield / player.maxShield) * 0.28})`;
                ctx.lineWidth = 2.5;
                ctx.stroke();
            }

            // Chama traseira do propulsor
            ctx.beginPath();
            ctx.moveTo(-6, 20);
            ctx.lineTo(0, 30 + Math.random() * 8);
            ctx.lineTo(6, 20);
            ctx.fillStyle = selectedShipType === 'awing' ? '#f97316' : '#06b6d4';
            ctx.fill();

            // Desenhar de acordo com o modelo selecionado no Canvas de Gameplay
            if (selectedShipType === 'xwing') {
                ctx.fillStyle = '#cbd5e1';
                ctx.beginPath();
                ctx.moveTo(-10, 5); ctx.lineTo(-32, -2); ctx.lineTo(-34, 14); ctx.lineTo(-10, 9); ctx.fill();
                ctx.beginPath();
                ctx.moveTo(10, 5); ctx.lineTo(32, -2); ctx.lineTo(34, 14); ctx.lineTo(10, 9); ctx.fill();
                ctx.fillStyle = '#ef4444';
                ctx.fillRect(-34, -10, 3, 18); ctx.fillRect(31, -10, 3, 18);
                ctx.fillStyle = '#e2e8f0';
                ctx.beginPath();
                ctx.moveTo(0, -24); ctx.lineTo(8, 14); ctx.lineTo(-8, 14); ctx.closePath(); ctx.fill();
                ctx.fillStyle = '#38bdf8';
                ctx.beginPath();
                ctx.moveTo(0, -11); ctx.lineTo(4, -3); ctx.lineTo(-4, -3); ctx.closePath(); ctx.fill();
            } 
            else if (selectedShipType === 'awing') {
                ctx.fillStyle = '#ef4444';
                ctx.beginPath();
                ctx.moveTo(0, -25); ctx.lineTo(16, 14); ctx.lineTo(-16, 14); ctx.closePath(); ctx.fill();
                ctx.fillStyle = '#f1f5f9';
                ctx.beginPath();
                ctx.moveTo(0, -14); ctx.lineTo(8, 9); ctx.lineTo(-8, 9); ctx.closePath(); ctx.fill();
                ctx.fillStyle = '#7f1d1d';
                ctx.fillRect(-17, 7, 3, 11); ctx.fillRect(14, 7, 3, 11);
                ctx.fillStyle = '#eab308';
                ctx.beginPath();
                ctx.moveTo(0, -5); ctx.lineTo(3.5, 2); ctx.lineTo(-3.5, 2); ctx.closePath(); ctx.fill();
            } 
            else if (selectedShipType === 'ywing') {
                ctx.fillStyle = '#cbd5e1';
                ctx.fillStyle = '#f59e0b';
                ctx.fillRect(-22, -10, 6, 36);
                ctx.fillRect(16, -10, 6, 36);
                ctx.fillStyle = '#78716c';
                ctx.fillRect(-16, 10, 32, 5);
                ctx.fillStyle = '#e2e8f0';
                ctx.beginPath();
                ctx.moveTo(0, -26);
                ctx.lineTo(8, 12);
                ctx.lineTo(-8, 12);
                ctx.closePath();
                ctx.fill();
                ctx.fillStyle = '#f59e0b';
                ctx.beginPath();
                ctx.moveTo(0, -26); ctx.lineTo(5, -12); ctx.lineTo(-5, -12); ctx.closePath(); ctx.fill();
            } 
            else if (selectedShipType === 'tieinterceptor') {
                ctx.beginPath();
                ctx.arc(0, 0, 8, 0, Math.PI * 2);
                ctx.fillStyle = '#475569';
                ctx.fill();
                ctx.lineWidth = 1.5;
                ctx.strokeStyle = '#1e293b';
                ctx.stroke();
                ctx.fillStyle = '#64748b';
                ctx.fillRect(-18, -2, 36, 4);
                ctx.fillStyle = '#1e293b';
                ctx.beginPath();
                ctx.moveTo(-18, -16); ctx.lineTo(-26, -10); ctx.lineTo(-18, 0); ctx.lineTo(-26, 10); ctx.lineTo(-18, 16); ctx.closePath(); ctx.fill();
                ctx.beginPath();
                ctx.moveTo(18, -16); ctx.lineTo(26, -10); ctx.lineTo(18, 0); ctx.lineTo(26, 10); ctx.lineTo(18, 16); ctx.closePath(); ctx.fill();
            } 
            else if (selectedShipType === 'millennium') {
                ctx.fillStyle = '#cbd5e1';
                ctx.beginPath();
                ctx.arc(0, 4, 22, 0, Math.PI * 2);
                ctx.fill();
                ctx.lineWidth = 1.5;
                ctx.strokeStyle = '#94a3b8';
                ctx.stroke();
                ctx.fillRect(-11, -20, 5, 14);
                ctx.fillRect(6, -20, 5, 14);
                ctx.fillStyle = '#475569';
                ctx.fillRect(18, -6, 8, 11);
                ctx.beginPath();
                ctx.arc(-10, -2, 4, 0, Math.PI * 2);
                ctx.fillStyle = '#78716c';
                ctx.fill();
            }

            ctx.restore();
        }

        // --- DESENHAR INIMIGOS, ASTEROIDES E CHEFES ---

        function drawEnemies() {
            enemies.forEach(enemy => {
                ctx.save();
                ctx.translate(enemy.x, enemy.y);

                ctx.beginPath();
                ctx.arc(0, 0, 7.5, 0, Math.PI * 2);
                ctx.fillStyle = '#334155';
                ctx.fill();
                ctx.lineWidth = 1.2;
                ctx.strokeStyle = '#000';
                ctx.stroke();

                ctx.beginPath();
                ctx.arc(0, 0, 3.5, 0, Math.PI * 2);
                ctx.fillStyle = '#020617';
                ctx.fill();

                if (enemy.type === 'tie') {
                    ctx.fillStyle = '#0f172a';
                    ctx.fillRect(-17, -17, 2.5, 34);
                    ctx.fillRect(14.5, -17, 2.5, 34);
                    ctx.strokeStyle = '#64748b';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.moveTo(-14.5, 0); ctx.lineTo(14.5, 0); ctx.stroke();
                } 
                else if (enemy.type === 'tie-interceptor') {
                    ctx.strokeStyle = '#64748b';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.moveTo(-14, 0); ctx.lineTo(14, 0); ctx.stroke(); // CORRIGIDO: de stroke() para ctx.stroke()

                    ctx.fillStyle = '#1e293b';
                    ctx.beginPath();
                    ctx.moveTo(-14, -17); ctx.lineTo(-22, -11); ctx.lineTo(-14, 0); ctx.lineTo(-22, 11); ctx.lineTo(-14, 17); ctx.closePath(); ctx.fill(); ctx.stroke();
                    ctx.beginPath();
                    ctx.moveTo(14, -17); ctx.lineTo(22, -11); ctx.lineTo(14, 0); ctx.lineTo(22, 11); ctx.lineTo(14, 17); ctx.closePath(); ctx.fill(); ctx.stroke();
                } 
                else if (enemy.type === 'tie-bomber') {
                    ctx.fillStyle = '#475569';
                    ctx.beginPath();
                    ctx.arc(-5, 0, 6.5, 0, Math.PI * 2);
                    ctx.arc(5, 0, 6.5, 0, Math.PI * 2);
                    ctx.fill();

                    ctx.fillStyle = '#0f172a';
                    ctx.beginPath();
                    ctx.moveTo(-16, -11); ctx.lineTo(-13, -5); ctx.lineTo(-13, 5); ctx.lineTo(-16, 11); ctx.closePath(); ctx.fill();
                    ctx.beginPath();
                    ctx.moveTo(16, -11); ctx.lineTo(13, -5); ctx.lineTo(13, 5); ctx.lineTo(16, 11); ctx.closePath(); ctx.fill();

                    ctx.fillStyle = '#334155';
                    ctx.fillRect(-13, -2.5, 26, 5);
                }

                if (enemy.health < enemy.maxHealth) {
                    ctx.fillStyle = '#dc2626';
                    ctx.fillRect(-14, -22, 28, 2.5);
                    ctx.fillStyle = '#22c55e';
                    ctx.fillRect(-14, -22, (enemy.health / enemy.maxHealth) * 28, 2.5);
                }

                ctx.restore();
            });
        }

        function drawBoss() {
            if (!bossActive || !boss) return;

            ctx.save();
            ctx.translate(boss.x, boss.y);

            if (boss.type === 'deathstar') {
                // DESENHAR ESTRELA DA MORTE 
                ctx.beginPath();
                ctx.arc(0, 0, 85, 0, Math.PI * 2);
                
                const grad = ctx.createRadialGradient(-20, -20, 5, 0, 0, 85);
                grad.addColorStop(0, '#64748b');
                grad.addColorStop(0.7, '#334155');
                grad.addColorStop(1, '#0f172a');
                ctx.fillStyle = grad;
                ctx.fill();
                ctx.lineWidth = 3;
                ctx.strokeStyle = '#475569';
                ctx.stroke();

                // Trincheira equatorial
                ctx.beginPath();
                ctx.arc(0, 0, 85, -Math.PI * 0.04, Math.PI * 0.04);
                ctx.lineTo(-85, 0);
                ctx.strokeStyle = '#1e293b';
                ctx.lineWidth = 4;
                ctx.stroke();

                // Foco Parabólico do Superlaser
                ctx.beginPath();
                ctx.arc(-28, -28, 18, 0, Math.PI * 2);
                ctx.fillStyle = '#1e293b';
                ctx.fill();
                ctx.lineWidth = 1.5;
                ctx.strokeStyle = '#475569';
                ctx.stroke();

                // Detalhes internos do foco do laser
                ctx.beginPath();
                ctx.arc(-28, -28, 6, 0, Math.PI * 2);
                ctx.fillStyle = '#0f172a';
                ctx.fill();

                // Efeito do Carregamento ou Disparo do Superlaser
                if (boss.superLaserWarning) {
                    ctx.beginPath();
                    ctx.arc(-28, -28, 14 + Math.random() * 4, 0, Math.PI * 2);
                    ctx.strokeStyle = 'rgba(34, 197, 94, 0.8)';
                    ctx.lineWidth = 2.5;
                    ctx.stroke();

                    ctx.beginPath();
                    ctx.arc(-28, -28, 4, 0, Math.PI * 2);
                    ctx.fillStyle = '#22c55e';
                    ctx.fill();
                }

                // Desenhar as baterias de canhões turbolasers
                boss.turrets.forEach(t => {
                    ctx.beginPath();
                    ctx.arc(t.xOffset, t.yOffset, 6.5, 0, Math.PI * 2);
                    ctx.fillStyle = '#1e293b';
                    ctx.fill();
                    ctx.strokeStyle = '#94a3b8';
                    ctx.stroke();
                });

                // Renderizar o feixe gigante do Superlaser se ativo
                if (boss.superLaserActive) {
                    ctx.restore(); // Limpar translação local

                    ctx.save();
                    ctx.shadowBlur = 35;
                    ctx.shadowColor = '#22c55e';
                    
                    const beamX = boss.x;
                    const beamYStart = boss.y;
                    
                    const laserGrad = ctx.createLinearGradient(beamX - 30, 0, beamX + 30, 0);
                    laserGrad.addColorStop(0, 'rgba(34, 197, 94, 0.2)');
                    laserGrad.addColorStop(0.3, 'rgba(220, 252, 231, 0.95)');
                    laserGrad.addColorStop(0.5, '#ffffff');
                    laserGrad.addColorStop(0.7, 'rgba(220, 252, 231, 0.95)');
                    laserGrad.addColorStop(1, 'rgba(34, 197, 94, 0.2)');

                    ctx.fillStyle = laserGrad;
                    ctx.fillRect(beamX - 25, beamYStart, 50, canvas.height);
                    
                    ctx.restore();
                    ctx.save();
                    ctx.translate(boss.x, boss.y);
                }

            } else {
                // DESENHAR STAR DESTROYER
                ctx.beginPath();
                ctx.moveTo(0, 85); 
                ctx.lineTo(-85, -35); 
                ctx.lineTo(-80, -45);
                ctx.lineTo(80, -45); 
                ctx.lineTo(85, -35);
                ctx.closePath();

                const grad = ctx.createLinearGradient(0, -45, 0, 85);
                grad.addColorStop(0, '#1e293b');
                grad.addColorStop(0.5, '#475569');
                grad.addColorStop(1, '#090d16');
                ctx.fillStyle = grad;
                ctx.fill();
                ctx.lineWidth = 2.5;
                ctx.strokeStyle = '#64748b';
                ctx.stroke();

                ctx.fillStyle = '#334155';
                ctx.fillRect(-28, -40, 56, 18);
                ctx.strokeStyle = '#94a3b8';
                ctx.strokeRect(-28, -40, 56, 18);

                ctx.beginPath();
                ctx.arc(-14, -40, 5, 0, Math.PI * 2);
                ctx.arc(14, -40, 5, 0, Math.PI * 2);
                ctx.fillStyle = '#94a3b8';
                ctx.fill();

                ctx.fillStyle = '#eab308';
                ctx.fillRect(-45, -10, 3.5, 2.5);
                ctx.fillRect(40, -10, 3.5, 2.5);

                boss.turrets.forEach(t => {
                    ctx.beginPath();
                    ctx.arc(t.xOffset, t.yOffset, 7.5, 0, Math.PI * 2);
                    ctx.fillStyle = '#090d16';
                    ctx.fill();
                    ctx.strokeStyle = '#ef4444';
                    ctx.stroke();
                });
            }

            ctx.restore();

            // Painel superior de vida do Boss (HUD)
            const label = boss.type === 'deathstar' ? "ESTRELA DA MORTE DE CLASSE I" : "STAR DESTROYER IMPERIAL";
            ctx.fillStyle = 'rgba(15, 23, 42, 0.85)';
            ctx.fillRect(canvas.width / 2 - 95, 105, 190, 16);
            ctx.strokeStyle = '#ef4444';
            ctx.strokeRect(canvas.width / 2 - 95, 105, 190, 16);

            ctx.fillStyle = '#ef4444';
            ctx.fillRect(canvas.width / 2 - 95 + 1.5, 106.5, (boss.health / boss.maxHealth) * 187, 13);

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 8.5px Orbitron';
            ctx.textAlign = 'center';
            ctx.fillText(label, canvas.width / 2, 116.5);
        }

        function drawAsteroids() {
            asteroids.forEach(a => {
                ctx.save();
                ctx.translate(a.x, a.y);
                ctx.rotate(a.rot);

                ctx.beginPath();
                ctx.moveTo(a.size, 0);
                for (let i = 1; i < 8; i++) {
                    const angle = (i * Math.PI) / 4;
                    const r = a.size * (0.8 + Math.random() * 0.35); 
                    ctx.lineTo(r * Math.cos(angle), r * Math.sin(angle));
                }
                ctx.closePath();

                ctx.fillStyle = '#44403c';
                ctx.fill();
                ctx.lineWidth = 1.2;
                ctx.strokeStyle = '#57534e';
                ctx.stroke();

                ctx.restore();
            });
        }

        function drawLasers() {
            lasers.forEach(laser => {
                ctx.shadowBlur = 10;
                ctx.shadowColor = '#ef4444';
                ctx.fillStyle = '#fca5a5';
                
                if (laser.isCharged) {
                    ctx.shadowColor = '#06b6d4';
                    ctx.fillStyle = '#cffafe';
                    ctx.fillRect(laser.x - 3.5, laser.y - 11, 7, 22);
                } else {
                    ctx.fillRect(laser.x - 2, laser.y - 9, 4, 18);
                }
                ctx.shadowBlur = 0;
            });

            enemyLasers.forEach(laser => {
                ctx.shadowBlur = 9;
                ctx.shadowColor = '#22c55e';
                ctx.fillStyle = '#bbf7d0';
                ctx.fillRect(laser.x - 2, laser.y, 4, 16);
                ctx.shadowBlur = 0;
            });
        }

        function drawItems() {
            items.forEach(item => {
                ctx.save();
                ctx.translate(item.x, item.y);

                if (item.type === 'scrap') {
                    ctx.beginPath();
                    ctx.arc(0, 0, 6.5, 0, Math.PI * 2);
                    ctx.fillStyle = '#d97706';
                    ctx.fill();
                    ctx.lineWidth = 1.2;
                    ctx.strokeStyle = '#f59e0b';
                    ctx.stroke();
                    for (let i = 0; i < 6; i++) {
                        ctx.rotate(Math.PI / 3);
                        ctx.fillRect(-1.5, -9, 3, 3);
                    }
                } else if (item.type === 'heal') {
                    ctx.shadowBlur = 12;
                    ctx.shadowColor = '#38bdf8';
                    ctx.fillStyle = '#0284c7';
                    ctx.fillRect(-7, -7, 14, 14);
                    ctx.fillStyle = '#fff';
                    ctx.fillRect(-1.5, -4.5, 3, 9);
                    ctx.fillRect(-4.5, -1.5, 9, 3);
                    ctx.shadowBlur = 0;
                }

                ctx.restore();
            });
        }

        function drawExplosions() {
            explosions.forEach(exp => {
                ctx.beginPath();
                ctx.arc(exp.x, exp.y, exp.radius, 0, Math.PI * 2);
                ctx.fillStyle = exp.color;
                ctx.fill();
            });
        }

        function drawStars() {
            ctx.fillStyle = '#ffffff';
            stars.forEach(star => {
                ctx.fillRect(star.x, star.y, star.size, star.size);
            });
        }

        // --- LOOP PRINCIPAL DO CANVAS ---
        function gameLoop() {
            if (!gameActive) {
                isLoopRunning = false; // Desativa sinalização de loop ativo ao finalizar
                return;
            }

            ctx.fillStyle = '#030712';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            drawStars();
            drawItems();
            drawLasers();
            drawEnemies();
            drawBoss();
            drawAsteroids();
            drawExplosions();
            drawPlayer();

            update();

            requestAnimationFrame(gameLoop);
        }

    </script>
</body>
</html>


