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
            max-width: 730px;
        }
        h2 {
            text-align: center;
            color: #1a252f;
            margin-bottom: 20px;
        }
        .dashboard {
            background: #1a252f;
            color: #fff;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            margin-bottom: 20px;
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
        .equation-box {
            background-color: #f8f9fa;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 25px;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.95rem;
            text-align: center;
            color: #2c3e50;
            box-shadow: inset 0 1px 3px rgba(0,0,0,0.02);
            line-height: 1.6;
        }
        .eq-highlight {
            font-weight: bold;
            color: #1a252f;
            border-bottom: 2px solid #bdc3c7;
            padding: 0 2px;
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
    
    <div class="dashboard">
        <h3>Predicted Motivation Score</h3>
        <div class="score" id="emScore">0%</div>
    </div>

    <div class="equation-box">
        <strong>Live Interactive Regression Model with Error Term:</strong><br>
        EM = 15% + 2.2(<span id="eqEA" class="eq-highlight">5</span>) 
        + 1.8(<span id="eqEB" class="eq-highlight">5</span>) 
        + 2.7(<span id="eqCR" class="eq-highlight">5</span>) 
        + 1.6(<span id="eqJS" class="eq-highlight">5</span>) 
        - 3.0(<span id="eqOC" class="eq-highlight">5</span>) 
        + 3.2(<span id="eqWC" class="eq-highlight">5</span>)
        <span id="eqSign">+</span> <span id="eqError" class="eq-highlight">0.00</span> (ε)
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

        // 2. Map current inputs to individual variable labels
        document.getElementById('valEA').innerText = ea;
        document.getElementById('valEB').innerText = eb;
        document.getElementById('valCR').innerText = cr;
        document.getElementById('valJS').innerText = js;
        document.getElementById('valOC').innerText = oc;
        document.getElementById('valWC').innerText = wc;

        // 3. Update variables inside the Live Equation
        document.getElementById('eqEA').innerText = ea;
        document.getElementById('eqEB').innerText = eb;
        document.getElementById('eqCR').innerText = cr;
        document.getElementById('eqJS').innerText = js;
        document.getElementById('eqOC').innerText = oc;
        document.getElementById('eqWC').innerText = wc;

        // 4. Generate a random error term (ε) between -3.0 and +3.0
        // This simulates natural, unmeasured data fluctuations.
        const errorTerm = (Math.random() * 6) - 3; 
        
        // Update the live equation box to show the exact error term value and correct math sign
        document.getElementById('eqSign').innerText = errorTerm >= 0 ? '+' : '-';
        document.getElementById('eqError').innerText = Math.abs(errorTerm).toFixed(2);

        // 5. Compute the final regression line including the error term
        let em = 15 + (2.2 * ea) + (1.8 * eb) + (2.7 * cr) + (1.6 * js) - (3.0 * oc) + (3.2 * wc) + errorTerm;

        // 6. Force boundary constraints between 0% and 100%
        em = Math.max(0, Math.min(100, em));

        // 7. Render final predicted motivation figure
        document.getElementById('emScore').innerText = em.toFixed(1) + '%';
    }

    // Call on document load
    calculateEM();
</script>

</body>
</html>
