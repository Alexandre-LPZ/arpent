# Contrepartie — la position du vendeur, côté acheteur

Doctrine de la maison (règle du 24/11/2026). Mieux on achète, mieux la marge est protégée.
Un vendeur a une motivation, une urgence, des besoins et des attentes. Ce qu'il dit (« je ne suis pas
pressé ») est **déclaré** ; les pièces publiques peuvent le confirmer ou le contredire. L'écart entre
les deux est un levier de négociation, et il s'écrit avec sa source et sa date comme tout le reste.

`vendeur.md` lit le vendeur du côté de l'agent qui le conseille ; ce module le lit du côté de
**l'acheteur** (marchand, investisseur). Il ne sert qu'à une acquisition réellement envisagée.

## Le champ : ce qu'on vérifie, ce qu'on ne cherche jamais
**Point d'entrée** : le vendeur tel qu'il figure dans les **pièces de la vente** (annonce, mandat,
avant-contrat, titre, diagnostics, expertise). Chaque vendeur s'ils sont plusieurs. C'est la
contrepartie d'une transaction en cours : la vérifier est de la due diligence, l'usage même pour
lequel les registres des sociétés sont publics.

- **Vendeur personne morale** (SCI, société, holding) : tout ce que publient les registres des
  sociétés et la publicité foncière.
- **SCI ou société détenue par quelques personnes** : son gérant et ses associés publiés (statuts,
  RNE) sont la **contrepartie économique**. Ils décident de la vente et, dans une société civile,
  répondent indéfiniment des dettes sociales à proportion de leurs parts (C. civ., art. 1857). On
  applique à chacun la règle du vendeur personne physique ci-dessous, et l'on note qui détient la
  majorité : c'est souvent lui, ou elle, qui décide. Au-delà (actionnaires d'une société cotée,
  fonds, sociétés à actionnariat large), non.
- **Vendeur personne physique** : ses **mandats de dirigeant et participations** publiés dans les
  registres des sociétés, puis l'analyse de ces sociétés. Avant tout usage, **écarter l'homonymie** :
  date de naissance portée par l'acte ou l'avant-contrat (filtre de Recherche d'entreprises), à
  défaut année de naissance (Recherche d'entreprises) puis mois et année (RNE), et commune du siège ou
  du domicile figurant dans les pièces. Sans contrôle concluant, la société s'écrit « non attribuée » et ne
  compte pas.
- **Hors champ, toujours** :
  - la vie privée : domicile hors des pièces, famille, santé, mœurs, réseaux sociaux personnels,
    état civil au-delà du contrôle d'homonymie ;
  - toute personne étrangère à la vente : les coassociés et co-dirigeants du vendeur **dans ses
    autres sociétés** apparaissent tels que ces sociétés les publient, sans recherche sur eux ;
  - tout contact avec un tiers sous un prétexte ;
  - les registres à accès restreint : registres des bénéficiaires effectifs (accès du public fermé
    depuis l'arrêt de la CJUE du 22/11/2022), fichiers bancaires (en France, aucun registre public
    des dettes d'un particulier) ; on ne contourne pas ;
  - toute fiche publiée ou conservée au-delà du dossier.
- **Données personnelles** : une donnée publique sur une personne reste une donnée personnelle.
  Traitement fondé sur l'intérêt légitime de l'acquéreur, limité à ce dossier, minimal, effacé avec
  lui. **À valider avec l'avocat.**

**Sobriété** : on ne fouille pas tout. Ordre de travail : (1) les pièces de la vente, (2) les
mandats du vendeur, (3) BODACC, (4) les comptes des seules sociétés liées au bien ou en difficulté,
(5) l'étranger seulement si une piste y mène. On s'arrête dès que la réponse V est établie.

## Où chercher
| Couche | Ce qu'on y lit | Source | Accès |
|---|---|---|---|
| **Le bien** | hypothèques, privilèges, commandement de payer valant saisie | service de la publicité foncière : demande de renseignements sur l'immeuble, ou par le notaire | payant, sur demande ; le résultat est une **pièce vérifiée** |
| | origine de propriété : date et prix d'acquisition par le vendeur → durée de détention, plus-value latente | titre de propriété ou avant-contrat (pièce) | par le notaire, le vendeur ou l'agent |
| | historique des mutations de la parcelle | DVF, sur la **parcelle** : un fait du bien, jamais un moyen d'identifier qui que ce soit | public |
| | durée de commercialisation, baisses de prix | annonces et leur historique (`vendeur.md`) | déclaré / indication |
| | vente forcée annoncée | tribunal judiciaire ; annonces d'adjudications | public |
| **Les sociétés (France)** | mandats d'un dirigeant | API Recherche d'entreprises : `nom_personne`, `prenoms_personne`, `type_personne=dirigeant` (renvoie l'année de naissance) | gratuit, sans compte ; **testé le 24/11/2026** |
| | procédures collectives, radiations, cessions, dissolutions | BODACC | gratuit |
| | capitaux propres, dettes financières et leurs échéances, pertes ; associés (statuts) | API RNE de l'INPI, **par SIREN uniquement** (comptes et actes) | compte gratuit ; comptes confidentiels → « manquant » |
| | privilèges du Trésor et de la sécurité sociale, nantissements | état des inscriptions au greffe (Infogreffe) | payant |
| **Hors de France** | existence, dirigeants, publications, faillites | Luxembourg : LBR, RESA · Suisse : Zefix, FOSC · Belgique : BCE, Moniteur belge · Royaume-Uni : Companies House · Allemagne : Handelsregister | conditions **à vérifier à l'usage** ; registre payant ou sur intérêt justifié : le dire et s'arrêter |
| | Suisse : poursuites pour dettes d'un vendeur domicilié en Suisse | office des poursuites du domicile : extrait sur **intérêt rendu vraisemblable** (LP, art. 8a) | **à valider avec l'avocat** ; une négociation réelle et documentée, jamais une curiosité |

### Pappers (optionnel, payant)
Pappers redistribue les mêmes sources (RNE, BODACC, comptes, Sirene) et y ajoute la cartographie
des liens entre sociétés, des ratios calculés et un scoring. Chaque appel consomme des crédits du
compte de l'utilisateur (testé le 24/11/2026 : un compte gratuit sans crédit voit l'appel refusé).
Arpent part des sources gratuites ; il n'utilise Pappers qu'avec l'accord de l'humain, en annonçant
la dépense quand l'outil l'indique, et **toujours avec des `return_fields` explicites** (les champs
par défaut ramènent tout).
- **Autorisé**, sur le vendeur et ses sociétés : `recherche-dirigeants` (filtre de date de
  naissance ; champs nom, prénom, date de naissance, qualités, entreprises, jamais l'adresse) ;
  `cartographie-entreprise`, `informations-entreprise` (procédures collectives, publications
  BODACC, actes, finances) et `comptes-entreprise` (dettes financières, dettes à un an au plus,
  autonomie financière), par SIREN ; décisions de justice **par SIREN** d'une société. Sur le bien :
  `recherche-parcelles` **par numéro de parcelle**, ou par SIREN d'une société du vendeur.
- **Interdit** : rechercher des parcelles par le nom ou l'âge d'un propriétaire ou d'un occupant
  personne physique, et tout champ `personnes_physiques`, email, téléphone ou réseau social ; les
  bénéficiaires effectifs (`recherche-beneficiaires`, champ `beneficiaires_effectifs`) : registre
  fermé au public, une copie reste un contournement ; `conformite-personne-physique` (personne
  politiquement exposée, sanctions) : c'est le contrôle du notaire ; emails et LinkedIn des
  dirigeants.
- Le `scoring_financier` (30 crédits, sur demande seulement) est une **indication Pappers**, pas un
  fait : il s'écrit « score Pappers (date) », jamais comme une pièce.

## La question V : position du vendeur
Commune à toutes les fiches de terrain (`terrain-regles.md`), posée après les huit questions de la
classe. Les lettres vont de « aucune contrainte » (A) à « vente forcée » (D).

| Réponse | Ce que disent les pièces | Effet sur la stratégie |
|---|---|---|
| **A** | aucune contrainte établie : pas d'inscription significative, sociétés saines, longue détention, durée de vente normale | négociation serrée : offre au prix maximal ou pas d'offre ; ne pas compter sur une remise |
| **B** | indices sans pièce : longue commercialisation, baisses successives, propos du vendeur ou de l'agent | offre d'ouverture sous le prix maximal, validité courte |
| **C** | contrainte **établie par pièce** : inscription importante sur le bien, échéance datée, procédure collective ou pertes lourdes dans une société qu'il dirige | offre ferme et rapide, conditions suspensives réduites, financement prouvé : la **certitude** est ce que ce vendeur achète |
| **D** | vente forcée en cours : commandement valant saisie publié, liquidation | le canal change : vente amiable autorisée par le juge, adjudication ou liquidateur, avec leurs règles et leur calendrier (**à valider avec l'avocat**) |

Deux règles de lecture, symétriques de « manquant n'est jamais A » :
- **Sans pièce, jamais C ni D.** Un propos (« je suis pressé », « je ne suis pas pressé ») et des
  indices font au mieux un B. Une société d'homonyme non écarté ne compte pas.
- **V non recherchée s'écrit « V non établie »** et la négociation se mène comme en A, l'hypothèse
  prudente pour l'acheteur. La V ne bloque jamais un GO.

**Règle d'or** : la position du vendeur ne modifie **jamais le prix d'achat maximal**. Celui-ci vient
de la revente, des coûts et de la marge (`marchand.md`). Elle modifie la **chance d'y arriver**,
l'**offre d'ouverture**, le **calendrier** et les **conditions**. Un vendeur pressé ne rend pas bonne
une mauvaise opération.

## Les limites légales de la négociation (à valider avec l'avocat)
- **Lésion** : le vendeur d'un immeuble lésé de plus des 7/12, donc payé moins des **5/12 de la
  valeur du bien dans son état**, peut demander la rescision pendant deux ans (C. civ., art. 1674 et
  s., `reglementation.md`). Toujours situer l'offre face à ce seuil.
- **Abus de l'état de dépendance** : il y a violence quand une partie abuse de l'état de dépendance
  de son cocontractant **à son égard** et en tire un avantage manifestement excessif (C. civ.,
  art. 1143) ; sanction : nullité. La gêne financière du vendeur n'est pas, en soi, une dépendance
  envers l'acheteur ; une offre basse sur une contrainte connue reste **justifiée par le tableau à
  rebours**, qui est la meilleure protection.
- **Ce qu'on tait, ce qu'on ne dit pas faux** : l'acheteur n'a pas à révéler sa propre estimation
  de la valeur (C. civ., art. 1112-1 al. 2 et 1137 al. 3), ni ce qu'il sait de la situation du
  vendeur. Il n'affirme rien de faux, ni sur lui ni sur les faits (dol, art. 1137).
- **Mandataire du vendeur lié à l'acheteur** (parent, associé, conjoint) : le mandataire doit
  loyauté à son mandant et ne peut utiliser contre lui ce qu'il sait par son mandat ; transparence
  écrite obligatoire (`vendeur.md`, `succession.md`). Si c'est le cas, le dire en tête du bilan et
  ne rien tirer de lui sur le vendeur.

## Format de sortie
Dans le bilan, après le verdict et le tableau à rebours, une section **« Position du vendeur »** :
1. les faits : tableau *fait / source / date / étiquette* ;
2. le contrôle d'homonymie : méthode et résultat ;
3. la réponse V (A à D) et pourquoi ;
4. la stratégie : offre d'ouverture (montant, écart au prix maximal, position face au seuil de
   lésion), validité, conditions, calendrier ;
5. ce qui manque, et où le trouver.

Cette section est **interne** : elle reste dans le `.md` du dossier ; le PDF destiné à un tiers
(banquier, associé) l'omet par défaut, et elle ne va jamais au vendeur ni à son mandataire.
