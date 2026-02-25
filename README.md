!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Uzbekistan Super League – Official System 2026</title>
    <style>
        :root {
            --bg-dark: #0b0d17;
            --bg-panel: #15192b;
            --primary: #00f0ff;
            --secondary: #2d34e6;
            --accent: #ff0055;
            --text-main: #ffffff;
            --text-dim: #8b9bb4;
            --rank-s: #ffd700;
            --rank-a: #bf00ff;
            --rank-b: #00ff66;
            --rank-c: #e0e0e0;
            --border: 1px solid rgba(0, 240, 255, 0.2);
            --font-main: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { 
            background: linear-gradient(135deg, #0b0d17 0%, #15192b 50%, #0f1222 100%); 
            color: var(--text-main); 
            font-family: var(--font-main); 
            overflow-x: hidden; 
            padding-bottom: 50px; 
            min-height: 100vh;
        }
        
        h1, h2, h3 { text-transform: uppercase; letter-spacing: 2px; }
        .neon-text { text-shadow: 0 0 10px var(--primary); color: var(--primary); }
        .hidden { display: none !important; }
        .btn { cursor: pointer; border: none; outline: none; padding: 10px 20px; font-weight: bold; text-transform: uppercase; transition: 0.3s; clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px); }
        .btn-primary { background: var(--primary); color: #000; }
        .btn-primary:hover { background: #fff; box-shadow: 0 0 15px var(--primary); }
        .btn-danger { background: var(--accent); color: #fff; }
        .btn-warning { background: var(--rank-s); color: #000; }
        
        .flex { display: flex; gap: 10px; flex-wrap: wrap; }
        .grid { display: grid; gap: 20px; }
        
        nav { 
            background: linear-gradient(90deg, rgba(11, 13, 23, 0.95) 0%, rgba(21, 25, 43, 0.95) 100%); 
            border-bottom: 1px solid var(--primary); 
            padding: 15px 20px; 
            position: sticky; 
            top: 0; 
            z-index: 100; 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            backdrop-filter: blur(5px); 
        }
        .nav-links { display: flex; align-items: center; flex-wrap: wrap; gap: 5px; }
        .nav-links button { background: transparent; color: var(--text-dim); border: none; font-size: 0.8rem; cursor: pointer; text-transform: uppercase; transition: 0.2s; padding: 5px 10px; }
        .nav-links button:hover, .nav-links button.active { color: var(--primary); text-shadow: 0 0 8px var(--primary); }
        .logo { font-size: 1.2rem; font-weight: 900; font-style: italic; border-left: 4px solid var(--accent); padding-left: 10px; cursor: pointer; transition: 0.3s; }
        .logo:hover { text-shadow: 0 0 15px var(--primary); }
        
        #adminBtn { border: 1px solid var(--accent); color: var(--accent); border-radius: 4px; margin-left: 10px; }
        #adminBtn:hover { background: var(--accent); color: white; box-shadow: 0 0 10px var(--accent); }

        main { padding: 30px 20px; max-width: 1400px; margin: 0 auto; min-height: 80vh; }
        .section { animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        input, select { background: rgba(0,0,0,0.3); border: 1px solid var(--primary); color: #fff; padding: 10px; width: 100%; outline: none; margin-bottom: 10px; }
        input:focus { box-shadow: 0 0 10px rgba(0, 240, 255, 0.3); }

        .card { 
            background: linear-gradient(145deg, rgba(21, 25, 43, 0.8) 0%, rgba(11, 13, 23, 0.9) 100%); 
            border: var(--border); 
            padding: 20px; 
            position: relative; 
            border-radius: 4px;
        }
        .card::before { content: ''; position: absolute; top: 0; left: 0; width: 4px; height: 100%; background: var(--primary); }

        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th { text-align: left; padding: 15px; background: rgba(0, 240, 255, 0.1); color: var(--primary); text-transform: uppercase; font-size: 0.8rem; }
        td { padding: 15px; border-bottom: 1px solid rgba(255,255,255,0.05); }
        tr:hover td { background: rgba(255,255,255,0.02); }

        .admin-only { display: none; }
        body.is-admin .admin-only { display: block; }
        .admin-controls { margin-bottom: 20px; padding: 15px; border: 1px dashed var(--accent); background: rgba(255, 0, 85, 0.05); }

        .rank-s-text { color: var(--rank-s); font-weight: bold; text-shadow: 0 0 5px var(--rank-s); }
        .rank-a-text { color: var(--rank-a); font-weight: bold; }
        .rank-b-text { color: var(--rank-b); }
        .rank-c-text { color: var(--text-dim); }

        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 1000; display: flex; justify-content: center; align-items: center; }
        .modal-content { background: var(--bg-panel); padding: 30px; border: 1px solid var(--primary); max-width: 800px; width: 95%; max-height: 90vh; overflow-y: auto; box-shadow: 0 0 30px rgba(0, 240, 255, 0.2); }
        
        .match-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 20px; }
        .match-card { 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            padding: 15px; 
            border: 1px solid #333; 
            background: linear-gradient(145deg, #0f121e 0%, #0a0c16 100%); 
        }
        .score-board { font-size: 2rem; font-weight: bold; margin: 10px 0; color: var(--primary); }

        .profile-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 20px; flex-wrap: wrap; gap: 10px; }
        .hype-btn { background: linear-gradient(45deg, #ff4d00, #ff9900); color: #fff; border: none; padding: 10px 20px; font-weight: bold; cursor: pointer; clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px); display: flex; align-items: center; gap: 5px; }
        .compare-val { font-family: monospace; font-size: 1.1rem; }
        .compare-val.winner { color: var(--rank-b); font-weight: bold; text-shadow: 0 0 5px var(--rank-b); }

        .awards-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; }
        .award-card { text-align: center; border: 1px solid var(--accent); background: linear-gradient(180deg, rgba(255,0,85,0.1), transparent); cursor: pointer; transition: 0.3s; }
        .award-card:hover { border-color: var(--primary); transform: translateY(-5px); box-shadow: 0 10px 20px rgba(0,240,255,0.2); }
        .award-icon { font-size: 3rem; margin-bottom: 10px; display: block; }
        .award-title { color: var(--accent); font-size: 0.9rem; margin-bottom: 5px; }
        .award-winner { font-size: 1.2rem; font-weight: bold; color: #fff; }
        .money { color: var(--rank-s); font-family: monospace; font-weight: bold; }
        
        .chk-container { display: flex; gap: 10px; align-items: center; font-size: 0.8rem; color: #aaa; }
        .chk-container input { width: auto; margin: 0; }
        .history-log { font-size: 0.8rem; color: #888; border-left: 2px solid #333; padding-left: 10px; margin-top: 5px; }
        .rank-list-item { display: flex; align-items: center; justify-content: space-between; padding: 10px; border-bottom: 1px solid rgba(255,255,255,0.05); cursor: pointer; transition: 0.2s; }
        .rank-list-item:hover { background: rgba(0,240,255,0.1); }
        .rank-1 { border-left: 3px solid var(--rank-s); background: linear-gradient(90deg, rgba(255, 215, 0, 0.1), transparent); }
        .rank-2 { border-left: 3px solid #c0c0c0; }
        .rank-3 { border-left: 3px solid #cd7f32; }

        .notification { position: fixed; bottom: 20px; right: 20px; background: var(--primary); color: #000; padding: 15px 25px; font-weight: bold; z-index: 2000; display: none; }
        
        .duo-list-item { padding: 8px 0; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 0.9rem; cursor: pointer; transition: 0.2s; }
        .duo-list-item:hover { background: rgba(0,240,255,0.1); padding-left: 10px; }
        .one-man-army-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-top: 20px; }
        
        .stats-btn { 
            background: linear-gradient(45deg, #2d34e6, #00f0ff); 
            color: white; 
            border: none; 
            padding: 8px 15px; 
            margin-top: 10px; 
            font-size: 0.8rem; 
            cursor: pointer; 
            display: flex; 
            align-items: center; 
            gap: 5px; 
            border-radius: 3px; 
            transition: 0.3s; 
            width: 100%;
            justify-content: center;
        }
        .stats-btn:hover { 
            background: linear-gradient(45deg, #00f0ff, #2d34e6); 
            box-shadow: 0 0 10px rgba(0, 240, 255, 0.5); 
        }
        
        .stats-modal-content { 
            max-width: 1000px; 
            width: 95%; 
            background: linear-gradient(145deg, #15192b 0%, #0b0d17 100%); 
        }
        
        .leg-section { 
            background: rgba(0, 0, 0, 0.3); 
            padding: 15px; 
            margin: 15px 0; 
            border-left: 4px solid var(--primary); 
        }
        
        .player-stat-row { 
            display: grid; 
            grid-template-columns: 2fr 1fr 1fr 1fr 1fr; 
            padding: 8px; 
            border-bottom: 1px solid rgba(255,255,255,0.05); 
            font-size: 0.85rem; 
            align-items: center;
        }
        
        .team-summary { 
            display: grid; 
            grid-template-columns: 1fr 1fr; 
            gap: 20px; 
            margin: 20px 0; 
        }
        
        .team-summary-card { 
            background: rgba(0, 0, 0, 0.2); 
            padding: 15px; 
            border: 1px solid rgba(0, 240, 255, 0.3); 
        }
        
        .stat-badge { 
            padding: 2px 6px; 
            border-radius: 3px; 
            font-size: 0.7rem; 
            font-weight: bold; 
            margin-left: 5px; 
        }
        
        .stat-badge.s { background: rgba(255, 215, 0, 0.2); color: var(--rank-s); }
        .stat-badge.a { background: rgba(191, 0, 255, 0.2); color: var(--rank-a); }
        .stat-badge.b { background: rgba(0, 255, 102, 0.2); color: var(--rank-b); }
        .stat-badge.c { background: rgba(224, 224, 224, 0.2); color: var(--text-dim); }
        
        .edit-match-form { 
            background: rgba(255, 0, 85, 0.05); 
            padding: 20px; 
            border: 1px dashed var(--accent); 
            margin-top: 20px; 
        }
        
        .edit-input { 
            background: rgba(0, 0, 0, 0.3); 
            border: 1px solid var(--accent); 
            color: white; 
            padding: 5px; 
            width: 60px; 
            text-align: center; 
        }
        
        .stats-header-row {
            display: grid; 
            grid-template-columns: 2fr 1fr 1fr 1fr 1fr; 
            padding: 8px; 
            background: rgba(0, 240, 255, 0.1);
            font-weight: bold;
            font-size: 0.8rem;
            margin-top: 10px;
        }
        
        .team-stats-header {
            color: var(--primary);
            margin-top: 15px;
            padding-bottom: 5px;
            border-bottom: 1px solid rgba(0, 240, 255, 0.3);
        }
        
        .leg-stats-container {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            margin: 15px 0;
            border: 1px solid rgba(0, 240, 255, 0.2);
        }
        
        .leg-title {
            color: var(--primary);
            margin-bottom: 15px;
            padding-bottom: 5px;
            border-bottom: 1px solid rgba(0, 240, 255, 0.2);
        }
        
        .player-leg-row {
            display: grid;
            grid-template-columns: 1fr repeat(4, 60px) auto;
            gap: 10px;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        .player-name-col {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .leg-checkbox {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .stat-input {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            padding: 8px;
            width: 100%;
            text-align: center;
            border-radius: 3px;
        }
        
        .stat-label {
            text-align: center;
            font-size: 0.7rem;
            color: var(--text-dim);
            margin-bottom: 5px;
        }
        
        .leg-total-display {
            background: rgba(0, 240, 255, 0.1);
            padding: 10px;
            margin: 10px 0;
            border-radius: 3px;
            font-size: 0.9rem;
        }
        
        .leg-total-row {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
        }
        
        .leg-total-label {
            color: var(--text-dim);
        }
        
        .leg-total-value {
            font-weight: bold;
            color: var(--primary);
        }
        
        .team-value-display {
            background: rgba(255, 215, 0, 0.1);
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .form-badge {
            display: inline-block;
            width: 20px;
            height: 20px;
            line-height: 20px;
            text-align: center;
            border-radius: 3px;
            font-size: 0.7rem;
            font-weight: bold;
            margin: 0 2px;
        }
        
        .form-badge.W { background: var(--rank-b); color: #000; }
        .form-badge.D { background: #666; color: #fff; }
        .form-badge.L { background: var(--accent); color: #fff; }
        
        .team-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .team-stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .team-stat-card {
            background: rgba(0,0,0,0.2);
            padding: 15px;
            border-radius: 5px;
            text-align: center;
            border: 1px solid rgba(0,240,255,0.1);
        }
        
        .team-stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary);
            margin: 5px 0;
        }
        
        .team-stat-label {
            font-size: 0.8rem;
            color: var(--text-dim);
        }
        
        .player-value-badge {
            background: rgba(255, 215, 0, 0.2);
            color: var(--rank-s);
            padding: 2px 6px;
            border-radius: 3px;
            font-size: 0.7rem;
            font-weight: bold;
            margin-left: 5px;
        }
        
        .team-name-link {
            color: inherit;
            cursor: pointer;
            text-decoration: none;
            transition: 0.3s;
            display: inline-block;
        }
        
        .team-name-link:hover {
            text-shadow: 0 0 8px currentColor;
            transform: scale(1.05);
        }
        
        .player-clickable {
            cursor: pointer;
            transition: 0.2s;
            display: inline-block;
        }
        .player-clickable:hover {
            text-shadow: 0 0 8px var(--primary);
            transform: scale(1.05);
        }
        
        .economy-badge {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 3px;
            font-size: 0.7rem;
            font-weight: bold;
            margin-left: 5px;
        }
        
        .economy-win { background: rgba(0, 255, 102, 0.2); color: var(--rank-b); }
        .economy-loss { background: rgba(255, 0, 85, 0.2); color: var(--accent); }
        .economy-draw { background: rgba(255, 255, 255, 0.2); color: var(--text-dim); }
        
        .team-roster-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }
        
        .team-roster-table th {
            background: rgba(0, 240, 255, 0.1);
            padding: 10px;
            font-size: 0.8rem;
            text-align: left;
        }
        
        .team-roster-table td {
            padding: 10px;
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        
        .team-roster-table tr:hover td {
            background: rgba(255,255,255,0.02);
        }
        
        .transfer-fee {
            color: var(--rank-s);
            font-size: 0.8rem;
            margin-top: 5px;
        }
        
        .loan-fee {
            color: #ff9900;
            font-size: 0.8rem;
            margin-top: 5px;
        }
        
        .insufficient-funds {
            color: var(--accent);
            font-size: 0.8rem;
            margin-top: 5px;
            font-weight: bold;
        }
        
        .edit-btn-small {
            background: rgba(0, 240, 255, 0.1);
            border: 1px solid var(--primary);
            color: var(--primary);
            padding: 2px 8px;
            font-size: 0.7rem;
            cursor: pointer;
            border-radius: 3px;
            margin-left: 5px;
        }
        
        .edit-btn-small:hover {
            background: var(--primary);
            color: #000;
        }
        
        .archive-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .archive-card {
            background: linear-gradient(145deg, rgba(11, 13, 23, 0.9) 0%, rgba(21, 25, 43, 0.8) 100%);
            border: 1px solid rgba(255, 215, 0, 0.3);
            padding: 20px;
            position: relative;
            cursor: pointer;
            transition: 0.3s;
        }
        
        .archive-card:hover {
            border-color: var(--rank-s);
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(255, 215, 0, 0.1);
        }
        
        .archive-badge {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(255, 215, 0, 0.2);
            color: var(--rank-s);
            padding: 2px 8px;
            border-radius: 3px;
            font-size: 0.7rem;
            font-weight: bold;
        }
        
        .archive-season-title {
            color: var(--rank-s);
            font-size: 1.2rem;
            margin-bottom: 10px;
            font-weight: bold;
        }
        
        .archive-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 15px;
            font-size: 0.8rem;
        }
        
        .archive-stat {
            background: rgba(0, 0, 0, 0.3);
            padding: 8px;
            border-radius: 3px;
            text-align: center;
        }
        
        .archive-stat-label {
            color: var(--text-dim);
            font-size: 0.7rem;
        }
        
        .archive-stat-value {
            color: var(--primary);
            font-weight: bold;
            margin-top: 3px;
        }
        
        .archive-view-container {
            background: rgba(0, 0, 0, 0.3);
            padding: 20px;
            margin-top: 20px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .archive-trophy {
            font-size: 2rem;
            text-align: center;
            margin: 20px 0;
            color: var(--rank-s);
        }
        
        .archive-readonly {
            opacity: 0.8;
            cursor: not-allowed;
        }
        
        .archive-readonly input,
        .archive-readonly select,
        .archive-readonly button {
            opacity: 0.5;
            pointer-events: none;
        }
        
        .delete-archive-btn {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(255, 0, 85, 0.2);
            border: 1px solid var(--accent);
            color: var(--accent);
            padding: 2px 8px;
            border-radius: 3px;
            font-size: 0.7rem;
            cursor: pointer;
            z-index: 10;
        }
        
        .delete-archive-btn:hover {
            background: var(--accent);
            color: white;
        }
        
        .leaderboard-container {
            max-height: 70vh;
            overflow-y: auto;
            border: 1px solid rgba(0, 240, 255, 0.2);
            border-radius: 5px;
            margin-top: 15px;
        }
        
        .search-bar {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid var(--primary);
            color: white;
            padding: 12px 15px;
            width: 100%;
            margin-bottom: 15px;
            border-radius: 5px;
            font-size: 0.9rem;
        }
        
        .search-bar::placeholder {
            color: var(--text-dim);
        }
        
        .gold-neon {
            color: #FFD700;
            text-shadow: 0 0 5px #FFD700, 0 0 10px #FFD700, 0 0 20px #FFC400, 0 0 40px #FFC400;
            font-weight: bold;
        }
        
        .silver-neon {
            color: #C0C0C0;
            text-shadow: 0 0 5px #C0C0C0, 0 0 10px #C0C0C0, 0 0 20px #AAAAAA, 0 0 40px #AAAAAA;
            font-weight: bold;
        }
        
        .bronze-neon {
            color: #CD7F32;
            text-shadow: 0 0 5px #CD7F32, 0 0 10px #CD7F32, 0 0 20px #B87333, 0 0 40px #B87333;
            font-weight: bold;
        }
        
        .award-filter-controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .award-filter-controls select,
        .award-filter-controls input {
            flex: 1;
            min-width: 200px;
            margin-bottom: 0;
        }
        
        .full-award-table {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 5px;
            overflow: hidden;
            margin-top: 15px;
        }
        
        .award-table-header {
            padding: 15px;
            background: rgba(0, 240, 255, 0.1);
            font-weight: bold;
            color: var(--primary);
            border-bottom: 1px solid rgba(0, 240, 255, 0.2);
        }
        
        .award-table-row {
            display: grid;
            grid-template-columns: 80px 1fr auto;
            padding: 12px 15px;
            border-bottom: 1px solid rgba(255,255,255,0.05);
            align-items: center;
            cursor: pointer;
            transition: 0.2s;
        }
        
        .award-table-row:hover {
            background: rgba(0,240,255,0.1);
        }
        
        .award-table-rank {
            font-weight: bold;
            font-size: 1.1rem;
            text-align: center;
        }
        
        .award-table-team {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .award-table-value {
            text-align: right;
            font-family: monospace;
            font-weight: bold;
        }
        
        .award-section {
            margin-bottom: 30px;
        }
        
        .fixtures-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }
        
        .fixture-card {
            background: linear-gradient(145deg, rgba(21, 25, 43, 0.9) 0%, rgba(11, 13, 23, 0.95) 100%);
            border: 1px solid rgba(0, 240, 255, 0.3);
            padding: 25px;
            position: relative;
            border-radius: 8px;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .fixture-card:hover {
            border-color: var(--primary);
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 240, 255, 0.15);
        }
        
        .fixture-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(0, 240, 255, 0.2);
        }
        
        .fixture-teams {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 25px 0;
            position: relative;
        }
        
        .fixture-team {
            display: flex;
            flex-direction: column;
            align-items: center;
            flex: 1;
        }
        
        .team-crest {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: rgba(0, 0, 0, 0.3);
            border: 2px solid currentColor;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            margin-bottom: 10px;
            cursor: pointer;
            transition: 0.3s;
        }
        .team-crest:hover {
            transform: scale(1.1);
            box-shadow: 0 0 15px currentColor;
        }
        
        .team-name {
            font-weight: bold;
            font-size: 1.1rem;
            text-align: center;
            cursor: pointer;
            transition: 0.3s;
        }
        .team-name:hover {
            text-shadow: 0 0 8px currentColor;
        }
        
        .vs-container {
            margin: 0 30px;
            position: relative;
        }
        
        .vs-text {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-size: 2.5rem;
            font-weight: 900;
            text-shadow: 0 0 20px rgba(0, 240, 255, 0.5);
        }
        
        .fixture-details {
            background: rgba(0, 0, 0, 0.4);
            padding: 15px;
            border-radius: 6px;
            margin-top: 20px;
            border-left: 4px solid var(--accent);
        }
        
        .fixture-status {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-top: 10px;
        }
        
        .status-upcoming { background: rgba(0, 240, 255, 0.2); color: var(--primary); }
        .status-live { background: rgba(255, 0, 85, 0.2); color: var(--accent); animation: pulse 1.5s infinite; }
        .status-completed { background: rgba(0, 255, 102, 0.2); color: var(--rank-b); }
        
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }
        
        .fixture-controls {
            display: flex;
            gap: 10px;
            margin-top: 20px;
            flex-wrap: wrap;
        }
        
        .tournament-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 30px;
            margin-top: 20px;
        }
        
        .tournament-card {
            background: linear-gradient(145deg, rgba(11, 13, 23, 0.95) 0%, rgba(21, 25, 43, 0.9) 100%);
            border: 1px solid rgba(255, 215, 0, 0.3);
            padding: 25px;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.3s;
        }
        .tournament-card:hover {
            border-color: var(--rank-s);
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(255,215,0,0.2);
        }
        
        .tournament-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(255, 215, 0, 0.2);
        }
        
        .tournament-title {
            color: var(--rank-s);
            font-size: 1.3rem;
            font-weight: bold;
        }
        
        .tournament-phase {
            color: var(--primary);
            font-size: 0.9rem;
            font-weight: bold;
        }
        
        .group-container {
            background: rgba(0, 0, 0, 0.3);
            padding: 20px;
            border-radius: 6px;
            margin-bottom: 25px;
            border: 1px solid rgba(0, 240, 255, 0.2);
        }
        
        .group-title {
            color: var(--primary);
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(0, 240, 255, 0.3);
            font-size: 1.1rem;
            font-weight: bold;
        }
        
        .bracket-container {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 20px;
            margin-top: 20px;
        }
        
        .bracket-round {
            flex: 1;
            min-width: 200px;
        }
        
        .bracket-match {
            background: rgba(0, 0, 0, 0.4);
            padding: 15px;
            margin-bottom: 15px;
            border-radius: 5px;
            border-left: 4px solid var(--primary);
            cursor: pointer;
            transition: 0.3s;
        }
        
        .bracket-match:hover {
            background: rgba(0, 0, 0, 0.6);
            border-left-color: var(--accent);
        }
        
        .bracket-team {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 0;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .bracket-team:last-child {
            border-bottom: none;
        }
        
        .bracket-team-name {
            font-weight: 500;
            cursor: pointer;
            transition: 0.2s;
        }
        .bracket-team-name:hover {
            text-shadow: 0 0 8px currentColor;
        }
        
        .bracket-team-score {
            background: rgba(0, 0, 0, 0.5);
            padding: 2px 8px;
            border-radius: 3px;
            font-family: monospace;
            font-weight: bold;
        }
        
        .tournament-creation-panel {
            background: rgba(0, 0, 0, 0.3);
            padding: 25px;
            border-radius: 8px;
            border: 2px dashed rgba(0, 240, 255, 0.4);
            margin-bottom: 30px;
        }
        
        .team-selection-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .team-selection-card {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 5px;
            border: 1px solid rgba(255,255,255,0.1);
            cursor: pointer;
            transition: 0.3s;
            text-align: center;
        }
        
        .team-selection-card:hover {
            border-color: var(--primary);
            background: rgba(0, 240, 255, 0.1);
        }
        
        .team-selection-card.selected {
            border-color: var(--rank-s);
            background: rgba(255, 215, 0, 0.1);
        }
        
        .hype-controls {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        .hype-control-btn {
            padding: 8px 15px;
            border: none;
            border-radius: 4px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            flex: 1;
            min-width: 120px;
        }
        
        .hype-add { background: rgba(0, 255, 102, 0.2); color: var(--rank-b); border: 1px solid var(--rank-b); }
        .hype-remove { background: rgba(255, 0, 85, 0.2); color: var(--accent); border: 1px solid var(--accent); }
        .hype-reset { background: rgba(255, 215, 0, 0.2); color: var(--rank-s); border: 1px solid var(--rank-s); }
        
        .hype-add:hover { background: var(--rank-b); color: #000; }
        .hype-remove:hover { background: var(--accent); color: #fff; }
        .hype-reset:hover { background: var(--rank-s); color: #000; }
        
        .legs-selector {
            display: flex;
            gap: 10px;
            margin: 15px 0;
            flex-wrap: wrap;
        }
        
        .leg-option {
            padding: 10px 20px;
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 4px;
            cursor: pointer;
            transition: 0.3s;
            text-align: center;
            flex: 1;
            min-width: 100px;
        }
        
        .leg-option:hover {
            border-color: var(--primary);
        }
        
        .leg-option.selected {
            border-color: var(--primary);
            background: rgba(0, 240, 255, 0.2);
            color: var(--primary);
        }
        
        .league-settings {
            background: rgba(0,0,0,0.3);
            padding: 20px;
            border-radius: 8px;
            border: 1px solid var(--primary);
            margin-bottom: 30px;
        }
        
        .compare-per-leg {
            font-size: 0.9rem;
        }
        .compare-per-leg .stat-highlight {
            color: var(--rank-s);
            font-weight: bold;
        }
        .per-leg-badge {
            font-size: 0.7rem;
            background: rgba(255,215,0,0.2);
            color: var(--rank-s);
            padding: 2px 6px;
            border-radius: 10px;
            margin-left: 8px;
        }
        
        .penalty-shootout {
            background: linear-gradient(45deg, #2d34e6, #ff0055);
            padding: 10px;
            border-radius: 5px;
            margin-top: 10px;
            text-align: center;
            font-weight: bold;
            cursor: pointer;
        }
        .penalty-shootout:hover {
            filter: brightness(1.2);
        }
    
        /* --- Fun emoji animations --- */
        @keyframes emojiFloat { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-6px); } }
        @keyframes emojiWiggle { 0%,100% { transform: rotate(0deg); } 25% { transform: rotate(6deg); } 75% { transform: rotate(-6deg); } }
        @keyframes emojiPop { 0% { transform: scale(1); } 50% { transform: scale(1.15); } 100% { transform: scale(1); } }
        .emoji-float { display:inline-block; animation: emojiFloat 2.6s ease-in-out infinite; }
        .emoji-wiggle { display:inline-block; animation: emojiWiggle 0.9s ease-in-out infinite; }
        .emoji-pop { display:inline-block; }
        button:active .emoji-pop { animation: emojiPop 0.22s ease-in-out; }


        /* =========================
           Cool polish + emoji motion
           ========================= */

        @keyframes emojiFloat {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-4px) rotate(-2deg); }
        }

        @keyframes emojiWiggle {
            0% { transform: rotate(0deg); }
            25% { transform: rotate(6deg); }
            50% { transform: rotate(0deg); }
            75% { transform: rotate(-6deg); }
            100% { transform: rotate(0deg); }
        }

        @keyframes emojiPop {
            0% { transform: scale(1); }
            35% { transform: scale(1.22); }
            100% { transform: scale(1); }
        }

        /* Make buttons feel snappier */
        .btn, .btn-primary, .btn-warning, .btn-danger, .stats-btn, .hype-btn, .hype-control-btn {
            transition: transform 140ms ease, filter 140ms ease, box-shadow 140ms ease, border-color 140ms ease;
            will-change: transform;
        }
        .btn:hover, .btn-primary:hover, .btn-warning:hover, .btn-danger:hover, .stats-btn:hover, .hype-btn:hover, .hype-control-btn:hover {
            transform: translateY(-1px);
            filter: brightness(1.04);
            box-shadow: 0 10px 26px rgba(0, 240, 255, 0.12);
            border-color: rgba(0, 240, 255, 0.45);
        }
        .btn:active, .btn-primary:active, .btn-warning:active, .btn-danger:active, .stats-btn:active, .hype-btn:active, .hype-control-btn:active {
            transform: translateY(0) scale(0.98);
            box-shadow: 0 6px 18px rgba(0, 240, 255, 0.08);
        }

        /* Emoji micro-interactions */
        .btn:hover .emoji-pop,
        .btn-primary:hover .emoji-pop,
        .btn-warning:hover .emoji-pop,
        .btn-danger:hover .emoji-pop,
        .stats-btn:hover .emoji-pop,
        .hype-btn:hover .emoji-pop,
        .hype-control-btn:hover .emoji-pop {
            animation: emojiPop 360ms ease;
        }
        .emoji-pop { transform-origin: 50% 60%; }
        .emoji-float { transform-origin: 50% 60%; }
        .emoji-wiggle { transform-origin: 50% 70%; }

        /* Subtle "glass" sheen on panels/cards without changing your layout */
        .card, .panel, .tournament-creation-panel, .modal-content, .stat-panel, .team-panel, .match-card, .archive-card {
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
        }

        /* Animated ambient glow behind the app (very subtle) */
        body::before {
            content: "";
            position: fixed;
            inset: -20%;
            background: radial-gradient(circle at 20% 20%, rgba(0, 240, 255, 0.10), transparent 35%),
                        radial-gradient(circle at 80% 30%, rgba(255, 0, 85, 0.08), transparent 40%),
                        radial-gradient(circle at 50% 80%, rgba(45, 52, 230, 0.10), transparent 45%);
            filter: blur(18px);
            opacity: 0.9;
            pointer-events: none;
            z-index: -1;
            animation: ambientDrift 10s ease-in-out infinite;
        }

        @keyframes ambientDrift {
            0%, 100% { transform: translate3d(0,0,0) scale(1); }
            50% { transform: translate3d(2%, -1.5%, 0) scale(1.02); }
        }

        /* Respect reduced-motion preferences */
        @media (prefers-reduced-motion: reduce) {
            .emoji-float, .emoji-wiggle { animation: none !important; }
            body::before { animation: none !important; }
            .btn, .btn-primary, .btn-warning, .btn-danger, .stats-btn, .hype-btn, .hype-control-btn {
                transition: none !important;
            }
        }


.empty-state{padding:14px; text-align:center; color:#bbb; border:1px dashed rgba(255,255,255,0.18); border-radius:12px; background:rgba(0,0,0,0.18);}


/* =========================
   NEON THEME OVERRIDES
   ========================= */
:root{
    --primary: #00f0ff;
    --accent: #ff2bd6;
    --success: #33ff99;
    --warn: #ffd84a;
    --danger: #ff3b3b;
    --bg: #050712;
    --panel: rgba(10, 14, 30, 0.72);
    --panel-2: rgba(12, 18, 40, 0.72);
    --text: #e8f7ff;
    --text-dim: rgba(232,247,255,0.72);
}

body{
    background: radial-gradient(circle at 15% 15%, rgba(0,240,255,0.12), transparent 40%),
                radial-gradient(circle at 85% 25%, rgba(255,43,214,0.10), transparent 44%),
                radial-gradient(circle at 50% 85%, rgba(51,255,153,0.10), transparent 40%),
                var(--bg);
    color: var(--text);
}

nav{
    background: rgba(5,7,18,0.58) !important;
    border-bottom: 1px solid rgba(0,240,255,0.22);
    box-shadow: 0 10px 40px rgba(0,240,255,0.08);
}

.neon-text, h1, h2, h3{
    text-shadow: 0 0 10px rgba(0,240,255,0.35), 0 0 22px rgba(255,43,214,0.14);
}

.card, .panel, .modal-content, .tournament-creation-panel, .stat-panel, .team-panel, .match-card, .archive-card{
    background: linear-gradient(180deg, rgba(10,14,30,0.70), rgba(7,10,22,0.78));
    border: 1px solid rgba(0,240,255,0.18);
    box-shadow: 0 14px 46px rgba(0,0,0,0.55), 0 0 22px rgba(0,240,255,0.08);
}

input, select, textarea{
    background: rgba(6,9,20,0.75) !important;
    border: 1px solid rgba(0,240,255,0.20) !important;
    color: var(--text) !important;
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.03);
}
input:focus, select:focus, textarea:focus{
    outline: none !important;
    border-color: rgba(0,240,255,0.55) !important;
    box-shadow: 0 0 0 3px rgba(0,240,255,0.12), 0 0 18px rgba(0,240,255,0.16);
}

.nav-links button.active{
    color: var(--primary) !important;
    text-shadow: 0 0 10px rgba(0,240,255,0.55);
}

/* Awards controls overflow fix */
.awards-controls, .award-controls, .filters, .controls { flex-wrap: wrap; }
.section input.search-bar{ max-width: 100%; box-sizing: border-box; }
</style>
</head>
<body>

<nav>
    <div class="logo" onclick="app.nav('standings')"><span id="league-title">Uzbekistan Super League</span> <span style="color:var(--primary)" id="season-display">2026</span></div>
    <div class="nav-links">
        <button onclick="app.nav('registry')">Registry</button>
        <button onclick="app.nav('match-center')">Match Center</button>
        <button onclick="app.nav('fixtures')">Fixtures</button>
        <button onclick="app.nav('results')">Results</button>
        <button onclick="app.nav('standings')">Standings</button>
        <button onclick="app.nav('leaderboard')">Players</button>
        <button onclick="app.nav('teams')">Teams</button>
        <button onclick="app.nav('tournament')">Tournament</button>
        <button onclick="app.nav('awards')">Awards</button>
        <button onclick="app.nav('archive')">Archive</button>
        <button onclick="app.nav('guide')" id="guideBtn">📘 Guide</button>
        <button onclick="app.openAdminLogs()" id="logsBtn" style="display:none">🧾 Logs</button>
        <button onclick="app.toggleAdmin()" id="adminBtn">ADMIN LOGIN</button>
    </div>
</nav>

<main id="app-container"></main>

<div id="modal-overlay" class="modal hidden">
    <div class="modal-content" id="modal-body"></div>
</div>

<div id="stats-modal-overlay" class="modal hidden">
    <div class="modal-content stats-modal-content" id="stats-modal-body"></div>
</div>

<div id="notification" class="notification">Action Successful</div>


<!-- Firebase (for public shared data) -->
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.1/anime.min.js"></script>
<script>
/** * UZBEKISTAN SUPER LEAGUE - COMPLETE VERSION WITH ALL FIXES */
const DB_KEY = 'usl_data_2026_complete_v8';  // increment to force migration
const ARCHIVE_KEY = 'usl_archive_v1';
const ADMIN_EMAILS = ["farruhbekboyboboyev@gmail.com"];
let __ADMIN_CACHE = { checked:false, isAdmin:false, email:null };
/** PUBLIC MODE (Firebase Firestore)
 *  - If you configure firebaseConfig below, ALL USERS will share the same data.
 *  - If you leave it as YOUR_..., the app continues working in localStorage (local-only).
 *
 *  IMPORTANT SECURITY NOTE:
 *  GitHub Pages is static hosting. Any password in this file is visible to the public.
 *  For a real secure admin system, use Firebase Auth + Firestore rules.
 */
const firebaseConfig = {
  apiKey: "AIzaSyBryj3amcFzlaI-Wsk6anOdc2mRd91RACE",
  authDomain: "neo-striker.firebaseapp.com",
  projectId: "neo-striker",
  storageBucket: "neo-striker.firebasestorage.app",
  messagingSenderId: "916642392399",
  appId: "1:916642392399:web:9278c2f5cce1d7ec1e7d3a",
  measurementId: "G-KRJK5HNQ00"
};

// Remote DB wiring
let __STATE_CACHE = null;
let __ARCHIVE_CACHE = null;
let __FIREBASE = { enabled: false, app: null, db: null, stateRef: null, archiveRef: null };

function firebaseEnabled(){
    return firebaseConfig && firebaseConfig.apiKey && firebaseConfig.apiKey !== "YOUR_API_KEY"
        && firebaseConfig.projectId && firebaseConfig.projectId !== "YOUR_PROJECT_ID";
}

function initFirebaseIfConfigured(){
    try{
        if(!firebaseEnabled()) return;
        __FIREBASE.app = firebase.initializeApp(firebaseConfig);
        __FIREBASE.db = firebase.firestore();
        __FIREBASE.stateRef = __FIREBASE.db.collection("usl").doc("state");
        __FIREBASE.archiveRef = __FIREBASE.db.collection("usl").doc("archive");
        __FIREBASE.enabled = true;

        // Auth state (admin UI)
        if(firebase.auth){
            firebase.auth().onAuthStateChanged(async ()=>{
                await refreshAdminCache();
                if(window.app && typeof window.app.refresh === 'function') window.app.refresh();
            });
        }


        // Live sync (public readers) - when state changes, refresh UI
        __FIREBASE.stateRef.onSnapshot((snap)=>{
            if(!snap.exists) return;
            __STATE_CACHE = snap.data().data || null;
            // If app already exists, refresh
            if(window.app && typeof window.app.refresh === 'function'){
                window.app.refresh();
            }
        });

        __FIREBASE.archiveRef.onSnapshot((snap)=>{
            if(!snap.exists) return;
            __ARCHIVE_CACHE = snap.data().data || [];
        });
    } catch(e){
        console.warn("Firebase init failed:", e);
    }
}


async function refreshAdminCache(){
    try{
        if(!__FIREBASE.enabled || !firebase.auth) {
            __ADMIN_CACHE = { checked:true, isAdmin:false, email:null };
            return __ADMIN_CACHE;
        }
        const user = firebase.auth().currentUser;
        if(!user){
            __ADMIN_CACHE = { checked:true, isAdmin:false, email:null };
            return __ADMIN_CACHE;
        }
        const email = (user.email || "").toLowerCase();
        let isAdmin = ADMIN_EMAILS.map(e=>e.toLowerCase()).includes(email);

        // Prefer custom-claims if set (most secure with Firestore rules)
        try{
            const token = await user.getIdTokenResult(true);
            if(token && token.claims && token.claims.admin === true) isAdmin = true;
        }catch(e){}

        __ADMIN_CACHE = { checked:true, isAdmin: !!isAdmin, email: email || null };
        return __ADMIN_CACHE;
    }catch(e){
        __ADMIN_CACHE = { checked:true, isAdmin:false, email:null };
        return __ADMIN_CACHE;
    }
}
function isAdminNow(){
    return __ADMIN_CACHE && __ADMIN_CACHE.isAdmin === true;
}


function wrapAnimatedEmojis(root){
    try{
        if(!root) return;
        // Only wrap inside elements that are likely safe (headings, buttons, labels, cards)
        const selectors = ['h1','h2','h3','.nav-links button','.btn','.btn-primary','.btn-warning','.btn-danger','.card','.panel','.match-card'];
        const nodes = root.querySelectorAll(selectors.join(','));
        const emojiRegex = /([\u{1F300}-\u{1FAFF}\u2600-\u27BF])/gu;

        nodes.forEach(el => {
            if(el.dataset.emojiWrapped === "1") return;
            // avoid inputs
            if(el.tagName === 'INPUT' || el.tagName === 'TEXTAREA') return;

            // replace text nodes only
            const walker = document.createTreeWalker(el, NodeFilter.SHOW_TEXT, null);
            const texts = [];
            while(walker.nextNode()) texts.push(walker.currentNode);

            texts.forEach(tn => {
                const txt = tn.nodeValue;
                if(!txt || !emojiRegex.test(txt)) return;

                const frag = document.createDocumentFragment();
                let last = 0;
                emojiRegex.lastIndex = 0;
                for(const m of txt.matchAll(emojiRegex)){
                    const i = m.index;
                    if(i > last) frag.appendChild(document.createTextNode(txt.slice(last,i)));
                    const span = document.createElement('span');
                    span.className = 'emoji-float emoji-pop';
                    span.textContent = m[0];
                    frag.appendChild(span);
                    last = i + m[0].length;
                }
                if(last < txt.length) frag.appendChild(document.createTextNode(txt.slice(last)));
                tn.parentNode.replaceChild(frag, tn);
            });

            el.dataset.emojiWrapped = "1";
        });
    }catch(e){}
}

function runNeonEntranceAnimations(){
    try{
        if(typeof anime === 'undefined') return;
        anime({
            targets: '.card, .panel, .match-card, .stat-panel, .team-panel, .archive-card',
            translateY: [10, 0],
            opacity: [0, 1],
            duration: 520,
            delay: anime.stagger(40),
            easing: 'easeOutQuad'
        });
        anime({
            targets: '.nav-links button',
            opacity: [0, 1],
            translateY: [-4, 0],
            duration: 360,
            delay: anime.stagger(18),
            easing: 'easeOutQuad'
        });
    }catch(e){}
}

function safeClone(obj){
    try { return JSON.parse(JSON.stringify(obj)); } catch(e){ return obj; }
}

// Simple admin log (last 200 entries shown)
async function writeAdminLog(action, beforeState, afterState){
    try{
        if(!__FIREBASE.enabled) return;
        const before = beforeState ? { teams: beforeState.teams?.length||0, players: beforeState.players?.length||0, matches: beforeState.matches?.length||0, fixtures: beforeState.fixtures?.length||0, tournaments: beforeState.tournaments?.length||0 } : null;
        const after  = afterState  ? { teams: afterState.teams?.length||0, players: afterState.players?.length||0, matches: afterState.matches?.length||0, fixtures: afterState.fixtures?.length||0, tournaments: afterState.tournaments?.length||0 } : null;
        await __FIREBASE.db.collection("usl_logs").add({
            ts: firebase.firestore.FieldValue.serverTimestamp(),
            action: action || "UPDATE",
            admin: (db.get()?.settings?.adminName) || "admin",
            before,
            after
        });
    } catch(e){
        console.warn("log write failed:", e);
    }
}


const initialState = {
    leagueName: "Uzbekistan Super League",
    seasonName: "2026 Season",
    teams: [],
    players: [],
    matches: [],
    fixtures: [],
    tournaments: [],
    settings: { isAdmin: false }
};

// Helper to recalc player value
const MAX_PLAYER_VALUE = 1000000000; // $1B cap (adjust if needed)
function recalcPlayerValue(player) {
    if (player.startingValue === undefined) player.startingValue = 1000000;
    if (player.growthValue === undefined) player.growthValue = 0;
    player.playerValue = Math.max(0, player.startingValue + player.growthValue);
    player.playerValue = Math.min(MAX_PLAYER_VALUE, player.playerValue);
    player.marketValue = player.playerValue;
    return player;
}

// Initialize with team economy - FIXED PLAYER VALUES
const initData = () => {
    let data = db.get();
    
    // Migrate players to new structure
    data.players.forEach(player => {
        if (player.startingValue === undefined) {
            player.startingValue = 1000000;
        }
        if (player.growthValue === undefined) {
            // Old player.value = total value? compute growth
            const oldValue = player.value !== undefined ? player.value : 1000000;
            player.growthValue = oldValue - player.startingValue;
            if (player.growthValue < 0) player.growthValue = 0;
        }
        recalcPlayerValue(player);
        delete player.value; // remove old property
    });
    
    // Migrate matches to use snapshots
    data.matches.forEach(match => {
        // Migrate MVP to snapshot
        if (match.mvpId && !match.mvpSnapshot) {
            const player = data.players.find(p => p.id === match.mvpId);
            const team = data.teams.find(t => t.id === match.teamAId || t.id === match.teamBId);
            if (player && team) {
                match.mvpSnapshot = {
                    playerId: player.id,
                    playerName: player.name,
                    teamId: team.id,
                    teamName: team.name
                };
            }
        }
        if (match.motmId && !match.motmSnapshot) {
            const player = data.players.find(p => p.id === match.motmId);
            const team = data.teams.find(t => t.id === match.teamAId || t.id === match.teamBId);
            if (player && team) {
                match.motmSnapshot = {
                    playerId: player.id,
                    playerName: player.name,
                    teamId: team.id,
                    teamName: team.name
                };
            }
        }
        // Migrate playerStats to snapshots
        if (match.playerStats && match.playerStats.length > 0) {
            match.playerStats.forEach(ps => {
                if (!ps.playerNameSnapshot) {
                    const player = data.players.find(p => p.id === ps.playerId);
                    const team = data.teams.find(t => t.id === ps.teamId);
                    if (player && team) {
                        ps.playerNameSnapshot = player.name;
                        ps.teamNameSnapshot = team.name;
                    }
                }
            });
        }
    });
    
    // Initialize team values - $250,000,000
    data.teams.forEach(team => {
        if (team.value === undefined) {
            team.value = 250000000; // $250,000,000
        }
        if (team.stats === undefined) {
            team.stats = {
                wins: 0, draws: 0, losses: 0,
                goalsFor: 0, goalsAgainst: 0,
                comebacks: 0, winStreak: 0, currentStreak: 0
            };
        }
    });
    
    // Initialize fixtures array if not exists
    if (!data.fixtures) data.fixtures = [];
    
    // Initialize tournaments array if not exists
    if (!data.tournaments) data.tournaments = [];
    
    db.save(data, 'ADMIN_LOGOUT');
    return data;
};

const db = {
    get: () => {
        // Prefer remote cache if Firebase configured
        if(__FIREBASE.enabled && __STATE_CACHE) return __STATE_CACHE;

        // Fallback to localStorage (works without Firebase config)
        try {
            const data = localStorage.getItem(DB_KEY);
            const parsed = data ? JSON.parse(data) : initialState;
            if(!__STATE_CACHE) __STATE_CACHE = parsed;
            parsed.settings = parsed.settings || {}; parsed.settings.isAdmin = isAdminNow();
            return parsed;
        } catch(e) {
            if(!__STATE_CACHE) __STATE_CACHE = initialState;
            initialState.settings = initialState.settings || {}; initialState.settings.isAdmin = isAdminNow();
            return initialState;
        }
    },
    save: async (data, metaAction) => {
        const before = safeClone(db.get());
        // Never persist admin flag into shared state
        const __toSave = safeClone(data);
        if(__toSave && __toSave.settings) __toSave.settings.isAdmin = false;
        __STATE_CACHE = data;

        // Always keep a local copy (offline-friendly)
        try { localStorage.setItem(DB_KEY, JSON.stringify(__toSave)); } catch(e){}

        // Remote write if enabled (shared/public)
        if(__FIREBASE.enabled){
            // Only admins can save to remote (enforced again by Firestore rules)
            await refreshAdminCache();
            if(!isAdminNow()){
                console.warn('Blocked remote write: not admin');
            } else {
            try{
                await __FIREBASE.stateRef.set({ data: __toSave, updatedAt: firebase.firestore.FieldValue.serverTimestamp() }, { merge: true });
                if(data?.settings?.isAdmin) await writeAdminLog(metaAction || "UPDATE", before, data);
            } catch(e){
                console.warn("Remote save failed:", e);
            }
            }
        }

        // Refresh UI
        if(window.app && typeof window.app.refresh === 'function'){
            window.app.refresh();
        }
    },
    update: async (cb, metaAction) => {
        const current = db.get();
        const newData = cb(safeClone(current));
        await db.save(newData, metaAction);
    }
};

const archiveDb = {
    get: () => {
        if(__FIREBASE.enabled && Array.isArray(__ARCHIVE_CACHE)) return __ARCHIVE_CACHE;

        try {
            const data = localStorage.getItem(ARCHIVE_KEY);
            const parsed = data ? JSON.parse(data) : [];
            if(!__ARCHIVE_CACHE) __ARCHIVE_CACHE = parsed;
            parsed.settings = parsed.settings || {}; parsed.settings.isAdmin = isAdminNow();
            return parsed;
        } catch(e) {
            if(!__ARCHIVE_CACHE) __ARCHIVE_CACHE = [];
            return [];
        }
    },
    save: async (data) => {
        __ARCHIVE_CACHE = data;
        try { localStorage.setItem(ARCHIVE_KEY, JSON.stringify(data)); } catch(e){}
        if(__FIREBASE.enabled){
            // Only admins can save to remote (enforced again by Firestore rules)
            if(!isAdminNow()){
                console.warn('Blocked remote write: not admin');
            } else {
                try{
                    await __FIREBASE.archiveRef.set({ data, updatedAt: firebase.firestore.FieldValue.serverTimestamp() }, { merge: true });
                } catch(e){
                    console.warn("Remote archive save failed:", e);
                }
            }
        }
        if(window.app && typeof window.app.refresh === 'function'){
            window.app.refresh();
        }
    },
    update: async (cb) => {
        const data = archiveDb.get();
        const newData = cb(safeClone(data));
        await archiveDb.save(newData);
    }
};

const util = {
    uuid: () => Date.now().toString(36) + Math.random().toString(36).substr(2),
    toInt: (v, def=0) => {
        const n = parseInt(v, 10);
        return Number.isFinite(n) ? n : def;
    },
    // Determine leg numbers supported for a match (1..4). Falls back to 2.
    getLegNumbers: (match) => {
        // Preferred: explicit match.format or match.legs (if you store it)
        const fmt = (match && match.format) ? String(match.format).toLowerCase() : '';
        if(fmt.includes('4')) return [1,2,3,4];
        if(fmt.includes('1')) return [1];

        // Detect from playerStats legs presence
        let maxLeg = 0;
        try{
            (match.playerStats || []).forEach(ps => {
                for(let i=1;i<=4;i++){
                    if(ps && ps['leg'+i] && (ps['leg'+i].played || ps['leg'+i].goals || ps['leg'+i].assists || ps['leg'+i].saves || ps['leg'+i].tackles)){
                        maxLeg = Math.max(maxLeg, i);
                    }
                }
            });
        }catch(e){}
        if(maxLeg === 0) maxLeg = 2;
        return Array.from({length:maxLeg}, (_,i)=>i+1);
    },
    sumMatchScore: (match, side) => {
        const legs = util.getLegNumbers(match);
        const keyBase = side === 'A' ? 'leg' : 'leg';
        // score keys are leg1ScoreA/leg1ScoreB etc (if not present, treated as 0)
        let total = 0;
        legs.forEach(i => {
            const k = `leg${i}Score${side}`;
            total += util.toInt(match && match[k], 0);
        });
        return total;
    },
    notify: (msg) => {
        const el = document.getElementById('notification');
        el.innerText = msg;
        el.style.display = 'block';
        setTimeout(() => el.style.display = 'none', 3000);
    },
    escapeHtml: (str) => {
        if(str === null || str === undefined) return '';
        return String(str)
            .replace(/&/g,'&amp;')
            .replace(/</g,'&lt;')
            .replace(/>/g,'&gt;')
            .replace(/\"/g,'&quot;')
            .replace(/'/g,'&#039;');
    },

    formatMoney: (amount) => {
        if (amount === undefined || amount === null || isNaN(amount)) {
            return '$0';
        }
        return '$' + amount.toLocaleString();
    },
    getRank: (val, type) => {
        if(type === 'goals') return val >= 3.5 ? 'S' : val >= 2.5 ? 'A' : val >= 1.5 ? 'B' : 'C';
        if(type === 'saves') return val >= 15 ? 'S' : val >= 10 ? 'A' : val >= 5 ? 'B' : 'C';
        if(type === 'tackles') return val >= 10 ? 'S' : val >= 7 ? 'A' : val >= 5 ? 'B' : 'C';
        return 'C';
    },
    getClass: (rank) => `rank-${rank.toLowerCase()}-text`,
    getRankBadge: (val, type) => {
        const rank = util.getRank(val, type);
        return `<span class="stat-badge ${rank.toLowerCase()}">${rank}</span>`;
    },
    calculateLegStats: (match, data, legNumber) => {
        const legStats = {
            teamA: { players: [], totals: { goals: 0, assists: 0, saves: 0, tackles: 0 } },
            teamB: { players: [], totals: { goals: 0, assists: 0, saves: 0, tackles: 0 } }
        };

        (match.playerStats || []).forEach(pStat => {
            const playerName = pStat.playerNameSnapshot || 'Unknown';
            const teamId = pStat.teamId;
            const isTeamA = teamId === match.teamAId;

            const legData = pStat && pStat['leg' + legNumber];

            if (legData && legData.played) {
                const playerStat = {
                    name: playerName,
                    goals: util.toInt(legData.goals || 0),
                    assists: util.toInt(legData.assists || 0),
                    saves: util.toInt(legData.saves || 0),
                    tackles: util.toInt(legData.tackles || 0)
                };

                const targetTeam = isTeamA ? legStats.teamA : legStats.teamB;
                targetTeam.players.push(playerStat);
                targetTeam.totals.goals += playerStat.goals;
                targetTeam.totals.assists += playerStat.assists;
                targetTeam.totals.saves += playerStat.saves;
                targetTeam.totals.tackles += playerStat.tackles;
            }
        });

        return legStats;
    },

    calculatePlayerEarnings: (playerStats, mvpId, motmId, playerId) => {
        let earnings = 0;

        // Calculate from legs (supports up to 4 legs)
        const legs = [];
        for(let i=1;i<=4;i++){
            if(playerStats && playerStats['leg'+i]) legs.push(playerStats['leg'+i]);
        }
        (legs.length ? legs : [playerStats.leg1, playerStats.leg2]).forEach(leg => {
            if (leg && leg.played) {
                earnings += (leg.goals || 0) * 2000000;      // $2,000,000 per goal
                earnings += (leg.assists || 0) * 1000000;    // $1,000,000 per assist
                earnings += (leg.saves || 0) * 200000;       // $200,000 per save
                earnings += (leg.tackles || 0) * 300000;     // $300,000 per tackle
            }
        });

        // MVP / MOTM bonuses
        if(playerId && mvpId && playerId === mvpId) earnings += 8000000;   // $8,000,000
        if(playerId && motmId && playerId === motmId) earnings += 5000000; // $5,000,000

        return earnings;
    },
    simulatePenaltyWinner: (teamA, teamB) => {
        // Random penalty shootout winner
        return Math.random() < 0.5 ? teamA : teamB;
    }
};

// --- APP LOGIC ---
window.app = {
    currentView: 'standings',
    sortBy: 'goals',
    selectedPlayerId: null,
    selectedTeamId: null,
    editingMatchId: null,
    viewingArchiveId: null,
    searchPlayerQuery: '',
    awardFilter: 'all',
    awardSearchQuery: '',
    selectedTournamentId: null,
    tournamentCreationStep: 1,
    selectedTeamsForTournament: [],

    init: () => {
        if (!localStorage.getItem(DB_KEY)) db.save(initialState);
        initData();
        window.app.render();
    },

    refresh: () => { window.app.render(); },

    nav: (view) => {
        window.app.currentView = view;
        window.app.viewingArchiveId = null;
        window.app.selectedTournamentId = null;
        window.app.searchPlayerQuery = '';
        window.app.awardFilter = 'all';
        window.app.awardSearchQuery = '';
        window.app.tournamentCreationStep = 1;
        window.app.selectedTeamsForTournament = [];
        document.querySelectorAll('.nav-links button').forEach(b => {
            if (b.id !== 'adminBtn') b.classList.remove('active');
        });
        const btns = Array.from(document.querySelectorAll('.nav-links button'));
        const activeBtn = btns.find(b => b.getAttribute('onclick')?.includes(view));
        if(activeBtn) activeBtn.classList.add('active');
        window.app.render();
    },


    openAdminLogs: async () => {
        const data = db.get();
        if(!data.settings.isAdmin){
            util.notify("Admin only");
            return;
        }

        let logs = [];
        if(__FIREBASE.enabled){
            if(!isAdminNow()){
                console.warn('Blocked logs read: not admin');
                util.notify("Admin only");
            } else {
                try{
                    const snap = await __FIREBASE.db.collection("usl_logs").orderBy("ts","desc").limit(200).get();
                    logs = snap.docs.map(d => ({ id: d.id, ...d.data() }));
                } catch(e){
                    console.warn(e);
                    util.notify("Could not load logs");
                }
            }
        } else {
            util.notify("Firebase is not configured. Logs are available only in public Firebase mode.");
        }

        const rows = logs.map(l => {
            const dt = l.ts && l.ts.toDate ? l.ts.toDate().toLocaleString() : "";
            const before = l.before ? `T:${l.before.teams} P:${l.before.players} M:${l.before.matches}` : "";
            const after  = l.after  ? `T:${l.after.teams} P:${l.after.players} M:${l.after.matches}` : "";
            return `<tr>
                <td style="white-space:nowrap">${dt}</td>
                <td>${(l.admin||"").toString().replace(/</g,'&lt;')}</td>
                <td>${(l.action||"UPDATE").toString().replace(/</g,'&lt;')}</td>
                <td style="font-family:monospace">${before}</td>
                <td style="font-family:monospace">${after}</td>
            </tr>`;
        }).join("");

        document.getElementById('modal-body').innerHTML = `
            <h2><span class="emoji-float">🧾</span> Admin Logs</h2>
            <p style="color:var(--text-dim); margin-top:6px;">Last 200 changes (summary counts).</p>
            <div style="overflow:auto; max-height:60vh; margin-top:12px; border: var(--border); border-radius: 10px;">
                <table style="width:100%; border-collapse:collapse;">
                    <thead>
                        <tr style="position:sticky; top:0; background:var(--bg-panel); border-bottom: var(--border);">
                            <th style="text-align:left; padding:10px;">Time</th>
                            <th style="text-align:left; padding:10px;">Admin</th>
                            <th style="text-align:left; padding:10px;">Action</th>
                            <th style="text-align:left; padding:10px;">Before</th>
                            <th style="text-align:left; padding:10px;">After</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${rows || `<tr><td colspan="5" style="padding:14px; color:var(--text-dim)">No logs yet.</td></tr>`}
                    </tbody>
                </table>
            </div>
            <div style="display:flex; gap:10px; justify-content:flex-end; margin-top:14px;">
                <button onclick="document.getElementById('modal-overlay').classList.add('hidden')">Close</button>
            </div>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },

    toggleAdmin: async () => {
        const data = db.get();
        if(data.settings.isAdmin) {
            data.settings.isAdmin = false;
            db.save(data, 'ADMIN_LOGIN');
            util.notify("Logged out");
        } else {
            setTimeout(async () => {
                if(!__FIREBASE.enabled || !firebase.auth){
                    alert("Firebase Auth is not enabled. Configure firebaseConfig first.");
                    return;
                }
                const user = firebase.auth().currentUser;
                if(user){
                    await firebase.auth().signOut();
                    await refreshAdminCache();
                    util.notify("SIGNED OUT");
                    window.app.render();
                    return;
                }
                const email = prompt("Admin email:");
                if(!email) return;
                const password = prompt("Password:");
                if(password === null) return;
                try{
                    await firebase.auth().signInWithEmailAndPassword(email, password);
                    await refreshAdminCache();
                    if(!isAdminNow()){
                        alert("Signed in, but not an admin. Ask the owner to grant admin access.");
                    } else {
                        util.notify("ADMIN SIGNED IN");
                    }
                    window.app.render();
                } catch(e){
                    alert("Login failed: " + (e && e.message ? e.message : e));
                }
            }, 50);
}
    },

    render: () => {
        const data = db.get();
        const container = document.getElementById('app-container');
        document.body.className = data.settings.isAdmin ? 'is-admin' : '';
        document.getElementById('season-display').innerText = data.seasonName;
        document.getElementById('league-title').innerText = data.leagueName || 'Uzbekistan Super League';
        
        const adminBtn = document.getElementById('adminBtn');
        const logsBtn = document.getElementById('logsBtn');
        if (data.settings.isAdmin) {
            if(logsBtn) logsBtn.style.display = 'inline-block';
            adminBtn.innerText = "LOGOUT ADMIN";
            adminBtn.style.borderColor = "var(--primary)";
            adminBtn.style.color = "var(--primary)";
        } else {
            if(logsBtn) logsBtn.style.display = 'none';
            adminBtn.innerText = "ADMIN LOGIN";
            adminBtn.style.borderColor = "var(--accent)";
            adminBtn.style.color = "var(--accent)";
        }

        if(window.app.currentView === 'registry') renderRegistry(container, data);
        else if(window.app.currentView === 'match-center') renderMatchCenter(container, data);
        else if(window.app.currentView === 'fixtures') renderFixtures(container, data);
        else if(window.app.currentView === 'results') renderResults(container, data);
        else if(window.app.currentView === 'standings') renderStandings(container, data);
        else if(window.app.currentView === 'leaderboard') renderLeaderboard(container, data);
        else if(window.app.currentView === 'teams') renderTeams(container, data);
        else if(window.app.currentView === 'tournament') renderTournament(container, data);
        else if(window.app.currentView === 'awards') renderAwards(container, data);
        else if(window.app.currentView === 'profile') renderProfile(container, data);
        else if(window.app.currentView === 'team-profile') renderTeamProfile(container, data);
        else if(window.app.currentView === 'archive') renderArchive(container, data);
        else if(window.app.currentView === 'archive-view') renderArchiveView(container, data);
        else if(window.app.currentView === 'guide') renderGuide(container, data);
        else if(window.app.currentView === 'fixture-detail') renderFixtureDetail(container, data);
        else if(window.app.currentView === 'award-ranking') renderAwardRanking(container, data);

        // Global micro-animations
        wrapAnimatedEmojis(document);
        runNeonEntranceAnimations();
    },

    openProfile: (pid) => {
        window.app.selectedPlayerId = pid;
        window.app.currentView = 'profile';
        window.app.render();
    },

    openTeam: (tid) => {
        window.app.selectedTeamId = tid;
        window.app.currentView = 'team-profile';
        window.app.render();
    },

    openArchive: (archiveId) => {
        window.app.viewingArchiveId = archiveId;
        window.app.currentView = 'archive-view';
        window.app.render();
    },

    openTournament: (tournamentId) => {
        window.app.selectedTournamentId = tournamentId;
        window.app.render();
    },
    
    openFixtureDetail: (fixtureId) => {
        window.app.selectedFixtureId = fixtureId;
        window.app.currentView = 'fixture-detail';
        window.app.render();
    },
    
    openAwardRanking: (awardType) => {
        window.app.selectedAward = awardType;
        window.app.currentView = 'award-ranking';
        window.app.render();
    },

    toggleTeamForTournament: (teamId) => {
        const data = db.get();
        const team = data.teams.find(t => t.id === teamId);
        if (!team) return;
        
        const index = window.app.selectedTeamsForTournament.indexOf(teamId);
        if (index > -1) {
            window.app.selectedTeamsForTournament.splice(index, 1);
        } else {
            if (window.app.selectedTeamsForTournament.length < 8) {
                window.app.selectedTeamsForTournament.push(teamId);
            } else {
                util.notify("Maximum 8 teams for tournament");
            }
        }
        window.app.render();
    },

    renderCompare: (oppId, myId) => {
        if(!oppId) { document.getElementById('compareResult').innerHTML = ''; return; }
        const data = db.get();
        const allStats = calculatePlayerStats(data);
        const me = allStats.find(p => p.id === myId);
        const opp = allStats.find(p => p.id === oppId);
        
        // PER-LEG comparison
        const meLegs = me.legsPlayed || 1;
        const oppLegs = opp.legsPlayed || 1;
        
        const meGoalsPerLeg = (me.goals / meLegs).toFixed(2);
        const oppGoalsPerLeg = (opp.goals / oppLegs).toFixed(2);
        const meAssistsPerLeg = (me.assists / meLegs).toFixed(2);
        const oppAssistsPerLeg = (opp.assists / oppLegs).toFixed(2);
        const meSavesPerLeg = (me.saves / meLegs).toFixed(2);
        const oppSavesPerLeg = (opp.saves / oppLegs).toFixed(2);
        const meTacklesPerLeg = (me.tackles / meLegs).toFixed(2);
        const oppTacklesPerLeg = (opp.tackles / oppLegs).toFixed(2);
        
        const row = (label, v1, v2, unit = '') => `
            <div style="display:flex; justify-content:space-between; border-bottom:1px solid #333; padding:10px 0;">
                <span class="${parseFloat(v1) > parseFloat(v2) ? 'compare-val winner' : 'compare-val'}">${v1}${unit}</span>
                <span style="color:#888; font-size:0.8rem;">${label}</span>
                <span class="${parseFloat(v2) > parseFloat(v1) ? 'compare-val winner' : 'compare-val'}">${v2}${unit}</span>
            </div>`;
            
        document.getElementById('compareResult').innerHTML = `
            <div style="text-align:center; margin-bottom:10px;">
                <span style="font-weight:bold; color:${me.teamColor}; cursor:pointer;" onclick="app.openProfile('${me.id}')" class="player-clickable">${me.name}</span> VS 
                <span style="font-weight:bold; color:${opp.teamColor}; cursor:pointer;" onclick="app.openProfile('${opp.id}')" class="player-clickable">${opp.name}</span>
                <div style="font-size:0.8rem; color:#888; margin-top:5px;">Per-Leg Averages</div>
            </div>
            ${row('GOALS / LEG', meGoalsPerLeg, oppGoalsPerLeg)}
            ${row('ASSISTS / LEG', meAssistsPerLeg, oppAssistsPerLeg)}
            ${row('SAVES / LEG', meSavesPerLeg, oppSavesPerLeg)}
            ${row('TACKLES / LEG', meTacklesPerLeg, oppTacklesPerLeg)}
            <div style="display:flex; justify-content:space-between; padding:8px 0; color:var(--text-dim);">
                <span>Legs Played: ${meLegs}</span>
                <span>Legs Played: ${oppLegs}</span>
            </div>
            <div style="display:flex; justify-content:space-between; padding:8px 0;">
                <span>MVP: ${me.mvpCount || 0}</span>
                <span>MVP: ${opp.mvpCount || 0}</span>
            </div>
            <div style="display:flex; justify-content:space-between; padding:8px 0;">
                <span>MOTM: ${me.motmCount || 0}</span>
                <span>MOTM: ${opp.motmCount || 0}</span>
            </div>
        `;
    }
};

// --- CALCULATION FUNCTIONS ---
function calculateTeamStandings(data) {
    return data.teams.map(team => {
        let stats = { 
            mp: 0, w: 0, d: 0, l: 0, gf: 0, ga: 0, pts: 0,
            winStreak: 0, currentStreak: 0,
            comeFromBehindWins: 0,
            totalTacklesSaves: 0,
            goalDistribution: {},
            form: [],
            h2hGoals: {},
            h2hMatches: {}
        };
        
        // Get team matches in chronological order
        const teamMatches = data.matches
            .filter(m => m.teamAId === team.id || m.teamBId === team.id)
            .sort((a, b) => a.timestamp - b.timestamp);
        
        teamMatches.forEach(match => {
            stats.mp++;
            const isA = match.teamAId === team.id;
            const opponentId = isA ? match.teamBId : match.teamAId;
            const myScore = isA ? (util.sumMatchScore(match,'A')) : 
                                 (util.sumMatchScore(match,'B'));
            const oppScore = isA ? (util.sumMatchScore(match,'B')) : 
                                 (util.sumMatchScore(match,'A'));
            
            // Track h2h
            if (!stats.h2hGoals[opponentId]) stats.h2hGoals[opponentId] = { for: 0, against: 0, matches: 0 };
            stats.h2hGoals[opponentId].for += myScore;
            stats.h2hGoals[opponentId].against += oppScore;
            stats.h2hGoals[opponentId].matches++;
            
            // Check for comeback
            const leg1Score = isA ? parseInt(match.leg1ScoreA) : parseInt(match.leg1ScoreB);
            const leg1OppScore = isA ? parseInt(match.leg1ScoreB) : parseInt(match.leg1ScoreA);
            
            if ((leg1Score < leg1OppScore || leg1Score === leg1OppScore) && 
                (myScore > oppScore)) {
                stats.comeFromBehindWins++;
            }
            
            stats.gf += myScore;
            stats.ga += oppScore;
            
            let result = '';
            if (myScore > oppScore) { 
                stats.w++; 
                stats.pts += 3; 
                result = 'W';
                stats.currentStreak = stats.currentStreak >= 0 ? stats.currentStreak + 1 : 1;
            } else if (myScore < oppScore) { 
                stats.l++; 
                result = 'L';
                stats.currentStreak = stats.currentStreak <= 0 ? stats.currentStreak - 1 : -1;
            } else { 
                stats.d++; 
                stats.pts += 1; 
                result = 'D';
                stats.currentStreak = 0;
            }
            
            stats.form.push(result);
            if (stats.form.length > 5) stats.form.shift();
            
            if (myScore > oppScore) {
                stats.winStreak = Math.max(stats.winStreak, stats.currentStreak);
            }
            
            // Calculate tackles and saves
            const matchStats = match.playerStats.filter(ps => {
                return ps.teamId === team.id;
            });
            
            matchStats.forEach(ps => {
                const leg1Stats = ps.leg1 || {};
                const leg2Stats = ps.leg2 || {};
                
                stats.totalTacklesSaves += (parseInt(leg1Stats.tackles || 0) + 
                                           parseInt(leg1Stats.saves || 0) +
                                           parseInt(leg2Stats.tackles || 0) +
                                           parseInt(leg2Stats.saves || 0));
            });
        });
        
        // Calculate goal distribution
        const teamPlayers = data.players.filter(p => p.teamId === team.id);
        teamPlayers.forEach(player => {
            const playerStats = calculatePlayerStats(data).find(p => p.id === player.id);
            if (playerStats && playerStats.goals > 0) {
                stats.goalDistribution[player.id] = playerStats.goals;
            }
        });
        
        const formDisplay = stats.form.map(r => `<span class="form-badge ${r}">${r}</span>`).join('');
        
        return { 
            ...team, 
            ...stats, 
            gd: stats.gf - stats.ga, 
            form: formDisplay,
            last5: stats.form.join(''),
            value: team.value || 250000000,
            h2hGoals: stats.h2hGoals
        };
    });
}

function calculatePlayerStats(data) {
    return data.players.map(p => {
        const team = data.teams.find(t => t.id === p.teamId) || {name:'Unknown', color:'#fff'};
        let stats = { 
            id: p.id, 
            name: p.name, 
            teamId: p.teamId, 
            teamName: team.name, 
            teamColor: team.color, 
            hype: p.hypeCount || 0, 
            goals:0, 
            assists:0, 
            saves:0, 
            tackles:0, 
            legsPlayed:0, 
            mvpCount:0, 
            motmCount:0, 
            matchLogs:[],
            startingValue: p.startingValue || 1000000,
            growthValue: p.growthValue || 0,
            playerValue: p.playerValue || 1000000,
            marketValue: p.marketValue || 1000000
        };
        
        data.matches.forEach(m => {
            const pMatch = m.playerStats.find(ps => ps.playerId === p.id);
            if(pMatch) {
                const leg1Played = pMatch.leg1 && pMatch.leg1.played;
                const leg2Played = pMatch.leg2 && pMatch.leg2.played;
                
                if(leg1Played) stats.legsPlayed++;
                if(leg2Played) stats.legsPlayed++;
                
                if(pMatch.leg1 && pMatch.leg1.played) {
                    stats.goals += parseInt(pMatch.leg1.goals || 0);
                    stats.assists += parseInt(pMatch.leg1.assists || 0);
                    stats.saves += parseInt(pMatch.leg1.saves || 0);
                    stats.tackles += parseInt(pMatch.leg1.tackles || 0);
                }
                
                if(pMatch.leg2 && pMatch.leg2.played) {
                    stats.goals += parseInt(pMatch.leg2.goals || 0);
                    stats.assists += parseInt(pMatch.leg2.assists || 0);
                    stats.saves += parseInt(pMatch.leg2.saves || 0);
                    stats.tackles += parseInt(pMatch.leg2.tackles || 0);
                }
                
                if(m.mvpId === p.id) stats.mvpCount++;
                if(m.motmId === p.id) stats.motmCount++;
                
                const oppId = m.teamAId === pMatch.teamId ? m.teamBId : m.teamAId;
                const oppName = (data.teams.find(t=>t.id===oppId) || {name:'?'}).name;
                
                stats.matchLogs.push({ 
                    matchId: m.id, 
                    opponentName: oppName, 
                    playedLeg1: leg1Played, 
                    playedLeg2: leg2Played,
                    goals: (pMatch.leg1?.goals || 0) + (pMatch.leg2?.goals || 0),
                    assists: (pMatch.leg1?.assists || 0) + (pMatch.leg2?.assists || 0)
                });
            }
        });
        
        // Market value is just playerValue, no extra multipliers
        stats.marketValue = p.playerValue || 1000000;
        
        return stats;
    });
}

function calculateTeamAwards(data) {
    const teamStandings = calculateTeamStandings(data);
    
    // A) Most Valued Team
    const mostValuedTeams = [...teamStandings].sort((a,b) => b.value - a.value);
    
    // B) German Football Machine (in top 4)
    const top4Teams = [...teamStandings].sort((a,b) => b.pts - a.pts).slice(0,4);
    let germanMachineTeams = top4Teams.map(team => {
        const goalEntries = Object.entries(team.goalDistribution || {});
        if(goalEntries.length === 0) return {...team, dependency: 100};
        
        const totalGoals = team.gf;
        const topScorerGoals = Math.max(...Object.values(team.goalDistribution || {}));
        const dependency = totalGoals > 0 ? (topScorerGoals / totalGoals) * 100 : 100;
        
        return {...team, dependency};
    }).sort((a,b) => a.dependency - b.dependency);
    
    // C) Remontada Kings
    const remontadaTeams = [...teamStandings].sort((a,b) => b.comeFromBehindWins - a.comeFromBehindWins);
    
    // D) The Wall Team
    const wallTeams = [...teamStandings].sort((a,b) => b.totalTacklesSaves - a.totalTacklesSaves);
    
    // E) Goal Hunters
    const goalHuntersTeams = [...teamStandings].sort((a,b) => b.gd - a.gd);
    
    // F) Winning Streak Kings
    const streakTeams = [...teamStandings].sort((a,b) => b.winStreak - a.winStreak);
    
    // G) Super Star Team (highest average player value)
    let superStarTeams = teamStandings.map(team => {
        const teamPlayers = data.players.filter(p => p.teamId === team.id);
        if(teamPlayers.length === 0) return {...team, avgValue: 0};
        
        const avgValue = teamPlayers.reduce((sum, p) => sum + p.playerValue, 0) / teamPlayers.length;
        
        return {...team, avgValue};
    }).sort((a,b) => b.avgValue - a.avgValue);
    
    return {
        mostValuedTeams,
        germanMachineTeams,
        remontadaTeams,
        wallTeams,
        goalHuntersTeams,
        streakTeams,
        superStarTeams
    };
}

function calculateDuos(data) {
    const pairMap = {};
    data.matches.forEach(m => {
        [1, 2].forEach(legNumber => {
            const legPlayers = {};
            
            m.playerStats.forEach(pStat => {
                const legData = legNumber === 1 ? pStat.leg1 : pStat.leg2;
                if(legData && legData.played) {
                    if(!legPlayers[pStat.teamId]) legPlayers[pStat.teamId] = [];
                    legPlayers[pStat.teamId].push({
                        playerId: pStat.playerId,
                        playerName: pStat.playerNameSnapshot || 'Unknown',
                        goals: parseInt(legData.goals || 0),
                        assists: parseInt(legData.assists || 0)
                    });
                }
            });
            
            Object.values(legPlayers).forEach(teamPlayers => {
                if(teamPlayers.length < 2) return;
                
                for(let i = 0; i < teamPlayers.length; i++) {
                    for(let j = i + 1; j < teamPlayers.length; j++) {
                        const p1 = teamPlayers[i];
                        const p2 = teamPlayers[j];
                        const key = [p1.playerId, p2.playerId].sort().join('_');
                        
                        if(!pairMap[key]) {
                            const tm = data.teams.find(t => t.id === m.playerStats.find(ps => ps.playerId === p1.playerId)?.teamId);
                            if(tm) {
                                pairMap[key] = { 
                                    total: 0, 
                                    p1Name: p1.playerName, 
                                    p2Name: p2.playerName, 
                                    p1Id: p1.playerId,
                                    p2Id: p2.playerId,
                                    teamId: tm.id,
                                    teamName: tm.name, 
                                    teamColor: tm.color,
                                    legsTogether: 0 
                                };
                            }
                        }
                        
                        if(pairMap[key]) {
                            pairMap[key].legsTogether++;
                            const p1Contrib = p1.goals + p1.assists;
                            const p2Contrib = p2.goals + p2.assists;
                            pairMap[key].total += (p1Contrib + p2Contrib);
                        }
                    }
                }
            });
        });
    });
    
    return Object.values(pairMap).sort((a,b) => b.total - a.total);
}

function calculateOneManArmy(data) {
    const playerMap = {};

    (data.matches || []).forEach(match => {
        const legs = util.getLegNumbers(match);

        // Aggregate per match per team per player across all legs
        const contribByTeam = {}; // teamId -> { playerId -> total }
        (match.playerStats || []).forEach(pStat => {
            const teamId = pStat.teamId;
            if(!teamId) return;

            if(!contribByTeam[teamId]) contribByTeam[teamId] = {};
            const playerId = pStat.playerId;
            if(!playerId) return;

            if(!playerMap[playerId]){
                const team = (data.teams || []).find(t => t.id === teamId);
                playerMap[playerId] = {
                    id: playerId,
                    name: pStat.playerNameSnapshot || 'Unknown',
                    teamId,
                    teamName: team?.name || 'Unknown',
                    teamColor: team?.color || '#fff',
                    omaCount: 0
                };
            }

            let total = 0;
            legs.forEach(i => {
                const leg = pStat['leg'+i];
                if(leg && leg.played){
                    total += util.toInt(leg.goals || 0) + util.toInt(leg.assists || 0) + util.toInt(leg.saves || 0) + util.toInt(leg.tackles || 0);
                }
            });

            contribByTeam[teamId][playerId] = (contribByTeam[teamId][playerId] || 0) + total;
        });

        Object.entries(contribByTeam).forEach(([teamId, mp]) => {
            // Determine top contributor (single winner; tie-breaker: smallest id)
            const entries = Object.entries(mp).filter(([,v]) => (v||0) > 0);
            if(entries.length === 0) return;

            entries.sort((a,b) => (b[1]-a[1]) || String(a[0]).localeCompare(String(b[0])));
            const topContributorId = entries[0][0];

            const mvpId = match.mvpId;
            const motmId = match.motmId;

            // Pick ONE OMA winner for this team in this match
            let winner = null;
            if(mvpId && mp[mvpId] !== undefined) winner = mvpId;
            else if(motmId && mp[motmId] !== undefined) winner = motmId;
            else winner = topContributorId;

            if(winner && playerMap[winner]){
                playerMap[winner].omaCount = (playerMap[winner].omaCount || 0) + 1;
            }
        });
    });

    return Object.values(playerMap)
        .filter(p => p.omaCount > 0)
        .sort((a, b) => b.omaCount - a.omaCount);
}
// --- VIEW FUNCTIONS ---
function renderRegistry(root, data) {
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Team & Player Registry</h2>
            ${data.settings.isAdmin ? `
            <div class="admin-controls admin-only">
                <h3>Admin Tools</h3>
                <div class="flex" style="margin-top:10px;">
                    <input type="text" id="newTeamName" placeholder="Team Name" style="width:200px;">
                    <input type="color" id="newTeamColor" value="#00f0ff" style="width:50px; height:42px; padding:0;">
                    <button class="btn btn-primary" onclick="actions.addTeam()">Add Team</button>
                    <button class="btn btn-warning" onclick="modals.openTransferMarket()">Transfer Market</button>
                    <button class="btn btn-danger" onclick="modals.openSeasonControl()">Season Control</button>
                </div>
            </div>
            ` : ''}
            <div class="grid" style="grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));">
                ${data.teams.map(t => `
                    <div class="card" style="border-color:${t.color}">
                        <div class="team-card-header">
                            <div>
                                <h3 style="font-weight:900; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${t.id}')">${t.name}</h3>
                                <div class="money" style="font-size:0.9rem;">${util.formatMoney((t.value ?? 250000000))}</div>
                            </div>
                            <div>
                                ${data.settings.isAdmin ? `
                                    <button class="edit-btn-small" onclick="modals.openEditTeam('${t.id}')">Edit</button>
                                    <button class="btn btn-danger" style="padding:2px 5px; font-size:0.7rem;" onclick="actions.deleteTeam('${t.id}')">X</button>
                                ` : ''}
                            </div>
                        </div>
                        <ul style="list-style:none; margin-bottom:15px;">
                            ${data.players.filter(p => p.teamId === t.id).map(p => `
                                <li style="padding:5px 0; border-bottom:1px solid rgba(255,255,255,0.1); display:flex; justify-content:space-between; align-items:center;">
                                    <div>
                                        <span style="color:${t.color}; cursor:pointer;" class="player-clickable" onclick="event.stopPropagation();app.openProfile('${p.id}')">${p.name}</span>
                                        ${p.loanStatus ? '<span style="font-size:0.7rem; background:#ff9900; color:black; padding:0 3px; border-radius:3px; margin-left:5px;">LOAN</span>' : ''}
                                    </div>
                                    <div style="display:flex; align-items:center; gap:5px;">
                                        <span class="money" style="font-size:0.7rem;">${util.formatMoney(p.playerValue)}</span>
                                        ${data.settings.isAdmin ? `
                                            <button class="edit-btn-small" onclick="modals.openEditPlayer('${p.id}')">Edit</button>
                                            <button onclick="actions.deletePlayer('${p.id}')" style="background:none; border:none; color:#555; cursor:pointer;">x</button>
                                        ` : ''}
                                    </div>
                                </li>
                            `).join('')}
                        </ul>
                        ${data.settings.isAdmin ? `
                        <div class="admin-only">
                            <div class="flex">
                                <input type="text" id="p-name-${t.id}" placeholder="Player Name" style="font-size:0.8rem; margin:0; flex:1;">
                                <button class="btn btn-primary" style="padding:5px 10px;" onclick="actions.addPlayer('${t.id}')">+</button>
                            </div>
                            <div style="font-size:0.7rem; color:#888; margin-top:5px;">New players start at $1,000,000</div>
                        </div>
                        ` : ''}
                    </div>
                `).join('')}
            </div>
            ${data.teams.length === 0 ? '<div class="card text-center" style="margin-top:20px;"><h3>SYSTEM EMPTY</h3><p>Please login as ADMIN to add teams.</p></div>' : ''}
        </div>
    `;
}

function renderMatchCenter(root, data) {
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">EGOIST GRADING SYSTEM</h2>
            <p style="color:var(--text-dim); margin-bottom:20px;">Players are graded based on stats PER LEG (calculated only for legs played).</p>
            <div class="grid" style="grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));">
                <div class="card"><h3 class="rank-s-text">S-RANK</h3><ul><li>3.5 Goals / Leg</li><li>15 Saves / Leg</li><li>10 Tackles / Leg</li></ul></div>
                <div class="card"><h3 class="rank-a-text">A-RANK</h3><ul><li>2.5 Goals / Leg</li><li>10 Saves / Leg</li><li>7 Tackles / Leg</li></ul></div>
                <div class="card"><h3 class="rank-b-text">B-RANK</h3><ul><li>1.5 Goals / Leg</li><li>5 Saves / Leg</li><li>5 Tackles / Leg</li></ul></div>
                <div class="card"><h3 class="rank-c-text">C-RANK</h3><p>Below average metrics.</p></div>
            </div>
            
            <div style="margin-top:30px; padding:20px; background:rgba(0,240,255,0.05); border:1px solid rgba(0,240,255,0.2);">
                <h3 class="neon-text">💰 PLAYER VALUE GROWTH SYSTEM</h3>
                <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap:15px; margin-top:15px;">
                    <div class="team-stat-card">
                        <div class="team-stat-label">Starting Player Value</div>
                        <div class="team-stat-value money">${util.formatMoney(1000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Goal</div>
                        <div class="team-stat-value" style="color:var(--rank-b);">+${util.formatMoney(2000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Assist</div>
                        <div class="team-stat-value" style="color:var(--rank-b);">+${util.formatMoney(1000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Save</div>
                        <div class="team-stat-value" style="color:var(--rank-b);">+${util.formatMoney(400000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Tackle</div>
                        <div class="team-stat-value" style="color:var(--rank-b);">+${util.formatMoney(100000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">MVP/MOTM</div>
                        <div class="team-stat-value" style="color:var(--rank-s);">+${util.formatMoney(3000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Hype Vote</div>
                        <div class="team-stat-value" style="color:var(--accent);">+${util.formatMoney(100000)}</div>
                    </div>
                </div>
                <p style="margin-top:15px; color:var(--text-dim); font-size:0.9rem;">All earnings are added to player's growthValue. Player Value = Starting + Growth.</p>
            </div>
            
            <div style="margin-top:30px; padding:20px; background:rgba(0,240,255,0.05); border:1px solid rgba(0,240,255,0.2);">
                <h3 class="neon-text">🏦 TEAM ECONOMY SYSTEM</h3>
                <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap:15px; margin-top:15px;">
                    <div class="team-stat-card">
                        <div class="team-stat-label">Team Start Value</div>
                        <div class="team-stat-value">${util.formatMoney(250000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Match Win</div>
                        <div class="team-stat-value economy-win">+${util.formatMoney(15000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Match Draw</div>
                        <div class="team-stat-value economy-draw">+${util.formatMoney(5000000)}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Match Loss</div>
                        <div class="team-stat-value economy-loss">-${util.formatMoney(10000000)}</div>
                    </div>
                </div>
                <p style="margin-top:15px; color:var(--text-dim); font-size:0.9rem;">Team values are automatically updated after each match. Transfer market uses team funds.</p>
            </div>
        </div>
    `;
}

function renderFixtures(root, data) {
    const upcomingFixtures = data.fixtures.filter(f => !f.played);
    const completedFixtures = data.fixtures.filter(f => f.played);
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Fixtures</h2>
            <p style="color:var(--text-dim); margin-bottom:20px;">Upcoming matches and tournament fixtures. Click any fixture for details.</p>
            
            ${data.settings.isAdmin ? `
            <div class="admin-controls admin-only">
                <button class="btn btn-primary" onclick="modals.openFixtureCreation()">+ CREATE NEW FIXTURE</button>
                <button class="btn btn-warning" onclick="modals.openTournamentCreation()">🏆 CREATE TOURNAMENT</button>
            </div>
            ` : ''}
            
            <h3 style="color:var(--primary); margin:30px 0 15px 0;">UPCOMING FIXTURES</h3>
            ${upcomingFixtures.length === 0 ? '<p style="color:#666; text-align:center; padding:20px;">No upcoming fixtures. Create one as admin.</p>' : ''}
            <div class="fixtures-grid">
                ${upcomingFixtures.map(fixture => {
                    const teamA = data.teams.find(t => t.id === fixture.teamAId) || {name:'?', color:'#fff'};
                    const teamB = data.teams.find(t => t.id === fixture.teamBId) || {name:'?', color:'#fff'};
                    const competition = fixture.competition || 'League';
                    const round = fixture.round || 'Matchday 1';
                    const date = fixture.date || 'TBD';
                    
                    return `
                        <div class="fixture-card" onclick="app.openFixtureDetail('${fixture.id}')">
                            <div class="fixture-header">
                                <div>
                                    <h4 style="color:var(--primary);">${competition}</h4>
                                    <div style="font-size:0.8rem; color:#888;">${round}</div>
                                </div>
                                <div style="text-align:right;">
                                    <div style="font-size:0.8rem; color:#888;">${date}</div>
                                    <div class="fixture-status status-upcoming">UPCOMING</div>
                                </div>
                            </div>
                            
                            <div class="fixture-teams">
                                <div class="fixture-team">
                                    <div class="team-crest" style="color:${teamA.color}" onclick="event.stopPropagation(); app.openTeam('${teamA.id}')">${teamA.name.substring(0,2)}</div>
                                    <div class="team-name" style="color:${teamA.color}" onclick="event.stopPropagation(); app.openTeam('${teamA.id}')">${teamA.name}</div>
                                </div>
                                
                                <div class="vs-container">
                                    <div class="vs-text">VS</div>
                                </div>
                                
                                <div class="fixture-team">
                                    <div class="team-crest" style="color:${teamB.color}" onclick="event.stopPropagation(); app.openTeam('${teamB.id}')">${teamB.name.substring(0,2)}</div>
                                    <div class="team-name" style="color:${teamB.color}" onclick="event.stopPropagation(); app.openTeam('${teamB.id}')">${teamB.name}</div>
                                </div>
                            </div>
                            
                            <div class="fixture-details">
                                <div style="font-size:0.9rem;">
                                    <div><strong>Format:</strong> ${fixture.legs || 1} leg${fixture.legs > 1 ? 's' : ''}</div>
                                    ${fixture.tournamentId ? `<div><strong>Tournament:</strong> ${data.tournaments.find(t => t.id === fixture.tournamentId)?.name || 'Unknown'}</div>` : ''}
                                </div>
                            </div>
                            
                            ${data.settings.isAdmin ? `
                                <div class="fixture-controls" onclick="event.stopPropagation();">
                                    <button class="btn btn-primary" style="flex:1;" onclick="actions.playFixture('${fixture.id}')">PLAY MATCH</button>
                                    <button class="btn btn-danger" style="flex:1;" onclick="actions.deleteFixture('${fixture.id}')">DELETE</button>
                                </div>
                            ` : ''}
                        </div>
                    `;
                }).join('')}
            </div>
            
            ${completedFixtures.length > 0 ? `
                <h3 style="color:var(--primary); margin:40px 0 15px 0;">COMPLETED FIXTURES</h3>
                <div class="fixtures-grid">
                    ${completedFixtures.slice(0, 6).map(fixture => {
                        const teamA = data.teams.find(t => t.id === fixture.teamAId) || {name:'?', color:'#fff'};
                        const teamB = data.teams.find(t => t.id === fixture.teamBId) || {name:'?', color:'#fff'};
                        const match = data.matches.find(m => m.fixtureId === fixture.id);
                        
                        return `
                            <div class="fixture-card" onclick="modals.openMatchStats('${match?.id}')">
                                <div class="fixture-header">
                                    <div>
                                        <h4 style="color:var(--primary);">${fixture.competition || 'League'}</h4>
                                        <div style="font-size:0.8rem; color:#888;">${fixture.round || 'Matchday'}</div>
                                    </div>
                                    <div class="fixture-status status-completed">COMPLETED</div>
                                </div>
                                
                                <div class="fixture-teams">
                                    <div class="fixture-team">
                                        <div class="team-crest" style="color:${teamA.color}" onclick="event.stopPropagation(); app.openTeam('${teamA.id}')">${teamA.name.substring(0,2)}</div>
                                        <div class="team-name" style="color:${teamA.color}" onclick="event.stopPropagation(); app.openTeam('${teamA.id}')">${teamA.name}</div>
                                    </div>
                                    
                                    <div class="vs-container">
                                        <div class="score-board" style="font-size:1.5rem;">
                                            ${match ? (util.sumMatchScore(match,'A')) : '?'} - ${match ? (util.sumMatchScore(match,'B')) : '?'}
                                        </div>
                                    </div>
                                    
                                    <div class="fixture-team">
                                        <div class="team-crest" style="color:${teamB.color}" onclick="event.stopPropagation(); app.openTeam('${teamB.id}')">${teamB.name.substring(0,2)}</div>
                                        <div class="team-name" style="color:${teamB.color}" onclick="event.stopPropagation(); app.openTeam('${teamB.id}')">${teamB.name}</div>
                                    </div>
                                </div>
                                
                                ${match ? `
                                    <div class="fixture-details">
                                        <div style="font-size:0.9rem;">
                                            <div><strong>MVP:</strong> <span class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${match.mvpSnapshot?.playerId}')">${match.mvpSnapshot?.playerName || 'N/A'}</span></div>
                                            <div><strong>MOTM:</strong> <span class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${match.motmSnapshot?.playerId}')">${match.motmSnapshot?.playerName || 'N/A'}</span></div>
                                        </div>
                                    </div>
                                ` : ''}
                            </div>
                        `;
                    }).join('')}
                </div>
            ` : ''}
        </div>
    `;
}

function renderResults(root, data) {
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Match Results</h2>
            ${data.settings.isAdmin ? `
            <div class="admin-controls admin-only">
                <button class="btn btn-primary" onclick="modals.openMatchCreation()">+ RECORD NEW MATCH</button>
            </div>
            ` : ''}
            <div class="match-grid">
                ${data.matches.map(m => {
                    const tA = data.teams.find(t => t.id === m.teamAId) || {name:'?', color:'#fff'};
                    const tB = data.teams.find(t => t.id === m.teamBId) || {name:'?', color:'#fff'};
                    const mvpName = m.mvpSnapshot?.playerName || 'N/A';
                    const mvpId = m.mvpSnapshot?.playerId;
                    const motmName = m.motmSnapshot?.playerName || 'N/A';
                    const motmId = m.motmSnapshot?.playerId;
                    const fixture = data.fixtures.find(f => f.id === m.fixtureId);
                    const competition = fixture ? `${fixture.competition} - ${fixture.round}` : 'League Match';
                    
                    return `
                    <div class="match-card">
                        <div style="width:100%; display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
                            <span style="color:${tA.color}; font-weight:bold; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${tA.id}')">${tA.name}</span>
                            <span style="font-size:0.8rem; color:#666;">VS</span>
                            <span style="color:${tB.color}; font-weight:bold; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${tB.id}')">${tB.name}</span>
                        </div>
                        <div class="score-board">${util.sumMatchScore(m,'A')} - ${util.sumMatchScore(m,'B')}</div>
                        <div style="font-size:0.8rem; color:#888; margin-bottom:10px;">${competition}</div>
                        <div style="font-size:0.8rem; color:#888; margin-bottom:10px;">(L1: ${m.leg1ScoreA}-${m.leg1ScoreB}, L2: ${m.leg2ScoreA}-${m.leg2ScoreB})</div>
                        <div style="width:100%; border-top:1px solid #333; padding-top:10px; font-size:0.8rem;">
                            <div><span class="neon-text">MVP:</span> <span class="player-clickable" onclick="event.stopPropagation();app.openProfile('${mvpId}')">${mvpName}</span></div>
                            <div><span style="color:var(--rank-s)">MOTM:</span> <span class="player-clickable" onclick="event.stopPropagation();app.openProfile('${motmId}')">${motmName}</span></div>
                        </div>
                        <button class="stats-btn" onclick="modals.openMatchStats('${m.id}')">
                            📊 VIEW STATS
                        </button>
                        ${data.settings.isAdmin ? `<button onclick="actions.deleteMatch('${m.id}')" style="margin-top:10px; background:maroon; border:none; color:white; font-size:0.7rem; width:100%;">DELETE MATCH</button>` : ''}
                    </div>`;
                }).join('')}
            </div>
            ${data.matches.length === 0 ? '<p style="color:#666; margin-top:20px;">No matches recorded yet.</p>' : ''}
        </div>
    `;
}

function renderStandings(root, data) {
    const tableData = calculateTeamStandings(data).sort((a,b) => b.pts - a.pts || b.gd - a.gd);
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">${data.leagueName || 'League'} Standings</h2>
            <div style="overflow-x:auto;">
                <table>
                    <thead>
                        <tr>
                            <th>Rk</th>
                            <th>Team</th>
                            <th>MP</th>
                            <th>W</th>
                            <th>D</th>
                            <th>L</th>
                            <th>GF</th>
                            <th>GA</th>
                            <th>GD</th>
                            <th>PTS</th>
                            <th>Value</th>
                            <th>Form</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${tableData.map((t, idx) => `
                            <tr>
                                <td>${idx + 1}</td>
                                <td>
                                    <span style="color:${t.color}; font-weight:bold; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${t.id}')">
                                        ${t.name}
                                    </span>
                                </td>
                                <td>${t.mp}</td>
                                <td>${t.w}</td>
                                <td>${t.d}</td>
                                <td>${t.l}</td>
                                <td>${t.gf}</td>
                                <td>${t.ga}</td>
                                <td>${t.gd > 0 ? '+' : ''}${t.gd}</td>
                                <td class="neon-text">${t.pts}</td>
                                <td class="money">${util.formatMoney(t.value)}</td>
                                <td>${t.form}</td>
                            </tr>
                        `).join('')}
                    </tbody>
                </table>
            </div>
            <div style="margin-top:20px; padding:15px; background:rgba(0,240,255,0.05); border:1px solid rgba(0,240,255,0.2);">
                <h4 style="color:var(--primary); margin-bottom:10px;">📊 Team Value Distribution</h4>
                <div style="display:flex; align-items:center; gap:10px; flex-wrap:wrap;">
                    ${tableData.map((t, idx) => `
                        <div style="text-align:center; cursor:pointer;" onclick="app.openTeam('${t.id}')">
                            <div style="width:40px; height:${t.value/5000000}px; background:${t.color}; margin:0 auto;"></div>
                            <div style="font-size:0.7rem; margin-top:5px; color:${t.color}">${t.name.substring(0,3)}</div>
                            <div style="font-size:0.6rem; color:#888;">${util.formatMoney(t.value).replace('$','')}</div>
                        </div>
                    `).join('')}
                </div>
            </div>
        </div>
    `;
}

function renderTeams(root, data) {
    const teams = data.teams.map(team => {
        const players = data.players.filter(p => p.teamId === team.id);
        const matches = data.matches.filter(m => m.teamAId === team.id || m.teamBId === team.id);
        const wins = matches.filter(m => {
            const isA = m.teamAId === team.id;
            const myScore = isA ? (util.sumMatchScore(m,'A')) : 
                                 (util.sumMatchScore(m,'B'));
            const oppScore = isA ? (util.sumMatchScore(m,'B')) : 
                                 (util.sumMatchScore(m,'A'));
            return myScore > oppScore;
        }).length;
        
        const draws = matches.filter(m => {
            const isA = m.teamAId === team.id;
            const myScore = isA ? (util.sumMatchScore(m,'A')) : 
                                 (util.sumMatchScore(m,'B'));
            const oppScore = isA ? (util.sumMatchScore(m,'B')) : 
                                 (util.sumMatchScore(m,'A'));
            return myScore === oppScore;
        }).length;
        
        const losses = matches.length - wins - draws;
        
        return {
            ...team,
            playerCount: players.length,
            matches: matches.length,
            wins,
            draws,
            losses,
            totalPlayerValue: players.reduce((sum, p) => sum + p.playerValue, 0)
        };
    }).sort((a,b) => b.value - a.value);
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Teams Overview</h2>
            <p style="color:var(--text-dim); margin-bottom:20px;">Click any team to view detailed profile and roster.</p>
            <div class="grid" style="grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));">
                ${teams.map(team => `
                    <div class="card" style="border-color:${team.color}; cursor:pointer;" onclick="app.openTeam('${team.id}')">
                        <div class="team-card-header">
                            <div>
                                <h3 style="color:${team.color}; font-weight:900;">${team.name}</h3>
                                <div class="money" style="font-size:0.9rem;">${util.formatMoney(team.value)}</div>
                            </div>
                            <div style="text-align:right;">
                                <div style="font-size:0.8rem; color:#888;">${team.playerCount} players</div>
                                <div style="font-size:0.8rem; color:#888;">${team.matches} matches</div>
                            </div>
                        </div>
                        <div style="margin-top:15px;">
                            <div style="display:flex; justify-content:space-between; margin-bottom:5px;">
                                <span>Record:</span>
                                <span>${team.wins}-${team.draws}-${team.losses}</span>
                            </div>
                            <div style="display:flex; justify-content:space-between; margin-bottom:5px;">
                                <span>Avg Player Value:</span>
                                <span class="money">${util.formatMoney(Math.floor(team.totalPlayerValue / (team.playerCount || 1)))}</span>
                            </div>
                        </div>
                        <div style="margin-top:15px; padding-top:15px; border-top:1px solid rgba(255,255,255,0.1);">
                            <div style="font-size:0.8rem; color:#888;">Top Players:</div>
                            <div style="font-size:0.8rem; margin-top:5px;">
                                ${data.players.filter(p => p.teamId === team.id).slice(0,3).map(p => `
                                    <div style="display:flex; justify-content:space-between; padding:2px 0;">
                                        <span style="color:${team.color}; cursor:pointer;" class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${p.id}')">${p.name}</span>
                                        <span class="money">${util.formatMoney(p.playerValue)}</span>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    </div>
                `).join('')}
            </div>
            ${teams.length === 0 ? '<p style="color:#666; margin-top:20px;">No teams registered yet.</p>' : ''}
        </div>
    `;
}

function renderLeaderboard(root, data) {
    const stats = calculatePlayerStats(data);
    const sortBy = window.app.sortBy;
    stats.sort((a,b) => b[sortBy] - a[sortBy]);
    
    // Filter players based on search query
    const searchQuery = window.app.searchPlayerQuery.toLowerCase();
    const filteredStats = searchQuery ? 
        stats.filter(p => p.name.toLowerCase().includes(searchQuery)) : 
        stats;
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Player Leaderboard</h2>
            
            <input 
                type="text" 
                class="search-bar" 
                placeholder="Search player..." 
                oninput="window.app.searchPlayerQuery = this.value.toLowerCase(); window.app.render();"
                value="${window.app.searchPlayerQuery}"
            <div class="flex" style="margin-bottom:15px;">
                ${['goals','assists','saves','tackles','playerValue','marketValue'].map(s => `<button class="btn ${sortBy===s?'btn-primary':''}" onclick="window.app.sortBy='${s}'; window.app.render()">${s === 'marketValue' ? 'MARKET' : s === 'playerValue' ? 'VALUE' : s.toUpperCase()}</button>`).join('')}
            </div>
            
            <div class="leaderboard-container">
                <table>
                    <thead>
                        <tr>
                            <th>Rk</th>
                            <th>Player</th>
                            <th>Team</th>
                            <th>${sortBy === 'marketValue' ? 'MARKET' : sortBy === 'playerValue' ? 'VALUE' : sortBy.toUpperCase()}</th>
                            <th>Growth</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${filteredStats.length ? filteredStats.map((p, idx) => {
                            const growth = p.playerValue - p.startingValue;
                            let rankClass = '';
                            if (idx === 0) rankClass = 'gold-neon';
                            else if (idx === 1) rankClass = 'silver-neon';
                            else if (idx === 2) rankClass = 'bronze-neon';
                            
                            return `
                            <tr onclick="app.openProfile('${p.id}')" style="cursor:pointer;">
                                <td>${idx + 1}</td>
                                <td>
                                    <span class="${rankClass} player-clickable">${p.name}</span>
                                </td>
                                <td style="color:${p.teamColor}; cursor:pointer;" onclick="event.stopPropagation(); app.openTeam('${p.teamId}')" class="team-name-link">${p.teamName}</td>
                                <td class="neon-text">${sortBy === 'marketValue' || sortBy === 'playerValue' ? util.formatMoney(p[sortBy]) : p[sortBy]}</td>
                                <td class="${growth > 0 ? 'rank-b-text' : 'rank-c-text'}">${growth > 0 ? '+' : ''}${util.formatMoney(growth)}</td>
                            </tr>`;
                        }).join('') : `<tr><td colspan=\"8\"><div class=\"empty-state\">No results found</div></td></tr>`}
                    </tbody>
                </table>
            </div>
            
            <div style="margin-top:20px; padding:15px; background:rgba(255,215,0,0.05); border:1px solid rgba(255,215,0,0.2);">
                <h4 style="color:var(--rank-s); margin-bottom:10px;">💰 Player Value Growth</h4>
                <p style="color:var(--text-dim); font-size:0.9rem;">All players start at $1,000,000. Values grow with match performance (goals, assists, saves, tackles, MVP/MOTM) and hype votes.</p>
                <div style="font-size:0.8rem; color:var(--text-dim); margin-top:10px;">
                    Showing ${filteredStats.length} of ${stats.length} players
                    ${searchQuery ? ` matching "${window.app.searchPlayerQuery}"` : ''}
                </div>
            </div>
        </div>
    `;
}

function renderTeamProfile(root, data) {
    const teamId = window.app.selectedTeamId;
    const team = data.teams.find(t => t.id === teamId);
    if(!team) return window.app.nav('teams');
    
    const teamPlayers = data.players.filter(p => p.teamId === teamId);
    const playerStats = calculatePlayerStats(data);
    const teamStandings = calculateTeamStandings(data);
    const teamStanding = teamStandings.find(t => t.id === teamId);
    
    const matches = data.matches.filter(m => m.teamAId === teamId || m.teamBId === teamId);
    const recentMatches = matches.slice(-5).reverse();
    
    root.innerHTML = `
        <div class="section">
            <button onclick="window.app.nav('teams')" style="margin-bottom:20px; background:none; border:1px solid #333; color:#fff; padding:5px 10px;">&larr; BACK TO TEAMS</button>
            
            <div class="profile-header">
                <div>
                    <h1 style="color:${team.color};">${team.name}</h1>
                    <h3 style="color:#666;">TEAM PROFILE</h3>
                </div>
                <div style="text-align:right;">
                    <h2 class="money">${util.formatMoney(team.value || 250000000)}</h2>
                    <div style="font-size:0.8rem; color:#888;">Team Treasury</div>
                    ${data.settings.isAdmin ? `<button class="edit-btn-small" onclick="modals.openEditTeam('${team.id}')">Edit Team</button>` : ''}
                </div>
            </div>
            
            <div class="team-stats-grid">
                <div class="team-stat-card">
                    <div class="team-stat-label">Matches Played</div>
                    <div class="team-stat-value">${teamStanding?.mp || 0}</div>
                </div>
                <div class="team-stat-card">
                    <div class="team-stat-label">Win Rate</div>
                    <div class="team-stat-value">${teamStanding?.mp ? Math.round((teamStanding.w / teamStanding.mp) * 100) : 0}%</div>
                </div>
                <div class="team-stat-card">
                    <div class="team-stat-label">Goal Difference</div>
                    <div class="team-stat-value" style="color:${(teamStanding?.gd || 0) > 0 ? 'var(--rank-b)' : (teamStanding?.gd || 0) < 0 ? 'var(--accent)' : 'var(--text-dim)'}">
                        ${(teamStanding?.gd || 0) > 0 ? '+' : ''}${teamStanding?.gd || 0}
                    </div>
                </div>
                <div class="team-stat-card">
                    <div class="team-stat-label">Points</div>
                    <div class="team-stat-value neon-text">${teamStanding?.pts || 0}</div>
                </div>
                <div class="team-stat-card">
                    <div class="team-stat-label">Players</div>
                    <div class="team-stat-value">${teamPlayers.length}</div>
                </div>
                <div class="team-stat-card">
                    <div class="team-stat-label">Avg Player Value</div>
                    <div class="team-stat-value money">${util.formatMoney(Math.floor(teamPlayers.reduce((sum, p) => sum + p.playerValue, 0) / (teamPlayers.length || 1)))}</div>
                </div>
            </div>
            
            <div class="grid" style="grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap:20px; margin-top:20px;">
                <div class="card">
                    <h3>RECENT MATCHES</h3>
                    <div style="margin-top:15px;">
                        ${recentMatches.map(match => {
                            const isA = match.teamAId === teamId;
                            const opponent = data.teams.find(t => t.id === (isA ? match.teamBId : match.teamAId));
                            const myScore = isA ? (util.sumMatchScore(match,'A')) : 
                                                 (util.sumMatchScore(match,'B'));
                            const oppScore = isA ? (util.sumMatchScore(match,'B')) : 
                                                 (util.sumMatchScore(match,'A'));
                            const result = myScore > oppScore ? 'W' : myScore < oppScore ? 'L' : 'D';
                            const economy = myScore > oppScore ? '+$15,000,000' : myScore < oppScore ? '-$10,000,000' : '+$5,000,000';
                            
                            return `
                                <div style="padding:10px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                                    <div style="display:flex; justify-content:space-between; align-items:center;">
                                        <div>
                                            <span style="color:${opponent?.color || '#fff'}; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${opponent?.id}')">vs ${opponent?.name || 'Unknown'}</span>
                                            <div style="font-size:0.7rem; color:#888;">${myScore}-${oppScore}</div>
                                        </div>
                                        <div style="text-align:right;">
                                            <span class="form-badge ${result}">${result}</span>
                                            <div style="font-size:0.7rem; color:#888; margin-top:2px;">${economy}</div>
                                        </div>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                        ${recentMatches.length === 0 ? '<p style="color:#666; text-align:center; padding:20px;">No matches played yet.</p>' : ''}
                    </div>
                </div>
                
                <div class="card">
                    <h3>TEAM AWARDS PROGRESS</h3>
                    <div style="margin-top:15px;">
                        <div style="padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                            <span style="color:#888;">🏆 Comeback Wins:</span>
                            <span style="float:right; color:var(--accent)">${teamStanding?.comeFromBehindWins || 0}</span>
                        </div>
                        <div style="padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                            <span style="color:#888;">🧱 Defensive Actions:</span>
                            <span style="float:right;">${teamStanding?.totalTacklesSaves || 0}</span>
                        </div>
                        <div style="padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                            <span style="color:#888;">📈 Best Win Streak:</span>
                            <span style="float:right; color:var(--rank-s)">${teamStanding?.winStreak || 0}</span>
                        </div>
                        <div style="padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                            <span style="color:#888;">⚖️ Goal Distribution:</span>
                            <span style="float:right;">${Object.keys(teamStanding?.goalDistribution || {}).length} players scored</span>
                        </div>
                        <div style="padding:8px 0;">
                            <span style="color:#888;">⭐ Team Value Rank:</span>
                            <span style="float:right;" class="money">${calculateTeamStandings(data).sort((a,b) => b.value - a.value).findIndex(t => t.id === teamId) + 1} / ${calculateTeamStandings(data).length}</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="card" style="margin-top:20px;">
                <h3>PLAYER ROSTER</h3>
                <div style="overflow-x:auto;">
                    <table class="team-roster-table">
                        <thead>
                            <tr>
                                <th>Player</th>
                                <th>G</th>
                                <th>A</th>
                                <th>S</th>
                                <th>T</th>
                                <th>MP</th>
                                <th>Value</th>
                                <th>Growth</th>
                                <th></th>
                            </tr>
                        </thead>
                        <tbody>
                            ${teamPlayers.map(player => {
                                const stats = playerStats.find(p => p.id === player.id) || {goals:0, assists:0, saves:0, tackles:0, legsPlayed:0, playerValue: player.playerValue};
                                const matchesPlayed = Math.ceil((stats.legsPlayed || 0) / 2);
                                const growth = player.playerValue - player.startingValue;
                                
                                return `
                                    <tr>
                                        <td>
                                            <span style="color:${team.color}; cursor:pointer;" class="player-clickable" onclick="event.stopPropagation();app.openProfile('${player.id}')">${player.name}</span>
                                            ${player.loanStatus ? '<span style="font-size:0.7rem; background:#ff9900; color:black; padding:0 3px; border-radius:3px; margin-left:5px;">LOAN</span>' : ''}
                                        </td>
                                        <td>${stats.goals || 0}</td>
                                        <td>${stats.assists || 0}</td>
                                        <td>${stats.saves || 0}</td>
                                        <td>${stats.tackles || 0}</td>
                                        <td>${matchesPlayed}</td>
                                        <td class="money">${util.formatMoney(player.playerValue)}</td>
                                        <td class="${growth > 0 ? 'rank-b-text' : 'rank-c-text'}">${growth > 0 ? '+' : ''}${util.formatMoney(growth)}</td>
                                        <td><button class="stats-btn" onclick="window.app.openProfile('${player.id}')" style="padding:2px 8px; font-size:0.7rem;">View</button></td>
                                    </tr>
                                `;
                            }).join('')}
                        </tbody>
                    </table>
                </div>
                ${teamPlayers.length === 0 ? '<p style="color:#666; text-align:center; padding:20px;">No players in this team.</p>' : ''}
                <div style="margin-top:15px; padding-top:15px; border-top:1px solid rgba(255,255,255,0.1);">
                    <div style="display:flex; justify-content:space-between; color:#888; font-size:0.9rem;">
                        <span>Total Roster Value:</span>
                        <span class="money">${util.formatMoney(teamPlayers.reduce((sum, p) => sum + p.playerValue, 0))}</span>
                    </div>
                </div>
            </div>
            
            ${data.settings.isAdmin ? `
                <div class="admin-controls" style="margin-top:20px;">
                    <h3>Team Management (ADMIN)</h3>
                    <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px;">
                        <div>
                            <label>Team Treasury</label>
                            <div class="flex">
                                <input type="number" id="editTeamValue" value="${team.value || 250000000}" style="width:200px;" placeholder="Team Value">
                                <button class="btn btn-primary" onclick="actions.updateTeamValue('${team.id}')">Update</button>
                            </div>
                        </div>
                        <div>
                            <label>Add Funds</label>
                            <div class="flex">
                                <input type="number" id="addFunds" value="10000000" style="width:200px;" placeholder="Amount">
                                <button class="btn btn-warning" onclick="actions.addTeamFunds('${team.id}')">Add Funds</button>
                            </div>
                        </div>
                    </div>
                </div>
            ` : ''}
        </div>
    `;
}

function renderProfile(root, data) {
    const pid = window.app.selectedPlayerId;
    const player = data.players.find(p => p.id === pid);
    if(!player) return window.app.nav('leaderboard');
    const team = data.teams.find(t => t.id === player.teamId);
    const pStats = calculatePlayerStats(data).find(p => p.id === pid);
    const legs = pStats.legsPlayed || 1; 
    const av = (val) => (val / legs).toFixed(2);
    const hasVoted = localStorage.getItem(`voted_${pid}`);
    const growth = player.playerValue - player.startingValue;

    root.innerHTML = `
        <div class="section">
            <button onclick="window.app.nav('leaderboard')" style="margin-bottom:20px; background:none; border:1px solid #333; color:#fff; padding:5px 10px;">&larr; BACK</button>
            <div class="profile-header">
                <div><h1 style="color:${team.color};">${player.name}</h1><h3 style="color:#666;">${team.name} ${player.loanStatus ? '(LOAN)' : ''}</h3></div>
                ${data.settings.isAdmin ? `<button class="edit-btn-small" onclick="modals.openEditPlayer('${pid}')">Edit Player</button>` : ''}
                <button class="hype-btn" onclick="actions.hypePlayer('${pid}')" ${hasVoted ? 'disabled style="opacity:0.5"' : ''}>🔥 HYPE <span>${player.hypeCount || 0}</span></button>
            </div>
            
            ${data.settings.isAdmin ? `
                <div class="hype-controls admin-only">
                    <button class="hype-control-btn hype-add" onclick="actions.adminAddHype('${pid}')">+ Add Hype</button>
                    <button class="hype-control-btn hype-remove" onclick="actions.adminRemoveHype('${pid}')">- Remove Hype</button>
                    <button class="hype-control-btn hype-reset" onclick="actions.adminResetHype('${pid}')">Reset Hype</button>
                </div>
            ` : ''}
            
            <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap:20px; margin-bottom:20px;">
                <div class="card">
                    <h3>CURRENT VALUE</h3>
                    <div style="margin-top:15px;">
                        <div style="text-align:center;">
                            <div class="money" style="font-size:2.5rem;">${util.formatMoney(player.playerValue)}</div>
                            <div style="color:#888; font-size:0.9rem;">Current Transfer Value</div>
                        </div>
                        <div style="margin-top:15px;">
                            <div style="display:flex; justify-content:space-between; padding:5px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                                <span>Starting Value:</span>
                                <span class="money">${util.formatMoney(player.startingValue)}</span>
                            </div>
                            <div style="display:flex; justify-content:space-between; padding:5px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                                <span>Total Growth:</span>
                                <span class="money" style="color:${growth > 0 ? 'var(--rank-b)' : 'inherit'}">${growth > 0 ? '+' : ''}${util.formatMoney(growth)}</span>
                            </div>
                            <div style="display:flex; justify-content:space-between; padding:5px 0; border-bottom:1px solid rgba(255,255,255,0.1);">
                                <span>Hype Bonus:</span>
                                <span class="money">${util.formatMoney((player.hypeCount || 0) * 100000)}</span>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="card">
                    <h3>MARKET VALUE</h3>
                    <div style="text-align:center; margin-top:15px;">
                        <div class="money" style="font-size:2.5rem;">${util.formatMoney(player.playerValue)}</div>
                        <div style="color:#888; font-size:0.9rem;">Calculated Performance Value</div>
                    </div>
                    <div style="margin-top:15px; padding:15px; background:rgba(0,0,0,0.3); border-radius:5px;">
                        <div style="font-size:0.8rem; color:var(--text-dim);">Performance Earnings:</div>
                        <div style="display:flex; justify-content:space-between; padding:3px 0;">
                            <span>Goals (${pStats.goals || 0}):</span>
                            <span class="money">${util.formatMoney((pStats.goals || 0) * 2000000)}</span>
                        </div>
                        <div style="display:flex; justify-content:space-between; padding:3px 0;">
                            <span>Assists (${pStats.assists || 0}):</span>
                            <span class="money">${util.formatMoney((pStats.assists || 0) * 1000000)}</span>
                        </div>
                        <div style="display:flex; justify-content:space-between; padding:3px 0;">
                            <span>Saves (${pStats.saves || 0}):</span>
                            <span class="money">${util.formatMoney((pStats.saves || 0) * 400000)}</span>
                        </div>
                        <div style="display:flex; justify-content:space-between; padding:3px 0;">
                            <span>Tackles (${pStats.tackles || 0}):</span>
                            <span class="money">${util.formatMoney((pStats.tackles || 0) * 100000)}</span>
                        </div>
                        <div style="display:flex; justify-content:space-between; padding:3px 0;">
                            <span>MVP/MOTM (${(pStats.mvpCount || 0) + (pStats.motmCount || 0)}):</span>
                            <span class="money">${util.formatMoney(((pStats.mvpCount || 0) + (pStats.motmCount || 0)) * 3000000)}</span>
                        </div>
                    </div>
                </div>
            </div>
            
            ${player.transferHistory ? `<div style="margin-bottom:20px;"><h4>Transfer History</h4>${player.transferHistory.map(h => `<div class="history-log">${h}</div>`).join('')}</div>` : ''}
            
            <div class="card">
                <h3>LEG ANALYSIS (${pStats.legsPlayed} Legs)</h3>
                <div style="margin-top:15px; display:grid; grid-template-columns:1fr 1fr; gap:15px;">
                    <div><span style="display:block; font-size:0.8rem; color:#888;">GOALS/LEG</span><span class="${util.getClass(util.getRank(av(pStats.goals), 'goals'))}" style="font-size:1.5rem;">${av(pStats.goals)}</span></div>
                    <div><span style="display:block; font-size:0.8rem; color:#888;">ASSISTS/LEG</span><span class="rank-c-text" style="font-size:1.5rem;">${av(pStats.assists)}</span></div>
                    <div><span style="display:block; font-size:0.8rem; color:#888;">SAVES/LEG</span><span class="${util.getClass(util.getRank(av(pStats.saves), 'saves'))}" style="font-size:1.5rem;">${av(pStats.saves)}</span></div>
                    <div><span style="display:block; font-size:0.8rem; color:#888;">TACKLES/LEG</span><span class="${util.getClass(util.getRank(av(pStats.tackles), 'tackles'))}" style="font-size:1.5rem;">${av(pStats.tackles)}</span></div>
                </div>
            </div>
            
            <div class="card" style="margin-top:20px;">
                <div class="flex" style="justify-content:space-between; align-items:center;"><h3>⚖️ COMPARE</h3><select id="compareSelect" onchange="window.app.renderCompare(this.value, '${pid}')" style="width:200px;"><option value="">Select Player...</option>${data.players.filter(p => p.id !== pid).map(p => `<option value="${p.id}">${p.name}</option>`).join('')}</select></div>
                <div id="compareResult" style="margin-top:15px;" class="compare-per-leg"></div>
            </div>
            <div class="card" style="margin-top:20px;">
                <h3>MATCH HISTORY</h3>
                 ${pStats.matchLogs.map(m => `
                    <div style="border-bottom:1px solid #333; padding:10px 0; font-size:0.9rem;">
                       <span style="color:#888;">vs</span> <span style="font-weight:bold; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${data.teams.find(t=>t.name===m.opponentName)?.id}')">${m.opponentName}</span>
                       <span style="float:right;">${m.goals}G ${m.assists}A ${m.playedLeg1?'<span style="color:var(--primary); font-size:0.7rem; border:1px solid var(--primary); padding:1px 4px;">L1</span>':''} ${m.playedLeg2?'<span style="color:var(--primary); font-size:0.7rem; border:1px solid var(--primary); padding:1px 4px;">L2</span>':''}</span>
                    </div>`).join('')}
            </div>
        </div>`;
}

function renderTournament(root, data) {
    const tournaments = data.tournaments;
    
    if (window.app.selectedTournamentId) {
        const tournament = tournaments.find(t => t.id === window.app.selectedTournamentId);
        if (!tournament) {
            window.app.selectedTournamentId = null;
            window.app.render();
            return;
        }
        
        renderTournamentDetails(root, data, tournament);
        return;
    }
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Tournaments</h2>
            <p style="color:var(--text-dim); margin-bottom:20px;">Create and manage 8-team tournaments with group stage and knockout rounds.</p>
            
            ${data.settings.isAdmin ? `
            <div class="admin-controls admin-only">
                <button class="btn btn-primary" onclick="modals.openTournamentCreation()">🏆 CREATE NEW TOURNAMENT</button>
            </div>
            ` : ''}
            
            ${tournaments.length === 0 ? `
                <div class="card" style="text-align:center; padding:40px; margin-top:20px;">
                    <div style="font-size:3rem; color:#666;">🏆</div>
                    <h3 style="color:#666; margin:20px 0;">No Tournaments</h3>
                    <p style="color:var(--text-dim);">Create a tournament to get started. Tournaments feature 8 teams in group stage followed by knockout rounds.</p>
                </div>
            ` : ''}
            
            <div class="tournament-grid">
                ${tournaments.map(tournament => {
                    const champion = tournament.winner ? data.teams.find(t => t.id === tournament.winner) : null;
                    const status = tournament.completed ? 'COMPLETED' : tournament.started ? 'IN PROGRESS' : 'UPCOMING';
                    const statusClass = tournament.completed ? 'status-completed' : tournament.started ? 'status-live' : 'status-upcoming';
                    
                    return `
                        <div class="tournament-card" onclick="app.openTournament('${tournament.id}')">
                            <div class="tournament-header">
                                <div class="tournament-title">${tournament.name}</div>
                                <div class="tournament-phase">${tournament.phase || 'Group Stage'}</div>
                            </div>
                            
                            <div style="margin-top:15px;">
                                <div style="font-size:0.9rem; color:#888;">Format: ${tournament.format || '2 legs'}</div>
                                <div style="font-size:0.9rem; color:#888;">Teams: ${tournament.teams?.length || 0}/8</div>
                                <div style="font-size:0.9rem; color:#888;">Created: ${new Date(tournament.created).toLocaleDateString()}</div>
                            </div>
                            
                            <div style="margin-top:20px;">
                                <div class="fixture-status ${statusClass}" style="display:inline-block;">${status}</div>
                                ${champion ? `<div style="margin-top:10px; padding:10px; background:rgba(255,215,0,0.1); border-radius:5px; border:1px solid rgba(255,215,0,0.3);">
                                    <div style="color:var(--rank-s); font-size:0.9rem;">Champion</div>
                                    <div style="color:${champion.color}; font-weight:bold; font-size:1.1rem; cursor:pointer;" onclick="event.stopPropagation(); app.openTeam('${champion.id}')">${champion.name}</div>
                                </div>` : ''}
                            </div>
                        </div>
                    `;
                }).join('')}
            </div>
            
            ${tournaments.length > 0 ? `
                <div style="margin-top:30px; padding:20px; background:rgba(0,0,0,0.3); border-radius:8px; border:1px solid rgba(0,240,255,0.2);">
                    <h3 style="color:var(--primary);">Tournament Format</h3>
                    <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap:20px; margin-top:15px;">
                        <div>
                            <h4 style="color:var(--rank-s);">Group Stage</h4>
                            <ul style="color:var(--text-dim); margin-top:10px; padding-left:20px;">
                                <li>2 groups of 4 teams</li>
                                <li>Round robin format</li>
                                <li>Top 2 qualify for knockout</li>
                            </ul>
                        </div>
                        <div>
                            <h4 style="color:var(--rank-s);">Knockout Stage</h4>
                            <ul style="color:var(--text-dim); margin-top:10px; padding-left:20px;">
                                <li>Semi-finals</li>
                                <li>Final</li>
                                <li>Penalty shootout if draw after all legs</li>
                            </ul>
                        </div>
                        <div>
                            <h4 style="color:var(--rank-s);">Match Formats</h4>
                            <ul style="color:var(--text-dim); margin-top:10px; padding-left:20px;">
                                <li>1 leg (single match)</li>
                                <li>2 legs (home & away)</li>
                                <li>4 legs (extended series)</li>
                            </ul>
                        </div>
                    </div>
                </div>
            ` : ''}
        </div>
    `;
}

function renderTournamentDetails(root, data, tournament) {
    const groups = tournament.groups || {};
    const fixtures = data.fixtures.filter(f => f.tournamentId === tournament.id);
    const groupFixtures = fixtures.filter(f => f.stage === 'group');
    const knockoutFixtures = fixtures.filter(f => f.stage === 'knockout');
    
    // Calculate group standings
    const groupStandings = {};
    Object.keys(groups).forEach(groupName => {
        const teamIds = groups[groupName];
        const standings = teamIds.map(teamId => {
            const team = data.teams.find(t => t.id === teamId);
            const teamFixtures = groupFixtures.filter(f => 
                (f.teamAId === teamId || f.teamBId === teamId) && f.played
            );
            
            let mp = 0, w = 0, d = 0, l = 0, gf = 0, ga = 0;
            
            teamFixtures.forEach(f => {
                const match = data.matches.find(m => m.fixtureId === f.id);
                if (!match) return;
                
                const isA = match.teamAId === teamId;
                const myScore = isA ? (util.sumMatchScore(match,'A')) : 
                                     (util.sumMatchScore(match,'B'));
                const oppScore = isA ? (util.sumMatchScore(match,'B')) : 
                                     (util.sumMatchScore(match,'A'));
                
                mp++;
                gf += myScore;
                ga += oppScore;
                
                if (myScore > oppScore) w++;
                else if (myScore < oppScore) l++;
                else d++;
            });
            
            return {
                teamId,
                teamName: team?.name || 'Unknown',
                teamColor: team?.color || '#fff',
                mp, w, d, l, gf, ga,
                gd: gf - ga,
                pts: (w * 3) + d
            };
        }).sort((a, b) => b.pts - a.pts || b.gd - a.gd);
        
        groupStandings[groupName] = standings;
    });
    
    root.innerHTML = `
        <div class="section">
            <button onclick="window.app.selectedTournamentId = null; window.app.render();" style="margin-bottom:20px; background:none; border:1px solid #333; color:#fff; padding:5px 10px;">&larr; BACK TO TOURNAMENTS</button>
            
            <div class="profile-header">
                <div>
                    <h1 class="neon-text">${tournament.name}</h1>
                    <h3 style="color:#666;">${tournament.completed ? 'COMPLETED TOURNAMENT' : tournament.started ? 'TOURNAMENT IN PROGRESS' : 'UPCOMING TOURNAMENT'}</h3>
                </div>
                <div style="text-align:right;">
                    <div class="fixture-status ${tournament.completed ? 'status-completed' : tournament.started ? 'status-live' : 'status-upcoming'}" style="font-size:0.9rem;">
                        ${tournament.completed ? 'COMPLETED' : tournament.started ? 'IN PROGRESS' : 'UPCOMING'}
                    </div>
                    <div style="font-size:0.8rem; color:#888; margin-top:5px;">${tournament.teams?.length || 0}/8 teams</div>
                </div>
            </div>
            
            ${tournament.completed && tournament.winner ? `
                <div class="card" style="border-color:var(--rank-s); text-align:center; margin-bottom:20px;">
                    <div style="font-size:3rem;">🏆</div>
                    <h2 style="color:var(--rank-s);">CHAMPION</h2>
                    <h1 style="color:${data.teams.find(t => t.id === tournament.winner)?.color || '#fff'}; font-size:2.5rem; cursor:pointer;" onclick="app.openTeam('${tournament.winner}')">
                        ${data.teams.find(t => t.id === tournament.winner)?.name || 'Unknown'}
                    </h1>
                </div>
            ` : ''}
            
            <div class="grid" style="grid-template-columns: repeat(auto-fit, minmax(400px, 1fr)); gap:30px; margin-top:20px;">
                ${Object.keys(groups).map(groupName => `
                    <div class="group-container">
                        <div class="group-title">${groupName}</div>
                        <div style="overflow-x:auto;">
                            <table style="width:100%;">
                                <thead>
                                    <tr>
                                        <th style="padding:10px; text-align:left;">Team</th>
                                        <th style="padding:10px;">MP</th>
                                        <th style="padding:10px;">W</th>
                                        <th style="padding:10px;">D</th>
                                        <th style="padding:10px;">L</th>
                                        <th style="padding:10px;">GF</th>
                                        <th style="padding:10px;">GA</th>
                                        <th style="padding:10px;">GD</th>
                                        <th style="padding:10px;">PTS</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    ${groupStandings[groupName].map((team, idx) => `
                                        <tr style="${idx < 2 ? 'background:rgba(0,255,102,0.1);' : ''}">
                                            <td style="padding:10px;">
                                                <span style="color:${team.teamColor}; font-weight:bold; cursor:pointer;" class="team-name-link" onclick="app.openTeam('${team.teamId}')">${team.teamName}</span>
                                                ${idx < 2 ? '<span style="font-size:0.7rem; background:var(--rank-b); color:#000; padding:1px 4px; border-radius:2px; margin-left:5px;">Q</span>' : ''}
                                            </td>
                                            <td style="padding:10px; text-align:center;">${team.mp}</td>
                                            <td style="padding:10px; text-align:center;">${team.w}</td>
                                            <td style="padding:10px; text-align:center;">${team.d}</td>
                                            <td style="padding:10px; text-align:center;">${team.l}</td>
                                            <td style="padding:10px; text-align:center;">${team.gf}</td>
                                            <td style="padding:10px; text-align:center;">${team.ga}</td>
                                            <td style="padding:10px; text-align:center;">${team.gd > 0 ? '+' : ''}${team.gd}</td>
                                            <td style="padding:10px; text-align:center; font-weight:bold;">${team.pts}</td>
                                        </tr>
                                    `).join('')}
                                </tbody>
                            </table>
                        </div>
                    </div>
                `).join('')}
            </div>
            
            ${knockoutFixtures.length > 0 ? `
                <div style="margin-top:40px;">
                    <h3 style="color:var(--primary);">Knockout Stage</h3>
                    <div class="bracket-container">
                        <div class="bracket-round">
                            <h4 style="color:var(--rank-s); margin-bottom:15px;">Semi Finals</h4>
                            ${knockoutFixtures.filter(f => f.round === 'Semi Final').map(fixture => {
                                const teamA = data.teams.find(t => t.id === fixture.teamAId);
                                const teamB = data.teams.find(t => t.id === fixture.teamBId);
                                const match = data.matches.find(m => m.fixtureId === fixture.id);
                                
                                return `
                                    <div class="bracket-match" onclick="modals.openMatchStats('${match?.id}')">
                                        <div class="bracket-team">
                                            <div class="bracket-team-name" style="color:${teamA?.color || '#fff'}" onclick="event.stopPropagation(); app.openTeam('${teamA?.id}')">${teamA?.name || 'TBD'}</div>
                                            <div class="bracket-team-score">${match ? (util.sumMatchScore(match,'A')) : '-'}</div>
                                        </div>
                                        <div class="bracket-team">
                                            <div class="bracket-team-name" style="color:${teamB?.color || '#fff'}" onclick="event.stopPropagation(); app.openTeam('${teamB?.id}')">${teamB?.name || 'TBD'}</div>
                                            <div class="bracket-team-score">${match ? (util.sumMatchScore(match,'B')) : '-'}</div>
                                        </div>
                                        ${fixture.played ? `<div style="font-size:0.8rem; color:#888; text-align:center; margin-top:5px;">${match ? (util.sumMatchScore(match,'A')) > (util.sumMatchScore(match,'B')) ? teamA?.name + ' advances' : (util.sumMatchScore(match,'A')) < (util.sumMatchScore(match,'B')) ? teamB?.name + ' advances' : '<span class="penalty-shootout" onclick="event.stopPropagation(); actions.resolvePenalty(\''+fixture.id+'\')">PENALTY SHOOTOUT</span>' : ''}</div>` : ''}
                                    </div>
                                `;
                            }).join('')}
                        </div>
                        
                        <div class="bracket-round">
                            <h4 style="color:var(--rank-s); margin-bottom:15px;">Final</h4>
                            ${knockoutFixtures.filter(f => f.round === 'Final').map(fixture => {
                                const teamA = data.teams.find(t => t.id === fixture.teamAId);
                                const teamB = data.teams.find(t => t.id === fixture.teamBId);
                                const match = data.matches.find(m => m.fixtureId === fixture.id);
                                
                                return `
                                    <div class="bracket-match" onclick="modals.openMatchStats('${match?.id}')">
                                        <div class="bracket-team">
                                            <div class="bracket-team-name" style="color:${teamA?.color || '#fff'}" onclick="event.stopPropagation(); app.openTeam('${teamA?.id}')">${teamA?.name || 'TBD'}</div>
                                            <div class="bracket-team-score">${match ? (util.sumMatchScore(match,'A')) : '-'}</div>
                                        </div>
                                        <div class="bracket-team">
                                            <div class="bracket-team-name" style="color:${teamB?.color || '#fff'}" onclick="event.stopPropagation(); app.openTeam('${teamB?.id}')">${teamB?.name || 'TBD'}</div>
                                            <div class="bracket-team-score">${match ? (util.sumMatchScore(match,'B')) : '-'}</div>
                                        </div>
                                        ${fixture.played && match ? `
                                            <div style="text-align:center; margin-top:10px;">
                                                <div style="color:var(--rank-s); font-weight:bold;">WINNER</div>
                                                <div style="color:${(util.sumMatchScore(match,'A')) > (util.sumMatchScore(match,'B')) ? teamA?.color : (util.sumMatchScore(match,'A')) < (util.sumMatchScore(match,'B')) ? teamB?.color : '#fff'}; font-size:1.2rem; cursor:pointer;" onclick="event.stopPropagation(); app.openTeam('${(util.sumMatchScore(match,'A')) > (util.sumMatchScore(match,'B')) ? teamA?.id : (util.sumMatchScore(match,'A')) < (util.sumMatchScore(match,'B')) ? teamB?.id : ''}')">
                                                    ${(util.sumMatchScore(match,'A')) > (util.sumMatchScore(match,'B')) ? teamA?.name : (util.sumMatchScore(match,'A')) < (util.sumMatchScore(match,'B')) ? teamB?.name : 'DRAW - PENALTIES'}
                                                </div>
                                                ${(util.sumMatchScore(match,'A')) === (util.sumMatchScore(match,'B')) ? `
                                                    <div class="penalty-shootout" onclick="event.stopPropagation(); actions.resolvePenalty('${fixture.id}')">🏆 SELECT PENALTY WINNER</div>
                                                ` : ''}
                                            </div>
                                        ` : ''}
                                    </div>
                                `;
                            }).join('')}
                        </div>
                    </div>
                </div>
            ` : tournament.started ? `
                <div style="margin-top:40px; text-align:center; padding:30px; background:rgba(0,0,0,0.3); border-radius:8px;">
                    <div style="font-size:3rem; color:#666;">⚽</div>
                    <h3 style="color:var(--primary); margin:15px 0;">Group Stage in Progress</h3>
                    <p style="color:var(--text-dim);">The knockout stage will begin after all group matches are completed.</p>
                </div>
            ` : ''}
            
            ${data.settings.isAdmin && !tournament.completed ? `
                <div class="admin-controls" style="margin-top:40px;">
                    <h3>Tournament Management (ADMIN)</h3>
                    <div class="fixture-controls">
                        ${tournament.started ? `
                            ${tournament.phase === 'group' && groupFixtures.filter(f => !f.played).length === 0 ? `
                                <button class="btn btn-primary" onclick="actions.advanceTournamentToKnockout('${tournament.id}')">Advance to Knockout Stage</button>
                            ` : ''}
                            <button class="btn btn-warning" onclick="modals.generateTournamentFixtures('${tournament.id}')">Generate Missing Fixtures</button>
                        ` : tournament.teams?.length === 8 ? `
                            <button class="btn btn-primary" onclick="actions.startTournament('${tournament.id}')">Start Tournament</button>
                        ` : `
                            <p style="color:var(--text-dim);">Need 8 teams to start tournament. Currently: ${tournament.teams?.length || 0}/8</p>
                        `}
                        <button class="btn btn-danger" onclick="actions.deleteTournament('${tournament.id}')">Delete Tournament</button>
                    </div>
                </div>
            ` : ''}
        </div>
    `;
}

function renderAwards(root, data) {
    const stats = calculatePlayerStats(data);
    const topScorer = [...stats].sort((a,b) => b.goals - a.goals)[0];
    const topPlaymaker = [...stats].sort((a,b) => b.assists - a.assists)[0];
    const topGlove = [...stats].sort((a,b) => b.saves - a.saves)[0];
    const topDefender = [...stats].sort((a,b) => b.tackles - a.tackles)[0];
    const topValue = [...stats].sort((a,b) => b.marketValue - a.marketValue)[0];
    const topDuos = calculateDuos(data).slice(0, 5);
    const oneManArmyTop = calculateOneManArmy(data)[0];
    const oneManArmyTop5 = calculateOneManArmy(data).slice(0, 5);
    
    // Team Awards
    const teamAwards = calculateTeamAwards(data);
    
    // Ballon d'Or
    const teamStandings = data.teams.map(team => {
        let pts = 0;
        data.matches.forEach(m => {
            if(m.teamAId !== team.id && m.teamBId !== team.id) return;
            const isA = m.teamAId === team.id;
            const myScore = isA ? (util.sumMatchScore(m,'A')) : (util.sumMatchScore(m,'B'));
            const oppScore = isA ? (util.sumMatchScore(m,'B')) : (util.sumMatchScore(m,'A'));
            pts += (myScore > oppScore) ? 3 : (myScore < oppScore ? 0 : 1);
        });
        return { id: team.id, pts };
    }).sort((a,b) => b.pts - a.pts);

    const ballonList = stats.map(p => {
        let pts = (p.goals * 5) + (p.assists * 5) + (p.saves * 1) + (p.tackles * 0.2);
        pts += (p.mvpCount + p.motmCount) * 10;
        const teamRank = teamStandings.findIndex(t => t.id === p.teamId);
        if(teamRank === 0) pts += 20;
        if(teamRank === 1) pts += 10;
        if(teamRank === 2) pts += 5;
        if(p.id === topScorer?.id) pts += 20;
        else if(p.id === topPlaymaker?.id) pts += 20;
        else if(p.id === topGlove?.id) pts += 20;
        else if(p.id === topDefender?.id) pts += 20;
        if(p.id === oneManArmyTop?.id) pts += 15;
        return { ...p, bPoints: pts };
    }).sort((a,b) => b.bPoints - a.bPoints).slice(0, 10);

    const card = (t, i, p, s, awardType) => `<div class="card award-card" onclick="app.openAwardRanking('${awardType}')"><span class="award-icon">${i}</span><div class="award-title">${t}</div>${p?`<div class="award-winner" style="color:${p.teamColor || p.color || '#fff'}; cursor:pointer;" onclick="event.stopPropagation(); app.openProfile('${p.id}')">${p.name}</div><div style="font-size:0.8rem; color:#888;">${p.teamName || ''}</div><div class="neon-text">${s}</div>`:'<div style="color:#666">No Data</div>'}</div>`;
    
    // Award filtering
    const awardFilter = window.app.awardFilter;
    const awardSearchQuery = window.app.awardSearchQuery.toLowerCase();
    
    // Function to render award table
    const renderAwardTable = (title, teams, valueFn, formatFn, awardType) => {
        let filteredTeams = teams;
        
        // Apply search filter
        if (awardSearchQuery) {
            filteredTeams = teams.filter(team => 
                team.name.toLowerCase().includes(awardSearchQuery)
            );
        }
        
        return `
            <div class="award-section">
                <h3 style="color:var(--primary); margin-bottom:15px;">${title}</h3>
                <div class="full-award-table">
                    <div class="award-table-header">
                        Rank | Team | ${title}
                    </div>
                    ${filteredTeams.map((team, idx) => {
                        const rankClass = idx === 0 ? 'gold-neon' : idx === 1 ? 'silver-neon' : idx === 2 ? 'bronze-neon' : '';
                        return `
                            <div class="award-table-row" onclick="app.openTeam('${team.id}')">
                                <div class="award-table-rank ${rankClass}">#${idx + 1}</div>
                                <div class="award-table-team">
                                    <div style="width:10px; height:10px; background:${team.color}; border-radius:50%;"></div>
                                    <span style="color:${team.color}">${team.name}</span>
                                </div>
                                <div class="award-table-value">
                                    ${formatFn ? formatFn(valueFn(team)) : valueFn(team)}
                                </div>
                            </div>
                        `;
                    }).join('')}
                    ${filteredTeams.length === 0 ? `
                        <div style="padding:20px; text-align:center; color:var(--text-dim);">
                            No teams match your search
                        </div>
                    ` : ''}
                </div>
            </div>
        `;
    };
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text" style="text-align:center; margin-bottom:30px;">Season Awards</h2>
            
            <div class="award-filter-controls">
                <select onchange="window.app.awardFilter = this.value; window.app.render();" style="flex: 0.5;">
                    <option value="all" ${window.app.awardFilter === 'all' ? 'selected' : ''}>All Awards</option>
                    <option value="team" ${window.app.awardFilter === 'team' ? 'selected' : ''}>Team Awards</option>
                    <option value="player" ${window.app.awardFilter === 'player' ? 'selected' : ''}>Player Awards</option>
                </select>
                <input 
                    type="text" 
                    class="search-bar" 
                    placeholder="Search team name..." 
                    oninput="window.app.awardSearchQuery = this.value; window.app.render();"
                    value="${window.app.awardSearchQuery}"
                    style="flex: 1;">
            </div>
            
            ${(window.app.awardFilter === 'all' || window.app.awardFilter === 'team') ? `
            <h3 style="color:var(--primary); margin:30px 0 15px 0; text-align:center;">🏆 TEAM AWARDS</h3>
            
            <div class="awards-grid">
                ${card("MOST VALUED", "💰", teamAwards.mostValuedTeams[0], util.formatMoney(teamAwards.mostValuedTeams[0]?.value || 0), 'mostValuedTeams')}
                ${card("GERMAN MACHINE", "⚙️", teamAwards.germanMachineTeams[0], `${teamAwards.germanMachineTeams[0]?.dependency?.toFixed(1) || '0'}% dependency`, 'germanMachine')}
                ${card("REMONTADA KINGS", "🔥", teamAwards.remontadaTeams[0], `${teamAwards.remontadaTeams[0]?.comeFromBehindWins || 0} comebacks`, 'remontada')}
                ${card("THE WALL", "🧱", teamAwards.wallTeams[0], `${teamAwards.wallTeams[0]?.totalTacklesSaves || 0} T+S`, 'wall')}
                ${card("GOAL HUNTERS", "🎯", teamAwards.goalHuntersTeams[0], `GD: +${teamAwards.goalHuntersTeams[0]?.gd || 0}`, 'goalHunters')}
                ${card("WIN STREAK", "📈", teamAwards.streakTeams[0], `${teamAwards.streakTeams[0]?.winStreak || 0} wins`, 'streak')}
                ${card("SUPER STARS", "⭐", teamAwards.superStarTeams[0], `Avg: ${util.formatMoney(Math.floor(teamAwards.superStarTeams[0]?.avgValue || 0))}`, 'superStar')}
            </div>
            
            <div style="margin-top:40px;">
                ${renderAwardTable('Most Valued Team', teamAwards.mostValuedTeams, t => t.value, util.formatMoney, 'mostValuedTeams')}
                ${renderAwardTable('German Football Machine', teamAwards.germanMachineTeams, t => `${t.dependency?.toFixed(1)}% dependency`, null, 'germanMachine')}
                ${renderAwardTable('Remontada Kings', teamAwards.remontadaTeams, t => `${t.comeFromBehindWins} comebacks`, null, 'remontada')}
                ${renderAwardTable('The Wall Team', teamAwards.wallTeams, t => `${t.totalTacklesSaves} T+S`, null, 'wall')}
                ${renderAwardTable('Goal Hunters', teamAwards.goalHuntersTeams, t => `GD: +${t.gd}`, null, 'goalHunters')}
                ${renderAwardTable('Winning Streak', teamAwards.streakTeams, t => `${t.winStreak} wins`, null, 'streak')}
                ${renderAwardTable('Superstar Team', teamAwards.superStarTeams, t => util.formatMoney(Math.floor(t.avgValue)), null, 'superStar')}
            </div>
            ` : ''}
            
            ${(window.app.awardFilter === 'all' || window.app.awardFilter === 'player') ? `
            <h3 style="color:var(--primary); margin:40px 0 15px 0; text-align:center;">🌟 PLAYER AWARDS</h3>
            <div class="awards-grid">
                ${card("GOLDEN BOOT", "👟", topScorer, (topScorer?.goals||0)+" Goals", 'goldenBoot')}
                ${card("PLAYMAKER", "🎯", topPlaymaker, (topPlaymaker?.assists||0)+" Assists", 'playmaker')}
                ${card("GOLDEN GLOVES", "🧤", topGlove, (topGlove?.saves||0)+" Saves", 'goldenGloves')}
                ${card("BEST DEFENDER", "🛡️", topDefender, (topDefender?.tackles||0)+" Tackles", 'defender')}
                ${card("ONE MAN ARMY", "🐺", oneManArmyTop, (oneManArmyTop?.omaCount||0)+" Matches", 'oneManArmy')}
                <div class="card award-card" onclick="app.openAwardRanking('bestDuo')"><span class="award-icon">👥</span><div class="award-title">BEST DUO</div>${topDuos[0]?`<div class="award-winner" style="font-size:1rem;">${topDuos[0].p1Name} + ${topDuos[0].p2Name}</div><div style="font-size:0.8rem; color:#888;">${topDuos[0].teamName}</div><div class="neon-text">${topDuos[0].total.toFixed(1)} (G+A)</div>`:'<div style="color:#666">No Data</div>'}</div>
            </div>
            ` : ''}
            
            ${(window.app.awardFilter === 'all' || window.app.awardFilter === 'player') ? `
            <div style="margin-top:30px; display:grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap:20px;">
                <div class="card" style="border-color:gold;"><h3 style="color:gold; text-align:center; cursor:pointer;" onclick="app.openAwardRanking('ballonDor')">🏆 BALLON D'OR TOP 10</h3><div style="margin-top:15px;">${ballonList.map((p,i)=>`<div class="rank-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')"><div><span style="font-weight:bold; margin-right:10px;">#${i+1}</span><span style="color:${p.teamColor}; font-weight:bold;" class="player-clickable">${p.name}</span><div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div></div><div class="neon-text">${p.bPoints.toFixed(1)}</div></div>`).join('')}</div></div>
                <div class="card" style="border-color:var(--rank-s);"><h3 style="color:var(--rank-s); text-align:center;" onclick="app.openAwardRanking('mostValuable')">💰 MOST VALUABLE PLAYER</h3>${topValue?`<div style="text-align:center; margin-top:15px;"><h1 style="color:${topValue.teamColor}; font-size:2.5rem; cursor:pointer;" class="player-clickable" onclick="event.stopPropagation();app.openProfile('${topValue.id}')">${topValue.name}</h1><p class="money">${util.formatMoney(topValue.marketValue)}</p><p style="color:#888; font-size:0.8rem;">Growth: ${util.formatMoney(topValue.marketValue - topValue.startingValue)}</p></div>`:''}</div>
            </div>
            
            <div class="one-man-army-grid">
                <div class="card">
                    <h3 style="color:#ff6600; text-align:center; cursor:pointer;" onclick="app.openAwardRanking('oneManArmy')">🐺 ONE MAN ARMY TOP 5</h3>
                    <div style="margin-top:15px;">
                        ${oneManArmyTop5.map((p,i) => `
                            <div class="duo-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')">
                                <div style="display:flex; justify-content:space-between; align-items:center;">
                                    <div>
                                        <span style="font-weight:bold; color:${p.teamColor};" class="player-clickable">${p.name}</span>
                                        <div style="font-size:0.7rem; color:#888;">${p.teamName}</div>
                                    </div>
                                    <div class="neon-text">${p.omaCount} matches</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
                <div class="card">
                    <h3 style="color:var(--rank-a); text-align:center; cursor:pointer;" onclick="app.openAwardRanking('bestDuo')">👥 BEST DUOS TOP 5</h3>
                    <div style="margin-top:15px;">
                        ${topDuos.map((d,i) => `
                            <div class="duo-list-item rank-${i+1}" onclick="app.openProfile('${d.p1Id}')">
                                <div>
                                    <div style="font-weight:bold;">#${i+1}: <span class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${d.p1Id}')">${d.p1Name}</span> + <span class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${d.p2Id}')">${d.p2Name}</span></div>
                                    <div style="font-size:0.7rem; color:#888;">${d.teamName} • ${d.legsTogether} legs</div>
                                </div>
                                <div class="neon-text">${d.total.toFixed(1)} (G+A)</div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            </div>
            ` : ''}
        </div>
    `;
}

function renderArchive(root, data) {
    const archives = archiveDb.get();
    
    root.innerHTML = `
        <div class="section">
            <h2 class="neon-text">Season Archive</h2>
            <p style="color:var(--text-dim); margin-bottom:20px;">View past seasons. Only admin can archive the current season.</p>
            
            ${data.settings.isAdmin ? `
                <div class="admin-controls">
                    <h3>Archive Control</h3>
                    <p style="color:var(--text-dim); font-size:0.9rem; margin-bottom:10px;">Archive the current season to preserve its data. This will create a read-only snapshot.</p>
                    <button class="btn btn-warning" onclick="actions.archiveCurrentSeason()">📦 ARCHIVE CURRENT SEASON</button>
                </div>
            ` : ''}
            
            <div class="archive-grid">
                ${archives.map((archive, idx) => `
                    <div class="archive-card" onclick="app.openArchive('${archive.id}')">
                        ${data.settings.isAdmin ? `<button class="delete-archive-btn" onclick="event.stopPropagation(); actions.deleteArchivedSeason('${archive.id}')">DELETE</button>` : ''}
                        <div class="archive-badge">ARCHIVED</div>
                        <div class="archive-season-title">${archive.seasonName}</div>
                        <div style="color:#888; font-size:0.9rem; margin-bottom:10px;">Archived: ${new Date(archive.timestamp).toLocaleDateString()}</div>
                        
                        <div class="archive-stats">
                            <div class="archive-stat">
                                <div class="archive-stat-label">Teams</div>
                                <div class="archive-stat-value">${archive.teams?.length || 0}</div>
                            </div>
                            <div class="archive-stat">
                                <div class="archive-stat-label">Players</div>
                                <div class="archive-stat-value">${archive.players?.length || 0}</div>
                            </div>
                            <div class="archive-stat">
                                <div class="archive-stat-label">Matches</div>
                                <div class="archive-stat-value">${archive.matches?.length || 0}</div>
                            </div>
                            <div class="archive-stat">
                                <div class="archive-stat-label">Champion</div>
                                <div class="archive-stat-value">${archive.championTeam || 'N/A'}</div>
                            </div>
                        </div>
                        
                        <div style="margin-top:15px; padding-top:15px; border-top:1px solid rgba(255,255,255,0.1);">
                            <div style="font-size:0.8rem; color:#888;">Top Player:</div>
                            <div style="font-size:0.9rem; margin-top:5px;">${archive.topPlayer || 'N/A'}</div>
                        </div>
                    </div>
                `).join('')}
            </div>
            
            ${archives.length === 0 ? `
                <div class="card" style="text-align:center; padding:40px; margin-top:20px;">
                    <div style="font-size:3rem; color:#666;">📦</div>
                    <h3 style="color:#666; margin:20px 0;">No Archived Seasons</h3>
                    <p style="color:var(--text-dim);">When a season ends, admins can archive it here for historical records.</p>
                </div>
            ` : ''}
        </div>
    `;
}

function renderArchiveView(root, data) {
    const archiveId = window.app.viewingArchiveId;
    const archives = archiveDb.get();
    const archive = archives.find(a => a.id === archiveId);
    
    if(!archive) {
        window.app.nav('archive');
        return;
    }
    
    // Calculate stats from archived data
    const teamStandings = archive.teamStandings || [];
    const playerStats = archive.playerStats || [];
    const awards = archive.awards || {};
    const ballonList = archive.ballonList || [];
    
    root.innerHTML = `
        <div class="section archive-readonly">
            <button onclick="window.app.nav('archive')" style="margin-bottom:20px; background:none; border:1px solid #333; color:#fff; padding:5px 10px;">&larr; BACK TO ARCHIVE</button>
            
            <div class="archive-trophy">🏆</div>
            <h1 class="neon-text" style="text-align:center;">${archive.seasonName}</h1>
            <p style="text-align:center; color:var(--text-dim); margin-bottom:30px;">Archived Season • Read Only View</p>
            
            ${data.settings.isAdmin ? `
                <div class="admin-controls">
                    <button class="btn btn-danger" onclick="actions.deleteArchivedSeason('${archive.id}')">🗑️ DELETE THIS ARCHIVED SEASON</button>
                    <p style="color:var(--text-dim); font-size:0.8rem; margin-top:10px;">Warning: This action cannot be undone. The archived season will be permanently deleted.</p>
                </div>
            ` : ''}
            
            <div class="card" style="border-color:var(--rank-s);">
                <h3 style="color:var(--rank-s); text-align:center;">SEASON CHAMPION</h3>
                <div style="text-align:center; margin-top:20px;">
                    <h1 style="font-size:2.5rem; color:var(--rank-s);">${archive.championTeam || 'Not Recorded'}</h1>
                    ${archive.championColor ? `<div style="width:100px; height:10px; background:${archive.championColor}; margin:10px auto;"></div>` : ''}
                </div>
            </div>
            
            <div style="margin-top:30px;">
                <h3 class="neon-text">Final Standings</h3>
                <div style="overflow-x:auto; margin-top:15px;">
                    <table>
                        <thead>
                            <tr>
                                <th>Rk</th>
                                <th>Team</th>
                                <th>MP</th>
                                <th>W</th>
                                <th>D</th>
                                <th>L</th>
                                <th>GF</th>
                                <th>GA</th>
                                <th>GD</th>
                                <th>PTS</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${teamStandings.slice(0, 10).map((t, idx) => `
                                <tr>
                                    <td>${idx + 1}</td>
                                    <td style="color:${t.color || '#fff'}">${t.name}</td>
                                    <td>${t.mp || 0}</td>
                                    <td>${t.w || 0}</td>
                                    <td>${t.d || 0}</td>
                                    <td>${t.l || 0}</td>
                                    <td>${t.gf || 0}</td>
                                    <td>${t.ga || 0}</td>
                                    <td>${(t.gd || 0) > 0 ? '+' : ''}${t.gd || 0}</td>
                                    <td class="neon-text">${t.pts || 0}</td>
                                </tr>
                            `).join('')}
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div style="margin-top:30px;">
                <h3 class="neon-text">Top Players</h3>
                <div style="overflow-x:auto; margin-top:15px;">
                    <table>
                        <thead>
                            <tr>
                                <th>Rk</th>
                                <th>Player</th>
                                <th>Team</th>
                                <th>G</th>
                                <th>A</th>
                                <th>S</th>
                                <th>T</th>
                                <th>Value</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${playerStats.slice(0, 10).map((p, idx) => `
                                <tr>
                                    <td>${idx + 1}</td>
                                    <td>${p.name}</td>
                                    <td style="color:${p.teamColor || '#fff'}">${p.teamName}</td>
                                    <td>${p.goals || 0}</td>
                                    <td>${p.assists || 0}</td>
                                    <td>${p.saves || 0}</td>
                                    <td>${p.tackles || 0}</td>
                                    <td class="money">${util.formatMoney(p.marketValue || 0)}</td>
                                </tr>
                            `).join('')}
                        </tbody>
                    </table>
                </div>
            </div>
            
            ${ballonList.length > 0 ? `
            <div style="margin-top:30px;">
                <h3 class="neon-text">Ballon d'Or Top 5</h3>
                <div style="margin-top:15px;">
                    ${ballonList.slice(0, 5).map((p, idx) => `
                        <div class="rank-list-item rank-${idx + 1}">
                            <div>
                                <span style="font-weight:bold; margin-right:10px;">#${idx + 1}</span>
                                <span style="color:${p.teamColor || '#fff'}; font-weight:bold;">${p.name}</span>
                                <div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div>
                            </div>
                            <div class="neon-text">${p.bPoints?.toFixed(1) || '0'}</div>
                        </div>
                    `).join('')}
                </div>
            </div>
            ` : ''}
            
            <div style="margin-top:30px; padding:20px; background:rgba(0,0,0,0.3); border:1px solid rgba(255,215,0,0.3);">
                <h3 style="color:var(--rank-s);">Season Statistics</h3>
                <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap:15px; margin-top:15px;">
                    <div class="team-stat-card">
                        <div class="team-stat-label">Total Teams</div>
                        <div class="team-stat-value">${archive.teams?.length || 0}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Total Players</div>
                        <div class="team-stat-value">${archive.players?.length || 0}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Total Matches</div>
                        <div class="team-stat-value">${archive.matches?.length || 0}</div>
                    </div>
                    <div class="team-stat-card">
                        <div class="team-stat-label">Avg Player Value</div>
                        <div class="team-stat-value money">${archive.players ? util.formatMoney(Math.floor(archive.players.reduce((sum, p) => sum + (p.playerValue || 0), 0) / (archive.players.length || 1))) : '$0'}</div>
                    </div>
                </div>
            </div>
        </div>
    `;
}

function renderFixtureDetail(root, data) {
    const fixtureId = window.app.selectedFixtureId;
    const fixture = data.fixtures.find(f => f.id === fixtureId);
    if(!fixture) return window.app.nav('fixtures');
    
    const teamA = data.teams.find(t => t.id === fixture.teamAId) || {name:'?', color:'#fff', value:0};
    const teamB = data.teams.find(t => t.id === fixture.teamBId) || {name:'?', color:'#fff', value:0};
    const match = data.matches.find(m => m.fixtureId === fixtureId);
    
    // Head-to-head history
    const h2hMatches = data.matches.filter(m => 
        (m.teamAId === teamA.id && m.teamBId === teamB.id) || 
        (m.teamAId === teamB.id && m.teamBId === teamA.id)
    );
    
    let teamAGoals = 0, teamBGoals = 0, teamAWins = 0, teamBWins = 0, draws = 0;
    h2hMatches.forEach(m => {
        const aScore = util.sumMatchScore(m,'A');
        const bScore = util.sumMatchScore(m,'B');
        if (m.teamAId === teamA.id) {
            teamAGoals += aScore;
            teamBGoals += bScore;
            if (aScore > bScore) teamAWins++;
            else if (aScore < bScore) teamBWins++;
            else draws++;
        } else {
            teamAGoals += bScore;
            teamBGoals += aScore;
            if (bScore > aScore) teamAWins++;
            else if (bScore < aScore) teamBWins++;
            else draws++;
        }
    });
    
    // Top scorers for each team
    const playerStats = calculatePlayerStats(data);
    
    const teamATopScorers = playerStats.filter(p => p.teamId === teamA.id).sort((a,b) => b.goals - a.goals).slice(0,3);
    const teamBTopScorers = playerStats.filter(p => p.teamId === teamB.id).sort((a,b) => b.goals - a.goals).slice(0,3);
    
    // Team standings
    const standings = calculateTeamStandings(data);
    const teamAStanding = standings.find(s => s.id === teamA.id);
    const teamBStanding = standings.find(s => s.id === teamB.id);
    
    root.innerHTML = `
        <div class="section">
            <button onclick="window.app.nav('fixtures')" style="margin-bottom:20px; background:none; border:1px solid #333; color:#fff; padding:5px 10px;">&larr; BACK TO FIXTURES</button>
            
            <div class="profile-header">
                <div>
                    <h1 class="neon-text">${fixture.competition} - ${fixture.round}</h1>
                    <h3 style="color:#666;">${fixture.date || 'Date TBD'}</h3>
                </div>
                <div class="fixture-status ${fixture.played ? 'status-completed' : 'status-upcoming'}">
                    ${fixture.played ? 'COMPLETED' : 'UPCOMING'}
                </div>
            </div>
            
            <div class="card" style="border-color:var(--primary);">
                <div style="display:flex; justify-content:space-between; align-items:center; padding:20px;">
                    <div style="text-align:center; flex:1; cursor:pointer;" onclick="app.openTeam('${teamA.id}')">
                        <div class="team-crest" style="color:${teamA.color}; width:80px; height:80px; font-size:2rem; margin:0 auto 15px;">${teamA.name.substring(0,2)}</div>
                        <h2 style="color:${teamA.color};">${teamA.name}</h2>
                        <div class="money">${util.formatMoney(teamA.value)}</div>
                        <div style="color:#888;">${teamAStanding ? `PTS: ${teamAStanding.pts}` : ''}</div>
                    </div>
                    
                    <div style="text-align:center; padding:0 30px;">
                        ${fixture.played && match ? `
                            <div class="score-board" style="font-size:3rem;">${util.sumMatchScore(match,'A')} - ${util.sumMatchScore(match,'B')}</div>
                            <div style="color:#888;">Leg 1: ${match.leg1ScoreA}-${match.leg1ScoreB} | Leg 2: ${match.leg2ScoreA}-${match.leg2ScoreB}</div>
                        ` : `
                            <div class="vs-text" style="font-size:3rem;">VS</div>
                            <div>${fixture.legs || 1} leg${fixture.legs > 1 ? 's' : ''}</div>
                        `}
                    </div>
                    
                    <div style="text-align:center; flex:1; cursor:pointer;" onclick="app.openTeam('${teamB.id}')">
                        <div class="team-crest" style="color:${teamB.color}; width:80px; height:80px; font-size:2rem; margin:0 auto 15px;">${teamB.name.substring(0,2)}</div>
                        <h2 style="color:${teamB.color};">${teamB.name}</h2>
                        <div class="money">${util.formatMoney(teamB.value)}</div>
                        <div style="color:#888;">${teamBStanding ? `PTS: ${teamBStanding.pts}` : ''}</div>
                    </div>
                </div>
            </div>
            
            <div style="display:grid; grid-template-columns: 1fr 1fr; gap:20px; margin-top:30px;">
                <div class="card">
                    <h3 style="color:${teamA.color};">${teamA.name} - Top Scorers</h3>
                    <div style="margin-top:15px;">
                        ${teamATopScorers.map(p => `
                            <div style="display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.05);">
                                <span class="player-clickable" onclick="event.stopPropagation();app.openProfile('${p.id}')">${p.name}</span>
                                <span>${p.goals}G ${p.assists}A</span>
                            </div>
                        `).join('')}
                    </div>
                </div>
                <div class="card">
                    <h3 style="color:${teamB.color};">${teamB.name} - Top Scorers</h3>
                    <div style="margin-top:15px;">
                        ${teamBTopScorers.map(p => `
                            <div style="display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.05);">
                                <span class="player-clickable" onclick="event.stopPropagation();app.openProfile('${p.id}')">${p.name}</span>
                                <span>${p.goals}G ${p.assists}A</span>
                            </div>
                        `).join('')}
                    </div>
                </div>
            </div>
            
            <div class="card" style="margin-top:20px;">
                <h3>Head to Head Record</h3>
                <div style="display:flex; justify-content:space-around; margin-top:20px; text-align:center;">
                    <div>
                        <div style="color:${teamA.color}; font-size:1.5rem;">${teamAWins}</div>
                        <div>${teamA.name} Wins</div>
                    </div>
                    <div>
                        <div style="color:#888; font-size:1.5rem;">${draws}</div>
                        <div>Draws</div>
                    </div>
                    <div>
                        <div style="color:${teamB.color}; font-size:1.5rem;">${teamBWins}</div>
                        <div>${teamB.name} Wins</div>
                    </div>
                </div>
                <div style="margin-top:15px; padding:10px; background:rgba(0,0,0,0.3); border-radius:5px;">
                    <div style="display:flex; justify-content:space-between;">
                        <span>Goals Scored:</span>
                        <span><span style="color:${teamA.color};">${teamAGoals}</span> - <span style="color:${teamB.color};">${teamBGoals}</span></span>
                    </div>
                </div>
            </div>
            
            ${fixture.played && match ? `
                <div style="margin-top:20px; text-align:center;">
                    <button class="stats-btn" onclick="modals.openMatchStats('${match.id}')" style="width:auto; padding:15px 30px;">📊 VIEW FULL MATCH STATS</button>
                </div>
            ` : ''}
        </div>
    `;
}

function renderAwardRanking(root, data) {
    const awardType = window.app.selectedAward;
    const stats = calculatePlayerStats(data);
    const teamStandings = calculateTeamStandings(data);
    const teamAwards = calculateTeamAwards(data);
    const duos = calculateDuos(data);
    const oneManArmy = calculateOneManArmy(data);
    
    // Ballon d'Or
    const ballonList = stats.map(p => {
        let pts = (p.goals * 5) + (p.assists * 5) + (p.saves * 1) + (p.tackles * 0.2);
        pts += (p.mvpCount + p.motmCount) * 10;
        pts += p.hype * 0.5;
        return { ...p, bPoints: pts };
    }).sort((a,b) => b.bPoints - a.bPoints);
    
    let title = "Award Ranking";
    let content = "";
    
    if (awardType === 'ballonDor') {
        title = "Ballon d'Or Rankings";
        content = ballonList.map((p, i) => `
            <div class="rank-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${p.teamColor}; font-weight:bold;" class="player-clickable">${p.name}</span>
                    <div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div>
                </div>
                <div class="neon-text">${p.bPoints.toFixed(1)} pts</div>
            </div>
        `).join('');
    } else if (awardType === 'oneManArmy') {
        title = "One Man Army Rankings";
        content = oneManArmy.map((p, i) => `
            <div class="rank-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${p.teamColor}; font-weight:bold;" class="player-clickable">${p.name}</span>
                    <div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div>
                </div>
                <div class="neon-text">${p.omaCount} matches</div>
            </div>
        `).join('');
    } else if (awardType === 'bestDuo') {
        title = "Best Duos Rankings";
        content = duos.map((d, i) => `
            <div class="rank-list-item rank-${i+1}">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${d.teamColor}; font-weight:bold;">
                        <span class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${d.p1Id}')">${d.p1Name}</span> + 
                        <span class="player-clickable" onclick="event.stopPropagation(); app.openProfile('${d.p2Id}')">${d.p2Name}</span>
                    </span>
                    <div style="font-size:0.7rem; color:#888; margin-left:30px;">${d.teamName} • ${d.legsTogether} legs</div>
                </div>
                <div class="neon-text">${d.total.toFixed(1)} (G+A)</div>
            </div>
        `).join('');
    } else if (awardType === 'mostValuable') {
        title = "Most Valuable Players";
        const sorted = [...stats].sort((a,b) => b.marketValue - a.marketValue);
        content = sorted.map((p, i) => `
            <div class="rank-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${p.teamColor}; font-weight:bold;" class="player-clickable">${p.name}</span>
                    <div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div>
                </div>
                <div class="money">${util.formatMoney(p.marketValue)}</div>
            </div>
        `).join('');
    } else if (awardType === 'goldenBoot') {
        title = "Golden Boot Rankings";
        const sorted = [...stats].sort((a,b) => b.goals - a.goals);
        content = sorted.map((p, i) => `
            <div class="rank-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${p.teamColor}; font-weight:bold;" class="player-clickable">${p.name}</span>
                    <div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div>
                </div>
                <div class="neon-text">${p.goals} goals</div>
            </div>
        `).join('');
    } else if (awardType === 'playmaker') {
        title = "Playmaker Rankings";
        const sorted = [...stats].sort((a,b) => b.assists - a.assists);
        content = sorted.map((p, i) => `
            <div class="rank-list-item rank-${i+1}" onclick="app.openProfile('${p.id}')">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${p.teamColor}; font-weight:bold;" class="player-clickable">${p.name}</span>
                    <div style="font-size:0.7rem; color:#888; margin-left:30px;">${p.teamName}</div>
                </div>
                <div class="neon-text">${p.assists} assists</div>
            </div>
        `).join('');
    } else {
        // Team awards
        let teamList = [];
        if (awardType === 'mostValuedTeams') teamList = teamAwards.mostValuedTeams;
        else if (awardType === 'germanMachine') teamList = teamAwards.germanMachineTeams;
        else if (awardType === 'remontada') teamList = teamAwards.remontadaTeams;
        else if (awardType === 'wall') teamList = teamAwards.wallTeams;
        else if (awardType === 'goalHunters') teamList = teamAwards.goalHuntersTeams;
        else if (awardType === 'streak') teamList = teamAwards.streakTeams;
        else if (awardType === 'superStar') teamList = teamAwards.superStarTeams;
        
        content = teamList.map((t, i) => `
            <div class="rank-list-item rank-${i+1}" onclick="app.openTeam('${t.id}')">
                <div>
                    <span style="font-weight:bold; margin-right:10px;">#${i+1}</span>
                    <span style="color:${t.color}; font-weight:bold;" class="team-name-link">${t.name}</span>
                </div>
                <div class="neon-text">${awardType === 'mostValuedTeams' ? util.formatMoney(t.value) : 
                    awardType === 'germanMachine' ? t.dependency?.toFixed(1) + '%' :
                    awardType === 'remontada' ? t.comeFromBehindWins + ' comebacks' :
                    awardType === 'wall' ? t.totalTacklesSaves + ' T+S' :
                    awardType === 'goalHunters' ? 'GD: +' + t.gd :
                    awardType === 'streak' ? t.winStreak + ' wins' :
                    awardType === 'superStar' ? util.formatMoney(Math.floor(t.avgValue)) : ''}</div>
            </div>
        `).join('');
    }
    
    root.innerHTML = `
        <div class="section">
            <button onclick="window.app.nav('awards')" style="margin-bottom:20px; background:none; border:1px solid #333; color:#fff; padding:5px 10px;">&larr; BACK TO AWARDS</button>
            
            <h1 class="neon-text" style="text-align:center; margin-bottom:30px;">${title}</h1>
            
            <div class="card">
                ${content || '<p style="color:#666; text-align:center;">No data available</p>'}
            </div>
        </div>
    `;
}

// --- ACTIONS & MODALS ---
window.actions = {
    addTeam: () => {
        const name = document.getElementById('newTeamName').value;
        const color = document.getElementById('newTeamColor').value;
        if(!name) return alert("Enter team name");
        db.update(data => { 
            data.teams.push({ 
                id: util.uuid(), 
                name, 
                color, 
                value: 250000000 // $250,000,000
            }); 
            return data; 
        });
        util.notify("Team Added with $250,000,000 treasury");
    },
    deleteTeam: (id) => {
        if(!confirm("Delete Team? This deletes players too.")) return;
        db.update(data => { 
            data.teams = data.teams.filter(t => t.id !== id); 
            data.players = data.players.filter(p => p.teamId !== id); 
            return data; 
        });
        util.notify("Team Deleted");
    },
    addPlayer: (teamId) => {
        const name = document.getElementById(`p-name-${teamId}`).value;
        
        if(!name) return alert("Enter player name");
        
        db.update(data => { 
            data.players.push({ 
                id: util.uuid(), 
                name, 
                teamId, 
                startingValue: 1000000,
                growthValue: 0,
                playerValue: 1000000,
                marketValue: 1000000,
                hypeCount: 0, 
                transferCount: 0, 
                loanStatus: null, 
                transferHistory: [] 
            }); 
            return data; 
        });
        util.notify("Player Added with $1,000,000 value");
    },
    deletePlayer: (id) => {
        if(!confirm("Delete Player?")) return;
        db.update(data => { data.players = data.players.filter(p => p.id !== id); return data; });
        util.notify("Player Deleted");
    },
    deleteMatch: (id) => {
        if(!confirm("Delete Match Result?")) return;
        db.update(data => { 
            const match = data.matches.find(m => m.id === id);
            if(match) {
                // Revert player earnings first (subtract from growthValue)
                match.playerStats.forEach(pStat => {
                    const player = data.players.find(p => p.id === pStat.playerId);
                    if(player) {
                        const earnings = util.calculatePlayerEarnings(pStat, match.mvpId, match.motmId, pStat.playerId);
                        player.growthValue -= earnings;
                        recalcPlayerValue(player);
                    }
                });
                
                // Recalculate team values after deletion
                const teamA = data.teams.find(t => t.id === match.teamAId);
                const teamB = data.teams.find(t => t.id === match.teamBId);
                
                if(teamA && teamB) {
                    const totalA = util.sumMatchScore(match,'A');
        const totalB = util.sumMatchScore(match,'B');

if(totalA > totalB) {
                        teamA.value -= 15000000;
                        teamB.value += 10000000;
                    } else if(totalA < totalB) {
                        teamB.value -= 15000000;
                        teamA.value += 10000000;
                    } else {
                        teamA.value -= 5000000;
                        teamB.value -= 5000000;
                    }
                }
            }
            
            data.matches = data.matches.filter(m => m.id !== id); 
            return data; 
        });
        util.notify("Match Deleted & Values Adjusted");
    },
    hypePlayer: (pid) => {
        if(localStorage.getItem(`voted_${pid}`)) return alert("Already voted!");
        db.update(data => { 
            const p = data.players.find(x => x.id === pid); 
            if(p) {
                p.hypeCount = (p.hypeCount || 0) + 1;
                p.growthValue += 100000;
                recalcPlayerValue(p);
            }
            return data; 
        });
        localStorage.setItem(`voted_${pid}`, 'true');
        util.notify("HYPE ADDED (+ $100,000 to player value)");
    },
    adminAddHype: (pid) => {
        db.update(data => { 
            const p = data.players.find(x => x.id === pid); 
            if(p) {
                p.hypeCount = (p.hypeCount || 0) + 1;
                p.growthValue += 100000;
                recalcPlayerValue(p);
            }
            return data; 
        });
        util.notify("Admin: Hype Added (+ $100,000)");
    },
    adminRemoveHype: (pid) => {
        db.update(data => { 
            const p = data.players.find(x => x.id === pid); 
            if(p && p.hypeCount > 0) {
                p.hypeCount -= 1;
                p.growthValue -= 100000;
                recalcPlayerValue(p);
            }
            return data; 
        });
        util.notify("Admin: Hype Removed (- $100,000)");
    },
    adminResetHype: (pid) => {
        db.update(data => { 
            const p = data.players.find(x => x.id === pid); 
            if(p) {
                const hypeValue = (p.hypeCount || 0) * 100000;
                p.hypeCount = 0;
                p.growthValue -= hypeValue;
                recalcPlayerValue(p);
            }
            return data; 
        });
        util.notify("Admin: All Hype Reset");
    },
    transferPlayer: () => {
        const pid = document.getElementById('tf-player').value;
        const tid = document.getElementById('tf-newteam').value;
        if(!pid || !tid) return alert("Select player and team");
        
        db.update(data => {
            const p = data.players.find(x => x.id === pid);
            const t = data.teams.find(x => x.id === tid);
            const oldTeam = data.teams.find(x => x.id === p.teamId);
            
            if(!p || !t || !oldTeam) return data;
            
            if((p.transferCount || 0) >= 2) {
                alert("Max 2 transfers reached.");
                return data;
            } 
            
            // Transfer money logic
            const transferAmount = p.playerValue;
            
            // Check if buying team has enough funds
            if (t.value < transferAmount) {
                alert(`Insufficient funds! ${t.name} needs ${util.formatMoney(transferAmount)} but has ${util.formatMoney(t.value)}`);
                return data;
            }
            
            // Execute transfer
            t.value -= transferAmount;
            oldTeam.value += transferAmount;
            
            p.transferHistory = p.transferHistory || []; 
            p.transferHistory.push(`Transferred to ${t.name} for ${util.formatMoney(transferAmount)}`);
            p.teamId = tid; 
            p.transferCount = (p.transferCount||0)+1; 
            p.loanStatus = null;
            
            util.notify(`Transfer Complete! ${util.formatMoney(transferAmount)} exchanged`);
            return data;
        });
        
        window.modals.openTransferMarket();
    },
    loanPlayer: () => {
        const pid = document.getElementById('ln-player').value;
        const tid = document.getElementById('ln-newteam').value;
        if(!pid || !tid) return alert("Select player and team");
        
        db.update(data => {
            const p = data.players.find(x => x.id === pid);
            const t = data.teams.find(x => x.id === tid);
            const oldTeam = data.teams.find(x => x.id === p.teamId);
            
            if(!p || !t || !oldTeam) return data;
            
            // Loan money logic (10% of player value)
            const loanFee = Math.floor(p.playerValue * 0.1);
            
            // Check if loaning team has enough funds
            if (t.value < loanFee) {
                alert(`Insufficient funds! ${t.name} needs ${util.formatMoney(loanFee)} but has ${util.formatMoney(t.value)}`);
                return data;
            }
            
            // Execute loan
            t.value -= loanFee;
            oldTeam.value += loanFee;
            
            p.transferHistory = p.transferHistory || []; 
            p.transferHistory.push(`Loaned to ${t.name} for ${util.formatMoney(loanFee)} (2 legs)`);
            p.loanStatus = { originalTeamId: p.teamId, legsRemaining: 2 }; 
            p.teamId = tid;
            
            util.notify(`Loan Started! Fee: ${util.formatMoney(loanFee)}`);
            return data;
        });
        
        window.modals.openTransferMarket();
    },
    renameSeason: () => {
        const name = document.getElementById('seasonNameInp').value;
        if(name) { 
            db.update(data => { 
                data.seasonName = name; 
                return data; 
            }); 
            util.notify("Season Renamed"); 
        }
    },
    renameLeague: () => {
        const name = document.getElementById('leagueNameInp').value;
        if(name) { 
            db.update(data => { 
                data.leagueName = name; 
                return data; 
            }); 
            util.notify("League Renamed"); 
        }
    },
    resetSeason: () => {
        if(confirm("DANGER: RESET SEASON? Matches will be deleted.")) {
            db.update(data => { 
                data.matches = []; 
                data.fixtures = [];
                data.tournaments = [];
                data.players.forEach(p => { 
                    p.hypeCount = 0; 
                    p.transferCount = 0; 
                    p.loanStatus = null; 
                    p.transferHistory = []; 
                    p.startingValue = 1000000;
                    p.growthValue = 0;
                    recalcPlayerValue(p);
                }); 
                data.teams.forEach(t => {
                    t.value = 250000000; // Reset to $250,000,000
                });
                return data; 
            });
            util.notify("Season Reset"); 
            window.app.nav('registry'); 
            document.getElementById('modal-overlay').classList.add('hidden');
        }
    },
    saveEditedMatch: (matchId) => {
        const tA=document.getElementById('edit-m-teamA').value;
        const tB=document.getElementById('edit-m-teamB').value;
        const mvp=document.getElementById('edit-m-mvp').value;
        const motm=document.getElementById('edit-m-motm').value;
        
        if(!mvp || !motm) return alert("Select MVP/MOTM");
        
        const data = db.get();
        const pStats = [];
        const allPlayers = [...data.players.filter(p=>p.teamId===tA), ...data.players.filter(p=>p.teamId===tB)];
        
        allPlayers.forEach(player => {
            const pStat = {
                playerId: player.id,
                playerNameSnapshot: player.name,
                teamId: player.teamId,
                teamNameSnapshot: data.teams.find(t => t.id === player.teamId)?.name || 'Unknown',
                leg1: { played: false, goals: 0, assists: 0, saves: 0, tackles: 0 },
                leg2: { played: false, goals: 0, assists: 0, saves: 0, tackles: 0 }
            };
            
            // Leg 1 stats
            const leg1Goals = document.querySelector(`input[data-pid="${player.id}"][data-leg="1"][data-type="goals"]`)?.value || 0;
            const leg1Assists = document.querySelector(`input[data-pid="${player.id}"][data-leg="1"][data-type="assists"]`)?.value || 0;
            const leg1Saves = document.querySelector(`input[data-pid="${player.id}"][data-leg="1"][data-type="saves"]`)?.value || 0;
            const leg1Tackles = document.querySelector(`input[data-pid="${player.id}"][data-leg="1"][data-type="tackles"]`)?.value || 0;
            const leg1Played = document.querySelector(`input[data-pid="${player.id}"][data-leg="1"][data-type="played"]`)?.checked || false;
            
            if(leg1Played) {
                pStat.leg1 = {
                    played: true,
                    goals: parseInt(leg1Goals),
                    assists: parseInt(leg1Assists),
                    saves: parseInt(leg1Saves),
                    tackles: parseInt(leg1Tackles)
                };
            }
            
            // Leg 2 stats
            const leg2Goals = document.querySelector(`input[data-pid="${player.id}"][data-leg="2"][data-type="goals"]`)?.value || 0;
            const leg2Assists = document.querySelector(`input[data-pid="${player.id}"][data-leg="2"][data-type="assists"]`)?.value || 0;
            const leg2Saves = document.querySelector(`input[data-pid="${player.id}"][data-leg="2"][data-type="saves"]`)?.value || 0;
            const leg2Tackles = document.querySelector(`input[data-pid="${player.id}"][data-leg="2"][data-type="tackles"]`)?.value || 0;
            const leg2Played = document.querySelector(`input[data-pid="${player.id}"][data-leg="2"][data-type="played"]`)?.checked || false;
            
            if(leg2Played) {
                pStat.leg2 = {
                    played: true,
                    goals: parseInt(leg2Goals),
                    assists: parseInt(leg2Assists),
                    saves: parseInt(leg2Saves),
                    tackles: parseInt(leg2Tackles)
                };
            }
            
            pStats.push(pStat);
        });

        db.update(d => {
            const matchIndex = d.matches.findIndex(m => m.id === matchId);
            if(matchIndex !== -1) {
                const oldMatch = d.matches[matchIndex];
                
                // Revert old match economy and player earnings first
                const oldTeamA = d.teams.find(t => t.id === oldMatch.teamAId);
                const oldTeamB = d.teams.find(t => t.id === oldMatch.teamBId);
                
                if(oldTeamA && oldTeamB) {
                    const oldTotalA = parseInt(oldMatch.leg1ScoreA) + parseInt(oldMatch.leg2ScoreA);
                    const oldTotalB = parseInt(oldMatch.leg1ScoreB) + parseInt(oldMatch.leg2ScoreB);
                    
                    if(oldTotalA > oldTotalB) {
                        oldTeamA.value -= 15000000;
                        oldTeamB.value += 10000000;
                    } else if(oldTotalA < oldTotalB) {
                        oldTeamB.value -= 15000000;
                        oldTeamA.value += 10000000;
                    } else {
                        oldTeamA.value -= 5000000;
                        oldTeamB.value -= 5000000;
                    }
                }
                
                // Revert old player earnings
                oldMatch.playerStats.forEach(pStat => {
                    const player = d.players.find(p => p.id === pStat.playerId);
                    if(player) {
                        const oldEarnings = util.calculatePlayerEarnings(pStat, oldMatch.mvpId, oldMatch.motmId, pStat.playerId);
                        player.growthValue -= oldEarnings;
                        recalcPlayerValue(player);
                    }
                });
                
                // Update match with new data
                d.matches[matchIndex] = {
                    ...d.matches[matchIndex],
                    teamAId: tA,
                    teamBId: tB,
                    leg1ScoreA: document.getElementById('edit-m-l1-a').value || 0,
                    leg1ScoreB: document.getElementById('edit-m-l1-b').value || 0,
                    leg2ScoreA: document.getElementById('edit-m-l2-a').value || 0,
                    leg2ScoreB: document.getElementById('edit-m-l2-b').value || 0,
                    mvpId: mvp,
                    motmId: motm,
                    playerStats: pStats,
                    mvpSnapshot: { playerId: mvp, playerName: d.players.find(p => p.id === mvp)?.name || 'Unknown', teamId: tA, teamName: d.teams.find(t => t.id === tA)?.name || 'Unknown' },
                    motmSnapshot: { playerId: motm, playerName: d.players.find(p => p.id === motm)?.name || 'Unknown', teamId: tB, teamName: d.teams.find(t => t.id === tB)?.name || 'Unknown' }
                };
                
                const newMatch = d.matches[matchIndex];
                const newTeamA = d.teams.find(t => t.id === tA);
                const newTeamB = d.teams.find(t => t.id === tB);
                
                // Apply new match economy
                if(newTeamA && newTeamB) {
                    const newTotalA = parseInt(newMatch.leg1ScoreA) + parseInt(newMatch.leg2ScoreA);
                    const newTotalB = parseInt(newMatch.leg1ScoreB) + parseInt(newMatch.leg2ScoreB);
                    
                    if(newTotalA > newTotalB) {
                        newTeamA.value += 15000000;
                        newTeamB.value -= 10000000;
                    } else if(newTotalA < newTotalB) {
                        newTeamB.value += 15000000;
                        newTeamA.value -= 10000000;
                    } else {
                        newTeamA.value += 5000000;
                        newTeamB.value += 5000000;
                    }
                }
                
                // Apply new player earnings
                pStats.forEach(ps => {
                    const player = d.players.find(p => p.id === ps.playerId);
                    if(player) {
                        const newEarnings = util.calculatePlayerEarnings(ps, mvp, motm, ps.playerId);
                        player.growthValue += newEarnings;
                        recalcPlayerValue(player);
                    }
                    
                    // Handle loan status
                    if(player && player.loanStatus) {
                        let used = (ps.leg1?.played ? 1 : 0) + (ps.leg2?.played ? 1 : 0);
                        player.loanStatus.legsRemaining -= used;
                        if(player.loanStatus.legsRemaining <= 0) { 
                            player.teamId = player.loanStatus.originalTeamId; 
                            player.loanStatus = null; 
                            player.transferHistory.push("Loan Ended"); 
                            util.notify(player.name + " returned from loan"); 
                        }
                    }
                });
            }
            return d;
        });
        
        document.getElementById('stats-modal-overlay').classList.add('hidden');
        util.notify("Match Updated & Economy Adjusted");
        window.app.refresh();
    },
    updateTeamValue: (teamId) => {
        const newValue = parseInt(document.getElementById('editTeamValue').value);
        if(isNaN(newValue)) return alert("Enter valid value");
        
        db.update(data => {
            const team = data.teams.find(t => t.id === teamId);
            if(team) team.value = newValue;
            return data;
        });
        
        util.notify("Team value updated");
        window.app.render();
    },
    addTeamFunds: (teamId) => {
        const amount = parseInt(document.getElementById('addFunds').value);
        if(isNaN(amount) || amount <= 0) return alert("Enter valid amount");
        
        db.update(data => {
            const team = data.teams.find(t => t.id === teamId);
            if(team) team.value += amount;
            return data;
        });
        
        util.notify(`Added ${util.formatMoney(amount)} to team treasury`);
        window.app.render();
    },
    editTeam: (teamId, newName, newColor) => {
        if(!newName) return alert("Enter team name");
        
        db.update(data => {
            const team = data.teams.find(t => t.id === teamId);
            if(team) {
                team.name = newName;
                if(newColor) team.color = newColor;
            }
            return data;
        });
        
        util.notify("Team updated successfully");
        window.app.render();
    },
    editPlayer: (playerId, newName, newValue) => {
        if(!newName) return alert("Enter player name");
        if(isNaN(newValue)) return alert("Enter valid value");
        
        db.update(data => {
            const player = data.players.find(p => p.id === playerId);
            if(player) {
                player.name = newName;
                // Set playerValue directly, then adjust growth
                player.playerValue = parseInt(newValue);
                player.growthValue = player.playerValue - player.startingValue;
                if (player.growthValue < 0) player.growthValue = 0;
                player.marketValue = player.playerValue;
            }
            return data;
        });
        
        util.notify("Player updated successfully");
        window.app.render();
    },
    archiveCurrentSeason: () => {
        const data = db.get();
        const playerStats = calculatePlayerStats(data);
        const teamStandings = calculateTeamStandings(data);
        const teamAwards = calculateTeamAwards(data);
        
        // Calculate Ballon d'Or for archive
        const ballonList = playerStats.map(p => {
            let pts = (p.goals * 5) + (p.assists * 5) + (p.saves * 1) + (p.tackles * 0.2);
            pts += (p.mvpCount + p.motmCount) * 10;
            pts += p.hype * 0.5;
            return { ...p, bPoints: pts };
        }).sort((a,b) => b.bPoints - a.bPoints).slice(0, 10);
        
        // Find champion team
        const champion = teamStandings.sort((a,b) => b.pts - a.pts || b.gd - a.gd)[0];
        
        const archive = {
            id: util.uuid(),
            seasonName: data.seasonName,
            timestamp: Date.now(),
            teams: JSON.parse(JSON.stringify(data.teams)),
            players: JSON.parse(JSON.stringify(data.players)),
            matches: JSON.parse(JSON.stringify(data.matches)),
            teamStandings: teamStandings.map(t => ({
                id: t.id,
                name: t.name,
                color: t.color,
                mp: t.mp,
                w: t.w,
                d: t.d,
                l: t.l,
                gf: t.gf,
                ga: t.ga,
                gd: t.gd,
                pts: t.pts,
                value: t.value
            })),
            playerStats: playerStats.map(p => ({
                id: p.id,
                name: p.name,
                teamName: p.teamName,
                teamColor: p.teamColor,
                goals: p.goals,
                assists: p.assists,
                saves: p.saves,
                tackles: p.tackles,
                marketValue: p.marketValue,
                startingValue: p.startingValue,
                growthValue: p.growthValue
            })),
            awards: teamAwards,
            ballonList: ballonList,
            championTeam: champion?.name || 'Unknown',
            championColor: champion?.color || '#fff',
            topPlayer: ballonList[0]?.name || 'Unknown'
        };
        
        archiveDb.add(archive);
        util.notify(`Season "${data.seasonName}" archived successfully!`);
        window.app.nav('archive');
    },
    deleteArchivedSeason: (archiveId) => {
        if(!confirm("Are you sure you want to delete this archived season? This action cannot be undone.")) {
            return;
        }
        
        const archives = archiveDb.remove(archiveId);
        util.notify("Archived season deleted successfully");
        
        // If we're currently viewing the deleted archive, navigate back to archive list
        if (window.app.viewingArchiveId === archiveId) {
            window.app.nav('archive');
        } else {
            window.app.render();
        }
    },
    createFixture: () => {
        const teamA = document.getElementById('fx-teamA').value;
        const teamB = document.getElementById('fx-teamB').value;
        const competition = document.getElementById('fx-competition').value;
        const round = document.getElementById('fx-round').value;
        const date = document.getElementById('fx-date').value;
        const legs = parseInt(document.getElementById('fx-legs').value);
        
        if(!teamA || !teamB || teamA === teamB) return alert("Select two different teams");
        if(!competition) return alert("Select competition type");
        if(!round) return alert("Enter round/matchday");
        
        db.update(data => {
            data.fixtures.push({
                id: util.uuid(),
                teamAId: teamA,
                teamBId: teamB,
                competition,
                round,
                date,
                legs,
                played: false,
                stage: competition === 'Tournament' ? 'group' : 'league',
                tournamentId: competition === 'Tournament' ? document.getElementById('fx-tournament').value : null
            });
            return data;
        });
        
        document.getElementById('modal-overlay').classList.add('hidden');
        util.notify("Fixture created successfully");
    },
    deleteFixture: (fixtureId) => {
        if(!confirm("Delete this fixture?")) return;
        
        db.update(data => {
            data.fixtures = data.fixtures.filter(f => f.id !== fixtureId);
            return data;
        });
        
        util.notify("Fixture deleted");
    },
    playFixture: (fixtureId) => {
        const data = db.get();
        const fixture = data.fixtures.find(f => f.id === fixtureId);
        if(!fixture) return;
        
        // Open match creation with fixture data
        window.app.editingFixtureId = fixtureId;
        modals.openMatchCreationFromFixture(fixture);
    },
    createTournament: async () => {
        const name = document.getElementById('tournament-name').value;
        const format = document.getElementById('tournament-format').value;

        if(!name) return alert("Enter tournament name");
        if(window.app.selectedTeamsForTournament.length !== 8) return alert("Select exactly 8 teams for tournament");

        const teams = [...window.app.selectedTeamsForTournament];
        const shuffled = teams.sort(() => 0.5 - Math.random());
        const groupA = shuffled.slice(0, 4);
        const groupB = shuffled.slice(4, 8);

        const tournamentId = util.uuid();

        await db.update(data => {
            data.tournaments = data.tournaments || [];
            data.tournaments.push({
                id: tournamentId,
                name,
                format,
                teams: window.app.selectedTeamsForTournament,
                groups: {
                    'Group A': groupA,
                    'Group B': groupB
                },
                phase: 'group',
                started: false,
                completed: false,
                created: Date.now()
            });
            return data;
        }, "CREATE_TOURNAMENT");

        document.getElementById('modal-overlay').classList.add('hidden');
        util.notify("Tournament created! Now generate fixtures.");
        window.app.selectedTournamentId = tournamentId;
        window.app.render();
    },
    startTournament: (tournamentId) => {
        db.update(data => {
            const tournament = data.tournaments.find(t => t.id === tournamentId);
            if(tournament) {
                tournament.started = true;
            }
            return data;
        });
        
        util.notify("Tournament started!");
        window.app.render();
    },
    deleteTournament: (tournamentId) => {
        if(!confirm("Delete this tournament and all its fixtures?")) return;
        
        db.update(data => {
            // Delete tournament fixtures
            data.fixtures = data.fixtures.filter(f => f.tournamentId !== tournamentId);
            // Delete tournament
            data.tournaments = data.tournaments.filter(t => t.id !== tournamentId);
            return data;
        });
        
        util.notify("Tournament deleted");
        window.app.selectedTournamentId = null;
        window.app.render();
    },
    advanceTournamentToKnockout: (tournamentId) => {
        db.update(data => {
            const tournament = data.tournaments.find(t => t.id === tournamentId);
            if(!tournament) return data;
            
            // Calculate group winners and runners-up
            const groups = tournament.groups;
            const groupStandings = {};
            
            // Calculate standings for each group
            Object.keys(groups).forEach(groupName => {
                const teamIds = groups[groupName];
                const standings = teamIds.map(teamId => {
                    const teamFixtures = data.fixtures.filter(f => 
                        f.tournamentId === tournamentId && 
                        f.stage === 'group' &&
                        f.played &&
                        (f.teamAId === teamId || f.teamBId === teamId)
                    );
                    
                    let mp = 0, w = 0, d = 0, l = 0, gf = 0, ga = 0;
                    
                    teamFixtures.forEach(f => {
                        const match = data.matches.find(m => m.fixtureId === f.id);
                        if (!match) return;
                        
                        const isA = match.teamAId === teamId;
                        const myScore = isA ? (util.sumMatchScore(match,'A')) : 
                                             (util.sumMatchScore(match,'B'));
                        const oppScore = isA ? (util.sumMatchScore(match,'B')) : 
                                             (util.sumMatchScore(match,'A'));
                        
                        mp++;
                        gf += myScore;
                        ga += oppScore;
                        
                        if (myScore > oppScore) w++;
                        else if (myScore < oppScore) l++;
                        else d++;
                    });
                    
                    return {
                        teamId,
                        mp, w, d, l, gf, ga,
                        gd: gf - ga,
                        pts: (w * 3) + d
                    };
                }).sort((a, b) => b.pts - b.pts || b.gd - a.gd);
                
                groupStandings[groupName] = standings;
            });
            
            // Get top 2 from each group
            const groupAWinner = groupStandings['Group A'][0]?.teamId;
            const groupARunner = groupStandings['Group A'][1]?.teamId;
            const groupBWinner = groupStandings['Group B'][0]?.teamId;
            const groupBRunner = groupStandings['Group B'][1]?.teamId;
            
            // Create semi-final fixtures
            const fixtures = [
                {
                    id: util.uuid(),
                    tournamentId,
                    teamAId: groupAWinner,
                    teamBId: groupBRunner,
                    competition: 'Tournament',
                    round: 'Semi Final',
                    legs: tournament.format === '1 leg' ? 1 : tournament.format === '2 legs' ? 2 : 4,
                    played: false,
                    stage: 'knockout'
                },
                {
                    id: util.uuid(),
                    tournamentId,
                    teamAId: groupBWinner,
                    teamBId: groupARunner,
                    competition: 'Tournament',
                    round: 'Semi Final',
                    legs: tournament.format === '1 leg' ? 1 : tournament.format === '2 legs' ? 2 : 4,
                    played: false,
                    stage: 'knockout'
                }
            ];
            
            // Add to data
            data.fixtures.push(...fixtures);
            tournament.phase = 'knockout';
            
            return data;
        });
        
        util.notify("Tournament advanced to knockout stage!");
        window.app.render();
    },
    resolvePenalty: (fixtureId) => {
        db.update(data => {
            const fixture = data.fixtures.find(f => f.id === fixtureId);
            if (!fixture) return data;
            
            const match = data.matches.find(m => m.fixtureId === fixtureId);
            if (!match) return data;
            
            const teamA = data.teams.find(t => t.id === fixture.teamAId);
            const teamB = data.teams.find(t => t.id === fixture.teamBId);
            
            const winner = util.simulatePenaltyWinner(teamA, teamB);
            
            // Update tournament winner if this is final
            if (fixture.round === 'Final') {
                const tournament = data.tournaments.find(t => t.id === fixture.tournamentId);
                if (tournament) {
                    tournament.winner = winner.id;
                    tournament.completed = true;
                }
            }
            
            util.notify(`${winner.name} wins on penalties!`);
            return data;
        });
        window.app.render();
    }
};

window.modals = {
    openSeasonControl: () => {
        const data = db.get();
        const b = document.getElementById('modal-body');
        b.innerHTML = `<h2 class="neon-text">Season Control</h2>
        <div class="league-settings">
            <h3>League Settings</h3>
            <div style="margin:20px 0;">
                <label>League Name</label>
                <div class="flex">
                    <input type="text" id="leagueNameInp" value="${data.leagueName || 'Uzbekistan Super League'}">
                    <button class="btn btn-primary" onclick="actions.renameLeague()">Save</button>
                </div>
            </div>
            <div style="margin:20px 0;">
                <label>Season Name</label>
                <div class="flex">
                    <input type="text" id="seasonNameInp" value="${data.seasonName}">
                    <button class="btn btn-primary" onclick="actions.renameSeason()">Save</button>
                </div>
            </div>
        </div>
        <div style="border-top:1px solid #333; padding-top:20px;">
            <button class="btn btn-danger" style="width:100%;" onclick="actions.resetSeason()">⚠️ RESTART SEASON</button>
        </div>
        <button class="btn" style="margin-top:20px;" onclick="document.getElementById('modal-overlay').classList.add('hidden')">Close</button>`;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    openTransferMarket: () => {
        const data = db.get();
        const b = document.getElementById('modal-body');
        b.innerHTML = `
            <h2 class="neon-text">Transfer Market</h2>
            <p style="color:var(--text-dim); margin-bottom:20px;">Transfer fees use team treasury. Loans cost 10% of player value for 2 legs.</p>
            
            <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px; margin-top:20px;">
                <div class="card">
                    <h3>TRANSFER PLAYER</h3>
                    <p style="font-size:0.8rem; color:#888;">Full player value paid to selling team</p>
                    <select id="tf-player" onchange="window.modals.updateTransferInfo()">
                        <option value="">Select Player</option>
                        ${data.players.map(p => {
                            const team = data.teams.find(t => t.id === p.teamId);
                            return `<option value="${p.id}" data-value="${p.playerValue}" data-team="${team?.name}">${p.name} (${team?.name}) - ${util.formatMoney(p.playerValue)}</option>`;
                        }).join('')}
                    </select>
                    <select id="tf-newteam" onchange="window.modals.updateTransferInfo()">
                        <option value="">To Team</option>
                        ${data.teams.map(t => `<option value="${t.id}" data-funds="${t.value}">${t.name} (${util.formatMoney(t.value)})</option>`).join('')}
                    </select>
                    <div id="transfer-info" style="margin-top:10px;"></div>
                    <button class="btn btn-primary" style="width:100%; margin-top:10px;" onclick="actions.transferPlayer()">Confirm Transfer</button>
                </div>
                
                <div class="card">
                    <h3>LOAN PLAYER (2 LEGS)</h3>
                    <p style="font-size:0.8rem; color:#888;">10% of player value paid to original team</p>
                    <select id="ln-player" onchange="window.modals.updateLoanInfo()">
                        <option value="">Select Player</option>
                        ${data.players.filter(p=>!p.loanStatus).map(p => {
                            const team = data.teams.find(t => t.id === p.teamId);
                            return `<option value="${p.id}" data-value="${p.playerValue}" data-team="${team?.name}">${p.name} (${team?.name}) - ${util.formatMoney(p.playerValue)}</option>`;
                        }).join('')}
                    </select>
                    <select id="ln-newteam" onchange="window.modals.updateLoanInfo()">
                        <option value="">To Team</option>
                        ${data.teams.map(t => `<option value="${t.id}" data-funds="${t.value}">${t.name} (${util.formatMoney(t.value)})</option>`).join('')}
                    </select>
                    <div id="loan-info" style="margin-top:10px;"></div>
                    <button class="btn btn-warning" style="width:100%; margin-top:10px;" onclick="actions.loanPlayer()">Confirm Loan</button>
                </div>
            </div>
            
            <button class="btn" style="margin-top:20px;" onclick="document.getElementById('modal-overlay').classList.add('hidden')">Close</button>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    updateTransferInfo: () => {
        const playerId = document.getElementById('tf-player').value;
        const teamId = document.getElementById('tf-newteam').value;
        const infoDiv = document.getElementById('transfer-info');
        
        if(!playerId || !teamId) {
            infoDiv.innerHTML = '';
            return;
        }
        
        const playerOption = document.querySelector(`#tf-player option[value="${playerId}"]`);
        const teamOption = document.querySelector(`#tf-newteam option[value="${teamId}"]`);
        
        const playerValue = parseInt(playerOption.getAttribute('data-value'));
        const teamFunds = parseInt(teamOption.getAttribute('data-funds'));
        const playerTeam = playerOption.getAttribute('data-team');
        const targetTeam = teamOption.textContent.split(' (')[0];
        
        if(teamFunds < playerValue) {
            infoDiv.innerHTML = `<div class="insufficient-funds">❌ Insufficient funds! Need ${util.formatMoney(playerValue)} but have ${util.formatMoney(teamFunds)}</div>`;
        } else {
            infoDiv.innerHTML = `
                <div class="transfer-fee">
                    💰 Transfer Fee: ${util.formatMoney(playerValue)}<br>
                    ${targetTeam} pays → ${playerTeam}
                </div>
            `;
        }
    },
    updateLoanInfo: () => {
        const playerId = document.getElementById('ln-player').value;
        const teamId = document.getElementById('ln-newteam').value;
        const infoDiv = document.getElementById('loan-info');
        
        if(!playerId || !teamId) {
            infoDiv.innerHTML = '';
            return;
        }
        
        const playerOption = document.querySelector(`#ln-player option[value="${playerId}"]`);
        const teamOption = document.querySelector(`#ln-newteam option[value="${teamId}"]`);
        
        const playerValue = parseInt(playerOption.getAttribute('data-value'));
        const loanFee = Math.floor(playerValue * 0.1);
        const teamFunds = parseInt(teamOption.getAttribute('data-funds'));
        const playerTeam = playerOption.getAttribute('data-team');
        const targetTeam = teamOption.textContent.split(' (')[0];
        
        if(teamFunds < loanFee) {
            infoDiv.innerHTML = `<div class="insufficient-funds">❌ Insufficient funds! Need ${util.formatMoney(loanFee)} but have ${util.formatMoney(teamFunds)}</div>`;
        } else {
            infoDiv.innerHTML = `
                <div class="loan-fee">
                    💰 Loan Fee (10%): ${util.formatMoney(loanFee)}<br>
                    ${targetTeam} pays → ${playerTeam}<br>
                    ⏱️ Duration: 2 legs
                </div>
            `;
        }
    },
    openMatchCreation: () => {
        const data = db.get();
        if(data.teams.length < 2) return alert("Need 2 teams.");
        const b = document.getElementById('modal-body');
        b.innerHTML = `
            <h2 class="neon-text">Record Match</h2>
            <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px; margin-bottom:20px;">
                <div><label>Team A</label><select id="m-teamA" onchange="window.modals.renderLegPlayers()"><option value="">Select Team</option>${data.teams.map(t=>`<option value="${t.id}">${t.name} (${util.formatMoney(t.value)})</option>`).join('')}</select></div>
                <div><label>Team B</label><select id="m-teamB" onchange="window.modals.renderLegPlayers()"><option value="">Select Team</option>${data.teams.map(t=>`<option value="${t.id}">${t.name} (${util.formatMoney(t.value)})</option>`).join('')}</select></div>
            </div>
            <div style="background:rgba(0,0,0,0.3); padding:10px; margin-bottom:20px;">
                <h4>Leg Scores</h4>
                <div class="flex"><input type="number" id="m-l1-a" placeholder="Leg 1 - Team A"><input type="number" id="m-l1-b" placeholder="Leg 1 - Team B"></div>
                <div class="flex" style="margin-top:10px;"><input type="number" id="m-l2-a" placeholder="Leg 2 - Team A"><input type="number" id="m-l2-b" placeholder="Leg 2 - Team B"></div>
            </div>
            <div id="m-player-leg-stats"></div>
            <div style="margin-top:20px; text-align:right;">
                <button class="btn btn-danger" onclick="document.getElementById('modal-overlay').classList.add('hidden')">Cancel</button> 
                <button class="btn btn-primary" onclick="window.modals.saveMatch()">SAVE MATCH</button>
            </div>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    openMatchCreationFromFixture: (fixture) => {
        const data = db.get();
        const b = document.getElementById('modal-body');
        
        // Pre-select teams from fixture
        const teamAOptions = data.teams.map(t => `<option value="${t.id}" ${t.id === fixture.teamAId ? 'selected' : ''}>${t.name} (${util.formatMoney(t.value)})</option>`).join('');
        const teamBOptions = data.teams.map(t => `<option value="${t.id}" ${t.id === fixture.teamBId ? 'selected' : ''}>${t.name} (${util.formatMoney(t.value)})</option>`).join('');
        
        b.innerHTML = `
            <h2 class="neon-text">Play Fixture: ${fixture.competition} - ${fixture.round}</h2>
            <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px; margin-bottom:20px;">
                <div><label>Team A</label><select id="m-teamA" onchange="window.modals.renderLegPlayers()">${teamAOptions}</select></div>
                <div><label>Team B</label><select id="m-teamB" onchange="window.modals.renderLegPlayers()">${teamBOptions}</select></div>
            </div>
            <div style="background:rgba(0,0,0,0.3); padding:10px; margin-bottom:20px;">
                <h4>Leg Scores</h4>
                ${fixture.legs === 1 ? `
                    <div class="flex"><input type="number" id="m-l1-a" placeholder="Score - Team A"><input type="number" id="m-l1-b" placeholder="Score - Team B"></div>
                    <input type="hidden" id="m-l2-a" value="0">
                    <input type="hidden" id="m-l2-b" value="0">
                ` : fixture.legs === 2 ? `
                    <div class="flex"><input type="number" id="m-l1-a" placeholder="Leg 1 - Team A"><input type="number" id="m-l1-b" placeholder="Leg 1 - Team B"></div>
                    <div class="flex" style="margin-top:10px;"><input type="number" id="m-l2-a" placeholder="Leg 2 - Team A"><input type="number" id="m-l2-b" placeholder="Leg 2 - Team B"></div>
                ` : `
                    <div class="flex"><input type="number" id="m-l1-a" placeholder="Leg 1 - Team A"><input type="number" id="m-l1-b" placeholder="Leg 1 - Team B"></div>
                    <div class="flex" style="margin-top:10px;"><input type="number" id="m-l2-a" placeholder="Leg 2 - Team A"><input type="number" id="m-l2-b" placeholder="Leg 2 - Team B"></div>
                    <div class="flex" style="margin-top:10px;"><input type="number" id="m-l3-a" placeholder="Leg 3 - Team A"><input type="number" id="m-l3-b" placeholder="Leg 3 - Team B"></div>
                    <div class="flex" style="margin-top:10px;"><input type="number" id="m-l4-a" placeholder="Leg 4 - Team A"><input type="number" id="m-l4-b" placeholder="Leg 4 - Team B"></div>
                `}
            </div>
            <div id="m-player-leg-stats"></div>
            <div style="margin-top:20px; text-align:right;">
                <button class="btn btn-danger" onclick="document.getElementById('modal-overlay').classList.add('hidden')">Cancel</button> 
                <button class="btn btn-primary" onclick="window.modals.saveMatchFromFixture('${fixture.id}')">SAVE MATCH & COMPLETE FIXTURE</button>
            </div>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
        setTimeout(() => window.modals.renderLegPlayers(), 100);
    },
    renderLegPlayers: () => {
        const tA = document.getElementById('m-teamA').value;
        const tB = document.getElementById('m-teamB').value;
        if(!tA || !tB || tA===tB) { 
            document.getElementById('m-player-leg-stats').innerHTML='<p style="color:#666; text-align:center;">Please select two different teams.</p>'; 
            return; 
        }
        
        const data = db.get();
        const allPlayers = [...data.players.filter(p=>p.teamId===tA), ...data.players.filter(p=>p.teamId===tB)];
        
        let html = `
            <div class="leg-stats-container">
                <h3 class="leg-title">Leg 1 Stats</h3>
                <div style="display:grid; grid-template-columns: 2fr repeat(4, 1fr) auto; gap:10px; margin-bottom:15px;">
                    <div class="stat-label">Player</div>
                    <div class="stat-label">Goals</div>
                    <div class="stat-label">Assists</div>
                    <div class="stat-label">Saves</div>
                    <div class="stat-label">Tackles</div>
                    <div class="stat-label">Play Leg 1</div>
                </div>
        `;
        
        allPlayers.forEach(p => {
            const team = data.teams.find(t=>t.id===p.teamId);
            html += `
                <div class="player-leg-row">
                    <div class="player-name-col">
                        <input type="checkbox" class="leg-checkbox" id="l1-play-${p.id}" data-pid="${p.id}" data-leg="1" checked>
                        <label for="l1-play-${p.id}" style="color:${team.color}; font-weight:500;">${p.name}</label>
                    </div>
                    <input type="number" class="stat-input" id="l1-g-${p.id}" data-pid="${p.id}" data-leg="1" data-type="goals" value="0" min="0">
                    <input type="number" class="stat-input" id="l1-a-${p.id}" data-pid="${p.id}" data-leg="1" data-type="assists" value="0" min="0">
                    <input type="number" class="stat-input" id="l1-s-${p.id}" data-pid="${p.id}" data-leg="1" data-type="saves" value="0" min="0">
                    <input type="number" class="stat-input" id="l1-t-${p.id}" data-pid="${p.id}" data-leg="1" data-type="tackles" value="0" min="0">
                    <div></div>
                </div>
            `;
        });
        
        html += `
            </div>
            <div class="leg-stats-container">
                <h3 class="leg-title">Leg 2 Stats</h3>
                <div style="display:grid; grid-template-columns: 2fr repeat(4, 1fr) auto; gap:10px; margin-bottom:15px;">
                    <div class="stat-label">Player</div>
                    <div class="stat-label">Goals</div>
                    <div class="stat-label">Assists</div>
                    <div class="stat-label">Saves</div>
                    <div class="stat-label">Tackles</div>
                    <div class="stat-label">Play Leg 2</div>
                </div>
        `;
        
        allPlayers.forEach(p => {
            const team = data.teams.find(t=>t.id===p.teamId);
            html += `
                <div class="player-leg-row">
                    <div class="player-name-col">
                        <input type="checkbox" class="leg-checkbox" id="l2-play-${p.id}" data-pid="${p.id}" data-leg="2" checked>
                        <label for="l2-play-${p.id}" style="color:${team.color}; font-weight:500;">${p.name}</label>
                    </div>
                    <input type="number" class="stat-input" id="l2-g-${p.id}" data-pid="${p.id}" data-leg="2" data-type="goals" value="0" min="0">
                    <input type="number" class="stat-input" id="l2-a-${p.id}" data-pid="${p.id}" data-leg="2" data-type="assists" value="0" min="0">
                    <input type="number" class="stat-input" id="l2-s-${p.id}" data-pid="${p.id}" data-leg="2" data-type="saves" value="0" min="0">
                    <input type="number" class="stat-input" id="l2-t-${p.id}" data-pid="${p.id}" data-leg="2" data-type="tackles" value="0" min="0">
                    <div></div>
                </div>
            `;
        });
        
        html += `
            </div>
            <div class="grid" style="grid-template-columns:1fr 1fr; margin-top:20px;">
                <div><label>MVP</label><select id="m-mvp"><option value="">Select MVP</option>${allPlayers.map(p=>`<option value="${p.id}">${p.name}</option>`).join('')}</select></div>
                <div><label>MOTM</label><select id="m-motm"><option value="">Select MOTM</option>${allPlayers.map(p=>`<option value="${p.id}">${p.name}</option>`).join('')}</select></div>
            </div>
        `;
        
        document.getElementById('m-player-leg-stats').innerHTML = html;
    },
    saveMatch: () => {
        const tA = document.getElementById('m-teamA').value;
        const tB = document.getElementById('m-teamB').value;
        const mvp = document.getElementById('m-mvp').value;
        const motm = document.getElementById('m-motm').value;
        
        if(!mvp || !motm) return alert("Select MVP and MOTM");
        
        const data = db.get();
        const pStats = [];
        const allPlayers = [...data.players.filter(p=>p.teamId===tA), ...data.players.filter(p=>p.teamId===tB)];
        
        allPlayers.forEach(player => {
            const pStat = {
                playerId: player.id,
                playerNameSnapshot: player.name,
                teamId: player.teamId,
                teamNameSnapshot: data.teams.find(t => t.id === player.teamId)?.name || 'Unknown',
                leg1: { played: false, goals: 0, assists: 0, saves: 0, tackles: 0 },
                leg2: { played: false, goals: 0, assists: 0, saves: 0, tackles: 0 }
            };
            
            // Leg 1 stats
            const leg1Played = document.getElementById(`l1-play-${player.id}`)?.checked || false;
            if(leg1Played) {
                pStat.leg1 = {
                    played: true,
                    goals: parseInt(document.getElementById(`l1-g-${player.id}`)?.value || 0),
                    assists: parseInt(document.getElementById(`l1-a-${player.id}`)?.value || 0),
                    saves: parseInt(document.getElementById(`l1-s-${player.id}`)?.value || 0),
                    tackles: parseInt(document.getElementById(`l1-t-${player.id}`)?.value || 0)
                };
            }
            
            // Leg 2 stats
            const leg2Played = document.getElementById(`l2-play-${player.id}`)?.checked || false;
            if(leg2Played) {
                pStat.leg2 = {
                    played: true,
                    goals: parseInt(document.getElementById(`l2-g-${player.id}`)?.value || 0),
                    assists: parseInt(document.getElementById(`l2-a-${player.id}`)?.value || 0),
                    saves: parseInt(document.getElementById(`l2-s-${player.id}`)?.value || 0),
                    tackles: parseInt(document.getElementById(`l2-t-${player.id}`)?.value || 0)
                };
            }
            
            pStats.push(pStat);
        });

        db.update(d => {
            const matchId = util.uuid();
            d.matches.push({
                id: matchId,
                teamAId: tA,
                teamBId: tB,
                leg1ScoreA: document.getElementById('m-l1-a').value || 0,
                leg1ScoreB: document.getElementById('m-l1-b').value || 0,
                leg2ScoreA: document.getElementById('m-l2-a').value || 0,
                leg2ScoreB: document.getElementById('m-l2-b').value || 0,
                mvpId: mvp,
                motmId: motm,
                mvpSnapshot: { playerId: mvp, playerName: d.players.find(p => p.id === mvp)?.name || 'Unknown', teamId: tA, teamName: d.teams.find(t => t.id === tA)?.name || 'Unknown' },
                motmSnapshot: { playerId: motm, playerName: d.players.find(p => p.id === motm)?.name || 'Unknown', teamId: tB, teamName: d.teams.find(t => t.id === tB)?.name || 'Unknown' },
                playerStats: pStats,
                timestamp: Date.now()
            });
            
            // Update team values based on match result
            const teamA = d.teams.find(t => t.id === tA);
            const teamB = d.teams.find(t => t.id === tB);
            
            if(teamA && teamB) {
                const totalA = parseInt(document.getElementById('m-l1-a').value || 0) + 
                              parseInt(document.getElementById('m-l2-a').value || 0);
                const totalB = parseInt(document.getElementById('m-l1-b').value || 0) + 
                              parseInt(document.getElementById('m-l2-b').value || 0);
                
                if(totalA > totalB) {
                    teamA.value += 15000000;
                    teamB.value -= 10000000;
                } else if(totalA < totalB) {
                    teamB.value += 15000000;
                    teamA.value -= 10000000;
                } else {
                    teamA.value += 5000000;
                    teamB.value += 5000000;
                }
            }
            
            // Update player values with earnings (add to growthValue)
            pStats.forEach(ps => {
                const p = d.players.find(x=>x.id===ps.playerId);
                if(p) {
                    const earnings = util.calculatePlayerEarnings(ps, mvp, motm, ps.playerId);
                    p.growthValue += earnings;
                    recalcPlayerValue(p);
                }
                
                if(p && p.loanStatus) {
                    let used = (ps.leg1?.played ? 1 : 0) + (ps.leg2?.played ? 1 : 0);
                    p.loanStatus.legsRemaining -= used;
                    if(p.loanStatus.legsRemaining <= 0) { 
                        p.teamId = p.loanStatus.originalTeamId; 
                        p.loanStatus = null; 
                        p.transferHistory.push("Loan Ended"); 
                        util.notify(p.name + " returned from loan"); 
                    }
                }
            });
            return d;
        });
        
        document.getElementById('modal-overlay').classList.add('hidden'); 
        util.notify("Match Saved & Player Values Updated");
    },
    saveMatchFromFixture: (fixtureId) => {
        const tA = document.getElementById('m-teamA').value;
        const tB = document.getElementById('m-teamB').value;
        const mvp = document.getElementById('m-mvp').value;
        const motm = document.getElementById('m-motm').value;
        
        if(!mvp || !motm) return alert("Select MVP and MOTM");
        
        const data = db.get();
        const fixture = data.fixtures.find(f => f.id === fixtureId);
        if(!fixture) return alert("Fixture not found");
        
        const pStats = [];
        const allPlayers = [...data.players.filter(p=>p.teamId===tA), ...data.players.filter(p=>p.teamId===tB)];
        
        allPlayers.forEach(player => {
            const pStat = {
                playerId: player.id,
                playerNameSnapshot: player.name,
                teamId: player.teamId,
                teamNameSnapshot: data.teams.find(t => t.id === player.teamId)?.name || 'Unknown',
                leg1: { played: false, goals: 0, assists: 0, saves: 0, tackles: 0 },
                leg2: { played: false, goals: 0, assists: 0, saves: 0, tackles: 0 }
            };
            
            // Leg 1 stats
            const leg1Played = document.getElementById(`l1-play-${player.id}`)?.checked || false;
            if(leg1Played) {
                pStat.leg1 = {
                    played: true,
                    goals: parseInt(document.getElementById(`l1-g-${player.id}`)?.value || 0),
                    assists: parseInt(document.getElementById(`l1-a-${player.id}`)?.value || 0),
                    saves: parseInt(document.getElementById(`l1-s-${player.id}`)?.value || 0),
                    tackles: parseInt(document.getElementById(`l1-t-${player.id}`)?.value || 0)
                };
            }
            
            // Leg 2 stats
            const leg2Played = document.getElementById(`l2-play-${player.id}`)?.checked || false;
            if(leg2Played) {
                pStat.leg2 = {
                    played: true,
                    goals: parseInt(document.getElementById(`l2-g-${player.id}`)?.value || 0),
                    assists: parseInt(document.getElementById(`l2-a-${player.id}`)?.value || 0),
                    saves: parseInt(document.getElementById(`l2-s-${player.id}`)?.value || 0),
                    tackles: parseInt(document.getElementById(`l2-t-${player.id}`)?.value || 0)
                };
            }
            
            pStats.push(pStat);
        });

        db.update(d => {
            const matchId = util.uuid();
            d.matches.push({
                id: matchId,
                teamAId: tA,
                teamBId: tB,
                leg1ScoreA: document.getElementById('m-l1-a').value || 0,
                leg1ScoreB: document.getElementById('m-l1-b').value || 0,
                leg2ScoreA: document.getElementById('m-l2-a').value || 0,
                leg2ScoreB: document.getElementById('m-l2-b').value || 0,
                mvpId: mvp,
                motmId: motm,
                mvpSnapshot: { playerId: mvp, playerName: d.players.find(p => p.id === mvp)?.name || 'Unknown', teamId: tA, teamName: d.teams.find(t => t.id === tA)?.name || 'Unknown' },
                motmSnapshot: { playerId: motm, playerName: d.players.find(p => p.id === motm)?.name || 'Unknown', teamId: tB, teamName: d.teams.find(t => t.id === tB)?.name || 'Unknown' },
                playerStats: pStats,
                fixtureId: fixtureId,
                timestamp: Date.now()
            });
            
            // Mark fixture as played
            const fixtureIndex = d.fixtures.findIndex(f => f.id === fixtureId);
            if(fixtureIndex !== -1) {
                d.fixtures[fixtureIndex].played = true;
            }
            
            // Update team values based on match result
            const teamA = d.teams.find(t => t.id === tA);
            const teamB = d.teams.find(t => t.id === tB);
            
            if(teamA && teamB) {
                const totalA = parseInt(document.getElementById('m-l1-a').value || 0) + 
                              parseInt(document.getElementById('m-l2-a').value || 0);
                const totalB = parseInt(document.getElementById('m-l1-b').value || 0) + 
                              parseInt(document.getElementById('m-l2-b').value || 0);
                
                if(totalA > totalB) {
                    teamA.value += 15000000;
                    teamB.value -= 10000000;
                } else if(totalA < totalB) {
                    teamB.value += 15000000;
                    teamA.value -= 10000000;
                } else {
                    teamA.value += 5000000;
                    teamB.value += 5000000;
                }
            }
            
            // Update player values with earnings (add to growthValue)
            pStats.forEach(ps => {
                const p = d.players.find(x=>x.id===ps.playerId);
                if(p) {
                    const earnings = util.calculatePlayerEarnings(ps, mvp, motm, ps.playerId);
                    p.growthValue += earnings;
                    recalcPlayerValue(p);
                }
                
                if(p && p.loanStatus) {
                    let used = (ps.leg1?.played ? 1 : 0) + (ps.leg2?.played ? 1 : 0);
                    p.loanStatus.legsRemaining -= used;
                    if(p.loanStatus.legsRemaining <= 0) { 
                        p.teamId = p.loanStatus.originalTeamId; 
                        p.loanStatus = null; 
                        p.transferHistory.push("Loan Ended"); 
                        util.notify(p.name + " returned from loan"); 
                    }
                }
            });
            return d;
        });
        
        document.getElementById('modal-overlay').classList.add('hidden'); 
        util.notify("Match Saved & Fixture Completed");
    },
    openMatchStats: (matchId) => {
        const data = db.get();
        const match = data.matches.find(m => m.id === matchId);
        if(!match) return;
        
        const teamA = data.teams.find(t => t.id === match.teamAId) || {name:'?', color:'#fff'};
        const teamB = data.teams.find(t => t.id === match.teamBId) || {name:'?', color:'#fff'};
        const mvp = match.mvpSnapshot || { playerName: 'N/A' };
        const motm = match.motmSnapshot || { playerName: 'N/A' };
        
        const totalA = util.sumMatchScore(match,'A');
        const totalB = util.sumMatchScore(match,'B');
        
        const legs = util.getLegNumbers(match);
        const legStatsArr = legs.map(n => ({ n, stats: util.calculateLegStats(match, data, n) }));

        const EMPTY_LEG = {
            teamA: { players: [], totals: { goals: 0, assists: 0, saves: 0, tackles: 0 } },
            teamB: { players: [], totals: { goals: 0, assists: 0, saves: 0, tackles: 0 } }
        };

        // Backwards-compatible variables (the UI below renders leg1/leg2 blocks)
        const leg1Stats = (legStatsArr.find(x => x.n === 1)?.stats) || EMPTY_LEG;
        const leg2Stats = (legStatsArr.find(x => x.n === 2)?.stats) || EMPTY_LEG;

        // Totals across ALL legs (1/2/4 supported)
        const teamATotal = { goals: 0, assists: 0, saves: 0, tackles: 0 };
        const teamBTotal = { goals: 0, assists: 0, saves: 0, tackles: 0 };
        legStatsArr.forEach(({ stats }) => {
            const a = stats?.teamA?.totals || {};
            const b = stats?.teamB?.totals || {};
            teamATotal.goals   += util.toInt(a.goals, 0);
            teamATotal.assists += util.toInt(a.assists, 0);
            teamATotal.saves   += util.toInt(a.saves, 0);
            teamATotal.tackles += util.toInt(a.tackles, 0);

            teamBTotal.goals   += util.toInt(b.goals, 0);
            teamBTotal.assists += util.toInt(b.assists, 0);
            teamBTotal.saves   += util.toInt(b.saves, 0);
            teamBTotal.tackles += util.toInt(b.tackles, 0);
        });
        
        // Calculate economy impact
        const economy = totalA > totalB ? 
            { teamA: "+$15,000,000", teamB: "-$10,000,000", result: "Win for " + teamA.name } : 
            totalA < totalB ? 
            { teamA: "-$10,000,000", teamB: "+$15,000,000", result: "Win for " + teamB.name } : 
            { teamA: "+$5,000,000", teamB: "+$5,000,000", result: "Draw" };
        
        // Calculate player earnings for this match
        let playerEarningsHTML = '';
        const allPlayers = [...data.players.filter(p=>p.teamId===match.teamAId), ...data.players.filter(p=>p.teamId===match.teamBId)];
        
        allPlayers.forEach(player => {
            const pStat = match.playerStats.find(ps => ps.playerId === player.id);
            if(pStat) {
                const earnings = util.calculatePlayerEarnings(pStat, match.mvpId, match.motmId, player.id);
                if(earnings > 0) {
                    playerEarningsHTML += `
                        <div style="padding:5px 0; border-bottom:1px solid rgba(255,255,255,0.05); font-size:0.8rem;">
                            <span style="color:${player.teamId === match.teamAId ? teamA.color : teamB.color}">${player.name}</span>
                            <span style="float:right; color:var(--rank-b)">+${util.formatMoney(earnings)}</span>
                        </div>
                    `;
                }
            }
        });
        
        let statsHTML = `
            <h2 class="neon-text">Match Statistics</h2>
            <div style="text-align:center; margin-bottom:20px;">
                <h3 style="color:${teamA.color}">${teamA.name}</h3>
                <div class="score-board">${totalA} - ${totalB}</div>
                <h3 style="color:${teamB.color}">${teamB.name}</h3>
                <p style="color:#888; margin-top:10px;">Leg 1: ${match.leg1ScoreA}-${match.leg1ScoreB} | Leg 2: ${match.leg2ScoreA}-${match.leg2ScoreB}</p>
                <div style="margin-top:10px; padding:10px; background:rgba(0,0,0,0.3); border-radius:5px;">
                    <div style="color:var(--primary); font-weight:bold;">${economy.result}</div>
                    <div style="font-size:0.9rem; margin-top:5px;">
                        <span style="color:${teamA.color}">${teamA.name}:</span> <span class="${totalA > totalB ? 'economy-win' : totalA < totalB ? 'economy-loss' : 'economy-draw'}">${economy.teamA}</span> |
                        <span style="color:${teamB.color}">${teamB.name}:</span> <span class="${totalB > totalA ? 'economy-win' : totalB < totalA ? 'economy-loss' : 'economy-draw'}">${economy.teamB}</span>
                    </div>
                </div>
            </div>
            
            <div class="team-summary">
                <div class="team-summary-card">
                    <h4 style="color:${teamA.color}">${teamA.name} Summary</h4>
                    <p>Goals: ${teamATotal.goals}</p>
                    <p>Assists: ${teamATotal.assists}</p>
                    <p>Saves: ${teamATotal.saves}</p>
                    <p>Tackles: ${teamATotal.tackles}</p>
                </div>
                <div class="team-summary-card">
                    <h4 style="color:${teamB.color}">${teamB.name} Summary</h4>
                    <p>Goals: ${teamBTotal.goals}</p>
                    <p>Assists: ${teamBTotal.assists}</p>
                    <p>Saves: ${teamBTotal.saves}</p>
                    <p>Tackles: ${teamBTotal.tackles}</p>
                </div>
            </div>
            
            ${playerEarningsHTML ? `
            <div style="margin-top:20px; padding:15px; background:rgba(0,255,102,0.05); border:1px solid rgba(0,255,102,0.2);">
                <h4 style="color:var(--rank-b);">💰 Player Earnings This Match</h4>
                <div style="margin-top:10px;">
                    ${playerEarningsHTML}
                </div>
                <p style="font-size:0.8rem; color:#888; margin-top:10px;">All earnings added to growthValue</p>
            </div>
            ` : ''}
            
            <h3 style="margin-top:20px;">Match Awards</h3>
            <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px; margin-bottom:20px;">
                <div style="border:1px solid var(--primary); padding:10px; text-align:center;">
                    <div style="color:var(--primary); font-size:0.9rem;">MVP</div>
                    <div style="font-weight:bold; font-size:1.2rem; cursor:pointer;" class="player-clickable" onclick="event.stopPropagation();app.openProfile('${mvp.playerId}')">${mvp.playerName}</div>
                    <div style="font-size:0.8rem; color:var(--rank-b);">+${util.formatMoney(3000000)}</div>
                </div>
                <div style="border:1px solid var(--rank-s); padding:10px; text-align:center;">
                    <div style="color:var(--rank-s); font-size:0.9rem;">MOTM</div>
                    <div style="font-weight:bold; font-size:1.2rem; cursor:pointer;" class="player-clickable" onclick="event.stopPropagation();app.openProfile('${motm.playerId}')">${motm.playerName}</div>
                    <div style="font-size:0.8rem; color:var(--rank-b);">+${util.formatMoney(3000000)}</div>
                </div>
            </div>
            
            <div class="leg-section">
                <h3>Leg 1 Details</h3>
                <div style="margin-bottom:20px;">
                    <h4 style="color:${teamA.color}">${teamA.name}</h4>
                    <div class="stats-header-row">
                        <div>Player</div><div>Goals</div><div>Assists</div><div>Saves</div><div>Tackles</div>
                    </div>
                    ${leg1Stats.teamA.players.map(p => `
                        <div class="player-stat-row">
                            <div>${p.name}</div><div>${p.goals}</div><div>${p.assists}</div><div>${p.saves}</div><div>${p.tackles}</div>
                        </div>
                    `).join('')}
                    <div class="player-stat-row" style="font-weight:bold; background:rgba(0,0,0,0.2);">
                        <div>Totals</div><div>${leg1Stats.teamA.totals.goals}</div><div>${leg1Stats.teamA.totals.assists}</div><div>${leg1Stats.teamA.totals.saves}</div><div>${leg1Stats.teamA.totals.tackles}</div>
                    </div>
                </div>
                <div>
                    <h4 style="color:${teamB.color}">${teamB.name}</h4>
                    <div class="stats-header-row">
                        <div>Player</div><div>Goals</div><div>Assists</div><div>Saves</div><div>Tackles</div>
                    </div>
                    ${leg1Stats.teamB.players.map(p => `
                        <div class="player-stat-row">
                            <div>${p.name}</div><div>${p.goals}</div><div>${p.assists}</div><div>${p.saves}</div><div>${p.tackles}</div>
                        </div>
                    `).join('')}
                    <div class="player-stat-row" style="font-weight:bold; background:rgba(0,0,0,0.2);">
                        <div>Totals</div><div>${leg1Stats.teamB.totals.goals}</div><div>${leg1Stats.teamB.totals.assists}</div><div>${leg1Stats.teamB.totals.saves}</div><div>${leg1Stats.teamB.totals.tackles}</div>
                    </div>
                </div>
            </div>
            
            <div class="leg-section">
                <h3>Leg 2 Details</h3>
                <div style="margin-bottom:20px;">
                    <h4 style="color:${teamA.color}">${teamA.name}</h4>
                    <div class="stats-header-row">
                        <div>Player</div><div>Goals</div><div>Assists</div><div>Saves</div><div>Tackles</div>
                    </div>
                    ${leg2Stats.teamA.players.map(p => `
                        <div class="player-stat-row">
                            <div>${p.name}</div><div>${p.goals}</div><div>${p.assists}</div><div>${p.saves}</div><div>${p.tackles}</div>
                        </div>
                    `).join('')}
                    <div class="player-stat-row" style="font-weight:bold; background:rgba(0,0,0,0.2);">
                        <div>Totals</div><div>${leg2Stats.teamA.totals.goals}</div><div>${leg2Stats.teamA.totals.assists}</div><div>${leg2Stats.teamA.totals.saves}</div><div>${leg2Stats.teamA.totals.tackles}</div>
                    </div>
                </div>
                <div>
                    <h4 style="color:${teamB.color}">${teamB.name}</h4>
                    <div class="stats-header-row">
                        <div>Player</div><div>Goals</div><div>Assists</div><div>Saves</div><div>Tackles</div>
                    </div>
                    ${leg2Stats.teamB.players.map(p => `
                        <div class="player-stat-row">
                            <div>${p.name}</div><div>${p.goals}</div><div>${p.assists}</div><div>${p.saves}</div><div>${p.tackles}</div>
                        </div>
                    `).join('')}
                    <div class="player-stat-row" style="font-weight:bold; background:rgba(0,0,0,0.2);">
                        <div>Totals</div><div>${leg2Stats.teamB.totals.goals}</div><div>${leg2Stats.teamB.totals.assists}</div><div>${leg2Stats.teamB.totals.saves}</div><div>${leg2Stats.teamB.totals.tackles}</div>
                    </div>
                </div>
            </div>
        `;
        
        if(data.settings.isAdmin) {
            statsHTML += `
                <div class="edit-match-form admin-only">
                    <h3 style="color:var(--accent);">✏️ EDIT MATCH (ADMIN)</h3>
                    <button class="btn btn-primary" onclick="modals.openMatchEdit('${matchId}')" style="margin-top:10px; width:100%;">EDIT MATCH STATS</button>
                </div>
            `;
        }
        
        statsHTML += `<button class="btn" style="margin-top:20px; width:100%;" onclick="document.getElementById('stats-modal-overlay').classList.add('hidden')">CLOSE</button>`;
        
        document.getElementById('stats-modal-body').innerHTML = statsHTML;
        document.getElementById('stats-modal-overlay').classList.remove('hidden');
    },
    openMatchEdit: (matchId) => {
        const data = db.get();
        const match = data.matches.find(m => m.id === matchId);
        if(!match) return;
        
        const teamA = data.teams.find(t => t.id === match.teamAId) || {name:'?', color:'#fff'};
        const teamB = data.teams.find(t => t.id === match.teamBId) || {name:'?', color:'#fff'};
        
        let editHTML = `
            <h2 class="neon-text">Edit Match</h2>
            <div style="margin-bottom:20px;">
                <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px;">
                    <div>
                        <label style="color:${teamA.color}">${teamA.name}</label>
                        <input type="hidden" id="edit-m-teamA" value="${match.teamAId}">
                    </div>
                    <div>
                        <label style="color:${teamB.color}">${teamB.name}</label>
                        <input type="hidden" id="edit-m-teamB" value="${match.teamBId}">
                    </div>
                </div>
                
                <div style="background:rgba(0,0,0,0.3); padding:15px; margin-top:15px;">
                    <h4>Leg Scores</h4>
                    <div style="display:grid; grid-template-columns:1fr 1fr; gap:10px;">
                        <div>
                            <label>Leg 1 - ${teamA.name}</label>
                            <input type="number" id="edit-m-l1-a" class="edit-input" value="${match.leg1ScoreA}">
                        </div>
                        <div>
                            <label>Leg 1 - ${teamB.name}</label>
                            <input type="number" id="edit-m-l1-b" class="edit-input" value="${match.leg1ScoreB}">
                        </div>
                        <div>
                            <label>Leg 2 - ${teamA.name}</label>
                            <input type="number" id="edit-m-l2-a" class="edit-input" value="${match.leg2ScoreA}">
                        </div>
                        <div>
                            <label>Leg 2 - ${teamB.name}</label>
                            <input type="number" id="edit-m-l2-b" class="edit-input" value="${match.leg2ScoreB}">
                        </div>
                    </div>
                </div>
                
                <div style="margin-top:20px;">
                    <h4>Player Stats (Leg-Specific)</h4>
                    <div style="overflow-x:auto; max-height:400px;">
                        <div style="min-width: 800px;">
                            <div style="display:grid; grid-template-columns: 2fr repeat(4, 1fr) auto repeat(4, 1fr) auto; gap:10px; padding:10px; background:rgba(0,240,255,0.1); font-weight:bold; font-size:0.8rem;">
                                <div>Player</div>
                                <div colspan="4" style="text-align:center;">Leg 1</div>
                                <div></div>
                                <div colspan="4" style="text-align:center;">Leg 2</div>
                                <div></div>
                            </div>
                            <div style="display:grid; grid-template-columns: 2fr repeat(4, 1fr) auto repeat(4, 1fr) auto; gap:10px; padding:10px; background:rgba(0,0,0,0.2); font-size:0.8rem;">
                                <div></div>
                                <div style="text-align:center;">G</div><div style="text-align:center;">A</div><div style="text-align:center;">S</div><div style="text-align:center;">T</div>
                                <div style="text-align:center;">Play</div>
                                <div style="text-align:center;">G</div><div style="text-align:center;">A</div><div style="text-align:center;">S</div><div style="text-align:center;">T</div>
                                <div style="text-align:center;">Play</div>
                            </div>
        `;
        
        const allPlayers = [...data.players.filter(p=>p.teamId===match.teamAId), ...data.players.filter(p=>p.teamId===match.teamBId)];
        
        allPlayers.forEach(player => {
            const pStat = match.playerStats.find(ps => ps.playerId === player.id) || {leg1: {played: false, goals:0, assists:0, saves:0, tackles:0}, leg2: {played: false, goals:0, assists:0, saves:0, tackles:0}};
            const team = data.teams.find(t => t.id === player.teamId);
            
            editHTML += `
                <div style="display:grid; grid-template-columns: 2fr repeat(4, 1fr) auto repeat(4, 1fr) auto; gap:10px; padding:10px; border-bottom:1px solid rgba(255,255,255,0.05); align-items:center;">
                    <div style="color:${team.color}; font-weight:500;">${player.name}</div>
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="1" data-type="goals" value="${pStat.leg1?.goals || 0}" min="0">
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="1" data-type="assists" value="${pStat.leg1?.assists || 0}" min="0">
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="1" data-type="saves" value="${pStat.leg1?.saves || 0}" min="0">
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="1" data-type="tackles" value="${pStat.leg1?.tackles || 0}" min="0">
                    <div style="text-align:center;"><input type="checkbox" data-pid="${player.id}" data-leg="1" data-type="played" ${pStat.leg1?.played ? 'checked' : ''}></div>
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="2" data-type="goals" value="${pStat.leg2?.goals || 0}" min="0">
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="2" data-type="assists" value="${pStat.leg2?.assists || 0}" min="0">
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="2" data-type="saves" value="${pStat.leg2?.saves || 0}" min="0">
                    <input type="number" class="edit-input" data-pid="${player.id}" data-leg="2" data-type="tackles" value="${pStat.leg2?.tackles || 0}" min="0">
                    <div style="text-align:center;"><input type="checkbox" data-pid="${player.id}" data-leg="2" data-type="played" ${pStat.leg2?.played ? 'checked' : ''}></div>
                </div>
            `;
        });
        
        editHTML += `
                        </div>
                    </div>
                </div>
                
                <div style="margin-top:20px; display:grid; grid-template-columns:1fr 1fr; gap:20px;">
                    <div>
                        <label>MVP</label>
                        <select id="edit-m-mvp">
                            <option value="">Select MVP</option>
                            ${allPlayers.map(p => `<option value="${p.id}" ${match.mvpId === p.id ? 'selected' : ''}>${p.name}</option>`).join('')}
                        </select>
                    </div>
                    <div>
                        <label>MOTM</label>
                        <select id="edit-m-motm">
                            <option value="">Select MOTM</option>
                            ${allPlayers.map(p => `<option value="${p.id}" ${match.motmId === p.id ? 'selected' : ''}>${p.name}</option>`).join('')}
                        </select>
                    </div>
                </div>
                
                <div style="margin-top:20px; display:flex; gap:10px;">
                    <button class="btn btn-danger" style="flex:1;" onclick="document.getElementById('stats-modal-overlay').classList.add('hidden')">CANCEL</button>
                    <button class="btn btn-primary" style="flex:1;" onclick="actions.saveEditedMatch('${matchId}')">SAVE CHANGES</button>
                </div>
            </div>
        `;
        
        document.getElementById('stats-modal-body').innerHTML = editHTML;
    },
    openEditTeam: (teamId) => {
        const data = db.get();
        const team = data.teams.find(t => t.id === teamId);
        if(!team) return;
        
        const b = document.getElementById('modal-body');
        b.innerHTML = `
            <h2 class="neon-text">Edit Team</h2>
            <div style="margin:20px 0;">
                <label>Team Name</label>
                <input type="text" id="edit-team-name" value="${team.name}" placeholder="Team Name">
                
                <label>Team Color</label>
                <input type="color" id="edit-team-color" value="${team.color}" style="width:100%; height:40px;">
                
                <label>Team Treasury</label>
                <input type="number" id="edit-team-value" value="${team.value}" placeholder="Team Value">
                
                <div style="margin-top:20px; display:flex; gap:10px;">
                    <button class="btn btn-danger" style="flex:1;" onclick="document.getElementById('modal-overlay').classList.add('hidden')">CANCEL</button>
                    <button class="btn btn-primary" style="flex:1;" onclick="actions.editTeam('${teamId}', document.getElementById('edit-team-name').value, document.getElementById('edit-team-color').value); document.getElementById('edit-team-value').value ? actions.updateTeamValue('${teamId}') : null">SAVE CHANGES</button>
                </div>
            </div>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    openEditPlayer: (playerId) => {
        const data = db.get();
        const player = data.players.find(p => p.id === playerId);
        if(!player) return;
        
        const team = data.teams.find(t => t.id === player.teamId);
        
        const b = document.getElementById('modal-body');
        b.innerHTML = `
            <h2 class="neon-text">Edit Player</h2>
            <div style="margin:20px 0;">
                <label>Player Name</label>
                <input type="text" id="edit-player-name" value="${player.name}" placeholder="Player Name">
                
                <label>Team</label>
                <select id="edit-player-team">
                    ${data.teams.map(t => `<option value="${t.id}" ${t.id === player.teamId ? 'selected' : ''}>${t.name}</option>`).join('')}
                </select>
                
                <label>Player Value</label>
                <input type="number" id="edit-player-value" value="${player.playerValue}" placeholder="Value">
                
                <div style="margin-top:20px; display:flex; gap:10px;">
                    <button class="btn btn-danger" style="flex:1;" onclick="document.getElementById('modal-overlay').classList.add('hidden')">CANCEL</button>
                    <button class="btn btn-primary" style="flex:1;" onclick="actions.editPlayer('${playerId}', document.getElementById('edit-player-name').value, document.getElementById('edit-player-value').value); if(document.getElementById('edit-player-team').value !== '${player.teamId}') { actions.transferPlayerManual('${playerId}', document.getElementById('edit-player-team').value); }">SAVE CHANGES</button>
                </div>
            </div>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    openFixtureCreation: () => {
        const data = db.get();
        const b = document.getElementById('modal-body');
        const tournaments = data.tournaments.filter(t => !t.completed);
        
        b.innerHTML = `
            <h2 class="neon-text">Create Fixture</h2>
            <div style="margin:20px 0;">
                <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px; margin-bottom:20px;">
                    <div><label>Team A</label><select id="fx-teamA"><option value="">Select Team</option>${data.teams.map(t=>`<option value="${t.id}">${t.name}</option>`).join('')}</select></div>
                    <div><label>Team B</label><select id="fx-teamB"><option value="">Select Team</option>${data.teams.map(t=>`<option value="${t.id}">${t.name}</option>`).join('')}</select></div>
                </div>
                
                <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px; margin-bottom:20px;">
                    <div>
                        <label>Competition</label>
                        <select id="fx-competition" onchange="window.modals.toggleTournamentField()">
                            <option value="League">League</option>
                            <option value="Tournament">Tournament</option>
                            <option value="Friendly">Friendly</option>
                        </select>
                    </div>
                    <div>
                        <label>Round/Matchday</label>
                        <input type="text" id="fx-round" placeholder="e.g., Matchday 3, Semi Final">
                    </div>
                </div>
                
                <div id="tournament-field" style="display:none; margin-bottom:20px;">
                    <label>Tournament</label>
                    <select id="fx-tournament">
                        <option value="">Select Tournament</option>
                        ${tournaments.map(t=>`<option value="${t.id}">${t.name}</option>`).join('')}
                    </select>
                </div>
                
                <div class="grid" style="grid-template-columns: 1fr 1fr; gap:20px; margin-bottom:20px;">
                    <div>
                        <label>Date</label>
                        <input type="text" id="fx-date" placeholder="e.g., 2026-03-15, TBD">
                    </div>
                    <div>
                        <label>Legs Format</label>
                        <select id="fx-legs">
                            <option value="1">1 leg</option>
                            <option value="2" selected>2 legs</option>
                            <option value="4">4 legs</option>
                        </select>
                    </div>
                </div>
                
                <div style="margin-top:20px; display:flex; gap:10px;">
                    <button class="btn btn-danger" style="flex:1;" onclick="document.getElementById('modal-overlay').classList.add('hidden')">CANCEL</button>
                    <button class="btn btn-primary" style="flex:1;" onclick="actions.createFixture()">CREATE FIXTURE</button>
                </div>
            </div>
        `;
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    toggleTournamentField: () => {
        const competition = document.getElementById('fx-competition').value;
        const tournamentField = document.getElementById('tournament-field');
        tournamentField.style.display = competition === 'Tournament' ? 'block' : 'none';
    },
    openTournamentCreation: () => {
        const data = db.get();
        
        if (window.app.tournamentCreationStep === 1) {
            const b = document.getElementById('modal-body');
            b.innerHTML = `
                <h2 class="neon-text">Create Tournament - Step 1/2</h2>
                <div style="margin:20px 0;">
                    <div style="margin-bottom:20px;">
                        <label>Tournament Name</label>
                        <input type="text" id="tournament-name" placeholder="e.g., Champions Cup 2026" style="width:100%;">
                    </div>
                    
                    <div style="margin-bottom:20px;">
                        <label>Match Format</label>
                        <select id="tournament-format" style="width:100%;">
                            <option value="1 leg">1 leg (single match)</option>
                            <option value="2 legs" selected>2 legs (home & away)</option>
                            <option value="4 legs">4 legs (extended series)</option>
                        </select>
                    </div>
                    
                    <div style="margin-top:30px;">
                        <h4 style="color:var(--primary);">Select 8 Teams</h4>
                        <p style="color:var(--text-dim); font-size:0.9rem;">Selected: ${window.app.selectedTeamsForTournament.length}/8</p>
                        <div class="team-selection-grid">
                            ${data.teams.map(team => {
                                const isSelected = window.app.selectedTeamsForTournament.includes(team.id);
                                return `
                                    <div class="team-selection-card ${isSelected ? 'selected' : ''}" onclick="app.toggleTeamForTournament('${team.id}')">
                                        <div style="color:${team.color}; font-weight:bold;">${team.name}</div>
                                        <div style="font-size:0.8rem; color:#888;">${util.formatMoney(team.value)}</div>
                                    </div>
                                `;
                            }).join('')}
                        </div>
                    </div>
                    
                    <div style="margin-top:30px; display:flex; gap:10px;">
                        <button class="btn btn-danger" style="flex:1;" onclick="document.getElementById('modal-overlay').classList.add('hidden')">CANCEL</button>
                        <button class="btn btn-primary" style="flex:1;" onclick="window.app.tournamentCreationStep = 2; window.modals.openTournamentCreation();">NEXT</button>
                    </div>
                </div>
            `;
        } else {
            // Step 2: Confirm tournament creation
            const selectedTeams = window.app.selectedTeamsForTournament.map(id => {
                const team = data.teams.find(t => t.id === id);
                return team;
            }).filter(t => t);
            
            const b = document.getElementById('modal-body');
            b.innerHTML = `
                <h2 class="neon-text">Create Tournament - Step 2/2</h2>
                <div style="margin:20px 0;">
                    <div style="margin-bottom:20px; padding:15px; background:rgba(0,0,0,0.3); border-radius:5px;">
                        <div><strong>Tournament Name:</strong> ${document.getElementById('tournament-name')?.value || 'Unnamed'}</div>
                        <div><strong>Format:</strong> ${document.getElementById('tournament-format')?.value || '2 legs'}</div>
                        <div><strong>Teams:</strong> ${selectedTeams.length}/8</div>
                    </div>
                    
                    <div style="margin-bottom:20px;">
                        <h4 style="color:var(--primary);">Selected Teams</h4>
                        <div style="display:grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap:10px; margin-top:10px;">
                            ${selectedTeams.map(team => `
                                <div style="padding:10px; background:rgba(0,0,0,0.2); border-radius:5px; border-left:4px solid ${team.color};">
                                    <div style="color:${team.color}; font-weight:bold;">${team.name}</div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                    
                    <div style="margin-top:30px; display:flex; gap:10px;">
                        <button class="btn btn-danger" style="flex:1;" onclick="window.app.tournamentCreationStep = 1; window.modals.openTournamentCreation();">BACK</button>
                        <button class="btn btn-primary" style="flex:1;" onclick="actions.createTournament()">CREATE TOURNAMENT</button>
                    </div>
                </div>
            `;
        }
        
        document.getElementById('modal-overlay').classList.remove('hidden');
    },
    generateTournamentFixtures: (tournamentId) => {
        const data = db.get();
        const tournament = data.tournaments.find(t => t.id === tournamentId);
        if(!tournament) return;
        
        const groups = tournament.groups;
        const existingFixtures = data.fixtures.filter(f => f.tournamentId === tournamentId);
        
        // Generate group stage fixtures
        let newFixtures = [];
        Object.keys(groups).forEach(groupName => {
            const teams = groups[groupName];
            
            // Create round robin fixtures
            for(let i = 0; i < teams.length; i++) {
                for(let j = i + 1; j < teams.length; j++) {
                    const teamA = teams[i];
                    const teamB = teams[j];
                    
                    // Check if fixture already exists
                    const exists = existingFixtures.some(f => 
                        ((f.teamAId === teamA && f.teamBId === teamB) || 
                         (f.teamAId === teamB && f.teamBId === teamA)) &&
                        f.stage === 'group'
                    );
                    
                    if(!exists) {
                        newFixtures.push({
                            id: util.uuid(),
                            tournamentId,
                            teamAId: teamA,
                            teamBId: teamB,
                            competition: 'Tournament',
                            round: `${groupName} - Matchday`,
                            legs: tournament.format === '1 leg' ? 1 : tournament.format === '2 legs' ? 2 : 4,
                            played: false,
                            stage: 'group'
                        });
                    }
                }
            }
        });
        
        if(newFixtures.length > 0) {
            db.update(d => {
                d.fixtures.push(...newFixtures);
                return d;
            });
            
            util.notify(`Generated ${newFixtures.length} new fixtures for ${tournament.name}`);
        } else {
            util.notify("All group stage fixtures already exist");
        }
        
        document.getElementById('modal-overlay').classList.add('hidden');
    }
};



/* ===== Guide + Neon/Emoji Animations helpers (merged) ===== */
function renderGuide(container, data){
    data.guideSections = data.guideSections || [];

    const isAdmin = !!(data.settings && data.settings.isAdmin);
    const sections = [...data.guideSections].sort((a,b)=>(b.updatedAt||b.createdAt||0)-(a.updatedAt||a.createdAt||0));

    container.innerHTML = `
        <div class="page-header">
            <h2 class="neon-text"><span class="emoji-float emoji-pop">📘</span> Guide</h2>
            <p style="color:var(--text-dim); margin-top:6px;">Admins can post updates, rules, or how-to notes. Everyone can read.</p>
            ${isAdmin ? `<div style="margin-top:10px; display:flex; gap:10px; flex-wrap:wrap;">
                <button class="btn-primary" onclick="app.openGuideEditor()">➕ Add Guide Item</button>
            </div>` : ``}
        </div>

        <div class="grid" style="margin-top:14px; display:grid; gap:12px;">
            ${sections.length ? sections.map(s => `
                <div class="card" style="padding:14px;">
                    <div style="display:flex; justify-content:space-between; gap:12px; align-items:flex-start;">
                        <div>
                            <h3 class="neon-text" style="margin:0 0 6px 0;">${util.escapeHtml(s.title || "Untitled")}</h3>
                            <div style="color:var(--text-dim); font-size:0.85rem;">
                                ${s.updatedAt ? `Updated: ${new Date(s.updatedAt).toLocaleString()}` : `Posted: ${new Date(s.createdAt||Date.now()).toLocaleString()}`}
                                ${s.by ? ` • by ${util.escapeHtml(s.by)}` : ``}
                            </div>
                        </div>
                        ${isAdmin ? `<div style="display:flex; gap:8px; flex-wrap:wrap;">
                            <button class="btn" onclick="app.openGuideEditor('${s.id}')">✏️ Edit</button>
                            <button class="btn-danger" onclick="app.deleteGuideItem('${s.id}')">🗑️ Delete</button>
                        </div>` : ``}
                    </div>
                    <div style="margin-top:10px; line-height:1.45; white-space:pre-wrap;">${util.escapeHtml(s.content || "")}</div>
                </div>
            `).join('') : `<div class="empty-state">No guide items yet.</div>`}
        </div>
    `;

    wrapAnimatedEmojis(container);
    runNeonEntranceAnimations();
}
// Initialize remote sync if configured
initFirebaseIfConfigured();

// Initialize the app
window.app.init();
</script>
</body>
</html>
