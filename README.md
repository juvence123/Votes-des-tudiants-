
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vote Étudiant - Élection des Délégués</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .vote-card {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }

        .header p {
            opacity: 0.9;
            font-size: 14px;
        }

        .student-info {
            background: #f8f9fa;
            padding: 20px 30px;
            border-bottom: 1px solid #e0e0e0;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }

        .info-badge {
            background: white;
            padding: 8px 16px;
            border-radius: 25px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .info-badge span:first-child {
            font-weight: bold;
            color: #667eea;
        }

        .vote-status {
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: bold;
        }

        .status-not-voted {
            background: #ffeaa7;
            color: #d63031;
        }

        .status-voted {
            background: #d4edda;
            color: #155724;
        }

        .candidates {
            padding: 30px;
        }

        .candidates h2 {
            color: #333;
            margin-bottom: 20px;
            font-size: 22px;
        }

        .candidate-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .candidate-item {
            background: #f8f9fa;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .candidate-item:hover {
            border-color: #667eea;
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .candidate-item.selected {
            border-color: #764ba2;
            background: #f3e8ff;
            border-width: 3px;
        }

        .candidate-info {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .candidate-avatar {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            font-weight: bold;
        }

        .candidate-details h3 {
            font-size: 18px;
            color: #333;
            margin-bottom: 5px;
        }

        .candidate-details p {
            font-size: 14px;
            color: #666;
        }

        .radio-custom {
            width: 24px;
            height: 24px;
            border: 2px solid #ccc;
            border-radius: 50%;
            transition: all 0.2s ease;
        }

        .candidate-item.selected .radio-custom {
            background: #764ba2;
            border-color: #764ba2;
            box-shadow: inset 0 0 0 4px white;
        }

        .vote-button {
            padding: 15px 30px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            width: 100%;
            margin-bottom: 20px;
        }

        .vote-button:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        .vote-button:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
        }

        .result-section {
            background: #f8f9fa;
            margin-top: 20px;
            padding: 20px;
            border-radius: 15px;
            display: none;
        }

        .result-section.show {
            display: block;
            animation: slideUp 0.5s ease;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .result-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #ddd;
        }

        .progress-bar {
            flex: 1;
            height: 30px;
            background: #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
            margin-left: 15px;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            display: flex;
            align-items: center;
            justify-content: flex-end;
            padding-right: 10px;
            color: white;
            font-size: 12px;
            font-weight: bold;
            transition: width 0.5s ease;
        }

        .reset-btn {
            background: #6c5ce7;
            margin-top: 10px;
            background: linear-gradient(135deg, #ff7675, #d63031);
        }

        footer {
            text-align: center;
            padding: 20px;
            color: white;
            font-size: 12px;
        }

        @media (max-width: 600px) {
            .student-info {
                flex-direction: column;
                text-align: center;
            }
            .candidate-info {
                flex-direction: column;
                text-align: center;
            }
            .candidate-item {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="vote-card">
            <div class="header">
                <h1>🗳️ Élection des Délégués Étudiants</h1>
                <p>Session 2025 - Vote électronique sécurisé</p>
            </div>

            <div class="student-info">
                <div class="info-badge">
                    <span>📚 Étudiant :</span> <span id="studentName">Emma Laurent</span>
                </div>
                <div class="info-badge">
                    <span>🆑 Code unique :</span> <span id="studentCode">ETU-2025-0042</span>
                </div>
                <div class="vote-status status-not-voted" id="voteStatus">
                    ⏳ Non votant
                </div>
            </div>

            <div class="candidates">
                <h2>👥 Choisissez votre délégué(e)</h2>
                <div class="candidate-list" id="candidateList"></div>
                
                <button class="vote-button" id="voteBtn" disabled>
                    ✅ Confirmer mon vote
                </button>
                
                <button class="vote-button reset-btn" id="resetBtn">
                    🔄 Réinitialiser (Admin)
                </button>
            </div>

            <div class="result-section" id="resultSection">
                <h3>📊 Résultats en temps réel</h3>
                <div id="results"></div>
            </div>
        </div>
        <footer>
            Système de vote fictif - À des fins éducatives uniquement
        </footer>
    </div>

    <script>
        // Données des candidats
        const candidates = [
            { id: 1, name: "Sophie Martin", program: "Génie Logiciel", color: "#667eea", votes: 0 },
            { id: 2, name: "Thomas Bernard", program: "Marketing Digital", color: "#f093fb", votes: 0 },
            { id: 3, name: "Lucas Dubois", program: "Finance", color: "#4facfe", votes: 0 },
            { id: 4, name: "Camille Rousseau", program: "Design UX/UI", color: "#43e97b", votes: 0 }
        ];

        let hasVoted = false;
        let selectedCandidateId = null;
        let totalVoters = 45; // Nombre total d'étudiants dans la simulation
        let currentVotersCount = 0;

        // Charger les données du localStorage
        function loadData() {
            const savedVotes = localStorage.getItem('studentVotes');
            const savedHasVoted = localStorage.getItem('hasVoted');
            const savedSelected = localStorage.getItem('selectedCandidateId');
            
            if (savedVotes) {
                const votes = JSON.parse(savedVotes);
                candidates.forEach((c, index) => {
                    c.votes = votes[index] || 0;
                });
                currentVotersCount = votes.reduce((a,b) => a + b, 0);
            }
            
            if (savedHasVoted === 'true') {
                hasVoted = true;
                if (savedSelected) selectedCandidateId = parseInt(savedSelected);
                document.getElementById('voteBtn').disabled = true;
                document.getElementById('voteStatus').className = 'vote-status status-voted';
                document.getElementById('voteStatus').innerHTML = '✅ Votre vote est enregistré';
            }
        }

        // Sauvegarder les données
        function saveData() {
            const votes = candidates.map(c => c.votes);
            localStorage.setItem('studentVotes', JSON.stringify(votes));
            localStorage.setItem('hasVoted', hasVoted);
            if (selectedCandidateId) localStorage.setItem('selectedCandidateId', selectedCandidateId);
        }

        // Afficher les candidats
        function renderCandidates() {
            const container = document.getElementById('candidateList');
            container.innerHTML = candidates.map(candidate => `
                <div class="candidate-item ${selectedCandidateId === candidate.id && !hasVoted ? 'selected' : ''}" 
                     data-id="${candidate.id}">
                    <div class="candidate-info">
                        <div class="candidate-avatar" style="background: ${candidate.color}">
                            ${candidate.name.charAt(0)}
                        </div>
                        <div class="candidate-details">
                            <h3>${candidate.name}</h3>
                            <p>${candidate.program}</p>
                        </div>
                    </div>
                    <div class="radio-custom"></div>
                </div>
            `).join('');

            // Ajouter les événements de sélection
            if (!hasVoted) {
                document.querySelectorAll('.candidate-item').forEach(item => {
                    item.addEventListener('click', () => {
                        if (!hasVoted) {
                            selectedCandidateId = parseInt(item.dataset.id);
                            renderCandidates();
                            document.getElementById('voteBtn').disabled = false;
                        }
                    });
                });
            }
        }

        // Afficher les résultats
        function renderResults() {
            const total = currentVotersCount;
            const resultDiv = document.getElementById('results');
            const resultSection = document.getElementById('resultSection');
            
            if (total > 0) {
                resultSection.classList.add('show');
                resultDiv.innerHTML = candidates.map(candidate => {
                    const percentage = total > 0 ? (candidate.votes / total * 100).toFixed(1) : 0;
                    return `
                        <div class="result-item">
                            <strong>${candidate.name}</strong>
                            <div class="progress-bar">
                                <div class="progress-fill" style="width: ${percentage}%; background: ${candidate.color}">
                                    ${percentage}%
                                </div>
                            </div>
                            <span>${candidate.votes} voix</span>
                        </div>
                    `;
                }).join('');
                resultDiv.innerHTML += `<div class="result-item"><strong>Total votants:</strong> <span>${total}/${totalVoters}</span></div>`;
            }
        }

        // Voter
        function vote() {
            if (hasVoted) {
                alert("Vous avez déjà voté !");
                return;
            }
            
            if (!selectedCandidateId) {
                alert("Veuillez sélectionner un candidat");
                return;
            }
            
            const candidate = candidates.find(c => c.id === selectedCandidateId);
            if (confirm(`Confirmez votre vote pour ${candidate.name} ?`)) {
                candidate.votes++;
                currentVotersCount++;
                hasVoted = true;
                
                // Mettre à jour l'affichage
                document.getElementById('voteBtn').disabled = true;
                document.getElementById('voteStatus').className = 'vote-status status-voted';
                document.getElementById('voteStatus').innerHTML = '✅ Votre vote est enregistré';
                
                saveData();
                renderCandidates();
                renderResults();
                alert(`Merci d'avoir voté pour ${candidate.name} !`);
            }
        }

        // Réinitialiser (simulation admin)
        function resetElection() {
            if (confirm("⚠️ Réinitialiser tous les votes ? Cette action est irréversible.")) {
                candidates.forEach(c => c.votes = 0);
                hasVoted = false;
                selectedCandidateId = null;
                currentVotersCount = 0;
                
                localStorage.clear();
                
                document.getElementById('voteBtn').disabled = false;
                document.getElementById('voteStatus').className = 'vote-status status-not-voted';
                document.getElementById('voteStatus').innerHTML = '⏳ Non votant';
                
                renderCandidates();
                renderResults();
                alert("Élection réinitialisée avec succès !");
            }
        }

        // Initialisation
        function init() {
            loadData();
            renderCandidates();
            renderResults();
            
            document.getElementById('voteBtn').addEventListener('click', vote);
            document.getElementById('resetBtn').addEventListener('click', resetElection);
        }
        
        init();
    </script>
</body>
</html>
