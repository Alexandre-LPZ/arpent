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
