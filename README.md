<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tirage de cartes - Atypique !</title>
    <style>
        /* Import des polices */
        @font-face {
            font-family: 'Tan Headline';
            src: url('https://fonts.cdnfonts.com/s/39753/TanHeadline-Regular.woff') format('woff');
        }
        @font-face {
            font-family: 'Dumondi Expanded';
            src: url('https://fonts.cdnfonts.com/s/39753/DumondiExpanded-Regular.woff') format('woff');
        }

        /* Style global */
        body {
            background-color: #0b4348;
            font-family: 'Dumondi Expanded', sans-serif;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }

        /* Titre du podcast */
        h1 {
            font-family: 'Tan Headline', serif;
            font-size: 3rem;
            margin-bottom: 20px;
        }

        /* Logo */
        .logo {
            width: 150px;
            height: auto;
            margin-top: 20px;
        }

        /* Bouton de tirage */
        button {
            background-color: #ffffff;
            color: #0b4348;
            border: none;
            padding: 15px 30px;
            font-size: 1.5rem;
            margin-top: 30px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #cfe3e3;
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

        /* Résultats */
        #result {
            margin-top: 40px;
        }
    </style>
</head>
<body>
    <!-- Logo -->
    <img src="ton_logo.png" alt="Logo du podcast" class="logo">

    <!-- Titre du podcast -->
    <h1>Atypique !</h1>

    <!-- Bouton de tirage -->
    <button onclick="drawCard()">Tirer une carte</button>

    <!-- Zone d'affichage des résultats -->
    <div id="result"></div>

    <!-- Script JavaScript pour le tirage -->
    <script>
        // Tableau contenant les 3 premières cartes (sans "s.png")
        let cards = ["c.png", "q.png", "d.png"];
        let specialCard = "s.png"; // La carte "spéciale" à tirer au 4e tirage
        let drawnCards = 0; // Compteur de tirages

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
            
            // Désactiver le bouton après le 4e tirage
            if (drawnCards === 4) {
                document.querySelector("button").disabled = true;
            }
        }
    </script>
</body>
</html>
