# podcast
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tirage de cartes</title>
    <style>
        .card {width: 200px; height: 300px; border: 1px solid #000; margin: 10px;}
        img {width: 100%; height: auto;}
        #result {margin-top: 20px;}
    </style>
</head>
<body>
    <h1>Tire une carte</h1>
    <button onclick="drawCard()">Tirer une carte</button>

    <div id="result"></div>

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

            // Afficher la carte tirée
            document.getElementById("result").innerHTML += `<div class="card"><img src="${card}" alt="Carte"></div>`;
            
            // Désactiver le bouton après le 4e tirage
            if (drawnCards === 4) {
                document.querySelector("button").disabled = true;
            }
        }
    </script>
</body>
</html>
