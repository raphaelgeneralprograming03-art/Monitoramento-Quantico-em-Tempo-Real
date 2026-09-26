
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monitoramento Quântico: Teatro de Guerra da Ucrânia</title>
    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            padding: 20px;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #030712;
            color: #f3f4f6;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        h1 {
            margin-bottom: 5px;
            font-size: 25px;
            text-align: center;
            color: #10b981;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 0 0 12px rgba(16, 185, 129, 0.4);
        }

        p.subtitle {
            color: #64748b;
            margin-top: 0;
            margin-bottom: 25px;
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 1px;
            text-align: center;
        }

        .container {
            display: flex;
            gap: 25px;
            max-width: 1100px;
            width: 100%;
            flex-wrap: wrap;
            justify-content: center;
        }

        /* PAINEL TÁTICO MILITAR REFORMULADO */
        .panel {
            background: linear-gradient(145deg, #0f172a, #090d16);
            border-radius: 12px;
            padding: 22px;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.7), 0 0 0 1px rgba(16, 185, 129, 0.25);
            width: 480px;
            box-sizing: border-box;
            position: relative;
        }

        .panel-title {
            font-size: 13px;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            margin-bottom: 15px;
            color: #10b981;
            border-bottom: 1px solid rgba(16, 185, 129, 0.3);
            padding-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .display-box {
            background-color: #020617;
            background-image: 
                radial-gradient(rgba(16, 185, 129, 0.08) 1px, transparent 0),
                linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
            background-size: 20px 20px, 20px 20px, 20px 20px;
            border-radius: 8px;
            height: 350px;
            position: relative;
            overflow: hidden;
            border: 1px solid #1e293b;
            box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.8);
        }

        /* MAPA DE SETORES EM GRADE 3x3 */
        #theaterView {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            padding: 20px;
            align-content: center;
            justify-items: center;
            box-sizing: border-box;
        }

        .controls {
            margin-top: 18px;
            display: flex;
            flex-direction: column;
            gap: 14px;
            width: 100%;
        }

        .btn-group {
            display: flex;
            gap: 12px;
        }

        /* NOVOS BOTÕES EM ESTILO HUD MILITAR */
        button {
            background: linear-gradient(180deg, #1e293b 0%, #0f172a 100%);
            color: #f59e0b;
            border: 1px solid #f59e0b;
            padding: 12px 14px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 700;
            font-size: 11px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            transition: all 0.25s ease;
            flex: 1;
            box-shadow: 0 4px 10px rgba(0,0,0,0.4);
        }

        button:hover {
            background: #f59e0b;
            color: #020617;
            box-shadow: 0 0 18px rgba(245, 158, 11, 0.6);
            transform: translateY(-1px);
        }

        button#quantum-scan {
            color: #ef4444;
            border-color: #ef4444;
        }

        button#quantum-scan:hover {
            background: #ef4444;
            color: #ffffff;
            box-shadow: 0 0 18px rgba(239, 68, 68, 0.6);
        }

        .slider-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
            font-size: 12px;
            color: #94a3b8;
            font-weight: bold;
        }

        .slider-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
        }

        input[type="range"] {
            flex: 1;
            accent-color: #10b981;
            cursor: pointer;
        }

        .stats {
            margin-top: 14px;
            font-size: 13px;
            color: #94a3b8;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            background: rgba(15, 23, 42, 0.6);
            padding: 10px 14px;
            border-radius: 6px;
            border: 1px solid #1e293b;
        }

        /* CARDS DE SETOR DO FRONT */
        .front-sector {
            width: 120px;
            height: 70px;
            background-color: #0f172a;
            border: 1px solid #334155;
            border-radius: 6px;
            transition: all 0.25s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            font-weight: 800;
            color: #64748b;
            text-align: center;
            padding: 6px;
            box-sizing: border-box;
            font-family: monospace;
        }

        /* DETECÇÕES VISUAIS NOS CARDS */
        .scanned-active {
            background-color: #f59e0b !important;
            border-color: #fbbf24 !important;
            color: #020617 !important;
            box-shadow: 0 0 20px #f59e0b;
            transform: scale(1.08);
        }

        .quantum-found {
            background-color: #ef4444 !important;
            border-color: #f87171 !important;
            color: #ffffff !important;
            box-shadow: 0 0 25px #ef4444;
            transform: scale(1.08);
        }

        /* ZONAS DO GRÁFICO DE SINAL */
        .chart-zone-top {
            position: absolute;
            left: 50px;
            top: 30px;
            width: 330px;
            height: 130px;
            background-color: rgba(245, 158, 11, 0.08);
            border-left: 2px solid #334155;
        }

        .chart-zone-bottom {
            position: absolute;
            left: 50px;
            top: 162px;
            width: 330px;
            height: 130px;
            background-color: rgba(239, 68, 68, 0.08);
            border-left: 2px solid #334155;
            border-bottom: 2px solid #334155;
        }

        .chart-line {
            position: absolute;
            left: 50px;
            top: 160px;
            width: 330px;
            height: 2px;
            background-color: #10b981;
            box-shadow: 0 0 8px #10b981;
        }

        .chart-label {
            position: absolute;
            font-size: 11px;
            font-weight: bold;
            font-family: monospace;
        }

        .dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            position: absolute;
            border: 2px solid #ffffff;
            transform: translate(-50%, -50%);
            animation: pop 0.25s ease-out;
        }

        @keyframes pop {
            0% { transform: translate(-50%, -50%) scale(0); }
            100% { transform: translate(-50%, -50%) scale(1); }
        }
    </style>
</head>
<body>

    <h1>Varredura Tática Quântica: Linhas de Frente na Ucrânia</h1>
    <p class="subtitle">Aplicação de Sensores Criogênicos e Gravimétricos de Partículas para Reconhecimento Geofísico</p>

    <div class="container">
        <!-- Painel Esquerdo -->
        <div class="panel">
            <div class="panel-title">🔬 Mapeamento de Setores Estratégicos</div>
            <div id="theaterView" class="display-box">
                <!-- Setores reais da Ucrânia gerados via JavaScript -->
            </div>
            <div class="controls">
                <div class="btn-group">
                    <button id="radar-scan">Radar de Superfície</button>
                    <button id="quantum-scan">Sondagem Gravimétrica</button>
                </div>
                <div class="slider-group">
                    <div class="slider-row">
                        <label>Sensibilidade do Sensor:</label>
                        <input type="range" id="sens-slider" min="10" max="200" value="120">
                        <span id="sens-val" style="color: #10b981;">120 mGal</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Painel Direito -->
        <div class="panel">
            <div class="panel-title">📊 Densidade de Massa / Flutuações de Vácuo</div>
            <div id="chartView" class="display-box">
                <div class="chart-zone-top"></div>
                <div class="chart-zone-bottom"></div>
                <div class="chart-line"></div>
                
                <div class="chart-label" style="left: 170px; top: 40px; color: #fbbf24;">Movimentações de Superfície</div>
                <div class="chart-label" style="left: 150px; top: 250px; color: #f87171;">Bunkers / Emissores EW Ocultos</div>
                <div class="chart-label" style="left: 140px; top: 315px; color: #64748b;">Assinatura Gravitacional &rarr;</div>
            </div>
            <div class="stats">
                <span>Alvos Superficiais: <strong id="count-normal" style="color:#fbbf24">0</strong></span>
                <span>Anomalias Subterrâneas: <strong id="count-quantum" style="color:#f87171">0</strong></span>
            </div>
        </div>
    </div>

    <script>
        const theaterView = document.getElementById('theaterView');
        const chartView = document.getElementById('chartView');
        const sensSlider = document.getElementById('sens-slider');
        const sensVal = document.getElementById('sens-val');

        let counters = { normal: 0, quantum: 0 };
        let currentSens = 120;

        sensSlider.addEventListener('input', function(e) {
            currentSens = parseInt(e.target.value);
            sensVal.innerText = currentSens + " mGal";
        });

        // Setores críticos reais no conflito
        const sectors = [
            "Zaporizhzhia", "Donetsk", "Bakhmut", 
            "Kherson", "Avdiivka", "Kupiansk", 
            "Luhansk", "Kharkiv", "Sumy"
        ];

        sectors.forEach(name => {
            let sectorBox = document.createElement('div');
            sectorBox.className = 'front-sector';
            sectorBox.innerText = name;
            theaterView.appendChild(sectorBox);
        });

        const sectorList = document.querySelectorAll('.front-sector');

        document.getElementById('radar-scan').addEventListener('click', function() {
            triggerScan('normal');
        });

        document.getElementById('quantum-scan').addEventListener('click', function() {
            triggerScan('quantum');
        });

        function triggerScan(mode) {
            let randomIndex = Math.floor(Math.random() * sectorList.length);
            let selectedSector = sectorList[randomIndex];

            let dot = document.createElement('div');
            dot.className = 'dot';

            let posX, posY;

            if (mode === 'normal') {
                // Animação visual no setor detectado
                selectedSector.classList.add('scanned-active');
                setTimeout(() => selectedSector.classList.remove('scanned-active'), 400);

                // Posição no gráfico (Zona Superior - Alvos Superficiais)
                posY = Math.floor(Math.random() * 95) + 45;
                posX = Math.floor(Math.random() * 280) + 70;

                dot.style.backgroundColor = '#fbbf24';
                dot.style.borderColor = '#f59e0b';
                dot.style.boxShadow = '0 0 10px #fbbf24';

                counters.normal++;
                document.getElementById('count-normal').innerText = counters.normal;
            } else if (mode === 'quantum') {
                // Animação visual no setor com anomalia gravimétrica
                selectedSector.classList.add('quantum-found');
                setTimeout(() => selectedSector.classList.remove('quantum-found'), 400);

                // Posição no gráfico (Zona Inferior - Anomalias Subterrâneas)
                posY = Math.floor(Math.random() * 90) + 175;

                // A escala no eixo X varia dinamicamente conforme a sensibilidade (mGal)
                let sensRatio = currentSens / 200;
                let minX = 60 + (sensRatio * 30);
                let rangeX = 160 + (sensRatio * 120);
                posX = Math.floor(Math.random() * rangeX) + minX;
                if (posX > 360) posX = 360;

                dot.style.backgroundColor = '#ef4444';
                dot.style.borderColor = '#f87171';
                dot.style.boxShadow = '0 0 10px #ef4444';

                counters.quantum++;
                document.getElementById('count-quantum').innerText = counters.quantum;
            }

            dot.style.left = posX + 'px';
            dot.style.top = posY + 'px';

            chartView.appendChild(dot);
        }
    </script>
</body>
</html>
