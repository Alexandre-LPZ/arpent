# Journal des versions — Arpent

## 0.3.0 — 18 novembre 2026
- **Nouveau module `/actif`** (`references/actif.md`) : le marchand de biens, c'est l'intention de
  revendre, pas la nature du bien. Même méthode à rebours que `/bilan`, appliquée aux parts de
  société et fonds de commerce, véhicules de collection, œuvres et objets, bateaux : sources de prix
  **réalisés** (enchères, cessions publiées, jamais des prix demandés), frais et fiscalité par classe
  (régime de la marge, droit de suite, taxe forfaitaire, droits d'enregistrement — tous « à valider »),
  ce qui tue l'opération. Rappel : garder l'actif au lieu de le revendre change le régime.
- Les prix de référence hors immobilier ne sont pas sur data.gouv : Arpent les lit avec l'outil web
  (résultats d'enchères cités avec maison, date et lot) ou écrit « non consulté ».

## 0.2.0 — 17 novembre 2026
- **Nouveau module `/marche`** (`references/marche.md`) : lecture du marché d'un territoire —
  acheteurs / équilibré / vendeurs — à partir du taux des crédits, des volumes, de l'indice de prix
  à qualité constante (Fonciris, sur DVF), des indices Notaires-Insee et de l'accessibilité. Chaque
  chiffre daté, la colonne « ce qui invaliderait la lecture » obligatoire, **jamais de prévision
  chiffrée**. Exemple vérifié sur les Yvelines. Branché sur `/bilan` : la lecture durcit ou
  assouplit l'hypothèse de revente.
- Deux jeux ajoutés à `sources.md` : indice Fonciris (`6ace116d…`) et accessibilité Terralyse
  (`6aa01497…`). Vérifié : les séries de taux et Notaires-Insee ne sont pas sur data.gouv.

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
