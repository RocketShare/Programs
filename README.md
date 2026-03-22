<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real Estate Showing Calculator</title>
    <style>
        /* CSS Reset and Variables */
        :root {
            --primary: #1A365D;
            --primary-light: #2c5282;
            --secondary: #D69E2E;
            --secondary-hover: #b7791f;
            --bg: #f7fafc;
            --surface: #ffffff;
            --text: #2d3748;
            --text-light: #718096;
            --border: #e2e8f0;
            --danger: #e53e3e;
            --danger-hover: #c53030;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            padding: 10px;
            line-height: 1.6;
            -webkit-tap-highlight-color: transparent;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: var(--surface);
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        header {
            text-align: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--border);
        }

        header h1 {
            color: var(--primary);
            font-size: 1.8rem;
            margin-bottom: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        header p {
            color: var(--text-light);
            font-size: 1rem;
        }

        .settings-panel {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            background: #edf2f7;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 25px;
            border-left: 5px solid var(--secondary);
        }

        .form-group {
            display: flex;
            flex-direction: column;
            flex: 1;
            min-width: 200px;
        }

        .form-group label {
            font-weight: 600;
            margin-bottom: 5px;
            color: var(--primary);
            font-size: 0.9rem;
        }

        .form-group input {
            padding: 12px;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 1rem;
            background: white;
            width: 100%;
        }

        .showings-container {
            margin-bottom: 20px;
            width: 100%;
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 600px;
        }

        th {
            background-color: var(--primary);
            color: white;
            padding: 12px;
            text-align: center;
            font-size: 0.9rem;
        }

        td {
            padding: 12px;
            border-bottom: 1px solid var(--border);
        }

        /* Center columns that contain labels or simple displays */
        td:first-child, 
        td:nth-child(4), 
        td:nth-child(5), 
        td:nth-child(7), 
        td:last-child {
            text-align: center;
        }

        input[type="text"], input[type="number"] {
            width: 100%;
            padding: 10px;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 1rem;
        }

        .time-display {
            font-weight: 600;
            color: var(--primary);
            background: #edf2f7;
            padding: 6px 10px;
            border-radius: 4px;
            display: inline-block;
            min-width: 85px;
            text-align: center;
            font-size: 0.95rem;
        }

        .st-window {
            color: #ffffff;
            background: var(--secondary);
            font-weight: 600;
            padding: 6px 10px;
            border-radius: 4px;
            display: inline-block;
            min-width: 85px;
            text-align: center;
            font-size: 0.95rem;
        }

        .actions {
            margin-top: 20px;
        }

        .btn {
            border: none;
            padding: 16px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 700;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            width: 100%;
            justify-content: center;
            transition: opacity 0.2s;
        }

        .btn:active {
            opacity: 0.7;
        }

        .btn-add {
            background: var(--primary);
            color: white;
        }

        .btn-remove {
            background: #fff5f5;
            color: var(--danger);
            border: 1px solid var(--danger);
            padding: 10px 15px;
            font-size: 0.85rem;
            width: auto;
        }

        .instructions {
            margin-top: 30px;
            padding: 25px;
            background: #ffffff;
            border: 1px solid var(--border);
            border-radius: 8px;
            font-size: 0.95rem;
            color: #4a5568;
        }

        .instructions h2 {
            font-size: 1.1rem;
            color: var(--primary);
            margin-bottom: 12px;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            border-bottom: 2px solid var(--secondary);
            display: inline-block;
            padding-bottom: 4px;
        }

        .instructions p, .instructions li {
            margin-bottom: 10px;
            line-height: 1.7;
        }

        .instructions ul {
            list-style: none;
            padding-left: 0;
            margin-bottom: 20px;
        }

        .instructions ul li {
            position: relative;
            padding-left: 0;
        }

        .instructions a {
            color: var(--primary);
            font-weight: 700;
            text-decoration: underline;
        }

        /* Mobile Optimization */
        @media (max-width: 860px) {
            .container { padding: 15px; }
            
            table { min-width: 100%; }

            table, thead, tbody, th, td, tr {
                display: block;
            }
            
            thead { display: none; }
            
            tr {
                margin-bottom: 20px;
                border: 2px solid var(--border);
                border-radius: 12px;
                padding: 12px;
                background: white;
            }
            
            td {
                border-bottom: 1px solid #f1f5f9;
                display: flex !important;
                align-items: center;
                justify-content: space-between;
                padding: 10px 0;
                text-align: left !important;
            }

            td:last-child { 
                border-bottom: none; 
                justify-content: center;
                padding-top: 15px;
            }
            
            td:before {
                content: attr(data-label);
                font-weight: 800;
                color: var(--primary);
                font-size: 0.8rem;
                text-transform: uppercase;
                flex: 1;
                text-align: left;
            }

            td > * {
                flex: 1.5;
                text-align: right;
            }

            input[type="text"], input[type="number"] {
                width: 100% !important;
                text-align: left;
            }

            td:first-child > * {
                text-align: center;
            }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>
            <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                <polyline points="9 22 9 12 15 12 15 22"></polyline>
            </svg>
            Showing Calculator
        </h1>
        <p>Build your tour schedule in seconds.</p>
    </header>

    <div class="settings-panel">
        <div class="form-group">
            <label for="globalStartTime">First Showing Start Time</label>
            <input type="time" id="globalStartTime" value="10:00">
        </div>
        <div class="form-group">
            <label for="globalDuration">Default Duration (mins)</label>
            <input type="number" id="globalDuration" value="20" min="5" step="5">
        </div>
    </div>

    <div class="showings-container">
        <table id="showingsTable">
            <thead>
                <tr>
                    <th>Stop</th>
                    <th>Address / Notes</th>
                    <th>Show Mins</th>
                    <th>Start</th>
                    <th>End</th>
                    <th>Drive Time</th>
                    <th>Schedule Time</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody id="showingsBody"></tbody>
        </table>
    </div>

    <div class="actions">
        <button id="addBtn" type="button" class="btn btn-add">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <line x1="12" y1="5" x2="12" y2="19"></line>
                <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
            Add Next Stop
        </button>
    </div>

    <div class="instructions">
        <h2>OBJECTIVE</h2>
        <p>To help real estate agents significantly reduce the time needed to schedule a seamless showing tour. Why? Because the showing scheduler shows only the drive time between showings but does take into account the 20 or so minutes for each showing. And then, add the drive time, so agents know what time is best to schedule the next showing to keep your showings tight together and not waste time or arrive too early or late. I created and have used a spreadsheet to do this for 6 years. Now, with Google Gemini AI as my personal programmer, I asked it to convert the spreadheet into a showing calculator in plain english. In my opinion, the showing calculator is a feature that should just be a part of the actual showing scheduler.</p>

        <h2>INSTRUCTIONS</h2>
        <ul>
            <li><strong>1.</strong> From MLS, add all addresses to a showing cart but do not schedule any showing times.</li>
            <li><strong>2.</strong> Use smart route to put the route in the most efficient route.</li>
            <li><strong>3.</strong> Finalize route if needed!</li>
            <li><strong>4.</strong> Open a browser and go to Showing Calculator.html to <a href="http://ShowingCalc.EverythingRealEstate.US" target="_blank">ShowingCalc.EverythingRealEstate.US</a></li>
            <li><strong>5. First Home Start Time:</strong> Enter the time for the first showing.</li>
            <li><strong>6. Default Showing Length:</strong> The default is 20 minutes which works great for me. You can set it to 30 min. and all properties in the list will default to 30 min.</li>
            <li><strong>7. Property Address / Notes:</strong> Optional, You can enter a street name or note to help you keep track of which showings you have scheduled.</li>
            <li><strong>8. Show Time (Mins):</strong> Allows you to adjust the length of the time for each showing individually.</li>
            <li><strong>9. Start Time:</strong> This column is calculated automatically based on the First Home Start Time you set above.</li>
            <li><strong>10. End Time:</strong> This column is calculated automatically based on the First Home Start Time you set above.</li>
            <li><strong>11. Drive Time:</strong> In the showing scheduling cart, find the driving time (between each address) and enter the estimated drive time into this column in the Showing Calculator.</li>
            <li><strong>12. Schedule Time:</strong> This column shows the Start Time to schedule each of the other showings. This is the objective of the showing calculator. The time is rounded down to the nearest quarter hour to match the showing schedule in the showing app.</li>
        </ul>

        <h2>TIPS</h2>
        <p>Schedule the duration of the showing for 1 hour to give you time in case there are any delays such as a bathroom or food break.</p>
        
        <p><a href="https://www.youtube.com/results?search_query=split+screen+windows+11" target="_blank">CLICK HERE</a> to see a YouTube video on How to use a Split Screen on Windows 11 with Examples. It Helps!</p>
    </div>
</div>

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const body = document.getElementById('showingsBody');
        const globalStart = document.getElementById('globalStartTime');
        const globalDur = document.getElementById('globalDuration');
        const addBtn = document.getElementById('addBtn');
        let rowCount = 0;

        if (!body || !globalStart || !addBtn) return;

        function formatTime(date) {
            try {
                let h = date.getHours();
                let m = date.getMinutes();
                let ampm = h >= 12 ? 'PM' : 'AM';
                h = h % 12;
                h = h ? h : 12;
                m = m < 10 ? '0' + m : m;
                return h + ':' + m + ' ' + ampm;
            } catch (e) {
                return "--:--";
            }
        }

        function calculateTimes() {
            const startTimeStr = globalStart.value;
            const defaultDuration = parseInt(globalDur.value) || 20;

            if (!startTimeStr) return;

            const parts = startTimeStr.split(':');
            if (parts.length < 2) return;

            const hours = parseInt(parts[0]);
            const minutes = parseInt(parts[1]);
            
            const currentTime = new Date();
            currentTime.setHours(hours, minutes, 0, 0);

            const rows = body.querySelectorAll('tr');

            rows.forEach((row, index) => {
                const stopLabel = row.querySelector('.stop-num');
                if (stopLabel) stopLabel.textContent = index + 1;

                let durationInput = row.querySelector('.showing-duration');
                let duration = (durationInput && durationInput.value !== "") ? parseInt(durationInput.value) : defaultDuration;

                // Start Time
                const startTimeEl = row.querySelector('.start-time');
                if (startTimeEl) startTimeEl.textContent = formatTime(currentTime);

                // Window Calculation (15m floor)
                const windowEl = row.querySelector('.st-window');
                if (windowEl) {
                    const stTime = new Date(currentTime);
                    const nearest15 = Math.floor(stTime.getMinutes() / 15) * 15;
                    stTime.setMinutes(nearest15);
                    windowEl.textContent = formatTime(stTime);
                }

                // End Time
                currentTime.setMinutes(currentTime.getMinutes() + duration);
                const endTimeEl = row.querySelector('.end-time');
                if (endTimeEl) endTimeEl.textContent = formatTime(currentTime);

                // Add Drive Time for NEXT row
                const driveInput = row.querySelector('.drive-time');
                const driveTime = (driveInput) ? (parseInt(driveInput.value) || 0) : 0;
                currentTime.setMinutes(currentTime.getMinutes() + driveTime);
            });
        }

        function addRow(address = '', customDuration = '', driveTime = 15) {
            rowCount++;
            const tr = document.createElement('tr');

            tr.innerHTML = `
                <td data-label="Stop #"><span class="stop-num">${rowCount}</span></td>
                <td data-label="Address"><input type="text" placeholder="Address/Note" value="${address}"></td>
                <td data-label="Show Mins"><input class="showing-duration" type="number" placeholder="Default" value="${customDuration}"></td>
                <td data-label="Start"><span class="start-time time-display">--:--</span></td>
                <td data-label="End"><span class="end-time time-display">--:--</span></td>
                <td data-label="Drive Time"><input class="drive-time" type="number" value="${driveTime}" min="0"></td>
                <td data-label="Schedule Time"><span class="st-window">--:--</span></td>
                <td data-label="Action"><button type="button" class="btn btn-remove">Remove</button></td>
            `;

            body.appendChild(tr);

            // Add events to new inputs
            tr.querySelectorAll('input').forEach(input => {
                input.addEventListener('input', calculateTimes);
            });
            tr.querySelector('.btn-remove').addEventListener('click', function() {
                tr.remove();
                calculateTimes();
            });

            calculateTimes();
        }

        // Global Listeners
        globalStart.addEventListener('change', calculateTimes);
        globalDur.addEventListener('input', calculateTimes);
        addBtn.addEventListener('click', function(e) {
            e.preventDefault();
            addRow();
        });

        // Initial rows
        addRow('', '', 15);
        addRow('', '', 10);
        addRow('', '', 10);
        calculateTimes();
    });
</script>

</body>
</html>
