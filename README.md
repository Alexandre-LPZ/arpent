# Arpent — l'immobilier français avec les données publiques

*Français ci-dessous · [English version](#arpent--french-real-estate-and-resale-assets-with-open-public-data)*

**Arpent** est un plug-in Claude pour les marchands de biens, et pour tous ceux qui cherchent,
achètent et revendent avec la même méthode : investisseurs, agents immobiliers, apporteurs
d'affaires, intermédiaires en succession, ceux qui travaillent avec un marchand de biens — pour tout
ce qui s'achète pour être revendu, immobilier ou non. Il branche Claude sur les données publiques de
**data.gouv.fr** (via le serveur MCP officiel `https://mcp.data.gouv.fr/mcp`, en lecture seule, sans
compte ni clé) et lui apprend à s'en servir avec la méthode du métier et les garde-fous du droit
français.

Construit avec Claude, par un marchand de biens qui voulait arrêter de chercher les bonnes données à
la main.

## Ce qu'il fait
| Commande | Usage |
|---|---|
| `/bilan` | Bilan d'opération de marchand de biens : méthode à rebours, TVA sur marge, **six fiches de terrain** dictées par un marchand de biens (habitation, commerces/bureaux, parts/fonds, véhicules, œuvres, bateaux ; règles communes et quatre verdicts dans `terrain-regles.md`) (8 questions du professionnel, réponses A–D, effets chiffrés), étiquettes pièce vérifiée / déclaré / hypothèse / manquant, verdict GO / À SÉCURISER / NO GO |
| `/actif` | Actif à revendre hors immobilier : parts de société, fonds de commerce, véhicule de collection, œuvre, bateau — même méthode à rebours, prix réalisés, frais et fiscalité de la classe (à valider), ce qui tue l'opération |
| `/estimer` | Estimation par comparables DVF (médiane, quartiles) et **dossier de prix juste** daté à archiver |
| `/fiche-bien` | Fiche d'un bien ou d'une parcelle en six thèmes : parcelle et propriétaire (personne morale), bâti, contraintes (PLU, abords ABF, risques, carrières), environnement (fibre, antennes), projets, prix — et où chercher ce que le public ne donne pas |
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

**Comptes annuels et actes déposés (API RNE de l'INPI)** : source optionnelle. Chaque utilisateur
ouvre son propre accès gratuit sur data.inpi.fr (trois minutes, procédure dans
`skills/arpent/references/sources.md`) et garde ses identifiants dans deux variables d'environnement
sur sa machine. Arpent ne contient aucun identifiant et n'appelle cette API que si ces variables
existent ; sinon il demande les comptes à l'humain. Le même compte, avec un accès « APIs PI »
activé à part, permet de vérifier que les marques, brevets et modèles d'une société sont bien
déposés à son nom.

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

## Sources et référencement
Arpent est référencé comme **réutilisation sur data.gouv.fr**, rattaché aux jeux de données DVF,
BODACC, Sirene, cadastre, DPE, comptes INPI et Fonciris :
https://www.data.gouv.fr/reuses/arpent-limmobilier-et-les-actifs-a-revendre-avec-les-donnees-publiques-plugin-claude
Le détail de chaque source, ses limites et les procédures testées sont dans
`skills/arpent/references/sources.md`.

## Licence
MIT — voir `LICENSE`. Données : licences de leurs producteurs (Licence Ouverte pour la plupart).

---

# Arpent — French real estate and resale assets with open public data

**Arpent** is a Claude plugin for French property dealers (*marchands de biens*), and for everyone
who hunts, buys and resells with the same method: investors, real-estate agents, deal finders, estate
intermediaries, anyone working alongside a dealer — for anything bought in order to resell, property
or not. It connects Claude to the French open-data portal **data.gouv.fr** (through
the official MCP server `https://mcp.data.gouv.fr/mcp`, read-only, no account or key) and teaches it
the trade's method and the guardrails of French law.

Built with Claude, by a property dealer who wanted to stop hunting for the right data by hand.
French is the working language of the plugin (the data, the law and the trade are French); this
section explains what it does for readers who don't read French.

## What it does
| Command | Use |
|---|---|
| `/bilan` | Dealer's deal appraisal: backward method from resale price, VAT on margin, **six field sheets** dictated by a property dealer (housing, shops/offices, company shares/goodwill, vehicles, artworks, boats; common rules and four verdicts in `terrain-regles.md`) (8 questions answered by the professional, A–D, with quantified effects), every line tagged verified document / declared / assumption / missing, verdict GO / SECURE-RENEGOTIATE / NO GO |
| `/actif` | Resale asset outside real estate: company shares, business goodwill (*fonds de commerce*), collector car, artwork, boat — same backward method, realised prices only, class-specific costs and taxes (flagged "to be validated"), deal-killers |
| `/estimer` | Valuation by DVF comparables (median, quartiles) and a dated **fair-price file** to archive |
| `/fiche-bien` | Property or parcel sheet in six themes: parcel and owner (legal entities only), building, constraints (PLU, heritage-protection perimeters, hazards, quarries), surroundings (fibre, cell towers), projects, prices — and where to look for what open data does not give |
| `/ville` | Attractiveness of a municipality: income, accessibility, jobs, market, projects |
| `/marche` | Reading of a territory's market: buyers', balanced or sellers' market, trend, dated sources, what would invalidate the reading — never a numeric forecast |
| `/succession` | Framing of an estate file with property or SCI shares: possible outcomes, transparency |

The skill also covers "ready-to-finish" new builds and a table of reference texts (Hoguet law,
lesion, VAT on margin, ten-year builder's liability, energy-sieve rules…).

## Rules it enforces
- Figures come from public data, with source and date — never from memory. Missing data is written
  "not found", never estimated in disguise.
- The human decides; Arpent computes, compares and alerts.
- Legal and tax points are flagged with their reference text and sent to the notary, lawyer or
  accountant. Arpent drafts no deed.
- No files on private individuals: DVF data is never used to identify a buyer or seller.

## What it runs and sends
Arpent contains **no script and no hook**. It declares one connector, the public data.gouv.fr MCP
server, which receives search queries (municipality names, keywords, dataset ids) and only reads.
The public APIs cited in the skill (cadastre, planning, Géorisques, BODACC, company search) are called
only when Claude's web tool is available.

**Filed annual accounts and deeds (INPI's RNE API)**: optional source. Each user opens their own free
access on data.inpi.fr (three minutes, procedure in `skills/arpent/references/sources.md`) and keeps
their credentials in two environment variables on their machine. Arpent ships no credentials and
calls this API only when those variables exist; otherwise it asks the human for the accounts. The
same account, with a separately activated "PI APIs" access, lets Arpent check that a company's
trademarks, patents and designs are registered in its own name (tested case: holding Renault SA,
0 trademarks; operating company Renault SAS, 1,216).

## Install
- **Claude app / Cowork**: Plug-ins → Add a marketplace → `Alexandre-LPZ/arpent` → install Arpent
  (to be confirmed on your version)
- **Claude Code**: `/plugin marketplace add Alexandre-LPZ/arpent`, then `/plugin install arpent@arpent`,
  then `/reload-plugins`; commands are `/arpent:ville`, `/arpent:marche`, etc.
- Already installed: `/plugin marketplace update arpent`, then `/reload-plugins`.

## Limits
- France only (data.gouv.fr data). Monaco and abroad: local sources.
- DVF: updated twice a year; Alsace-Moselle and Mayotte not covered.
- Legal rules change: every reference is to be checked in its current version.

## Sources and listing
Arpent is listed as a **reuse on data.gouv.fr**, attached to the DVF, BODACC, Sirene, cadastre, DPE,
INPI accounts and Fonciris datasets:
https://www.data.gouv.fr/reuses/arpent-limmobilier-et-les-actifs-a-revendre-avec-les-donnees-publiques-plugin-claude

## License
MIT — see `LICENSE`. Data: the producers' licences (mostly the French *Licence Ouverte*).
