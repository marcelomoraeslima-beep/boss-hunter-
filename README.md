<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Boss Hunter - V7.3 Clean Evolution</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        /* CONFIGURAÇÃO DOS TEMAS COM VARIÁVEIS CSS */
        :root {
            --bg-dark: #090d16;
            --panel-bg: rgba(17, 24, 39, 0.95);
            --border-color: #1e293b;
            --primary: #3b82f6;
            --danger: #ef4444; 
            --success: #22c55e; 
            --gold: #fbbf24; 
            --text: #f8fafc; 
            --purple: #a855f7;
            --souls: #00f0ff;
            --blackmarket: #bd00ff;
            --theme-glow: #3b82f6;
        }

        /* TEMA 1: NEON CYBERPUNK (PADRÃO) */
        body.theme-cyberpunk {
            --bg-dark: #090d16;
            --panel-bg: rgba(17, 24, 39, 0.95);
            --border-color: #1e293b;
            --primary: #bd00ff;
            --danger: #ef4444;
            --success: #22c55e;
            --gold: #fbbf24;
            --text: #f8fafc;
            --purple: #a855f7;
            --souls: #00f0ff;
            --blackmarket: #bd00ff;
            --theme-glow: #bd00ff;
        }

        /* TEMA 2: MINIMALIST VOID */
        body.theme-minimalist {
            --bg-dark: #050508;
            --panel-bg: rgba(20, 20, 25, 0.98);
            --border-color: #2a2a2f;
            --primary: #64748b;
            --danger: #94a3b8;
            --success: #475569;
            --gold: #cbd5e1;
            --text: #e2e8f0;
            --purple: #475569;
            --souls: #94a3b8;
            --blackmarket: #334155;
            --theme-glow: #475569;
        }

        /* TEMA 3: TOXIC ACID */
        body.theme-toxic {
            --bg-dark: #050c05;
            --panel-bg: rgba(10, 24, 10, 0.95);
            --border-color: #14532d;
            --primary: #22c55e;
            --danger: #ef4444;
            --success: #4ade80;
            --gold: #84cc16;
            --text: #f0fdf4;
            --purple: #166534;
            --souls: #22c55e;
            --blackmarket: #15803d;
            --theme-glow: #22c55e;
        }

        /* TEMA 4: IMPERIAL GOLD */
        body.theme-gold {
            --bg-dark: #120c02;
            --panel-bg: rgba(26, 18, 5, 0.96);
            --border-color: #45300d;
            --primary: #fbbf24;
            --danger: #f59e0b;
            --success: #10b981;
            --gold: #fef08a;
            --text: #fefcf0;
            --purple: #ca8a04;
            --souls: #fbbf24;
            --blackmarket: #d97706;
            --theme-glow: #fbbf24;
        }

        /* TRANSITIONS SUAVES PARA MUDANÇA DE TEMA */
        body, .tab-content, .card-item, .global-header, .arena-box, .tab-btn {
            transition: background-color 0.3s ease, border-color 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; user-select: none; font-family: 'Poppins', sans-serif; }
        body { background-color: var(--bg-dark); color: var(--text); display: flex; flex-direction: column; align-items: center; min-height: 100vh; padding: 10px; background-image: radial-gradient(circle at center, rgba(30,41,59,0.2) 0%, var(--bg-dark) 100%); }

        /* HEADER DO STATUS MUNDIAL */
        .global-header { width: 100%; max-width: 700px; display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin-bottom: 10px; background: var(--panel-bg); padding: 10px; border-radius: 12px; border: 1px solid var(--border-color); text-align: center; font-family: 'Orbitron', sans-serif; }
        .header-stat { background: rgba(0,0,0,0.3); padding: 6px; border-radius: 8px; font-size: 0.8rem; border: 1px solid rgba(255,255,255,0.05); }
        .header-stat label { display: block; font-size: 0.6rem; color: #94a3b8; margin-bottom: 2px; }

        /* MONITOR DA ARENA CENTRAL */
        .arena-box { width: 100%; max-width: 700px; background: var(--panel-bg); border-radius: 16px; border: 2px solid var(--border-color); padding: 15px; display: flex; flex-direction: column; align-items: center; position: relative; box-shadow: 0 8px 32px rgba(0,0,0,0.5); margin-bottom: 12px; }
        .boss-title-container { display: flex; justify-content: space-between; width: 100%; font-family: 'Orbitron'; margin-bottom: 8px; font-size: 0.85rem; }
        .boss-element-badge { padding: 2px 8px; border-radius: 20px; font-weight: bold; font-size: 0.75rem; text-shadow: 0 0 5px rgba(0,0,0,0.5); }
        
        .hp-container { width: 100%; height: 24px; background: #020617; border-radius: 12px; overflow: hidden; position: relative; border: 1px solid var(--border-color); display: flex; align-items: center; justify-content: center; }
        .hp-fill { height: 100%; background: linear-gradient(90deg, var(--danger), #b91c1c); width: 100%; position: absolute; left: 0; top: 0; transition: width 0.1s linear; }
        .hp-text { position: relative; z-index: 2; font-family: 'Orbitron', sans-serif; font-weight: 700; font-size: 0.8rem; text-shadow: 0 1px 3px black; }

        .boss-avatar-zone { width: 140px; height: 140px; margin: 15px 0; display: flex; align-items: center; justify-content: center; font-size: 5rem; cursor: pointer; position: relative; transition: transform 0.05s ease; }
        .boss-avatar-zone:active { transform: scale(0.92); }
        
        /* TABS RESPONSIVAS */
        .tabs-menu { display: flex; width: 100%; max-width: 700px; gap: 4px; overflow-x: auto; margin-bottom: 10px; scrollbar-width: none; }
        .tabs-menu::-webkit-scrollbar { display: none; }
        .tab-btn { flex: 1; min-width: 95px; padding: 10px 4px; text-align: center; font-size: 0.65rem; font-family: 'Orbitron', sans-serif; background: #1e293b; color: #94a3b8; border: 1px solid var(--border-color); border-radius: 8px; cursor: pointer; white-space: nowrap; transition: 0.2s; }
        .tab-btn.active { background: var(--primary); color: white; box-shadow: 0 0 10px var(--theme-glow); border-color: var(--primary); }

        /* CONTAINERS DAS ABAS */
        .tab-content { display: none; width: 100%; max-width: 700px; background: var(--panel-bg); border-radius: 16px; padding: 15px; border: 1px solid var(--border-color); }
        .tab-content.active { display: block; }

        /* UTILS DE GRID & CARDS */
        .panel-title { font-family: 'Orbitron', sans-serif; font-size: 1.1rem; margin-bottom: 12px; border-bottom: 1px solid var(--border-color); padding-bottom: 6px; display: flex; justify-content: space-between; align-items: center; }
        .grid-list { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        @media(max-width: 500px) { .grid-list { grid-template-columns: 1fr; } }
        
        .card-item { background: rgba(15, 23, 42, 0.6); border: 1px solid var(--border-color); padding: 10px; border-radius: 10px; display: flex; justify-content: space-between; align-items: center; }
        .card-info h4 { font-size: 0.85rem; color: #f1f5f9; }
        .card-info p { font-size: 0.7rem; color: #94a3b8; }
        
        /* BOTÕES */
        .action-btn { background: var(--primary); color: white; border: none; padding: 6px 12px; border-radius: 6px; font-size: 0.75rem; font-weight: 600; cursor: pointer; font-family: 'Orbitron'; transition: 0.2s; }
        .action-btn:hover { filter: brightness(1.2); }
        .action-btn:disabled { background: #334155; color: #64748b; cursor: not-allowed; }

        /* FENDAS CÓSMICAS FLUTUANTES */
        #cosmicEvent { position: fixed; width: 50px; height: 50px; border-radius: 50%; background: radial-gradient(circle, #00f0ff, #bd00ff); box-shadow: 0 0 20px #bd00ff; cursor: pointer; z-index: 9999; display: none; align-items: center; justify-content: center; font-size: 1.5rem; animation: pulseCosmic 0.8s infinite alternate; }
        @keyframes pulseCosmic { 0% { transform: scale(0.9); box-shadow: 0 0 10px #00f0ff; } 100% { transform: scale(1.1); box-shadow: 0 0 25px #bd00ff; } }

        /* EFEITO NÚMERO DE CLIQUE POPUP */
        .click-pop { position: absolute; color: var(--gold); font-family: 'Orbitron'; font-weight: 900; font-size: 1.2rem; pointer-events: none; animation: floatUp 0.6s ease-out forwards; text-shadow: 0 2px 4px black; z-index: 100; }
        @keyframes floatUp { 0% { opacity: 1; transform: translateY(0) scale(1); } 100% { opacity: 0; transform: translateY(-60px) scale(0.8); } }

        /* ELEMENTOS CORES */
        .elem-fogo { background: #ef4444; color: white; }
        .elem-gelo { background: #38bdf8; color: #0f172a; }
        .elem-trovao { background: #eab308; color: #0f172a; }
        .elem-vazio { background: #a855f7; color: white; }

        /* LISTAGEM DE PETS */
        .pets-rack { display: flex; flex-direction: column; gap: 8px; max-height: 280px; overflow-y: auto; margin-top: 10px; padding-right: 4px; }
        .pet-strip { background: rgba(30,41,59,0.4); border: 1px solid var(--border-color); padding: 8px; border-radius: 8px; display: flex; align-items: center; justify-content: space-between; }
        .pet-meta { display: flex; align-items: center; gap: 10px; }
        .pet-icon-frame { font-size: 1.6rem; position: relative; }
        .pet-stars { color: var(--gold); font-size: 0.65rem; display: block; }
        
        /* SKILL TREE MAP */
        .skill-tree-branch { display: flex; flex-direction: column; gap: 8px; background: rgba(0,0,0,0.2); padding: 10px; border-radius: 10px; border: 1px solid rgba(255,255,255,0.05); }
        .skill-tree-branch h5 { font-family: 'Orbitron'; font-size: 0.8rem; border-bottom: 1px solid #334155; padding-bottom: 4px; margin-bottom: 4px; }

        /* DUNGEON OVERLAY */
        .dungeon-overlay { display: none; flex-direction: column; align-items: center; justify-content: center; position: fixed; top:0; left:0; width:100vw; height:100vh; background: rgba(2,6,23,0.98); z-index: 10000; text-align: center; }
        .dungeon-timer { font-size: 3rem; font-family: 'Orbitron'; color: var(--danger); font-weight: bold; text-shadow: 0 0 15px rgba(239,68,68,0.5); }
    </style>
</head>
<body class="theme-cyberpunk">

    <div id="cosmicEvent" onclick="triggerCosmicClick()">🌀</div>

    <div id="dungeonOverlay" class="dungeon-overlay">
        <h1 style="font-family:'Orbitron'; color:var(--souls); margin-bottom:10px;">⚔️ MASMORRA DO TEMPO LIMITE</h1>
        <div class="dungeon-timer" id="dungeonTimer">30</div>
        <p style="color:#94a3b8; margin: 15px 0;">Clique loucamente para eliminar monstros!</p>
        <div id="dungeonMonster" style="font-size:5rem; cursor:pointer; animation: pulseCosmic 0.5s infinite alternate;" onclick="hitDungeonMonster()">👾</div>
        <h2 style="font-family:'Orbitron'; margin-top:20px;">Eliminações: <span id="dungeonKills" style="color:var(--success)">0</span></h2>
    </div>

    <div class="global-header">
        <div class="header-stat"><label>💰 OURO</label><span id="statGold" style="color:var(--gold)">0</span></div>
        <div class="header-stat"><label>🩵 ALMAS CÓSMICAS</label><span id="statSouls" style="color:var(--souls)">0</span></div>
        <div class="header-stat"><label>💎 GEMAS DO VAZIO</label><span id="statGems" style="color:#22c55e">0</span></div>
        <div class="header-stat"><label>🔑 CHAVES DE MASMORRA</label><span id="statKeys" style="color:var(--purple)">0</span></div>
    </div>

    <div class="arena-box">
        <div class="boss-title-container">
            <div><b id="bossNameDisplay">Chefe</b> (Nvl <span id="bossLevelDisplay">1</span>)</div>
            <div id="bossElementBadge" class="boss-element-badge elem-fogo">Fogo 🔥</div>
        </div>
        <div class="hp-container">
            <div class="hp-fill" id="bossHpFill"></div>
            <div class="hp-text" id="bossHpText">0 / 0</div>
        </div>
        <div class="boss-avatar-zone" id="bossTarget" onclick="dealManualDamage(event)">👾</div>
        <div style="font-size:0.7rem; color:#64748b; font-family:'Orbitron';">DPS ATUAL: <span id="displayTotalDps">0</span> | CLIQUE: <span id="displayTotalClick">1</span></div>
    </div>

    <div class="tabs-menu">
        <button class="tab-btn active" id="btn-tab-arena" onclick="switchTab('arena')">⚔️ ARENA</button>
        <button class="tab-btn" id="btn-tab-loja" onclick="switchTab('loja')">🛒 LOJA & CRAFT</button>
        <button class="tab-btn" id="btn-tab-pets" onclick="switchTab('pets')">🧬 PETS & FUSÃO</button>
        <button class="tab-btn" id="btn-tab-expedicoes" onclick="switchTab('expedicoes')">🧭 EXPEDIÇÕES</button>
        <button class="tab-btn" id="btn-tab-skills" onclick="switchTab('skills')">🌳 SKILLS</button>
        <button class="tab-btn" id="btn-tab-dungeon" onclick="switchTab('dungeon')">🔑 MASMORRA</button>
        <button class="tab-btn" id="btn-tab-market" onclick="switchTab('market')">🕵️‍♂️ MERCADO NEGRO</button>
        <button class="tab-btn" id="btn-tab-themes" onclick="switchTab('themes')">🎨 TEMAS</button>
    </div>

    <div id="tab-arena" class="tab-content active">
        <div class="panel-title"><span>⚔️ Zona de Combate Principal</span></div>
        <p style="font-size:0.8rem; color:#94a3b8; text-align:center; margin-bottom: 15px;">Seus Pets atacam automaticamente a cada segundo!</p>
        
        <div class="panel-title"><span>🔥 Habilidades Ativas dos Pets Equipados</span></div>
        <div id="activeAbilitiesContainer" style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
            </div>
    </div>

    <div id="tab-loja" class="tab-content">
        <div class="panel-title"><span>🛒 Upgrades e Manufatura</span></div>
        <div class="grid-list">
            <div class="card-item">
                <div class="card-info"><h4 id="lblUpgradeClick">Força Bruta</h4><p>+1 Dano base por clique</p></div>
                <button class="action-btn" id="btnUpgradeClick" onclick="buyBaseUpgrade('click')">💰 <span id="costUpgradeClick">10</span></button>
            </div>
            <div class="card-item">
                <div class="card-info"><h4 id="lblUpgradeDps">Treinador Passivo</h4><p>+2 Dano Automático base</p></div>
                <button class="action-btn" id="btnUpgradeDps" onclick="buyBaseUpgrade('dps')">💰 <span id="costUpgradeDps">50</span></button>
            </div>
        </div>
        <div class="panel-title" style="margin-top:20px;"><span>🔨 Forja de Chaves Cósmicas</span></div>
        <div class="card-item">
            <div class="card-info"><h4>Forjar Chave da Masmorra 🔑</h4><p>Custo: 15.000 Ouro e 10 Gemas do Vazio</p></div>
            <button class="action-btn" onclick="craftDungeonKey()">Forjar</button>
        </div>
    </div>

    <div id="tab-pets" class="tab-content">
        <div class="panel-title"><span>🥚 Incubadora do Multiverso</span></div>
        <div style="display:flex; gap:10px; margin-bottom:15px;">
            <button class="action-btn" style="flex:1; background:var(--purple);" onclick="hatchEgg()">🥚 Chocar Ovo Cósmico (💰 <span id="eggPriceDisplay">100</span>)</button>
            <button class="action-btn" style="background:var(--success);" onclick="triggerAutoFusion()">🧬 Auto-Fundir Triplicados</button>
        </div>
        <div class="pets-rack" id="petsInventoryContainer"></div>
    </div>

    <div id="tab-expedicoes" class="tab-content">
        <div class="panel-title"><span>🧭 Viagens Interdimensionais</span></div>
        <div class="grid-list" id="expeditionsTargetContainer"></div>
    </div>

    <div id="tab-skills" class="tab-content">
        <div class="panel-title"><span>🌳 Árvore de Talentos Estelares</span> <span style="font-size:0.7rem; color:var(--souls)">Almas: <span id="skillSoulsDisplay">0</span></span></div>
        <div style="display:grid; grid-template-columns: 1fr 1fr 1fr; gap:8px;">
            <div class="skill-tree-branch">
                <h5>⚔️ Guerreiro</h5>
                <button class="action-btn" onclick="investSkill('warrior')">Upar (<span id="skillLvl_warrior">0</span>/5)</button>
            </div>
            <div class="skill-tree-branch">
                <h5>🔮 Conjurador</h5>
                <button class="action-btn" onclick="investSkill('conjurer')">Upar (<span id="skillLvl_conjurer">0</span>/5)</button>
            </div>
            <div class="skill-tree-branch">
                <h5>🧪 Alquimista</h5>
                <button class="action-btn" onclick="investSkill('alchemist')">Upar (<span id="skillLvl_alchemist">0</span>/5)</button>
            </div>
        </div>
        <button class="action-btn" style="width:100%; margin-top:20px; background:var(--danger);" onclick="triggerAscensionRebirth()">🌌 REALIZAR ASCENSÃO (REBIRTH)<br><span style="font-size:0.65rem; font-weight:normal;">Zera Ouro e Upgrades por Almas. Reseta o Mercado Negro!</span></button>
    </div>

    <div id="tab-dungeon" class="tab-content">
        <div class="panel-title"><span>🔑 Prova de Sobrevivência</span></div>
        <button class="action-btn" style="width:100%; padding:12px; background:linear-gradient(45deg, #a855f7, #3b82f6);" onclick="startDungeonMode()">⚔️ ENTRAR NA MASMORRA (-1 🔑)</button>
    </div>

    <div id="tab-market" class="tab-content">
        <div class="panel-title"><span>🕵️‍♂️ Contrabando Interdimensional</span></div>
        <p style="font-size:0.75rem; color:#94a3b8; margin-bottom:15px;">Trocas com lógica flutuante. Expiram a cada ciclo de Ascensão.</p>
        <div class="grid-list" id="marketDealsContainer"></div>
        <button class="action-btn" style="width:100%; margin-top:15px; background:#5500aa;" onclick="rerollMarketDeals()">🔄 Subornar Mercador (Custo: 2 Almas)</button>
    </div>

    <div id="tab-themes" class="tab-content">
        <div class="panel-title"><span>🎨 Customização e Temas Visuais</span></div>
        <p style="font-size:0.75rem; color:#94a3b8; margin-bottom:15px;">Personalize a interface do seu Boss Hunter. Novas opções exigem Gemas do Vazio.</p>
        <div class="grid-list" id="themesContainer"></div>
    </div>

    <script>
        // --- PROPRIEDADES DE ESTADO ---
        let gold = 0;
        let bossSouls = 0;
        let gems = 0;
        let dungeonKeys = 1;
        let lvlClick = 0;
        let lvlDps = 0;
        let eggCost = 100;
        let bossLevel = 1;
        let bossMaxHp = 50;
        let bossCurrentHp = 50;
        let bossElement = "🔥 Fogo";
        let bossName = "Slime";
        let pets = [];
        let skillTree = { warrior: 0, conjurer: 0, alchemist: 0 };
        
        let marketDeals = []; 

        // ESTADO DE CUSTOMIZAÇÃO DE TEMAS
        let activeTheme = "cyberpunk";
        let unlockedThemes = ["cyberpunk", "minimalist"];

        const themesData = [
            { id: "cyberpunk", name: "Neon Cyberpunk 🌌", desc: "Paleta clássica com luzes violetas e azuladas.", cost: 0 },
            { id: "minimalist", name: "Minimalist Void 🌑", desc: "Baixo contraste. Confortável para grinds e noites de jogo.", cost: 0 },
            { id: "toxic", name: "Toxic Acid 🧪", desc: "Verde neon corrosivo. Sinta-se dentro de um sistema hacker.", cost: 20 },
            { id: "gold", name: "Imperial Gold 👑", desc: "Tema de luxo com correntes de ouro e âmbar. Exclusivo.", cost: 50 }
        ];

        let expeditions = [
            { id: 1, name: "Planeta Ígneo 🌋", duration: 30, active: false, timeLeft: 0, rewardType: "gold", rewardAmt: 1000, petId: null },
            { id: 2, name: "Nebulosa Gelada ❄️", duration: 90, active: false, timeLeft: 0, rewardType: "gems", rewardAmt: 15, petId: null },
            { id: 3, name: "Fenda Estática ⚡", duration: 240, active: false, timeLeft: 0, rewardType: "keys", rewardAmt: 2, petId: null }
        ];

        const elementsList = ["🔥 Fogo", "❄️ Gelo", "⚡ Trovão", "🌌 Vazio"];
        const elementCounters = { "🔥 Fogo": "❄️ Gelo", "❄️ Gelo": "⚡ Trovão", "⚡ Trovão": "🌌 Vazio", "🌌 Vazio": "🔥 Fogo" };
        const rarities = [
            { name: "Comum", mult: 1, color: "#a0a0a0" },
            { name: "Incomum", mult: 3, color: "#22c55e" },
            { name: "Épico", mult: 8, color: "#3b82f6" },
            { name: "Lendário", mult: 25, color: "#eab308" },
            { name: "Cósmico", mult: 100, color: "#00f0ff" }
        ];
        const petIcons = ["🦊", "🦉", "🦁", "🐉", "🤖", "👾", "🛸", "🪐", "🦄", "🦅", "🦈", "🐺", "👻", "🎃", "💀", "🐦", "🐸", "🐈", "🦖", "🦂", "🐙", "🐝"];
        const petNames = ["Alfa", "Ciborgue", "Espectral", "Rúnico", "Quântico", "Abissal", "Celestial", "Temporal", "Divino", "Estelar", "Radioativo", "Mutante", "Sombrio", "Cortex", "Glitch", "Fênix", "Nebuloso", "Ancestral", "Void", "Titan", "Spectre", "Overlord"];

        let superOverloadActive = false;
        let superOverloadTimer = 0;
        let inDungeon = false;
        let dungeonTimer = 30;
        let dungeonKills = 0;
        let dungeonInterval = null;

        window.onload = function() {
            loadGame();
            applyTheme(activeTheme);
            generateMarketDeals(); 
            setInterval(gameTick, 1000);
            setInterval(spawnRandomScreenEvent, 60000);
            updateUI();
            spawnBoss();
        }

        function gameTick() {
            if(!inDungeon) dealDamage(calculateTotalDps());
            expeditions.forEach(exp => {
                if(exp.active) {
                    exp.timeLeft--;
                    if(exp.timeLeft <= 0) completeExpedition(exp);
                }
            });
            if(superOverloadActive) {
                superOverloadTimer--;
                if(superOverloadTimer <= 0) superOverloadActive = false;
            }
            updateUI();
        }

        function renderThemes() {
            let container = document.getElementById("themesContainer");
            if(!container) return;
            container.innerHTML = "";

            themesData.forEach(t => {
                let isUnlocked = unlockedThemes.includes(t.id);
                let isActive = activeTheme === t.id;
                let btnHtml = "";

                if(isActive) {
                    btnHtml = `<button class="action-btn" style="background:#475569;" disabled>ATIVO ⚡</button>`;
                } else if(isUnlocked) {
                    btnHtml = `<button class="action-btn" style="background:var(--success);" onclick="selectTheme('${t.id}')">Equipar</button>`;
                } else {
                    btnHtml = `<button class="action-btn" style="background:var(--blackmarket);" onclick="buyTheme('${t.id}', ${t.cost})">💎 ${t.cost}</button>`;
                }

                container.innerHTML += `
                    <div class="card-item" style="border-color: ${isActive ? 'var(--primary)' : 'var(--border-color)'}">
                        <div class="card-info">
                            <h4>${t.name}</h4>
                            <p>${t.desc}</p>
                        </div>
                        <div>
                            ${btnHtml}
                        </div>
                    </div>
                `;
            });
        }

        function selectTheme(themeId) {
            activeTheme = themeId;
            applyTheme(themeId);
            renderThemes();
            saveGame();
        }

        function applyTheme(themeId) {
            document.body.className = "";
            document.body.classList.add("theme-" + themeId);
        }

        function buyTheme(themeId, cost) {
            if(gems >= cost) {
                gems -= cost;
                unlockedThemes.push(themeId);
                alert(`🎨 Tema Desbloqueado com sucesso!`);
                selectTheme(themeId);
            } else {
                alert("Gemas do Vazio insuficientes para desbloquear este tema.");
            }
        }

        function generateMarketDeals() {
            marketDeals = [];

            const pool = [
                { 
                    text: "Trocar 5.000 Ouro por 10 Gemas do Vazio 💎", 
                    check: () => gold >= 5000, 
                    pay: () => gold -= 5000, 
                    give: () => gems += 10 
                },
                { 
                    text: "Contrabando: 3 Pets Ociosos por 1 Chave 🔑", 
                    check: () => pets.filter(p => !p.equipped && !p.onExpedition).length >= 3, 
                    pay: () => {
                        let removidos = 0;
                        pets = pets.filter(p => {
                            if(!p.equipped && !p.onExpedition && removidos < 3) { removidos++; return false; }
                            return true;
                        });
                    }, 
                    give: () => dungeonKeys += 1 
                },
                { 
                    text: "Trocar 40 Gemas por 2 Almas Cósmicas 🩵", 
                    check: () => gems >= 40, 
                    pay: () => gems -= 40, 
                    give: () => bossSouls += 2 
                },
                { 
                    text: "Suborno: 3 Almas por 35.000 Moedas de Ouro 💰", 
                    check: () => bossSouls >= 3, 
                    pay: () => bossSouls -= 3, 
                    give: () => gold += 35000 
                },
                { 
                    text: "Liquidando 1 Chave por 20 Gemas do Vazio 💎", 
                    check: () => dungeonKeys >= 1, 
                    pay: () => dungeonKeys -= 1, 
                    give: () => gems += 20 
                }
            ];

            let shuffled = pool.sort(() => 0.5 - Math.random());
            marketDeals = shuffled.slice(0, 3);
            
            renderMarket();
        }

        function renderMarket() {
            let container = document.getElementById("marketDealsContainer");
            if(!container) return;
            container.innerHTML = "";

            marketDeals.forEach((deal, index) => {
                container.innerHTML += `
                    <div class="card-item" style="border: 1px solid var(--blackmarket); background: rgba(30,20,50,0.4);">
                        <div class="card-info">
                            <h3 style="color:var(--blackmarket); font-size:0.85rem; font-family:'Orbitron';">Acordo Proibido #${index + 1}</h3>
                            <p style="font-size:0.75rem; margin-top:2px;">${deal.text}</p>
                        </div>
                        <button class="action-btn" style="background:var(--blackmarket);" onclick="executeMarketDeal(${index})">Trocar 🤝</button>
                    </div>
                `;
            });
        }

        function executeMarketDeal(index) {
            let deal = marketDeals[index];
            
            if (deal.check()) {
                deal.pay();  
                deal.give(); 
                alert("Negócio fechado! O contrabandista agradece. 👽");
                
                marketDeals.splice(index, 1);
                
                renderPets();
                updateUI();
                renderMarket();
            } else {
                alert("Você não tem os recursos necessários para este contrabando!");
            }
        }

        function rerollMarketDeals() {
            if (bossSouls >= 2) {
                bossSouls -= 2;
                generateMarketDeals();
                updateUI();
            } else {
                alert("Almas insuficientes para subornar o mercador.");
            }
        }

        function triggerAscensionRebirth() {
            if(bossLevel < 20) {
                alert("Atinja o Nível 20 de chefe para poder ascender!");
                return;
            }

            let almasGanhas = Math.floor(bossLevel / 10);
            if(confirm(`Deseja ascender? Você ganhará +${almasGanhas} Almas. Ouro e upgrades resets. O Mercado Negro e temas serão recalculados.`)) {
                bossSouls += almasGanhas;
                gold = 0;
                lvlClick = 0;
                lvlDps = 0;
                bossLevel = 1;
                
                generateMarketDeals(); 
                
                spawnBoss();
                updateUI();
            }
        }

        function calculateTotalClick() {
            let base = 1 + lvlClick;
            let skillMult = 1 + (skillTree.warrior * 0.3);
            let petBonus = 0;
            pets.forEach(p => { if(p.equipped && p.statType === "clique") petBonus += (p.power * p.stars); });
            let final = (base + petBonus) * skillMult * iceFreezeBonus;
            if(superOverloadActive) final *= 10;
            return Math.floor(final);
        }

        function calculateTotalDps() {
            let base = lvlDps;
            let skillMult = 1 + (skillTree.conjurer * 0.4);
            let petBonus = 0;
            pets.forEach(p => { if(p.equipped && p.statType === "dps") petBonus += (p.power * p.stars); });
            let finalDps = Math.floor((base + petBonus) * skillMult * iceFreezeBonus);
            if(thunderDpsTimer > 0) finalDps *= 2;
            return finalDps;
        }

        function spawnBoss() {
            bossMaxHp = Math.floor(50 * Math.pow(1.3, bossLevel - 1));
            bossCurrentHp = bossMaxHp;
            bossElement = elementsList[Math.floor(Math.random() * elementsList.length)];
            bossName = "Boss Nvl " + bossLevel;

            let badge = document.getElementById("bossElementBadge");
            if(badge) {
                badge.className = "boss-element-badge";
                if(bossElement.includes("Fogo")) badge.classList.add("elem-fogo");
                if(bossElement.includes("Gelo")) badge.classList.add("elem-gelo");
                if(bossElement.includes("Trovão")) badge.classList.add("elem-trovao");
                if(bossElement.includes("Vazio")) badge.classList.add("elem-vazio");
                badge.innerText = bossElement;
            }

            let nameDisp = document.getElementById("bossNameDisplay");
            if(nameDisp) nameDisp.innerText = bossName;
            let lvlDisp = document.getElementById("bossLevelDisplay");
            if(lvlDisp) lvlDisp.innerText = bossLevel;
            updateUI();
        }

        function dealDamage(amount) {
            if(inDungeon) return;
            bossCurrentHp -= amount;
            if(bossCurrentHp <= 0) {
                let skillGoldMult = 1 + (skillTree.alchemist * 0.5);
                gold += Math.floor((bossLevel * 15) * skillGoldMult);
                if(Math.random() < 0.15) gems += 1;
                bossLevel++;
                spawnBoss();
            }
            updateUI();
        }

        function dealManualDamage(event) {
            let dmg = calculateTotalClick();
            let counter = false;
            pets.forEach(p => { if(p.equipped && elementCounters[p.element] === bossElement) counter = true; });
            if(counter) dmg = Math.floor(dmg * 1.5);
            createFloatingText(event, `+${dmg}`, counter ? "#ff9900" : "var(--gold)");
            dealDamage(dmg);
        }

        function createFloatingText(event, text, color) {
            let zone = document.getElementById("bossTarget");
            if(!zone) return;
            let pop = document.createElement("div");
            pop.className = "click-pop";
            pop.innerText = text;
            pop.style.color = color;
            pop.style.left = (event.offsetX || 50) + "px";
            pop.style.top = (event.offsetY || 50) + "px";
            zone.appendChild(pop);
            setTimeout(() => pop.remove(), 600);
        }

        function buyBaseUpgrade(type) {
            if(type === 'click') {
                let cost = Math.floor(10 * Math.pow(1.5, lvlClick));
                if(gold >= cost) { gold -= cost; lvlClick++; }
            } else {
                let cost = Math.floor(50 * Math.pow(1.6, lvlDps));
                if(gold >= cost) { gold -= cost; lvlDps++; }
            }
            updateUI();
        }

        function craftDungeonKey() {
            if(gold >= 15000 && gems >= 10) { gold -= 15000; gems -= 10; dungeonKeys++; alert("Chave Criada! 🔑"); }
            else { alert("Recursos insuficientes!"); }
            updateUI();
        }

        function hatchEgg() {
            if(gold >= eggCost) {
                gold -= eggCost;
                eggCost = Math.floor(eggCost * 1.25);
                let rand = Math.random();
                let rarity = rarities[0];
                if(rand < 0.02) rarity = rarities[4];
                else if(rand < 0.08) rarity = rarities[3];
                else if(rand < 0.20) rarity = rarities[2];
                else if(rand < 0.50) rarity = rarities[1];

                let type = Math.random() > 0.5 ? "clique" : "dps";
                let element = elementsList[Math.floor(Math.random() * elementsList.length)];
                let name = rarity.name + " " + petNames[Math.floor(Math.random()*petNames.length)] + " " + petIcons[Math.floor(Math.random()*petIcons.length)];
                let pwr = Math.floor((Math.random() * 5 + 2) * rarity.mult);

                pets.push({ id: Date.now() + Math.random().toString(), name: name, rarity: rarity.name, color: rarity.color, statType: type, element: element, power: pwr, stars: 1, equipped: false, onExpedition: false, lastUsedAbility: 0 });
                alert(`🥚 Você obteve: ${name}!`);
                renderPets();
                updateUI();
            } else { alert("Sem ouro!"); }
        }

        function renderPets() {
            let container = document.getElementById("petsInventoryContainer");
            if(!container) return;
            container.innerHTML = "";
            if(pets.length === 0){ container.innerHTML = "<p style='color:#64748b; font-size:0.75rem;'>Sem pets.</p>"; return; }
            pets.forEach(p => {
                container.innerHTML += `
                    <div class="pet-strip" style="border-left: 4px solid ${p.color}">
                        <div>
                            <h4 style="color:${p.color}; font-size:0.8rem;">${p.name}</h4>
                            <p style="font-size:0.65rem;">+${p.power * p.stars} ${p.statType.toUpperCase()} | ${p.element} | ${"⭐".repeat(p.stars)}</p>
                        </div>
                        <button class="action-btn" onclick="toggleEquipPet('${p.id}')">${p.onExpedition ? 'Missão' : (p.equipped ? 'Desequipar' : 'Equipar')}</button>
                    </div>
                `;
            });
        }

        // --- SISTEMA DE HABILIDADES ATIVAS DE PETS ---
        let iceFreezeBonus = 1; 
        let thunderDpsTimer = 0; 

        function renderActiveAbilities() {
            let container = document.getElementById("activeAbilitiesContainer");
            if(!container) return;
            container.innerHTML = "";
            
            let equipped = pets.filter(p => p.equipped);
            if(equipped.length === 0) {
                container.innerHTML = "<p style='color:#64748b; font-size:0.75rem; grid-column: span 2; text-align:center;'>Nenhum pet equipado para usar habilidades!</p>";
                return;
            }

            let now = Date.now();
            equipped.forEach(p => {
                let elemSymbol = p.element.split(" ")[1] || "🔥";
                let skillName = "";
                let skillDesc = "";

                if(p.element.includes("Fogo")) { skillName = "Impacto Ígneo"; skillDesc = "Dano instantâneo massivo"; }
                else if(p.element.includes("Gelo")) { skillName = "Sopro Glacial"; skillDesc = "+50% dano global (5s)"; }
                else if(p.element.includes("Trovão")) { skillName = "Sobrecarga"; skillDesc = "Dobra o DPS por 8 segundos"; }
                else if(p.element.includes("Vazio")) { skillName = "Fenda da Fortuna"; skillDesc = "Gera Ouro e chance de Gemas"; }

                let lastUsed = p.lastUsedAbility || 0;
                let cooldownLeft = Math.max(0, Math.ceil((lastUsed + 30000 - now) / 1000));
                let btnText = cooldownLeft > 0 ? `Recarga: ${cooldownLeft}s` : "ATIVAR!";
                let disabledAttr = cooldownLeft > 0 ? "disabled" : "";

                container.innerHTML += `
                    <div class="card-item" style="border: 1px solid ${p.color}; display: flex; flex-direction: column; align-items: stretch; gap: 6px;">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <span style="font-size:1rem;">${p.name.split(" ").slice(-1)[0]} ${elemSymbol}</span>
                            <span style="font-size:0.6rem; background: rgba(255,255,255,0.1); padding: 2px 6px; border-radius: 4px;">Nível ${p.stars}</span>
                        </div>
                        <div style="text-align: left;">
                            <h5 style="color: ${p.color}; font-size: 0.75rem; font-family: 'Orbitron';">${skillName}</h5>
                            <p style="font-size: 0.6rem; color: #94a3b8;">${skillDesc}</p>
                        </div>
                        <button class="action-btn" style="width: 100%; background: ${cooldownLeft > 0 ? '#334155' : 'var(--primary)'};" onclick="usePetAbility('${p.id}')" ${disabledAttr}>${btnText}</button>
                    </div>
                `;
            });
        }

        function usePetAbility(petId) {
            let pet = pets.find(p => p.id === petId);
            if(!pet) return;
            let now = Date.now();
            let lastUsed = pet.lastUsedAbility || 0;
            if(now - lastUsed < 30000) return;

            pet.lastUsedAbility = now;

            if(pet.element.includes("Fogo")) {
                let damage = calculateTotalClick() * 20 * pet.stars;
                dealDamage(damage);
                createFloatingText({offsetX: 70, offsetY: 40}, `💥 ${damage.toLocaleString()}`, "#f97316");
                alert(`${pet.name} usou Impacto Ígneo e causou ${damage.toLocaleString()} de dano!`);
            } 
            else if(pet.element.includes("Gelo")) {
                iceFreezeBonus = 1.5;
                setTimeout(() => { iceFreezeBonus = 1; renderActiveAbilities(); }, 5000);
                alert(`${pet.name} usou Sopro Glacial! Todo o dano aumentado em +50% por 5 segundos!`);
            } 
            else if(pet.element.includes("Trovão")) {
                thunderDpsTimer = 8;
                let thInterval = setInterval(() => {
                    thunderDpsTimer--;
                    if(thunderDpsTimer <= 0) {
                        clearInterval(thInterval);
                        renderActiveAbilities();
                    }
                }, 1000);
                alert(`${pet.name} usou Sobrecarga! Seu DPS automático foi duplicado por 8 segundos!`);
            } 
            else if(pet.element.includes("Vazio")) {
                let goldGained = Math.floor(bossLevel * 500 * pet.stars);
                gold += goldGained;
                let gemFound = Math.random() < 0.25;
                if(gemFound) {
                    gems += 1;
                    alert(`${pet.name} abriu uma Fenda Cósmica e trouxe +💰 ${goldGained.toLocaleString()} de Ouro e +💎 1 Gema do Vazio!`);
                } else {
                    alert(`${pet.name} abriu uma Fenda Cósmica e trouxe +💰 ${goldGained.toLocaleString()} de Ouro!`);
                }
            }

            renderActiveAbilities();
            updateUI();
        }

        setInterval(() => {
            if(document.getElementById("tab-arena").classList.contains("active")) {
                renderActiveAbilities();
            }
        }, 1000);

        function toggleEquipPet(id) {
            let pet = pets.find(p => p.id === id);
            if(!pet || pet.onExpedition) return;
            if(pet.equipped) pet.equipped = false;
            else {
                if(pets.filter(p => p.equipped).length >= 4) return alert("Máximo 4 equipados!");
                pet.equipped = true;
            }
            renderPets();
            updateUI();
            renderActiveAbilities();
        }

        function triggerAutoFusion() {
            let lists = {};
            let fuseCount = 0;
            pets.forEach(p => { if(!p.equipped && !p.onExpedition) { let k = `${p.rarity}_${p.statType}_${p.stars}`; if(!lists[k]) lists[k] = []; lists[k].push(p); } });
            
            for(let k in lists) {
                while(lists[k].length >= 3) {
                    let sub = lists[k].splice(0, 3);
                    let base = sub[0];
                    pets = pets.filter(p => !sub.includes(p));
                    fuseCount++;
                    if(base.stars < 3) { base.stars++; base.id = Date.now() + Math.random().toString(); pets.push(base); } 
                    else {
                        let idx = Math.min(rarities.findIndex(r => r.name === base.rarity) + 1, rarities.length - 1);
                        let nr = rarities[idx];
                        pets.push({ id: Date.now() + Math.random().toString(), name: nr.name + " Evoluído 🧬", rarity: nr.name, color: nr.color, statType: base.statType, element: elementsList[0], power: Math.floor(5 * nr.mult), stars: 1, equipped: false, onExpedition: false, lastUsedAbility: 0 });
                    }
                }
            }
            if(fuseCount > 0) { renderPets(); updateUI(); alert("Fusão realizada!"); }
        }

        function renderExpeditions() {
            let container = document.getElementById("expeditionsTargetContainer");
            if(!container) return;
            container.innerHTML = "";
            expeditions.forEach(exp => {
                container.innerHTML += `
                    <div class="card-item" style="flex-direction:column; align-items:flex-start; gap:6px;">
                        <h4>${exp.name}</h4>
                        <p style="font-size:0.65rem;">${exp.active ? 'Restam: ' + exp.timeLeft + 's' : 'Prêmio: ' + exp.rewardAmt + ' ' + exp.rewardType}</p>
                        <button class="action-btn" style="width:100%;" ${exp.active ? 'disabled' : ''} onclick="startExpedition(${exp.id})">${exp.active ? 'Explorando' : 'Enviar Pet'}</button>
                    </div>
                `;
            });
        }

        function startExpedition(id) {
            let exp = expeditions.find(e => e.id === id);
            let pet = pets.find(p => !p.equipped && !p.onExpedition);
            if(!pet) return alert("Nenhum pet ocioso!");
            pet.onExpedition = true; exp.active = true; exp.timeLeft = exp.duration; exp.petId = pet.id;
            renderPets(); renderExpeditions();
        }

        function completeExpedition(exp) {
            exp.active = false;
            let pet = pets.find(p => p.id === exp.petId);
            if(pet) pet.onExpedition = false;
            if(exp.rewardType === "gold") gold += exp.rewardAmt;
            if(exp.rewardType === "gems") gems += exp.rewardAmt;
            if(exp.rewardType === "keys") dungeonKeys += exp.rewardAmt;
            exp.petId = null;
            renderPets(); renderExpeditions(); updateUI();
            alert(`🧭 Expedição concluída! +${exp.rewardAmt} ${exp.rewardType.toUpperCase()}`);
        }

        function spawnRandomScreenEvent() {
            let ev = document.getElementById("cosmicEvent");
            if(!ev) return;
            ev.style.left = (Math.random() * (window.innerWidth - 60)) + "px";
            ev.style.top = (Math.random() * (window.innerHeight - 60)) + "px";
            ev.style.display = "flex";
            setTimeout(() => { if(ev) ev.style.display = "none"; }, 8000);
        }

        function triggerCosmicClick() {
            let ev = document.getElementById("cosmicEvent");
            if(ev) ev.style.display = "none";
            let r = Math.random();
            if(r < 0.4) { gems += 5; alert("Fenda de Gemas! +5 Gemas 💎"); }
            else if(r < 0.7) { bossCurrentHp = Math.max(1, Math.floor(bossCurrentHp / 2)); alert("Meteoro! Vida do chefe cortada pela metade!"); }
            else { superOverloadActive = true; superOverloadTimer = 15; alert("Dano de clique x10 por 15 segundos! ⚡"); }
            updateUI();
        }

        function investSkill(branch) {
            if(bossSouls >= 1 && skillTree[branch] < 5) { bossSouls--; skillTree[branch]++; updateUI(); }
        }

        function saveGame() {
            let data = { gold, bossSouls, gems, dungeonKeys, lvlClick, lvlDps, eggCost, bossLevel, pets, skillTree, activeTheme, unlockedThemes };
            localStorage.setItem("bossHunter_v7.0_save", JSON.stringify(data));
        }

        function loadGame() {
            let save = localStorage.getItem("bossHunter_v7.0_save");
            if(save) {
                let d = JSON.parse(save);
                gold = d.gold || 0; bossSouls = d.bossSouls || 0; gems = d.gems || 0;
                dungeonKeys = d.dungeonKeys !== undefined ? d.dungeonKeys : 1;
                lvlClick = d.lvlClick || 0; lvlDps = d.lvlDps || 0; eggCost = d.eggCost || 100;
                bossLevel = d.bossLevel || 1; pets = d.pets || [];
                skillTree = d.skillTree || { warrior: 0, conjurer: 0, alchemist: 0 };
                activeTheme = d.activeTheme || "cyberpunk";
                unlockedThemes = d.unlockedThemes || ["cyberpunk", "minimalist"];
            }
        }

        function startDungeonMode() {
            if(dungeonKeys <= 0) return alert("Sem chaves!");
            dungeonKeys--; inDungeon = true; dungeonTimer = 30; dungeonKills = 0;
            let overlay = document.getElementById("dungeonOverlay");
            if(overlay) overlay.style.display = "flex";
            dungeonInterval = setInterval(() => {
                dungeonTimer--;
                let timerDisp = document.getElementById("dungeonTimer");
                if(timerDisp) timerDisp.innerText = dungeonTimer;
                if(dungeonTimer <= 0) {
                    clearInterval(dungeonInterval);
                    if(overlay) overlay.style.display = "none";
                    inDungeon = false;
                    let pg = dungeonKills * 300; gold += pg;
                    alert(`Fim! ${dungeonKills} abates. Conseguiu +💰 ${pg} Ouro!`);
                    updateUI();
                }
            }, 1000);
        }

        function hitDungeonMonster() {
            dungeonKills++;
            let killsDisp = document.getElementById("dungeonKills");
            if(killsDisp) killsDisp.innerText = dungeonKills;
        }

        function updateUI() {
            let elGold = document.getElementById("statGold"); if(elGold) elGold.innerText = gold.toLocaleString();
            let elSouls = document.getElementById("statSouls"); if(elSouls) elSouls.innerText = bossSouls;
            let elGems = document.getElementById("statGems"); if(elGems) elGems.innerText = gems;
            let elKeys = document.getElementById("statKeys"); if(elKeys) elKeys.innerText = dungeonKeys;
            
            let elHpText = document.getElementById("bossHpText"); if(elHpText) elHpText.innerText = `${bossCurrentHp.toLocaleString()} / ${bossMaxHp.toLocaleString()}`;
            let elHpFill = document.getElementById("bossHpFill"); if(elHpFill) elHpFill.style.width = `${Math.max(0, (bossCurrentHp / bossMaxHp) * 100)}%`;
            
            let elUpClick = document.getElementById("costUpgradeClick"); if(elUpClick) elUpClick.innerText = Math.floor(10 * Math.pow(1.5, lvlClick)).toLocaleString();
            let elUpDps = document.getElementById("costUpgradeDps"); if(elUpDps) elUpDps.innerText = Math.floor(50 * Math.pow(1.6, lvlDps)).toLocaleString();
            
            let elEgg = document.getElementById("eggPriceDisplay"); if(elEgg) elEgg.innerText = eggCost.toLocaleString();
            let elTotClick = document.getElementById("displayTotalClick"); if(elTotClick) elTotClick.innerText = calculateTotalClick();
            let elTotDps = document.getElementById("displayTotalDps"); if(elTotDps) elTotDps.innerText = calculateTotalDps();
            
            let elSkSouls = document.getElementById("skillSoulsDisplay"); if(elSkSouls) elSkSouls.innerText = bossSouls;
            let elSkW = document.getElementById("skillLvl_warrior"); if(elSkW) elSkW.innerText = skillTree.warrior;
            let elSkC = document.getElementById("skillLvl_conjurer"); if(elSkC) elSkC.innerText = skillTree.conjurer;
            let elSkA = document.getElementById("skillLvl_alchemist"); if(elSkA) elSkA.innerText = skillTree.alchemist;
            saveGame();
        }

        function switchTab(id) {
            document.querySelectorAll(".tab-content").forEach(el => el.classList.remove("active"));
            document.querySelectorAll(".tab-btn").forEach(el => el.classList.remove("active"));
            
            let elTab = document.getElementById(`tab-${id}`); if(elTab) elTab.classList.add("active");
            let elBtn = document.getElementById(`btn-tab-${id}`); if(elBtn) elBtn.classList.add("active");
            
            if(id === 'pets') renderPets();
            if(id === 'expedicoes') renderExpeditions();
            if(id === 'market') renderMarket();
            if(id === 'themes') renderThemes();
            if(id === 'arena') renderActiveAbilities();
        }
    </script>
</body>
</html>
