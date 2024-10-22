<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tirage de cartes - Atypique !</title>
    <style>
        /* Style global */
        body {
            background-color: #0b4348;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }

        /* Logo */
        .logo {
            width: 150px;
            height: auto;
            margin-top: 20px;
        }

        /* Buzzer */
        .buzzer {
            width: 150px;
            height: auto;
            margin-top: 30px;
            cursor: pointer;
        }

        /* Zone des cartes tirées */
        .card {
            width: 200px;
            height: 300px;
            margin: 20px auto;
            border: 1px solid white;
            border-radius: 10px;
            overflow: hidden;
        }

        .card img {
            width: 100%;
            height: auto;
        }

        /* Zone d'animation de la roue */
        .wheel {
            width: 200px;
            height: 200px;
            margin: 20px auto;
            border: 5px solid white;
            border-radius: 50%;
            animation: spin 0s linear infinite; /* Animation par défaut désactivée */
        }

        /* Résultats */
        #result {
            margin-top: 40px;
        }

        /* Animation de rotation de la roue */
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <!-- Logo -->
    <img src="ton_logo.png" alt="Logo du podcast" class="logo">

    <!-- Buzzer pour tirer une carte -->
    <img src="b.png" alt="Buzzer" class="buzzer" onclick="startSpin()">

    <!-- Zone d'animation de la roue -->
    <div id="wheel-container" class="wheel" style="display: none;"></div>

    <!-- Zone d'affichage des résultats -->
    <div id="result"></div>

    <!-- Script JavaScript pour le tirage et l'animation -->
    <script>
        // Tableau contenant les 3 premières cartes (sans "s.png")
        let cards = ["c.png", "q.png", "d.png"];
        let specialCard = "s.png"; // La carte spéciale à tirer au 4e tirage
        let drawnCards = 0; // Compteur de tirages

        function startSpin() {
            // Afficher la roue et démarrer l'animation
            let wheel = document.getElementById("wheel-container");
            wheel.style.display = "block"; 
            wheel.style.animation = "spin 2s linear infinite";

            // Après 2 secondes, arrêter l'animation et tirer la carte
            setTimeout(() => {
                stopSpin();
                drawCard();
            }, 3000); // Dure 3 secondes avant de tirer la carte
        }

        function stopSpin() {
            // Arrêter l'animation de la roue
            let wheel = document.getElementById("wheel-container");
            wheel.style.animation = "spin 0s linear infinite"; // Désactiver l'animation
            wheel.style.display = "none"; // Cacher la roue après tirage
        }

        function drawCard() {
            let card;
            drawnCards++;

            // Si on est au 4e tirage, on affiche la carte spéciale
            if (drawnCards === 4) {
                card = specialCard;
            } else {
                // Tirage aléatoire parmi les cartes restantes
                let randomIndex = Math.floor(Math.random() * cards.length);
                card = cards[randomIndex];
                cards.splice(randomIndex, 1); // Retirer la carte tirée du tableau
            }

            // Remplacer la carte affichée par la nouvelle carte tirée
            document.getElementById("result").innerHTML = `<div class="card"><img src="${card}" alt="Carte"></div>`;
            
            // Désactiver le buzzer après le 4e tirage
            if (drawnCards === 4) {
                document.querySelector(".buzzer").style.display = "none";
            }
        }
    </script>
</body>
</html>
