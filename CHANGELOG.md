# Journal des versions — Arpent

## 0.1.1 — 17 novembre 2026
Corrections issues du premier test réel (Le Chesnay-Rocquencourt, 78158) :
- **Emploi** : la grille d'attractivité mesure l'emploi *au lieu de travail* et l'indice de
  concentration de l'emploi, plus seulement les actifs résidents. Deux jeux de données vérifiés
  ajoutés à `sources.md`.
- **Grands équipements** : nouveau critère (centre commercial régional, hôpital, campus…) avec la
  requête Sirene qui fait sortir les grands employeurs d'une commune, et sa limite (effectif de
  l'unité légale, pas de l'établissement).
- **Vendeur** : nouvelle fiche `vendeur.md` — prix affiché ≠ prix de marché, décalage compromis →
  acte, qualification A/B/C, mandat exclusif, bien surexposé.
- **DVF** : procédure d'extraction testée (fichier national par année, filtre par commune), règles
  de nettoyage écrites pour que deux calculs donnent le même chiffre, interdiction de parler de
  « tendance » sous l'écart interquartile.

## 0.1.0 — 17 novembre 2026
Première version : connecteur data.gouv.fr + skill métier (bilan de marchand de biens, estimation
DVF, fiche d'un bien, attractivité d'une commune, construction prête à finir, succession) et
garde-fous réglementaires français. Cinq commandes : `/bilan`, `/estimer`, `/fiche-bien`,
`/ville`, `/succession`.
