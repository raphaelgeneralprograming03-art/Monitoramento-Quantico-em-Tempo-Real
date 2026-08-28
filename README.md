<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monitoramento Quântico: Teatro de Guerra da Ucrânia</title>
    <style>
        body {
            margin: 0;
            padding: 20px;
            font-family: sans-serif;
            background-color: #0f172a;
            color: #f8fafc;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            margin-bottom: 5px;
            font-size: 24px;
            text-align: center;
        }

        p.subtitle {
            color: #94a3b8;
            margin-top: 0;
            margin-bottom: 20px;
            font-size: 14px;
        }

        .container {
            display: flex;
            gap: 20px;
            max-width: 1100px;
            width: 100%;
            flex-wrap: wrap;
            justify-content: center;
        }

        /* PAINEL LARANJA EXIGIDO */
        .panel {
            background-color: #ea580c;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            width: 450px;
            box-sizing: border-box;
        }

        .panel-title {
            font-size: 14px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            margin-bottom: 15px;
            color: #ffffff;
            border-bottom: 1px solid #ff7a33;
            padding-bottom: 5px;
        }

        .display-box {
            background-color: #020617;
            border-radius: 8px;
            height: 350px;
            position: relative;
            overflow: hidden;
            border: 1px solid #334155;
        }

        /* COMPARTIMENTO DE GRADE DO MAPA DE SETORES */
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
            margin-top: 15px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            width: 100%;
        }

        .btn-group {
            display: flex;
            gap: 10px;
        }

        /* BOTÕES PRETO E VERDE EXIGIDOS */
        button {
            background-color: #000000;
            color: #10b981;
            border: 2px solid #10b981;
            padding: 12px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            font-size: 12px;
            text-transform: uppercase;
            transition: all 0.2s;
            flex: 1;
        }

        button:hover {
            background-color: #10b981;
            color: #000000;
        }

        .slider-group {
            display: flex;
            flex-direction: column;
            gap: 5px;
            font-size: 12px;
            color: #ffffff;
            font-weight: bold;
        }

        .slider-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 10px;
        }

        input[type="range"] {
            flex: 1;
            accent-color: #000000;
        }

        .stats {
            margin-top: 10px;
            font-size: 13px;
            color: #ffffff;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
        }

        /* CARDS DO FRONT E SÍTIO DE COMBATE */
        .front-sector {
            width: 110px;
            height: 65px;
            background-color: #1e293b;
            border: 1px solid #475569;
            border-radius: 6px;
            transition: all 0.2s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            font-weight: bold;
            color: #94a3b8;
            text-align: center;
            padding: 5px;
            box-sizing: border-box;
        }

        /* ASSINATURA DETECTADA (CONVENCIONAL VS SUBTERRÂNEA QUÂNTICA) */
        .scanned-active {
            background-color: #ffd700 !important;
            border-color: #fbbf24 !important;
            color: #000000 !important;
            box-shadow: 0 0 15px #ffd700;
        }

        .quantum-found {
            background-color: #ef4444 !important;
            border-color: #f87171 !important;
            color: #ffffff !important;
            box-shadow: 0 0 20px #ef4444;
            transform: scale(1.05);
        }

        /* ELEMENTOS GRÁFICOS DO PAINEL DE SINAL */
        .chart-zone-top {
            position: absolute;
            left: 50px;
            top: 30px;
            width: 330px;
            height: 130px;
            background-color: rgba(251, 191, 36, 0.08);
            border-left: 2px solid #64748b;
        }

        .chart-zone-bottom {
            position: absolute;
            left: 50px;
            top: 162px;
            width: 330px;
            height: 130px;
            background-color: rgba(239, 68, 68, 0.12);
            border-left: 2px solid #64748b;
            border-bottom: 2px solid #64748b;
        }

        .chart-line {
            position: absolute;
            left: 50px;
            top: 160px;
            width: 330px;
            height: 2px;
            background-color: #475569;
        }

        .chart-label {
            position: absolute;
            font-size: 11px;
            font-weight: bold;
        }

        .dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            position: absolute;
            border: 1px solid #ffffff;
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
                <!-- Setores reais da Ucrânia injetados aqui -->
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
                        <span id="sens-val">120 mGal</span>
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
                <div class="chart-label" style="left: 160px; top: 250px; color: #f87171;">Bunkers / Emissores EW Ocultos</div>
                <div class="chart-label" style="left: 150px; top: 310px; color: #64748b;">Assinatura Gravitacional &rarr;</div>
            </div>
            <div class="stats">
                <span>Alvos Superficiais: <strong id="count-normal" style="color:#000000">0</strong></span>
                <span>Anomalias Subterrâneas: <strong id="count-quantum" style="color:#ffffff">0</strong></span>
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

        // Setores críticos reais mapeados no conflito
        const sectors = [
            "Zaporizhzhia", "Donetsk", "Bakhmut", 
            "Kherson", "Avdiivka", "Kupiansk", 
            "Luhansk", "Kharkiv", "Sumy"
        ];

        sectors.forEach(name => {
            let sectorBox = document.createElement('div');
            sectorBox.className = 'front-sector';
            sectorBox.innerHTML = `<span>${name}</span>`;
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

            if (mode === 'normal') {
