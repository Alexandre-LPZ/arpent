# Journal des versions — Arpent

## 0.8.3 — 20 novembre 2026
- **Pièces visuelles** : toute photo ou plan disponible est exploité, y compris à l'intérieur d'un PDF,
  d'un Word, d'une annonce ou d'une page web (rendre les pages en images si l'outil n'extrait que le
  texte). Observation écrite « vu sur photo (source, date) », valeur d'indication : hypothèse étayée,
  jamais pièce vérifiée ni expertise ; peut dégrader une réponse de fiche, jamais l'améliorer ; ce qui
  n'est pas photographié s'écrit « non vu ». Règle dans `terrain-regles.md`, rappel dans SKILL.md et
  dans les commandes `bilan`, `fiche-bien`, `estimer`, `actif`. Née d'un cas réel : un dossier de
  diagnostic et une expertise en PDF lus sans leurs photos.

## 0.8.2 — 20 novembre 2026
- Aperçu et présentation : Arpent dit d'abord **pour qui** il est — les marchands de biens, et tous
  ceux qui cherchent, achètent et revendent avec la même méthode (investisseurs, agents immobiliers,
  apporteurs d'affaires, ceux qui travaillent avec un marchand de biens). Même phrase dans
  `marketplace.json` (l'aperçu du panneau Cowork), `plugin.json`, le README (FR/EN) et le SKILL.md.

## 0.8.1 — 19 novembre 2026
- Livrables : tout résultat à conserver ou transmettre sort **en Markdown (source, pour l'humain et
  l'IA) et en PDF (envoi)**, Word seulement si un tiers doit modifier ; nommage des fichiers.

## 0.8.0 — 19 novembre 2026 — les six fiches de terrain
- Trois nouvelles fiches dictées par le marchand : `terrain-vehicules.md` (liquidité du modèle,
  historique, état réel, configuration, cessibilité et import, canal, durée, stress test),
  `terrain-oeuvres.md` (marché secondaire pour ce type d'œuvre, représentativité, conservation,
  circulation et biens culturels, canal et net vendeur, solidité du prix, détention, net en scénario
  défavorable), `terrain-bateaux.md` (marché, état au-delà de l'apparence, obsolescence, juridique et
  TVA historique, garde et déplacement, coûts de détention, commercialisation, stress test à six mois).
- `terrain-regles.md`, règles communes aux six classes : une information manquante n'est jamais un A ;
  un défaut chiffrable réduit le prix et modifie frais, imprévus ou délai ; un blocage non résolu
  suspend l'engagement, une baisse de prix ne le supprime pas ; le GO se conditionne à la marge en
  euros, à la liquidité et à la trésorerie. **Quatre verdicts** : GO, À SÉCURISER / RENÉGOCIER,
  **NO GO en l'état** (réexaminable après pièce, expertise ou régularisation), **NO GO définitif**.
  Chaque question doit modifier une variable du tableau à rebours ou produire un blocage, sinon elle
  sort de la fiche.
- Les trois premières fiches et `/bilan`, `/actif` renvoient aux règles communes.

## 0.7.2 — 19 novembre 2026 — fiche de terrain, classe 3 : parts de société et fonds de commerce
- Nouvelle fiche `references/terrain-parts-fonds.md`, dictée par le marchand : fonds ≠ parts (tableau),
  trois valeurs à ne pas confondre (comptable, exploitation, revente), huit questions d'avant-signature
  (périmètre transféré, rentabilité reproductible, trésorerie à financer, continuité dès le lendemain,
  équipe et engagements sociaux, investissements de maintien, garanties mobilisables, sortie et
  durée), et pour chaque réponse défavorable **le levier** : baisse de prix, provision, garantie,
  délai, ou impossible.
- Règle nouvelle, appliquée aussi dans `actif.md` : **le risque inconnu ne se provisionne pas** pour
  faire passer l'opération ; il s'écrit « manquant » et appelle l'audit ou l'abandon. Fin de l'aléa
  forfaitaire « comptes non vus » sur les parts et les fonds.
- `/actif` lit la fiche quand ses réponses sont dans le message.

## 0.7.1 — 19 novembre 2026 — fiche de terrain, classe 2 : commerces et bureaux
- Nouvelle fiche `references/terrain-commerces-bureaux.md`, dictée par le marchand : commerce et
  bureau lus séparément (ce qui fait la valeur, ce qu'on regarde sur place, contraintes propres,
  ce que le public donne), huit questions avec **effets chiffrés** (décotes bornées, délais, imprévus),
  deux valeurs de sortie (utilisateur sur ventes signées / investisseur = revenu net ÷ rendement),
  tableau à rebours à deux colonnes, grille de décision, les trois pièges (décote ≠ opportunité,
  loyer artificiel, transformation spéculative). Pas de score additionné : des paramètres.
- Classe 1 : Q8 se donne en euros (la lettre se déduit du calcul) ; décote Q6 = C bornée à 5–10 %.
- `reglementation.md` : la lésion s'apprécie sur la valeur du bien dans son état, pas rénové (vu
  au test du 19/11).

## 0.7.0 — 19 novembre 2026 — fiche de terrain, classe 1 : habitation
- Nouvelle fiche `references/terrain-habitation.md`, **dictée par le marchand de biens** : huit
  questions (prix de sortie, état et travaux, configuration, obstacles juridiques, occupation,
  défauts à la revente, calendrier jusqu'à l'encaissement, marge et capital), réponses A à D et ce
  que chacune change dans le calcul.
- Quatre étiquettes obligatoires sur chaque ligne d'un bilan : **pièce vérifiée / déclaré /
  hypothèse / manquant**. Une date de visite ne transforme pas une déclaration en fait.
- Tableau à rebours opérationnel (revente HT, TVA traitée à part, scénarios central et prudent,
  capital immobilisé) et **grille de décision** GO / À SÉCURISER-RENÉGOCIER / NO GO : première
  réponse bloquante, jamais de moyenne. La marge se définit en euros ; la cible 5–15 % devient un
  contrôle.
- `/bilan` lit la fiche si elle est dans le message, sinon termine par les questions sans réponse.
- `sources.md` : conseil d'installation de pyarrow quand il manque (vu au test du 19/11).

## 0.6.1 — 19 novembre 2026
- **BDNB testée** : l'API Open ne demande ni compte ni clé (10 000 appels/mois/IP). Géocodage puis
  données par clé BAN ; champs utiles et limites de couverture documentés sur deux adresses réelles.
  La 0.6.0 disait « compte gratuit requis » : c'était faux, corrigé.

## 0.6.0 — 19 novembre 2026 — « le bâti et son environnement »
Issue de la revue de 38 « sites pratiques » d'un architecte : 5 sources publiques retenues, les
autres écartées ou renvoyées au professionnel (`fiche-bien.md`, colonne « où chercher »).
- `/fiche-bien` réorganisé en six thèmes : parcelle et propriété, bâti, contraintes, environnement,
  projets, prix. Verdict en tête ; chaque donnée absente dit où la chercher.
- **Servitudes AC1 / AC4** (abords de monuments, sites patrimoniaux) lues sur l'API Carto GPU —
  testé : le centre du Chesnay-Rocquencourt est dans les abords du Domaine de Versailles.
- **Fibre** (ARCEP, commune et immeuble) — testé : 98 % des locaux éligibles à 78158.
- **Antennes relais** (ANFR, supports avec hauteur et coordonnées) — testé : 30 supports à 78158.
- **Propriétaires personnes morales** (DGFiP, version unifiée parquet) — testé : 972 parcelles à
  78158. Jamais de recherche sur une personne physique (règle 4).
- **BDNB** (bâti : année, matériaux, hauteur) : accès documenté (API, compte gratuit, 10 000
  appels/mois, variable `BDNB_API_KEY`), **appels non testés** faute de compte ; sans accès, repli sur
  les DPE ADEME et « bâti : non documenté ».
- `vendeur.md` : lecture de l'historique d'une annonce (outil du professionnel, prix affichés,
  « déclaré »).

## 0.5.3 — 19 novembre 2026
- Description du plugin dans `marketplace.json` mise à jour (marché, actifs, INPI) : c'est elle que
  l'app Claude affiche dans la liste des plug-ins.

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
