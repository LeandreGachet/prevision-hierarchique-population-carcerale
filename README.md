# Prévision hiérarchique de la population carcérale australienne

Combien de places de prison faudra-t-il au trimestre prochain : au niveau national, mais aussi par État, par statut juridique et par genre ?

Douze ans de données trimestrielles, structurées en arbre : 32 séries élémentaires au croisement de 8 États, 2 genres et 2 statuts (prévenu ou condamné). Le problème n'est pas de prévoir une série, mais 32 : et de faire en sorte que les totaux soient cohérents avec leurs composantes.

Projet de Master 2 en binôme.

## Démarche

Diagnostic préalable : le test de Ljung-Box sur les résidus du modèle agrégé révèle une autocorrélation saisonnière significative, un modèle unique sur le total ne capte pas la complexité des dynamiques. C'est ce constat qui justifie l'approche ascendante plutôt que de la choisir par défaut.

Arbitrage entre méthodes : lissage exponentiel plutôt qu'ARIMA, au vu du nombre de séries, ARIMA aurait imposé des tests de stationnarité sur chacune des 32, là où le lissage exponentiel modélise explicitement tendance et niveau avec sélection automatique.

Prévision ascendante : chaque série élémentaire modélisée séparément, puis agrégation des prévisions à chaque niveau de l'arbre.

Propagation de l'incertitude : les intervalles à 95 % sont construits en agrégeant les variances résiduelles des 32 séries élémentaires, à chaque niveau. C'est la partie que la plupart des travaux omettent : une prévision agrégée sans son incertitude agrégée n'est qu'à moitié utile.

## Ce que ça produit

Une prévision disponible à tous les niveaux de lecture, assortie de sa mesure d'incertitude : et un dimensionnement de capacité fondé sur la borne haute de l'intervalle plutôt que sur la prévision centrale, parce qu'une place de prison manquante coûte plus cher qu'une place vide.

## Contenu

| | |
|---|---|
| `traitement.rpf` | le programme, en WinRATS |
| `rapport/rapport.pdf` | le rapport (16 pages) |
| `data/` | les données trimestrielles |

Le programme est écrit pour WinRATS, logiciel d'économétrie des séries temporelles.

---

**Léandre Gachet**, Master Science des données, statistique et économétrie, Université de Rennes
