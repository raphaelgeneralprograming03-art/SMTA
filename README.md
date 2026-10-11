
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SMTA - Sistema de Mitigação Termomecânica Avançada</title>
    <style>
        :root {
            --bg-color: #020617;
            --panel-bg: rgba(10, 22, 40, 0.9);
            --border-color: #38bdf8;
            --accent-green: #22c55e;
            --accent-red: #ef4444;
            --accent-orange: #f97316;
            --accent-cyan: #06b6d4;
            --text-main: #e2e8f0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Courier New', Courier, monospace;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        header {
            background: linear-gradient(90deg, #020617, #0f172a, #020617);
            border-bottom: 2px solid var(--border-color);
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        header h1 {
            font-size: 1.05rem;
            color: var(--border-color);
            letter-spacing: 2px;
        }

        .status-badge {
            background: rgba(56, 189, 248, 0.2);
            border: 1px solid var(--border-color);
            color: var(--border-color);
            padding: 4px 10px;
            font-size: 0.75rem;
            font-weight: bold;
            border-radius: 3px;
            letter-spacing: 1px;
        }

        .main-container {
            display: flex;
            flex: 1;
            gap: 12px;
            padding: 12px;
            overflow: hidden;
        }

        /* Painel de Controle Esquerdo */
        .control-panel {
            width: 330px;
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 12px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            box-shadow: 0 0 15px rgba(56, 189, 248, 0.1);
        }

        .panel-section h3 {
            font-size: 0.8rem;
            color: var(--border-color);
            margin-bottom: 6px;
            border-bottom: 1px solid rgba(56, 189, 248, 0.3);
            padding-bottom: 3px;
            letter-spacing: 1px;
        }

        .btn-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
        }

        button {
            background: rgba(56, 189, 248, 0.1);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 8px 10px;
            text-align: left;
            font-size: 0.75rem;
            cursor: pointer;
            border-radius: 4px;
            transition: all 0.3s ease;
        }

        button:hover {
            background: rgba(56, 189, 248, 0.3);
            color: #fff;
            box-shadow: 0 0 8px var(--border-color);
        }

        button.action-plasma {
            border-color: var(--accent-orange);
            background: rgba(249, 115, 22, 0.1);
            color: #fed7aa;
        }
        button.action-plasma:hover {
            background: rgba(249, 115, 22, 0.3);
        }

        /* Centro: Canvas e Logs */
        .center-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 12px;
            overflow: hidden;
        }

        .viewport-container {
            flex: 1.4;
            background: #010409;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            display: flex;
            flex-direction: column;
            position: relative;
            overflow: hidden;
        }

        .viewport-header {
            background: rgba(56, 189, 248, 0.05);
            padding: 6px 12px;
            font-size: 0.7rem;
            display: flex;
            justify-content: space-between;
            border-bottom: 1px solid rgba(56, 189, 248, 0.2);
        }

        canvas {
            flex: 1;
            display: block;
            width: 100%;
            height: 100%;
        }

        .ai-log-panel {
            flex: 1;
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 10px;
            display: flex;
            flex-direction: column;
            gap: 6px;
            font-size: 0.72rem;
            overflow-y: auto;
        }

        .log-title {
            color: var(--accent-green);
            font-weight: bold;
            border-bottom: 1px solid rgba(34, 197, 94, 0.3);
            padding-bottom: 2px;
        }

        .log-content {
            color: #cbd5e1;
            line-height: 1.4;
        }

        /* Telemetria Direita */
        .telemetry-panel {
            width: 310px;
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 12px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .metric-box {
            background: rgba(2, 6, 23, 0.7);
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-radius: 4px;
            padding: 8px;
        }

        .metric-title {
            font-size: 0.65rem;
            color: var(--border-color);
            margin-bottom: 3px;
        }

        .metric-value {
            font-size: 0.9rem;
            font-weight: bold;
            color: #fff;
        }

        .status-ok { color: var(--accent-green); }
        .status-alert { color: var(--accent-red); }
        .status-heat { color: var(--accent-orange); }
    </style>
</head>
<body>

    <header>
        <h1>SISTEMA DE MITIGAÇÃO TERMOMECÂNICA AVANÇADA (SMTA)</h1>
        <div class="status-badge">PROTÓTIPO: CONE OGIVAL [600mm x 350mm]</div>
    </header>

    <div class="main-container">
        <!-- 1. Painel de Controle -->
        <div class="control-panel">
            <div class="panel-section">
                <h3>TESTES DE ESTRESSE</h3>
                <div class="btn-group">
                    <button class="action-plasma" onclick="startHypersonicTest()">Iniciar Teste Plasma (Mach 8 - 2.100°C)</button>
                    <button onclick="toggleSensorsView()">Alternar Camadas / Sensores</button>
                    <button onclick="resetSystem()">Resetar Protótipo</button>
                </div>
            </div>

            <div class="panel-section">
                <h3>ESPECIFICAÇÕES GEOMÉTRICAS</h3>
                <div style="font-size: 0.68rem; line-height: 1.3; color: #94a3b8;">
                    • Comprimento Eixo X: 600 mm (60 cm)<br>
                    • Diâmetro da Base: 350 mm (35 cm)<br>
                    • Raio do Nariz (Ponto Crit.): 25 mm<br>
                    • Casca Externa (C/SiC): 12 mm<br>
                    • Revestimento de Ablação: 3 mm<br>
                    • Aerogel Térmico: 25 mm<br>
                    • Chassi Ti-6Al-4V: 8 mm
                </div>
            </div>

            <div class="panel-section">
                <h3>SUBSISTEMAS ATIVOS</h3>
                <div style="font-size: 0.68rem; line-height: 1.3; color: #94a3b8;">
                    • 06x Termopares Tipo S (Platina/Ródio)<br>
                    • 04x Sensores Schmidt-Boelter (Fluxo)<br>
                    • 04x Piezoelétricos de Alta Pressão<br>
                    • FPGA Xilinx Kintex UltraScale+<br>
                    • Telemetria Blindada Banda S/Ka
                </div>
            </div>
        </div>

        <!-- 2. Centro: Canvas & Logs -->
        <div class="center-container">
            <div class="viewport-container">
                <div class="viewport-header">
                    <span id="view-status">VISUALIZAÇÃO TRANSVERSAL DO CONE OGIVAL E GRADIENTE TÉRMICO</span>
                    <span id="test-mode">STATUS: PRONTO PARA TESTE</span>
                </div>
                <canvas id="simCanvas"></canvas>
            </div>

            <div class="ai-log-panel">
                <div class="log-title">[ TELEMETRIA FPGA & RELATÓRIO DO NÚCLEO ISOLADO ]</div>
                <div class="log-content" id="smta-log-text">
                    [14:00:01] SMTA inicializado. FPGA Xilinx UltraScale+ operando com isolamento galvânico.<br>
                    [14:00:02] Calibração de termopares Tipo S concluída (Leitura nominal 24.5 °C).<br>
                    [14:00:03] Barreira térmica de Aerogel e selagem de zircônia íntegras. Aguardando ignição.
                </div>
            </div>
        </div>

        <!-- 3. Telemetria Direita -->
        <div class="telemetry-panel">
            <div class="panel-section">
                <h3>LEITURA DE SENSORES</h3>
            </div>
            <div class="metric-box">
                <div class="metric-title">NARIZ (PONTO CRÍTICO - TERMOCOPAR S)</div>
                <div class="metric-value status-ok" id="stat-nose-temp">24.5 °C</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">FLUXO DE CALOR (SCHMIDT-BOELTER)</div>
                <div class="metric-value status-ok" id="stat-heat-flux">0.0 kW/cm²</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">PRESSÃO DINÂMICA / ATRITO</div>
                <div class="metric-value status-ok" id="stat-pressure">1.0 atm (Nominal)</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">NÚCLEO INTERNO (ISOLAMENTO)</div>
                <div class="metric-value status-ok" id="stat-core-temp">22.0 °C (Seguro)</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">TRANSMISSÃO TELEMETRIA (BANDA S/Ka)</div>
                <div class="metric-value status-ok" id="stat-telemetry">ESTÁVEL [100% PACOTES]</div>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');

        let testActive = false;
        let noseTemp = 24.5;
        let coreTemp = 22.0;
        let heatFlux = 0.0;
        let pressureVal = 1.0;
        let plasmaParticles = [];
        let showSensorsOverlay = true;

        function resizeCanvas() {
            canvas.width = canvas.parentElement.clientWidth;
            canvas.height = canvas.parentElement.clientHeight - 30;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        function logSMTA(message) {
            let logDiv = document.getElementById('smta-log-text');
            let timeStr = new Date().toTimeString().split(' ')[0];
            logDiv.innerHTML += `<br>[${timeStr}] ${message}`;
            logDiv.scrollTop = logDiv.scrollHeight;
        }

        function startHypersonicTest() {
            testActive = true;
            noseTemp = 2120.0;
            coreTemp = 39.4;
            heatFlux = 45.8;
            pressureVal = 12.4;

            document.getElementById('test-mode').innerText = 'STATUS: TESTE HIPERSÔNICO ATIVO (MACH 8)';
            document.getElementById('test-mode').style.color = 'var(--accent-orange)';
            document.getElementById('stat-nose-temp').innerText = '2120.0 °C';
            document.getElementById('stat-nose-temp').className = 'metric-value status-heat';
            document.getElementById('stat-heat-flux').innerText = '45.8 kW/cm²';
            document.getElementById('stat-heat-flux').className = 'metric-value status-heat';
            document.getElementById('stat-pressure').innerText = '12.4 atm (Alto Estresse)';
            document.getElementById('stat-pressure').className = 'metric-value status-alert';
            document.getElementById('stat-core-temp').innerText = '39.4 °C (Nominal)';
            document.getElementById('stat-core-temp').className = 'metric-value status-ok';

            logSMTA("🔥 Ignição em túnel Arc Jet bem-sucedida. Fluxo hipersônico Mach 8 atingiu o cone ogival.");
            logSMTA(">>> RELATÓRIO DO TERMOCOPAR S: Nariz registrou 2.120°C. Casca C/SiC e MoS₂ mitigaram atrito.");
            logSMTA(">>> BARREIRA TÉRMICA: Aerogel de sílica isolou com sucesso, mantendo o núcleo interno a 39.4°C.");
        }

        function toggleSensorsView() {
            showSensorsOverlay = !showSensorsOverlay;
            logSMTA(`⚙️ Visualização de sensores e camadas alternada: ${showSensorsOverlay ? 'Ligada' : 'Simplificada'}`);
        }

        function resetSystem() {
            testActive = false;
            noseTemp = 24.5;
            coreTemp = 22.0;
            heatFlux = 0.0;
            pressureVal = 1.0;
            plasmaParticles = [];

            document.getElementById('test-mode').innerText = 'STATUS: PRONTO PARA TESTE';
            document.getElementById('test-mode').style.color = 'var(--text-main)';
            document.getElementById('stat-nose-temp').innerText = '24.5 °C';
            document.getElementById('stat-nose-temp').className = 'metric-value status-ok';
            document.getElementById('stat-heat-flux').innerText = '0.0 kW/cm²';
            document.getElementById('stat-heat-flux').className = 'metric-value status-ok';
            document.getElementById('stat-pressure').innerText = '1.0 atm (Nominal)';
            document.getElementById('stat-pressure').className = 'metric-value status-ok';
            document.getElementById('stat-core-temp').innerText = '22.0 °C (Seguro)';
            document.getElementById('stat-core-temp').className = 'metric-value status-ok';

            logSMTA("🔄 Protótipo SMTA reinicializado para condições nominais de laboratório.");
        }

        // Loop de Renderização Canvas 2D
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Grid de fundo tático
            ctx.strokeStyle = 'rgba(56, 189, 248, 0.04)';
            ctx.lineWidth = 1;
            let gridSize = 40;
            for (let x = 0; x < canvas.width; x += gridSize) {
                ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, canvas.height); ctx.stroke();
            }
            for (let y = 0; y < canvas.height; y += gridSize) {
                ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(canvas.width, y); ctx.stroke();
            }

            let cx = canvas.width / 2 - 50;
            let cy = canvas.height / 2;

            // Gerar partículas de plasma se o teste estiver ativo
            if (testActive && Math.random() < 0.7) {
                plasmaParticles.push({
                    x: cx - 180,
                    y: cy + (Math.random() - 0.5) * 120,
                    vx: 14 + Math.random() * 8,
                    vy: (Math.random() - 0.5) * 4,
                    size: 2 + Math.random() * 4
                });
            }

            // Atualizar e desenhar plasma lateral
            for (let i = plasmaParticles.length - 1; i >= 0; i--) {
                let p = plasmaParticles[i];
                p.x += p.vx;
                p.y += p.vy;

                ctx.fillStyle = '#f97316';
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                ctx.fill();

                if (p.x > cx + 50) {
                    plasmaParticles.splice(i, 1);
                }
            }

            // Desenhar Cone Ogival (Corte Transversal)
            // Dimensões proporcionais: Comprimento 600mm, Base 350mm, Raio ponta 25mm
            let coneLength = 360; // escala visual
            let coneBaseHeight = 200;

            let tipX = cx - 140;
            let tipY = cy;
            let baseX = tipX + coneLength;
            let baseTopY = cy - coneBaseHeight / 2;
            let baseBotY = cy + coneBaseHeight / 2;

            // Camada Externa (C/SiC)
            ctx.fillStyle = testActive ? '#ef4444' : '#1e293b';
            ctx.strokeStyle = '#38bdf8';
            ctx.lineWidth = 2;

            ctx.beginPath();
            ctx.moveTo(tipX, tipY);
            // Curvatura ogival do nariz (raio 25mm)
            ctx.quadraticCurveTo(tipX + 80, tipY - 40, baseX, baseTopY);
            ctx.lineTo(baseX, baseBotY);
            ctx.quadraticCurveTo(tipX + 80, tipY + 40, tipX, tipY);
            ctx.closePath();
            ctx.fill();
            ctx.stroke();

            // Camada de Isolamento Térmico (Aerogel de Sílica)
            ctx.fillStyle = '#0f172a';
            ctx.beginPath();
            let offset = 22;
            let innerTipX = tipX + 35;
            ctx.moveTo(innerTipX, tipY);
            ctx.lineTo(baseX - 10, baseTopY + offset);
            ctx.lineTo(baseX - 10, baseBotY - offset);
            ctx.closePath();
            ctx.fill();
            ctx.strokeStyle = '#06b6d4';
            ctx.stroke();

            // Núcleo Ativo / Chassi Interno (Ti-6Al-4V) e FPGA
            ctx.fillStyle = '#020617';
            ctx.fillRect(baseX - 120, cy - 35, 90, 70);
            ctx.strokeStyle = '#22c55e';
            ctx.strokeRect(baseX - 120, cy - 35, 90, 70);

            ctx.fillStyle = '#22c55e';
            ctx.font = '10px Courier New';
            ctx.fillText('FPGA / NÚCLEO', baseX - 115, cy - 15);
            ctx.fillText('ISOLADO', baseX - 100, cy + 3);

            // Rótulos e Indicadores de Sensores (se ativado)
            if (showSensorsOverlay) {
                ctx.fillStyle = '#f97316';
                // Termopar Nariz
                ctx.beginPath(); ctx.arc(tipX + 15, tipY, 4, 0, Math.PI*2); ctx.fill();
                ctx.fillText('Termopar S (Nariz)', tipX - 40, tipY - 25);

                // Sensores de Fluxo
                ctx.fillStyle = '#38bdf8';
                ctx.beginPath(); ctx.arc(tipX + 120, tipY - 45, 4, 0, Math.PI*2); ctx.fill();
                ctx.fillText('Schmidt-Boelter', tipX + 80, tipY - 60);

                // Sensores de Pressão
                ctx.beginPath(); ctx.arc(tipX + 220, tipY - 70, 4, 0, Math.PI*2); ctx.fill();
                ctx.fillText('Piezoelétrico', tipX + 190, tipY - 85);
            }

            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
