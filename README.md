# Arpent — l'immobilier français avec les données publiques

**Arpent** est un plug-in Claude pour les professionnels de l'immobilier en France : marchands de
biens, agents, intermédiaires en succession — et pour tout ce qu'un marchand de biens achète pour
revendre, immobilier ou non. Il branche Claude sur les données publiques de
**data.gouv.fr** (via le serveur MCP officiel `https://mcp.data.gouv.fr/mcp`, en lecture seule, sans
compte ni clé) et lui apprend à s'en servir avec la méthode du métier et les garde-fous du droit
français.

Construit avec Claude, par un marchand de biens qui voulait arrêter de chercher les bonnes données à
la main.

## Ce qu'il fait
| Commande | Usage |
|---|---|
| `/bilan` | Bilan d'opération de marchand de biens : méthode à rebours, TVA sur marge, verdict par rapport à une cible de 5 à 15 % de marge |
| `/actif` | Actif à revendre hors immobilier : parts de société, fonds de commerce, véhicule de collection, œuvre, bateau — même méthode à rebours, prix réalisés, frais et fiscalité de la classe (à valider), ce qui tue l'opération |
| `/estimer` | Estimation par comparables DVF (médiane, quartiles) et **dossier de prix juste** daté à archiver |
| `/fiche-bien` | Fiche d'un bien ou d'une parcelle : cadastre, urbanisme (PLU), risques (Géorisques), DPE, historique de prix |
| `/ville` | Attractivité d'une commune : revenus, accessibilité, dynamisme, marché, projets |
| `/marche` | Lecture du marché d'un territoire : acheteurs, équilibré ou vendeurs, tendance, sources datées, ce qui invaliderait la lecture — jamais de prévision chiffrée |
| `/succession` | Cadrage d'un dossier de succession avec biens ou parts de SCI : issues possibles, transparence |

Le skill couvre aussi la construction neuve « prête à finir » et un tableau des textes de référence
(loi Hoguet, lésion, TVA sur marge, décennale, passoires thermiques…).

## Règles qu'il applique
- Les chiffres viennent des données publiques, avec leur source et leur date — jamais de la mémoire.
- L'humain décide ; Arpent calcule, compare et alerte.
- Les points juridiques et fiscaux sont signalés avec leur texte et renvoyés au notaire, à l'avocat ou
  à l'expert-comptable. Arpent ne rédige aucun acte.
- Pas de fiches sur des particuliers : les données DVF ne servent jamais à identifier un vendeur ou
  un acheteur.

## Ce qu'il exécute et envoie
Arpent ne contient **aucun script ni hook**. Il déclare un seul connecteur : le serveur MCP public de
data.gouv.fr, qui reçoit les requêtes de recherche (noms de communes, mots-clés, identifiants de jeux
de données) et ne fait que de la lecture. Les API publiques citées dans le skill (cadastre, urbanisme,
Géorisques, BODACC, Recherche d'entreprises) sont interrogées seulement si l'outil web de Claude est
disponible.

## Installation
- **Application Claude / Cowork** : Plug-ins → Ajouter un marketplace → `Alexandre-LPZ/arpent` → installer Arpent (à confirmer sur votre version)
- **Claude Code** : `/plugin marketplace add Alexandre-LPZ/arpent` puis `/plugin install arpent@arpent`, puis `/reload-plugins` ; les commandes s'appellent `/arpent:ville`, `/arpent:marche`, etc.
- **Claude (chat, Cowork)** : depuis le répertoire des plug-ins une fois publié, ou en ajoutant le
  connecteur `https://mcp.data.gouv.fr/mcp` et le skill séparément.

Si vous avez déjà ajouté le connecteur data.gouv.fr à la main, vous pouvez le retirer après
l'installation d'Arpent, qui le fournit.

## Limites
- France uniquement (les données de data.gouv.fr). Monaco et l'étranger : sources locales.
- DVF : mise à jour semestrielle, Alsace-Moselle et Mayotte non couvertes.
- Les règles juridiques évoluent : chaque référence est à vérifier dans sa version en vigueur.

## Licence
MIT — voir `LICENSE`. Données : licences de leurs producteurs (Licence Ouverte pour la plupart).
