<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>THE M.O.E. GROUP - Downline Forge Tracker</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --gold: #D4AF37;
            --marble-white: #F4F5F7;
            --dark-slate: #1C2321;
            --warm-light: #FDFBF7;
            --border-color: rgba(212, 175, 55, 0.3);
            --neon-green: #39FF14;
        }

        body {
            font-family: 'Courier New', Courier, monospace;
            background-color: var(--dark-slate);
            color: var(--warm-light);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            width: 100%;
            max-width: 950px;
            background: linear-gradient(145deg, #151a19, #222b29);
            border: 2px solid var(--gold);
            box-shadow: 0 0 20px rgba(214, 175, 55, 0.15);
            padding: 25px;
            border-radius: 4px;
        }

        .header {
            text-align: center;
            border-bottom: 2px dashed var(--gold);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }

        .header h1 {
            margin: 0;
            font-size: 24px;
            letter-spacing: 4px;
            color: var(--gold);
            text-shadow: 0 0 10px rgba(214, 175, 55, 0.3);
        }

        .header p {
            margin: 5px 0 0 0;
            font-size: 14px;
            opacity: 0.8;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
            background-color: rgba(0, 0, 0, 0.2);
        }

        th, td {
            border: 1px solid var(--border-color);
            padding: 12px;
            text-align: center;
            font-size: 13px;
        }

        th {
            background-color: rgba(212, 175, 55, 0.1);
            color: var(--gold);
            font-weight: bold;
            letter-spacing: 1px;
        }

        tr:hover {
            background-color: rgba(212, 175, 55, 0.05);
        }

        .editable {
            background-color: rgba(255, 255, 255, 0.05);
            border: 1px dashed transparent;
            border-radius: 3px;
            padding: 6px;
            color: var(--warm-light);
            font-weight: bold;
            text-align: center;
            width: 80%;
            margin: 0 auto;
            transition: all 0.3s;
        }

        .editable:focus {
            outline: none;
            border-color: var(--gold);
            background-color: rgba(0, 0, 0, 0.5);
            box-shadow: 0 0 8px rgba(214, 175, 55, 0.4);
        }

        select.editable-select {
            background-color: #222b29;
            border: 1px solid var(--border-color);
            cursor: pointer;
            width: 90%;
        }

        .status-badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 3px;
            font-size: 11px;
            text-transform: uppercase;
            font-weight: bold;
            letter-spacing: 1px;
        }

        .status-srank {
            background-color: rgba(57, 255, 20, 0.2);
            color: var(--neon-green);
            border: 1px solid var(--neon-green);
            text-shadow: 0 0 5px rgba(57, 255, 20, 0.5);
        }

        .status-standard {
            background-color: rgba(214, 175, 55, 0.2);
            color: var(--gold);
            border: 1px solid var(--gold);
        }

        .status-warn {
            background-color: rgba(255, 57, 57, 0.2);
            color: #ff3939;
            border: 1px solid #ff3939;
        }

        .progress-bar-container {
            width: 100%;
            background-color: rgba(255, 255, 255, 0.1);
            height: 8px;
            border-radius: 4px;
            margin-top: 6px;
            overflow: hidden;
            border: 1px solid rgba(255,255,255,0.05);
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--gold), var(--neon-green));
            width: 0%;
            transition: width 0.5s ease-in-out;
        }

        .totals-row {
            background-color: rgba(212, 175, 55, 0.15) !important;
            font-weight: bold;
        }

        .totals-row td {
            color: var(--gold);
            border-top: 2px double var(--gold);
        }

        .controls {
            margin-top: 20px;
            display: flex;
            justify-content: space-between;
        }

        button {
            background-color: transparent;
            color: var(--gold);
            border: 1px solid var(--gold);
            padding: 10px 20px;
            font-family: 'Courier New', Courier, monospace;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s;
            border-radius: 3px;
        }

        button:hover {
            background-color: var(--gold);
            color: var(--dark-slate);
            box-shadow: 0 0 12px rgba(214, 175, 55, 0.4);
        }

        .hint {
            font-size: 11px;
            color: #888;
            margin-top: 15px;
            text-align: center;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <h1>THE M.O.E. GROUP</h1>
        <p>ORGANIZATIONAL SYSTEM TRACKER // DOWNLINE FORGE</p>
    </div>

    <table id="forgeTable">
        <thead>
            <tr>
                <th>Partner Name</th>
                <th>Current Tier</th>
                <th>May PPV (VP)</th>
                <th>June Goal (VP)</th>
                <th>Supervisor Gap (VP)</th>
                <th>Velocity Status / Progress</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><input type="text" class="editable" value="Partner A"></td>
                <td>
                    <select class="editable editable-select" onchange="calculateForge()">
                        <option value="25">25% (Distributor)</option>
                        <option value="35" selected>35% (Senior Consultant)</option>
                        <option value="42">42% (Success Builder/QP)</option>
                        <option value="50">50% (Supervisor)</option>
                    </select>
                </td>
                <td><input type="number" class="editable vp-input may-ppv" value="500" oninput="calculateForge()"></td>
                <td><input type="number" class="editable vp-input june-goal" value="1500" oninput="calculateForge()"></td>
                <td class="gap-display">3500</td>
                <td>
                    <span class="status-badge status-standard">Consolidated Steady</span>
                    <div class="progress-bar-container"><div class="progress-bar"></div></div>
                </td>
            </tr>
            <tr>
                <td><input type="text" class="editable" value="Partner B"></td>
                <td>
                    <select class="editable editable-select" onchange="calculateForge()">
                        <option value="25">25% (Distributor)</option>
                        <option value="35">35% (Senior Consultant)</option>
                        <option value="42" selected>42% (Success Builder/QP)</option>
                        <option value="50">50% (Supervisor)</option>
                    </select>
                </td>
                <td><input type="number" class="editable vp-input may-ppv" value="1000" oninput="calculateForge()"></td>
                <td><input type="number" class="editable vp-input june-goal" value="1500" oninput="calculateForge()"></td>
                <td class="gap-display">3000</td>
                <td>
                    <span class="status-badge status-srank">High-Velocity Ramp</span>
                    <div class="progress-bar-container"><div class="progress-bar"></div></div>
                </td>
            </tr>
            <tr>
                <td><input type="text" class="editable" value="Partner C"></td>
                <td>
                    <select class="editable editable-select" onchange="calculateForge()">
                        <option value="25">25% (Distributor)</option>
                        <option value="35">35% (Senior Consultant)</option>
                        <option value="42" selected>42% (Success Builder/QP)</option>
                        <option value="50">50% (Supervisor)</option>
                    </select>
                </td>
                <td><input type="number" class="editable vp-input may-ppv" value="1000" oninput="calculateForge()"></td>
                <td><input type="number" class="editable vp-input june-goal" value="1500" oninput="calculateForge()"></td>
                <td class="gap-display">3000</td>
                <td>
                    <span class="status-badge status-srank">High-Velocity Ramp</span>
                    <div class="progress-bar-container"><div class="progress-bar"></div></div>
                </td>
            </tr>
            <tr class="totals-row">
                <td>TOTALS</td>
                <td>-</td>
                <td id="totalMay">2,500</td>
                <td id="totalJune">4,500</td>
                <td id="totalGap">9,500</td>
                <td><span class="status-badge status-standard" id="overallStatus" style="border-color: var(--gold); color: var(--gold)">ACTIVE ROADMAP</span></td>
            </tr>
        </tbody>
    </table>

    <div class="controls">
        <button onclick="addNewRow()">+ Add New Node</button>
        <button onclick="triggerConfetti()">Simulate Success</button>
    </div>
    
    <div class="hint">* Click any dark input block or dropdown arrow to update values in real time. Dynamic progress engines recalculate instantly.</div>
</div>

<script>
    function calculateForge() {
        const rows = document.querySelectorAll("#forgeTable tbody tr:not(.totals-row)");
        let totalMay = 0;
        let totalJune = 0;
        let totalGap = 0;
        let milestoneReached = false;

        rows.forEach(row => {
            const mayPPV = parseFloat(row.querySelector(".may-ppv").value) || 0;
            const juneGoal = parseFloat(row.querySelector(".june-goal").value) || 0;
            const tierSelect = row.querySelector(".editable-select");
            const currentTier = parseInt(tierSelect.value);
            
            // Auto-Calculations
            const supervisorGap = Math.max(0, 4000 - mayPPV);
            row.querySelector(".gap-display").textContent = supervisorGap;

            totalMay += mayPPV;
            totalJune += juneGoal;
            totalGap += supervisorGap;

            // Gamified Status & Progress Calculation
            const progressPercent = Math.min(100, (mayPPV / 4000) * 100);
            const progressBar = row.querySelector(".progress-bar");
            progressBar.style.width = progressPercent + "%";

            const statusBadge = row.querySelector(".status-badge");
            
            if (currentTier === 50 || mayPPV >= 4000) {
                statusBadge.textContent = "SUPERVISOR LOCK";
                statusBadge.className = "status-badge status-srank";
                statusBadge.style.borderColor = "var(--neon-green)";
                tierSelect.value = "50";
                row.querySelector(".gap-display").textContent = "0";
            } else if (mayPPV >= 1000) {
                statusBadge.textContent = "S-RANK VELOCITY";
                statusBadge.className = "status-badge status-srank";
            } else if (mayPPV >= 500) {
                statusBadge.textContent = "STANDARD TRACKING";
                statusBadge.className = "status-badge status-standard";
            } else {
                statusBadge.textContent = "REQ INTERVENTION";
                statusBadge.className = "status-badge status-warn";
            }
        });

        // Update Table Footer Values
        document.getElementById("totalMay").textContent = totalMay.toLocaleString();
        document.getElementById("totalJune").textContent = totalJune.toLocaleString();
        document.getElementById("totalGap").textContent = totalGap.toLocaleString();
    }

    function addNewRow() {
        const tableBody = document.querySelector("#forgeTable tbody");
        const totalsRow = document.querySelector(".totals-row");
        const newRow = document.createElement("tr");

        newRow.innerHTML = `
            <td><input type="text" class="editable" value="New Node"></td>
            <td>
                <select class="editable editable-select" onchange="calculateForge()">
                    <option value="25" selected>25% (Distributor)</option>
                    <option value="35">35% (Senior Consultant)</option>
                    <option value="42">42% (Success Builder/QP)</option>
                    <option value="50">50% (Supervisor)</option>
                </select>
            </td>
            <td><input type="number" class="editable vp-input may-ppv" value="0" oninput="calculateForge()"></td>
            <td><input type="number" class="editable vp-input june-goal" value="1000" oninput="calculateForge()"></td>
            <td class="gap-display">4000</td>
            <td>
                <span class="status-badge status-warn">REQ INTERVENTION</span>
                <div class="progress-bar-container"><div class="progress-bar"></div></div>
            </td>
        `;

        tableBody.insertBefore(newRow, totalsRow);
        calculateForge();
    }

    function triggerConfetti() {
        confetti({
            particleCount: 150,
            spread: 80,
            origin: { y: 0.6 },
            colors: ['#D4AF37', '#39FF14', '#ffffff']
        });
    }

    // Run calculations on initial load
    window.onload = calculateForge;
</script>

</body>
</html>
