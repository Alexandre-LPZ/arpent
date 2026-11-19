# Sources — où trouver chaque donnée (vérifiées le 17/11/2026 sur data.gouv.fr)

Partir de ces identifiants avec `get_dataset_info` / `list_dataset_resources`. Toujours relire la date
de dernière mise à jour avant de citer un chiffre.

## Prix et transactions
| Donnée | Jeu de données | Organisme | ID data.gouv |
|---|---|---|---|
| Ventes immobilières (prix, surface, type, date) | Demandes de valeurs foncières (DVF) | DGFiP | `5c4ae55a634f4117716d5656` |
| DVF géolocalisé, fichiers par commune | Demandes de valeurs foncières géolocalisées | data.gouv.fr | `5cc1b94a634f4165e96436c1` |
| DVF enrichi, séries longues | DVF+ open-data | Cerema | `5d78f093634f411f434cd637` |
| Indicateurs de prix agrégés par commune | Données valeurs foncières à la commune par période | Caisse des Dépôts | `62e9bbe102256eedbd0505d1` |
| **Indice de prix à qualité constante** (hédonique sur DVF), trimestriel France/régions/départements, annuel 420 communes et 794 EPCI, base 100 = 2021T1, avec nombre de ventes | Indice Fonciris des prix des logements anciens | Fonciris (tiers, note de méthode publiée, corrélé 0,973 à Notaires-Insee) | `6ace116dd047c826d7f7b3bd` — fichiers `indice-departements.csv`, `indice-communes-annuel.csv`, `indice-epcis-annuel.csv` (colonnes `periode, indice, ic_bas, ic_haut, ventes, code, type`) |
| Accessibilité : le ménage médian peut-il acheter le logement médian ? (3 822 communes, 2026) | Acheter dans sa ville | Terralyse (tiers, à partir de DVF, Insee, Banque de France) | `6aa01497eb15f2bce626c53e` |

Limites DVF à connaître : mise à jour **semestrielle** (décalage de plusieurs mois) ; les ventes
d'Alsace-Moselle (livre foncier) et de Mayotte n'y figurent pas — à confirmer sur la fiche du jeu ;
**données personnelles** : réutilisation encadrée par la DGFiP, aucune ré-identification des parties.

### Extraire les ventes d'une commune — procédure testée le 17/11/2026 (Le Chesnay-Rocquencourt, 78158)
Le jeu `5cc1b94a634f4165e96436c1` publie **un fichier national par année** (et par semestre pour
l'année en cours), au format csv.gz, plus un fichier unique sur 5 ans (≈ 580 Mo, à éviter).
1. `list_dataset_resources` sur ce jeu → repérer les ressources des années voulues.
2. **Aperçu** : `query_resource_data` avec `filter_column = code_commune`, `filter_value = <code Insee>`
   (ex. ressource 2026 S1 `4fa87df4-ac08-447f-8460-2daed16c2cfb` → 377 lignes pour 78158). Bon pour
   compter et vérifier les colonnes ; **ne pas paginer des centaines de lignes dans la conversation**.
3. **Calcul** : si un shell est disponible, télécharger le fichier national de l'année (URL donnée par
   `get_resource_info`), le filtrer à la volée sur `code_commune` (11e colonne) et calculer en code.
   Testé : 2026 S1, 49 Mo, 377 lignes extraites, identique au comptage de l'API tabulaire.
   L'API tabulaire en REST direct a renvoyé des 504 répétés sur la pagination : ne pas en dépendre.
4. Sans shell : rapporter le comptage et l'aperçu, et dire que le calcul complet n'a pas été fait.

À ne plus utiliser : les fichiers par commune `files.data.gouv.fr/geo-dvf/latest/csv/<année>/communes/…`
(archive « livraison avril », sans 2026, annoncée **supprimée fin novembre 2026**). La ressource CSV
de la Caisse des Dépôts (`62e9bbe1…`) **n'est pas** dans l'API tabulaire, et son API OpenDataSoft
était instable le 17/11/2026 : source d'appoint seulement.

## Emploi et dynamisme (vérifiés le 17/11/2026 sur 78158)
| Donnée | Jeu de données | Organisme | ID / ressource |
|---|---|---|---|
| Indice de concentration de l'emploi par commune (2012, 2017, 2023) : emplois pour 100 actifs résidents, avec numérateur (emplois) et dénominateur | Indice de concentration de l'emploi | Tableau de bord des mobilités durables (source Insee RP) | jeu `69b9896d1c7cf501adf140fa`, ressource commune `b4f1bb42-ab1b-4493-8639-0b2ab7a9fb3b` (6,8 Mo, colonnes `annee, geocode_commune, valeur, numerateur, denominateur`) |
| Emplois au lieu de travail par grand secteur (NA5, RP 2021) | Emplois au lieu de travail par grand secteur d'activité | TACCT (source Insee) | jeu `6a5e2c6ef1e50b63d84e2b8b`, ressource `066a8328-e72d-40fc-901c-dd48a01d5198` (séparateur `;`, colonne `code_geographique`, sommes `NA5AZ…NA5OQ`) |
| Établissements d'une commune, par tranche d'effectifs (grands équipements, employeurs) | Sirene | Insee | API Sirene / Recherche d'entreprises — attention : l'effectif est celui de l'unité légale, pas de l'établissement, sauf champ dédié |

Exemple 78158 (2023) : indice 93, soit 12 509 emplois pour 13 433 actifs résidents ; 11 699 emplois
RP 2021 dont 5 597 commerce-services et 5 527 administration-santé-éducation. Vélizy : indice 339.

Trouver les grands équipements d'une commune (testé le 17/11/2026) :
`https://recherche-entreprises.api.gouv.fr/search?code_commune=<insee>&tranche_effectif_salarie=42,51,52,53`
liste les unités légales de 500 salariés et plus ayant un établissement dans la commune — l'effectif
est celui de l'unité légale entière (La Poste, EDF…), pas de l'établissement local : lire les
adresses des établissements, pas le chiffre. Sur 78158, cette lecture a fait apparaître le Centre
hospitalier de Versailles (siège 177 rue de Versailles, hôpital André-Mignot, SIREN 267802718, tranche
2 000-4 999 salariés), les enseignes de Parly 2 et un hôpital privé (21 rue Moxouris). Le siège d'un
groupe privé (Ramsay) est ailleurs : son établissement local n'apparaît qu'en cherchant l'adresse.
Fréquentation d'un centre commercial : chiffre de l'exploitant via la presse (ex. Westfield Parly 2 :
« 12 millions de visiteurs » en 2024, +5,5 %, 190 boutiques — mesinfos.fr, 07/03/2025, interview de la
directrice, non audité).

## Le bien et la parcelle
| Donnée | Source | Accès |
|---|---|---|
| Parcelles, contenances, géométries | API Carto — module Cadastre (IGN) | `https://apicarto.ign.fr/api/cadastre` |
| Cadastre Etalab par commune | API Cadastre (data.gouv.fr) | `https://cadastre.data.gouv.fr/bundler/cadastre-etalab/` |
| Zonage PLU, servitudes, prescriptions | API Carto — Géoportail de l'Urbanisme (IGN) | `https://apicarto.ign.fr/api/gpu` |
| Risques naturels et technologiques, catastrophes naturelles | API Géorisques (BRGM) | `https://georisques.gouv.fr/api/v1/` |
| DPE des logements existants (depuis 07/2021) | ADEME | jeu `67f7e557cb268460ce66c8d4` |
| DPE avant 07/2021 / logements neufs | ADEME | `5ee2391763c79811ddfbc86a` / `67f7e5758ffc5d79ab9e8c27` |
| Friches recensées | Sites référencés dans Cartofriches (Cerema) | `61892a26c94e39bde1dbf7ac` |
| **Propriétaire personne morale** (société, SCI, collectivité, État) | Fichier des parcelles des personnes morales (DGFiP), version unifiée parquet | `6900772ca5c4fa6c5687b3bd` |
| **Fibre à l'adresse / dans la commune** | ARCEP « Ma connexion internet » | `5e836644ca07c8558d91a6fc` |
| **Antennes relais (supports, hauteur, type)** | ANFR, installations radioélectriques > 5 W | `551d4ff3c751df55da0cd89f` |
| **Bâti : année, matériaux, hauteur, DPE rattachés** | API BDNB Open (CSTB), sans clé, 10 000 appels/mois/IP | `61dc7157488f8cdb4283e3c3` |

### Servitudes AC1 / AC4 (abords de monuments, sites patrimoniaux) — testé le 19/11/2026
API Carto GPU, `GET https://apicarto.ign.fr/api/gpu/assiette-sup-s?geom=<GeoJSON Point>` → chaque
`feature.properties` donne `suptype` (`ac1` abords, `ac4` site patrimonial remarquable…), `typeass`
(« Périmètre des abords »), `nomsuplitt` (le monument), `fichier` (l'acte). Même appel avec
`zone-urba` pour le zonage PLU (`libelle`, `typezone`, `partition` = `DU_<insee>`). Cas vérifié :
point 2.1226 / 48.8277 (Le Chesnay) → AC1 « Domaine national de Versailles et de Trianon »,
périmètre des abords, acte du 07/07/2016 ; point 2.1301 / 48.8049 → AC4 « Site patrimonial
remarquable de Versailles ». Conséquence à écrire : avis de l'ABF sur tout permis.

### Fibre — ARCEP « Ma connexion internet » (testé le 19/11/2026)
Les ressources de data.gouv.fr renvoient vers des dossiers sur `data.arcep.fr` (suivre les
redirections, `curl -L`). Deux niveaux :
- **Commune** : `https://data.arcep.fr/fixe/maconnexioninternet/statistiques/last/commune/commune_techno.csv`
  (2,3 Mo, `;`) : `code_insee`, `nbr` (locaux), `elig_ftth`, `elig_coax`, `elig_cu`, `elig_4gf`,
  `date`. Cas vérifié : 78158, 18 602 locaux, 18 275 éligibles fibre (98 %) au 30/06/2026.
- **Immeuble** : `https://data.arcep.fr/fixe/maconnexioninternet/base_imb/last/departement/base_imb_<dep>.csv.gz`
  (78 : 16 Mo) : un identifiant par immeuble avec adresse BAN (`addr_numero`, `addr_nom_voie`,
  `addr_code_insee`) ; l'éligibilité par immeuble est dans `eligibilite/last/` (même arborescence).
  3 148 immeubles pour 78158.
Écrire « fibre : éligible (ARCEP, 30/06/2026) » ou le taux communal si l'adresse n'est pas trouvée.

### Antennes relais — ANFR (testé le 19/11/2026)
Jeu `551d4ff3…`, ressource « Tables supports antennes émetteurs bandes <mois> » (zip 62 Mo, mensuel ;
prendre le plus récent). Dans le zip : `SUP_SUPPORT.txt` (`;`, latin-1, 199 000 lignes) : `SUP_ID`,
`NAT_ID` (nature : pylône, château d'eau, toit…), coordonnées en degrés-minutes-secondes
(`COR_NB_DG_LAT`, `COR_NB_MN_LAT`, `COR_NB_SC_LAT`, `COR_CD_NS_LAT`, idem LON), `SUP_NM_HAUT`
(hauteur en m), adresse, `COM_CD_INSEE`. `SUP_ANTENNE.txt` et `SUP_EMETTEUR.txt` donnent les
opérateurs et bandes. Procédure : filtrer `COM_CD_INSEE` = commune (et voisines), convertir en
décimal, calculer la distance au bien, lister ceux à moins de 300 m. Cas vérifié : 30 supports au
Chesnay-Rocquencourt (ex. château d'eau des Hubies 49,6 m ; Quartier Parly 2, 9 rue Potier, 29 m).
Arpent écrit la distance, la hauteur et la nature ; **aucun jugement sanitaire**.

### Propriétaires personnes morales — DGFiP (testé le 19/11/2026)
Fichiers officiels : `605d268f4661cf23272817c3` (zips par millésime, lourds, téléchargement parfois
coupé). Version unifiée par la communauté, plus pratique : `6900772ca5c4fa6c5687b3bd`,
`parcelles_personnes_morales_<année>.parquet` (2025 : 376 Mo, 21 M de lignes, lecture avec un
filtre `code_insee`, pyarrow suffit ; s'il manque : `pip install pyarrow`, à proposer à l'humain, pas
à exécuter sans accord). Colonnes : `code_insee`, `section`, `numero_parcelle`,
`prefixe`, `numero_siren`, `denomination`, `forme_juridique_abregee`, `code_droit_libelle`
(propriétaire, usufruitier…), `numero_voirie`, `nom_voie`, `contenance_parcelle_centiare`. Cas
vérifié : 972 parcelles de personnes morales à 78158 (commune 162, État 54, syndicat de copropriété
Chesnay-Trianon 47, SCI des Peupliers 39, bailleurs sociaux…). Une parcelle absente du fichier
appartient à une personne physique : **on s'arrête là** (règle 4). Dire le millésime (situation au
1er janvier).

### Bâti — API BDNB Open du CSTB (testée le 19/11/2026, sans compte ni clé)
Les exports complets font 37 à 48 Go : inutilisables. L'**API BDNB Open** suffit : niveau « ouvert,
pas de souscription », **10 000 appels par mois et par adresse IP, 120 par minute, 10 objets par
requête au maximum**. Base `https://api.bdnb.io/v1/bdnb`. Deux appels :
1. `GET /geocodage?q=<adresse>` → `features[0].properties.id` = clé d'interopérabilité BAN
   (ex. `78158_1110_00177` pour 177 rue de Versailles, Le Chesnay) et le score.
2. `GET /donnees/batiment_groupe_complet/adresse?cle_interop_adr=eq.<clé>&limit=5` → une liste de
   groupes de bâtiments, 152 champs chacun. Utiles : `annee_construction`, `mat_mur_txt`,
   `mat_toit_txt`, `hauteur_mean` (m) et `fiabilite_hauteur`, `nb_niveau`, `nb_log`,
   `usage_niveau_1_txt` (résidentiel / tertiaire), `s_geom_groupe` (emprise au sol, m²),
   `classe_bilan_dpe` et `nb_classe_bilan_dpe_a…g` (répartition des DPE du groupe),
   `l_denomination_proprietaire` (personnes morales seulement), `denomination_monument_historique`
   (monument à proximité). Même route par parcelle (`/parcelle`), par identifiant RNB (`/rnb`) ou par
   boîte englobante (`/bbox`). Métadonnées des champs : `GET /metadonnees`.
Cas vérifiés : hôpital, 177 rue de Versailles → emprise 23 777 m², hauteur 12 m, 3 niveaux, année
2008, propriétaire « Centre hospitalier de Versailles », monument proche « château (ancien) » ;
9 rue Potier (Parly 2) → 2 groupes, année et matériaux **non renseignés**, propriétaire commune pour
l'un, aucun pour l'autre. **Limites** : la couverture est inégale (beaucoup de `INDETERMINE` et de
`None` sur le résidentiel privé) ; les propriétaires personnes physiques n'y sont jamais (tant mieux,
règle 4) ; un champ vide s'écrit « non renseigné (BDNB) », pas zéro. Sans réponse, repli sur les DPE
ADEME (année et surface quand le DPE les porte).

## Territoire
| Donnée | Source | Accès |
|---|---|---|
| Revenus des ménages par commune | Revenus localisés sociaux et fiscaux (Insee) | `5b156279c751df40bb588de9` |
| Revenus à la maille fine (carreaux) | Données carroyées (Insee) | `5d8e16106f44410332a79994` |
| Gares de voyageurs (accessibilité ferroviaire) | Gares de voyageurs (SNCF) | `65d81858179dc96581d981db` |
| Gares d'Île-de-France | Liste des gares de voyageurs (Région IdF) | `5369991ba3a729239d20515e` |

À localiser au besoin : la base nationale des permis de construire (Sitadel) — seules des versions
régionales ont été trouvées au 17/11/2026.

## Sociétés (SCI, marchands, agences)
| Donnée | Source | Accès |
|---|---|---|
| Identité d'une société, dirigeants publiés, siège, date de création | API Recherche d'entreprises (DINUM) | `https://recherche-entreprises.api.gouv.fr` |
| Annonces légales : cessions, dissolutions, procédures collectives | API BODACC (DILA) | `https://bodacc-datadila.opendatasoft.com/api/explore/v2.0` |
| Répertoire Sirene | API Sirene (Insee, compte requis) | `https://api.insee.fr/api-sirene/3.11` |
| **Comptes annuels déposés, actes (statuts, PV), informations RNE** | **API RNE (INPI)**, compte gratuit requis | voir ci-dessous |

### Comptes annuels et actes — API RNE de l'INPI (testée le 18/11/2026)
C'est la source primaire : le dépôt légal lui-même. Elle ferme le principal manque de `/actif` et
de `/succession` (les comptes d'une société, les statuts d'une SCI). Elle demande un compte, que
chaque utilisateur ouvre pour lui ; **aucun identifiant n'est dans Arpent**.

**Ouvrir l'accès (trois minutes, accès immédiat le 18/11/2026)** : compte sur `data.inpi.fr`, puis
espace personnel → **« Mes accès API / SFTP »** → « Accès APIs RNE » → formulaire « Demande de
données RNE » (`https://data.inpi.fr/demande-de-donnees-rne`) : mode d'accès **API**, bases
**Informations des entreprises**, **Comptes annuels**, **Actes**, licence acceptée. Description du projet : usage, requêtes unitaires par SIREN, pas de téléchargement de
masse, aucun fichier sur des personnes physiques.

**Identifiants sur la machine de l'utilisateur**, jamais dans un fichier du projet : deux variables
d'environnement, `INPI_RNE_USER` (l'email du compte) et `INPI_RNE_PASSWORD`. Conseil : un mot de
passe propre à ce compte, pas un mot de passe réutilisé, car une variable d'environnement est
lisible par les programmes de la session. **Sans ces deux variables, Arpent ne tente rien** : il
écrit « comptes non consultés (pas d'accès INPI) » et demande les liasses à l'humain.

**Appels** (base `https://registre-national-entreprises.inpi.fr/api`) :
1. `POST /sso/login`, corps JSON `{"username": …, "password": …}` → `token` (valable pour la
   session ; le redemander en cas de 401). En-tête ensuite : `Authorization: Bearer <token>`.
2. `GET /companies/{siren}/attachments` → trois listes : `actes` (PDF : statuts, PV, liste des
   souscripteurs…), `bilans` (PDF des comptes), `bilansSaisis` (comptes en données). Chaque entrée :
   `id`, `dateCloture`, `dateDepot`, `typeBilan` (C complet, S simplifié, K consolidé),
   `confidentiality`. Une liste vide ou absente = **« aucun compte déposé à ce jour »** (cas vérifié
   sur une SARL créée en 2025) ; ce n'est pas une anomalie, c'est une information.
3. `GET /bilans-saisis/{id}` → `bilanSaisi.bilan.identite` (SIREN, clôture N et N−1, durée, code
   activité, devise, code confidentialité) et `bilanSaisi.bilan.detail.pages[].liasses[]`, chaque
   ligne = `code` de la liasse fiscale + colonnes `m1`…`m4`.
4. `GET /bilans/{id}/download` → le PDF des comptes, quand les données saisies manquent.

Les actes (`actes[].id`) sont très souvent des **scans** (statuts signés photographiés) : sans outil
de reconnaissance de texte, Arpent écrit « acte téléchargé, à relire à la main » et ne devine pas
son contenu (date de clôture, clauses d'agrément).

**Lire les liasses** : les codes sont ceux des formulaires Cerfa 2050 à 2053 (régime réel normal) ou
2033 (simplifié). Montants : chaînes de 15 caractères, en euros, sans décimale, signe « - » en tête
pour les négatifs (`000056232000000` = 56 232 000 000 €). Colonnes : page bilan actif, `m1` brut N,
`m2` amortissements, `m3` net N, `m4` net N−1 ; page passif, `m1` N, `m2` N−1 ; compte de résultat,
`m3` N, `m4` N−1 (`m1`/`m2` France/export sur les lignes de ventes). Codes utiles pour un bilan
d'acquisition (à confirmer sur la notice Cerfa de l'exercice, et citer le code utilisé) :
`FL` chiffre d'affaires net, `GG` résultat d'exploitation, `HN` résultat de l'exercice, `DL` total
des capitaux propres, `EC` total des dettes, `DU` emprunts auprès des établissements de crédit,
`DX` dettes fournisseurs, `DY` dettes fiscales et sociales, `CF` disponibilités, `BT` stock de
marchandises (net), `CO` total de l'actif. Un code absent de la liasse = « non renseigné », pas zéro.

**Limites** : comptes non confidentiels seulement (une petite société peut avoir opté pour la
confidentialité du compte de résultat : l'écrire) ; dépôts depuis 2017 ; quota 10 000 appels par
jour ; licence INPI : pas de rediffusion en masse, retirer tout document marqué `deleted: true`.
Dans l'app Claude sans outil shell, Arpent ne peut pas appeler cette API : il le dit et demande les
comptes à l'humain.

### Marques, brevets, dessins et modèles — API PI de l'INPI (testée le 18/11/2026)
Sert à une vérification précise dans `/actif` et `/succession` : **les marques, brevets ou modèles
exploités par la société sont-ils déposés à son nom ?** Cas vérifié le 18/11/2026 : SIREN
441 639 465 (Renault SA, holding) → 0 marque française ; SIREN 780 129 987 (Renault s.a.s.,
exploitation) → 1 216 marques. Acheter les parts de la mauvaise entité, c'est acheter sans la marque.

**Ouvrir l'accès** : même compte `data.inpi.fr`, « Mes accès API / SFTP » → « Accès APIs PI » →
formulaire : mode **API**, bases marques, brevets, dessins et modèles, licence. L'accès est accordé
tout de suite, **mais la passerelle PI est un autre système** : un email « Activation de votre
compte APIs diffusion PI » (expéditeur `nepasrepondre@inpi.fr`) arrive dans la minute, avec un lien
`api-gateway.inpi.fr/account/reset/finish?key=…`. La page se présente comme une réinitialisation de
mot de passe : c'est là qu'on le **définit**, le même que data.inpi.fr pour garder les deux variables
`INPI_RNE_USER` / `INPI_RNE_PASSWORD`. Tant que ce n'est pas fait, le login renvoie 401. Contact
INPI pour ces accès : licences@inpi.fr.

**Appels** (base `https://api-gateway.inpi.fr`), avec gestion de cookies :
1. `GET /services/uaa/api/authenticate` → répond 401, c'est normal : il pose le cookie `XSRF-TOKEN`.
2. `POST /auth/login`, corps `{"username", "password", "rememberMe": true}`, en-tête
   `X-XSRF-TOKEN` = valeur du cookie → 200 et cookies `access_token`, `refresh_token`.
3. Chaque appel suivant renvoie les cookies de session et un en-tête `X-XSRF-TOKEN` **relu dans le
   cookie à chaque appel** (il change à chaque réponse ; un jeton figé donne 403).
4. Recherche : `POST /services/apidiffusion/api/marques/search` (ou `brevets/search`,
   `modeles/search`), `Accept: application/json`, corps
   `{"collections":["FR"],"query":"[ApplicantIdentifier=<SIREN>]","fields":["ApplicationNumber","Mark","MarkCurrentStatusCode","DEPOSANT"],"size":20}`.
   Réponse : `metadata.count` (nombre total) et `results[].fields[]` (nom/valeur). Pour les brevets,
   le SIREN se cherche avec `DESI` (déposant) ou `TISI` (titulaire) ; pour les modèles,
   `ApplicantIdentifier`. Marques en vigueur seulement : ajouter `ET [ExpiryDate=AAAAMMJJ:99991231]`.
   Notice complète d'un titre : `GET /services/apidiffusion/api/marques/notice/FR<numéro>` (XML).

**Limites** : `ApplicantIdentifier` ne couvre que les titres **français** (collection FR) ; les
marques de l'UE et internationales se cherchent par nom (`DEPOSANT`), moins fiable. Seule la
recherche de marques par SIREN a été testée ; brevets et modèles suivent la même doc (v1.0 du
11/10/2021) mais n'ont pas été vérifiés : le dire si on s'en sert. Quotas non chiffrés par l'INPI.

**Alternatives privées** (Pappers, Infogreffe/DataInfogreffe, Societe.com) : mêmes données,
confort en plus, payantes au-delà d'un palier. Si un connecteur de ce type est chargé dans la
session, Arpent peut s'en servir et cite alors le revendeur comme source, avec la date.
