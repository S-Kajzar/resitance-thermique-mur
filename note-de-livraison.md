# Note de livraison — Résistance thermique et flux thermique d'un mur

`index.html` a été reconstruit sur le gabarit `gabarit-exercice-interactif.html`. Le bloc `<style>` et le moteur de correction (Grading) sont repris sans aucune modification. Dans le moteur applicatif, seuls les réglages propres au sujet ont changé :

- `CONSEIL_MIN` = 45 (durée conseillée totale) ;
- `DECOR` et `DR_NAMES` sont vides (aucun tracé).

## Architecture

- Page d'accueil avec illustration, 4 chiffres clés et choix du mode (entraînement ou examen).
- Documents en rail à droite : DP1 (enceinte d'essai et courbe), DP2 (mur étudié), DT1 (formulaire), DT2 (tableau des R<sub>th</sub>).
- Bandeau avec note pondérée et chronomètre.
- Récapitulatif par partie avec un seul bouton « Imprimer ma copie ».
- Barème : partie 1 = 15 min (33,3 %, 4 points) ; partie 2 = 30 min (66,7 %, 9 points). Les durées ne figuraient pas dans le source : elles ont été fixées d'après le volume de travail.

## Questions reformulées ou découpées

Le moteur attend une réponse par champ. Les anciennes questions à plusieurs champs ont donc été découpées :

| Ancien | Nouveau |
|---|---|
| Q1 (R<sub>th</sub>) | Q1.1 T en régime permanent, Q1.2 T extérieure, Q1.3 flux (= P), Q1.4 R<sub>th</sub> |
| Q2 (3 flux) | Q2.2, Q2.3, Q2.4 |
| Q3 (conclusion) | Q2.5 meilleur mur, Q2.6 évolution du flux |
| Q4 (4ᵉ solution) | Q2.7 matériau, Q2.8 R<sub>th</sub> totale, Q2.9 flux |

Questions ajoutées : Q2.1 (surface du mur), ainsi que Q1.1 à Q1.3, qui sont les étapes intermédiaires de l'ancienne Q1.

## Erreurs relevées dans le source et arbitrages

1. **Ancienne Q4 incohérente.** L'énoncé disait « on garde l'isolant et on *remplace* le parpaing par la brique ». Le corrigé additionnait pourtant 1,17 + 2,1 = 3,27 m²·K·W⁻¹. Or 2,1 est la résistance du mur *parpaing + isolant* : ce calcul correspond donc à l'*ajout* d'une brique au mur parpaing + isolant. Un vrai remplacement donnerait 1,17 + (2,1 − 0,38) = 2,89 m²·K·W⁻¹, soit φ ≈ 40,69 W.
   - Arbitrage : l'énoncé est reformulé en « on *ajoute* au mur parpaing + isolant une couche du matériau le plus isolant ». Les résultats 3,27 m²·K·W⁻¹ et 35,96 W sont conservés. Cette lecture est cohérente avec la figure DP2 : brique + maçonnerie + isolant. La solution par remplacement est donnée dans l'explication comme autre réponse défendable.
   - L'ancienne « autre réponse » (parpaing + brique + isolant = 3,65) comptait le parpaing deux fois : elle a été supprimée.
2. **Courbe de DP1.** La droite étiquetée « 142 °C » se trouve vers 137 °C sur les graduations de l'axe. On retient la valeur étiquetée, 142 °C, qui est la donnée voulue par l'auteur. Signalé sans modifier l'image.
3. **Flux sur « une journée ».** Le flux est une puissance et ne dépend pas de la durée. L'énergie journalière reste mentionnée en remarque.

## Décisions de correction et de tolérance

- **Unités notées pour un demi-point**, selon le gabarit. Les consignes n'annoncent plus l'unité attendue.
- **Q1.4** : K·W⁻¹ et m²·K·W⁻¹ sont acceptés tous les deux, car S = 1 m². **Q2.8** : seule l'unité surfacique m²·K·W⁻¹ est acceptée. Les formes °C/W, K/W, m2.K/W, m^2.K.W^-1, etc. sont reconnues.
- **Lectures graphiques (Q1.1 et Q1.2)** : précision ± 1 °C. **Calculs** : arrondi au centième, tolérance ± 0,01.
- **Q2.3, Q2.8 et Q2.9** dépendent de la valeur trouvée en Q1.4. Il n'y a pas de report d'erreur : une R<sub>th</sub> fausse en Q1.4 entraîne des réponses fausses ensuite.
- **Q2.5** : toute réponse citant l'isolant est juste, sauf si elle cite la brique. **Q2.6** : « diminue », « plus faible », « inversement proportionnel »… sont acceptés. **Q2.7** : « brique » ou « terre cuite » ; le parpaing et le béton sont refusés.

## Tests

- 89 cas unitaires en Node : réponses justes, fausses, sans unité, avec une mauvaise unité, avec accents ou fautes de frappe.
- Parcours Playwright :
  - entraînement : sujet parfait = 20/20, demi-point d'unité, verrouillage des réponses ;
  - examen : aucune fuite de corrigé à l'impression avant la remise, confirmation en deux temps, note pondérée ;
  - affichage mobile 390 px sans défilement horizontal ;
  - aucune erreur JavaScript.
