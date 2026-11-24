# Fiche d'un bien ou d'une parcelle (diligences avant offre)

Pour une adresse ou une référence cadastrale, réunir **par thème**, chaque ligne avec sa source et
sa date. Une page. Une ligne n'y entre que si elle peut changer une décision (acheter, à quel prix,
quels travaux, quel délai). Ce que les données publiques ne donnent pas est écrit dans la colonne
« où chercher », jamais deviné.

## 1. Parcelle et propriété
- **Cadastre** : parcelle(s), contenance, forme, accès sur rue (API Carto Cadastre).
- **Propriétaire** : si c'est une **personne morale** (société, SCI, collectivité, État, bailleur),
  son nom, sa forme et son SIREN sont publics : fichier des parcelles des personnes morales (DGFiP,
  `sources.md`). Si la parcelle n'y figure pas, écrire « propriétaire : particulier, non recherché »
  (règle 4) ; on ne cherche jamais qui. Si ce propriétaire est le vendeur d'une acquisition
  envisagée, son nom vient des pièces de la vente, et sa position se lit par `contrepartie.md`,
  jamais par le cadastre.
- **Division en cours ou passée** : DVF (ventes de lots de la même parcelle).

## 2. Bâti
- **Ce que le bâti est** : année de construction, matériaux, hauteur, nombre de logements, DPE
  rattachés. Source : **API BDNB Open** (CSTB, sans clé, `sources.md`) ; un champ vide s'écrit « non
  renseigné (BDNB) ». En complément, l'année et la surface apparaissent souvent dans les DPE de
  l'adresse (ADEME). Sans rien : « bâti : non documenté, à relever sur place ».
- **État** : pas de donnée publique. Trois niveaux à faire déclarer par le professionnel (coup de
  frais / rénovation / lourd) et un montant de travaux **par devis**, jamais par ratio. Étiquette
  « déclaré, visite du … ».
- **Énergie** : DPE connus à l'adresse (ADEME), ce que la classe implique (interdiction de louer les
  G, puis F, puis E : `reglementation.md`).

## 3. Contraintes : ce qui limite ce qu'on peut faire
- **PLU** : zone, règles principales (hauteur, emprise, recul), prescriptions ; révision en cours
  (API Carto GPU). Conclure sur la **divisibilité** et le **potentiel d'extension** comme hypothèse,
  à confirmer par un certificat d'urbanisme.
- **Servitudes d'utilité publique** (API Carto GPU, couche `assiette-sup-s`) : en particulier
  **AC1 abords de monument historique** et **AC4 site patrimonial remarquable** = avis de
  l'Architecte des Bâtiments de France sur tout permis et toute déclaration de travaux : délais
  allongés, matériaux imposés. Lire `suptype`, `typeass`, `nomsuplitt`. Cas vérifié le 19/11/2026 : le
  centre du Chesnay-Rocquencourt est dans le périmètre des abords du Domaine national de Versailles.
- **Risques** : inondation, argiles, **cavités et anciennes carrières**, sols pollués (BASOL, BASIAS :
  ancien usage industriel ou station-service), installations classées, arrêtés de catastrophe
  naturelle (API Géorisques ; GASPAR si l'API est injoignable).
- **Réseaux enterrés** : pas de donnée ouverte à la parcelle ; avant tout terrassement, la
  déclaration DT-DICT est obligatoire (reseaux-et-canalisations.ineris.fr, compte). À écrire comme
  étape, pas comme donnée.
- **Friche** : la parcelle figure-t-elle dans Cartofriches ?

## 4. Environnement
- **Fibre** : éligibilité à l'adresse ou, à défaut, part des locaux éligibles dans la commune
  (ARCEP « Ma connexion internet », `sources.md`). Un argument de revente ; une absence est une
  décote.
- **Antennes relais** : supports ANFR dans un rayon de 300 m, avec hauteur et type ; un support
  visible depuis le bien est une décote connue à la revente (`sources.md`). Pas de jugement
  sanitaire : la distance et la visibilité, c'est tout.
- **Orientation et ombres** : pas de donnée publique exploitable ; « à regarder avant visite » avec
  un outil d'ensoleillement (suncalc.org, jveuxdusoleil.fr, shadowmap.org) et Street View.
- **Usage passé du site** : photos aériennes anciennes (remonterletemps.ign.fr) : un atelier, une
  cuve, une station-service visibles sur les clichés = risque de pollution à faire lever (étude de
  sol). « À regarder avant offre ».
- **Nuisances** : voies bruyantes (classement sonore des infrastructures, en préfecture ou sur le
  GPU), aéroport (PEB).

## 5. Projets autour
- Ce que les données donnent : PLU en révision (GPU), ZAC et opérations d'aménagement (GPU,
  prescriptions), gares et lignes en projet (`territoire.md`).
- Où chercher le reste : concertations et conseils municipaux (site de la ville), permis délivrés
  (Sitadel, par commune, non géolocalisé ; registre des permis en mairie ; Géofoncier pour la
  localisation), programmes des aménageurs (EPFIF, EPA).

## 6. Prix
- **Historique** : ventes DVF de la parcelle et des voisines (sans données personnelles).
- **Marché** : médiane et quartiles du secteur (`estimation.md`), lecture du marché (`marche.md`).

## Format de sortie
Verdict en une ligne (ce que le bien permet, et le point qui bloque s'il y en a un), puis les six
thèmes en tableau court, puis :
- **potentiel** (ce que le bien permet),
- **risques** (ce qui peut faire perdre de l'argent),
- **à vérifier sur place ou en mairie**, avec pour chaque point **où** (lien ou service),
- **déclaré par le professionnel** : les lignes qui viennent de lui, datées.
