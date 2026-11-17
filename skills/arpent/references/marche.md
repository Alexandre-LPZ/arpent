# Lecture du marché — où en est-on, et dans quel sens ça va (sans prévoir un chiffre)

## Ce que ce module fait, et ne fait pas
Il répond à : « sur ce territoire, à cette date, sommes-nous en **marché d'acheteurs**, **équilibré**
ou **marché de vendeurs**, et la tendance des derniers trimestres va-t-elle dans quel sens ? »

Il **ne prévoit jamais un prix ni un pourcentage à six mois**. Personne ne sait le faire de façon
vérifiable (notaires, banques et portails se trompent régulièrement sur le sens même du mouvement).
Un chiffre prévisionnel serait une invention déguisée en fait, ce que la règle n° 1 d'Arpent interdit.
Le livrable est une **direction argumentée avec ce qui l'invaliderait**, pas une prédiction.

Usage pour le marchand : si la lecture dit « acheteurs », on durcit l'hypothèse de revente dans
`/bilan` et le prix d'achat maximum baisse. La marge se fait à l'achat.

## Les signaux, dans l'ordre où ils bougent
| # | Signal | Ce qu'il dit | Source (vérifiée le 17/11/2026) | Type |
|---|---|---|---|---|
| 1 | **Taux des crédits à l'habitat** | le pouvoir d'achat immobilier, c'est le taux ; il bouge avant les prix | Banque de France, Stat Info mensuel « Crédits aux particuliers » (PDF, webstat) ; taux d'usure trimestriel | primaire |
| 2 | **Volume de ventes** | le volume chute ou repart avant les prix (2023 : volumes −20 % avant la baisse des prix) | DVF (notre extraction par commune, `sources.md`) ; nombre de ventes par trimestre dans les fichiers Fonciris | primaire |
| 3 | **Indice de prix à qualité constante** | l'évolution réelle, débarrassée du mélange de biens vendus | **Indice Fonciris** (jeu `6ace116dd047c826d7f7b3bd`) : trimestriel France / régions / départements, annuel pour 420 communes et 794 EPCI ; méthode hédonique sur DVF, corrélée à 0,973 avec Notaires-Insee | secondaire, méthode publiée |
| 4 | **Indice Notaires-Insee** et **avant-contrats** | la référence ; les avant-contrats regardent 3 mois devant | Insee (indices trimestriels) ; note de conjoncture des Notaires de France (web) | primaire |
| 5 | **Accessibilité** | le ménage médian de la commune peut-il acheter le logement médian ? | jeu Terralyse `6aa01497eb15f2bce626c53e` (3 822 communes, millésime 2026) | secondaire |
| 6 | **Stock et délais de vente** | l'offre s'accumule-t-elle ? | portails (annonces) : source **secondaire et biaisée**, à dire ; jamais comme comparable | secondaire |
| 7 | Macro, deux indicateurs au plus | coût des travaux (énergie), emploi de la zone (`territoire.md`) | Insee, Banque de France | contexte |

Ce qui n'est **pas** sur data.gouv (vérifié) : les séries de taux (OAT, crédits) et les indices
Notaires-Insee. On les lit sur les sites de la Banque de France et de l'Insee avec l'outil web ; sans
outil web, on donne le lien et on écrit « non consulté ».

## Lecture
1. Extraire pour le territoire (commune → EPCI → département, selon ce qui existe) : indice Fonciris
   et volumes sur 8 trimestres, médianes DVF sur 24 mois (`estimation.md`), accessibilité.
2. Poser le taux du mois et son sens sur 6 mois.
3. Qualifier, avec la grille :

| Lecture | Volumes | Prix (indice) | Taux | Accessibilité |
|---|---|---|---|---|
| **Marché d'acheteurs** | en baisse ou bas | stables ou en baisse | hauts ou en hausse | dégradée |
| **Équilibré** | en reprise | stables | stables | stable |
| **Marché de vendeurs** | en hausse | en hausse | en baisse | correcte |

Les cas mixtes sont la règle, pas l'exception : on l'écrit tel quel (« volumes en reprise, prix
encore en baisse : sortie de marché d'acheteurs **possible**, non confirmée »).

4. Écrire **ce qui invaliderait la lecture** (ex. : « si le taux moyen repasse au-dessus de X %, la
   reprise des volumes s'arrête »).
5. Dater chaque chiffre et rappeler le retard : Fonciris et DVF sont publiés avec 4 à 10 mois de
   décalage ; le taux est du mois ; les avant-contrats sont la seule donnée en avance.

## Exemple (Yvelines, extrait le 17/11/2026)
- Indice Fonciris « ensemble » 78 : 99,0 (2024T1) → 97,3 (2024T4) → 96,3 (2025T4) ; France : 105,2 →
  107,0 sur la même période. Les Yvelines baissent pendant que la France remonte.
- Volumes 78 : 12 089 ventes en 2024 → 14 610 en 2025 (+21 %).
- Lecture : **volumes en nette reprise, prix encore en baisse** → marché d'acheteurs en fin de
  cycle, sortie possible, non confirmée. À confirmer par le taux du mois et les avant-contrats.
- Le Chesnay-Rocquencourt n'a pas d'indice communal Fonciris (trop peu de ventes pour la méthode) :
  on lit l'EPCI (Versailles Grand Parc) et le département, et les médianes DVF de la commune.

## Jamais
- Un pourcentage de prix à horizon futur.
- Une lecture sans la colonne « ce qui l'invaliderait ».
- Un tableau de dix indicateurs pour faire sérieux : quatre suffisent, les autres sont du contexte.
