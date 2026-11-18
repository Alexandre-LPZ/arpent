# Journal des versions — Arpent

## 0.5.2 — 18 novembre 2026
- README bilingue (français, puis anglais complet) et lien vers la fiche de réutilisation
  data.gouv.fr (9 jeux de données rattachés).

## 0.5.1 — 18 novembre 2026
- Procédure d'activation de la passerelle PI précisée d'après l'email reçu (intitulé, expéditeur,
  page « réinitialisation » qui sert à définir le mot de passe, contact INPI).

## 0.5.0 — 18 novembre 2026
- **Marques, brevets, dessins et modèles : API PI de l'INPI** (`references/sources.md`), testée le
  18/11/2026 : recherche des marques françaises par SIREN du titulaire. Cas vérifié : la holding
  Renault SA n'a aucune marque, Renault s.a.s. en a 1 216. Nouvelle ligne « tue l'opération » dans
  `/actif` : titres exploités mais déposés au nom du dirigeant ou d'une autre entité. Même compte
  INPI, mais passerelle distincte avec son email d'activation ; procédure et pièges (jeton XSRF à
  relire à chaque appel) documentés. Brevets et modèles non testés, dit tel quel.
- Leçons du premier bilan réel avec l'API RNE (garage, Yvelines) : chemin « Mes accès API / SFTP »,
  actes souvent scannés (« à relire à la main »), service public injoignable → « non vérifié ».

## 0.4.0 — 18 novembre 2026
- **Comptes annuels et actes déposés : API RNE de l'INPI** (`references/sources.md`), testée le
  18/11/2026 sur une SARL de 2025 (aucun compte : l'API le dit) et sur un grand groupe (bilans saisis
  2024 et 2025 lus ligne à ligne). Source primaire, gratuite, compte ouvert par chaque utilisateur en
  trois minutes ; **aucun identifiant dans Arpent**, deux variables d'environnement sur la machine.
  Sans accès, Arpent écrit « comptes non consultés » et demande les liasses. Structure des bilans
  saisis et codes de liasse utiles documentés.
- `/actif` et la fiche sociétés renvoient à cette source pour les trois derniers exercices.

## 0.3.1 — 18 novembre 2026
Corrections après le premier test réel de `/actif` (SARL de négoce automobile, Yvelines) :
- Chaque ligne fiscale ou financière du tableau à rebours écrit sa **formule** (base × taux =
  montant) ; la base de la plus-value imposable est écrite en clair. Un montant qui ne se recalcule
  pas à partir du tableau est une erreur.
- Parts de société : le prix des parts additionne actif net corrigé et valeur du fonds **seulement si**
  le fonds n'est pas déjà au bilan (fonds acheté = immobilisation incorporelle à retirer avant).
- `/actif` : le verdict en une ligne vient en premier, comme pour les autres commandes.

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
