<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Motivation Regression Simulator</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f7fa;
            color: #2c3e50;
            padding: 20px;
            display: flex;
            justify-content: center;
        }
        .container {
            background-color: #fff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.06);
            width: 100%;
            max-width: 700px;
        }
        h2, h4 {
            text-align: center;
            color: #1a252f;
            margin-top: 0;
            margin-bottom: 5px;
        }
        h4 {
            font-weight: 500;
            color: #7f8c8d;
            margin-bottom: 25px;
        }
        .dashboard {
            background: #1a252f;
            color: #fff;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            margin-bottom: 30px;
        }
        .dashboard h3 {
            margin: 0;
            font-size: 1.1rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #bdc3c7;
        }
        .score {
            font-size: 3.5rem;
            font-weight: bold;
            color: #2ecc71;
            margin-top: 5px;
        }
        .slider-group {
            margin-bottom: 22px;
        }
        .slider-label {
            display: flex;
            justify-content: space-between;
            font-weight: 600;
            margin-bottom: 6px;
        }
        input[type=range] {
            -webkit-appearance: none;
            width: 100%;
            height: 12px;
            border-radius: 6px;
            outline: none;
        }
        input[type=range]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 22px;
            height: 22px;
            border-radius: 50%;
            background: #fff;
            border: 3px solid #7f8c8d;
            cursor: pointer;
            box-shadow: 0 2px 4px rgba(0,0,0,0.15);
            margin-top: -5px;
        }
        
        /* Softer, Lighter Distinct Track Colors */
        #EA::-webkit-slider-runnable-track { background: #5dade2; border-radius: 6px; height: 12px; }
        #EB::-webkit-slider-runnable-track { background: #bb8fce; border-radius: 6px; height: 12px; }
        #CR::-webkit-slider-runnable-track { background: #f5b041; border-radius: 6px; height: 12px; }
        #JS::-webkit-slider-runnable-track { background: #76d7c4; border-radius: 6px; height: 12px; }
        #OC::-webkit-slider-runnable-track { background: #f1948a; border-radius: 6px; height: 12px; }
        #WC::-webkit-slider-runnable-track { background: #f7dc6f; border-radius: 6px; height: 12px; }

        /* Firefox Compatibility Fallbacks */
        #EA::-moz-range-track { background: #5dade2; border-radius: 6px; height: 12px; }
        #EB::-moz-range-track { background: #bb8fce; border-radius: 6px; height: 12px; }
        #CR::-moz-range-track { background: #f5b041; border-radius: 6px; height: 12px; }
        #JS::-moz-range-track { background: #76d7c4; border-radius: 6px; height: 12px; }
        #OC::-moz-range-track { background: #f1948a; border-radius: 6px; height: 12px; }
        #WC::-moz-range-track { background: #f7dc6f; border-radius: 6px; height: 12px; }

        .ticks {
            display: flex;
            justify-content: space-between;
            padding: 0 4px;
            font-size: 0.8rem;
            color: #95a5a6;
            margin-top: 4px;
            font-weight: 500;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Employee Motivation (EM) Model</h2>
    <h4>EM = 15% + 2.2(EA) + 1.8(EB) + 2.7(CR) + 1.6(JS) - 3.0(OC) + 3.2(WC) + ε</h4>
    
    <div class="dashboard">
        <h3>Predicted Motivation Score</h3>
        <div class="score" id="emScore">0%</div>
    </div>

    <div class="slider-group">
        <div class="slider-label"><span>Employee Autonomy (EA)</span> <span id="valEA">5</span></div>
        <input type="range" id="EA" min="1" max="10" value="5" oninput="calculateEM()">
        <div class="ticks"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span><span>6</span><span>7</span><span>8</span><span>9</span><span>10</span></div>
    </div>

    <div class="slider-group">
        <div class="slider-label"><span>Employee Belongingness (EB)</span> <span id="valEB">5</span></div>
        <input type="range" id="EB" min="1" max="10" value="5" oninput="calculateEM()">
        <div class="ticks"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span><span>6</span><span>7</span><span>8</span><span>9</span><span>10</span></div>
    </div>

    <div class="slider-group">
        <div class="slider-label"><span>Competitive Remuneration (CR)</span> <span id="valCR">5</span></div>
        <input type="range" id="CR" min="1" max="10" value="5" oninput="calculateEM()">
        <div class="ticks"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span><span>6</span><span>7</span><span>8</span><span>9</span><span>10</span></div>
    </div>

    <div class="slider-group">
        <div class="slider-label"><span>Job Security (JS)</span> <span id="valJS">5</span></div>
        <input type="range" id="JS" min="1" max="10" value="5" oninput="calculateEM()">
        <div class="ticks"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span><span>6</span><span>7</span><span>8</span><span>9</span><span>10</span></div>
    </div>

    <div class="slider-group">
        <div class="slider-label"><span>Organizational Constraints (OC) <small style="color:#c0392b;">(Negative Impact)</small></span> <span id="valOC">5</span></div>
        <input type="range" id="OC" min="1" max="10" value="5" oninput="calculateEM()">
        <div class="ticks"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span><span>6</span><span>7</span><span>8</span><span>9</span><span>10</span></div>
    </div>

    <div class="slider-group">
        <div class="slider-label"><span>Workplace Culture (WC)</span> <span id="valWC">5</span></div>
        <input type="range" id="WC" min="1" max="10" value="5" oninput="calculateEM()">
        <div class="ticks"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span><span>6</span><span>7</span><span>8</span><span>9</span><span>10</span></div>
    </div>
</div>

<script>
    function calculateEM() {
        // 1. Read input values from UI sliders
        const ea = parseInt(document.getElementById('EA').value);
        const eb = parseInt(document.getElementById('EB').value);
        const cr = parseInt(document.getElementById('CR').value);
        const js = parseInt(document.getElementById('JS').value);
        const oc = parseInt(document.getElementById('OC').value);
        const wc = parseInt(document.getElementById('WC').value);

        // 2. Map current inputs to individual variable text metrics
        document.getElementById('valEA').innerText = ea;
        document.getElementById('valEB').innerText = eb;
        document.getElementById('valCR').innerText = cr;
        document.getElementById('valJS').innerText = js;
        document.getElementById('valOC').innerText = oc;
        document.getElementById('valWC').innerText = wc;

        // 3. Generate dynamic random error noise component between -3.0 and +3.0
        const errorTerm = (Math.random() * 6) - 3; 

        // 4. Mathematical engine execution matching specified variables
        let em = 15 + (2.2 * ea) + (1.8 * eb) + (2.7 * cr) + (1.6 * js) - (3.0 * oc) + (3.2 * wc) + errorTerm;

        // 5. Clean boundary constraints to strictly format between 0% and 100%
        em = Math.max(0, Math.min(100, em));

        // 6. Write final computed motivation figure into the dashboard viewport
        document.getElementById('emScore').innerText = em.toFixed(1) + '%';
    }

    // Call on document parse initialization
    calculateEM();
</script>

</body>
</html>
