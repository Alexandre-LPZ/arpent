# Attractivité d'une commune — grille applicable à toute la France

Le terrain de jeu est **toute la France** (et, hors connecteur, l'Europe). Une commune mérite une
opération quand les gens qui ont les moyens d'acheter du beau ont des raisons d'y vivre. Grille :

| Critère | Ce qu'on mesure | Source |
|---|---|---|
| Revenus | Revenu médian, part des hauts revenus | Insee — revenus localisés |
| Accessibilité | Gare TGV ou grande ligne à moins de 30 min ; aéroport à moins d'1 h ; axes routiers | SNCF — gares ; carte |
| Dynamisme économique | **Emplois au lieu de travail** (pas les actifs résidents), indice de concentration de l'emploi, grands employeurs | Insee RP via `sources.md` (jeux vérifiés), API Recherche d'entreprises |
| Grands équipements | Centre commercial régional, hôpital, campus, siège, base militaire : ce qui fait venir des gens et des emplois chaque jour | Sirene (établissements de la commune, tranche d'effectifs), presse spécialisée (CNCC, LSA) |
| Attractivité touristique | Fréquentation, hébergement, notoriété | Insee, offices de tourisme |
| Marché | Volume de ventes DVF sur 12 mois et tendance du prix médian | DVF |
| Projets | Nouvelles gares, lignes, zones d'activité, grands équipements | Collectivités, maîtres d'ouvrage |
| Risques | Exposition de la commune (inondation, argiles…) | Géorisques |

Verdict en trois niveaux : **cible** / **à creuser** / **hors cible**, toujours justifié critère par
critère. Une ville sans dynamisme économique reste hors cible, même pas chère.

Deux pièges constatés au premier test (Le Chesnay-Rocquencourt, 17/11/2026) :
- **Actifs résidents ≠ emplois.** Le recensement donne les deux. Une commune dont les actifs
  résidents baissent peut gagner des emplois. Le bon chiffre est l'emploi **au lieu de travail** et
  l'**indice de concentration** (emplois pour 100 actifs résidents ; > 100 = pôle d'emploi).
- **Un grand équipement ne se voit pas dans les statistiques résidentielles.** Un centre commercial
  régional, un hôpital ou un campus apporte des emplois et des flux sans changer les revenus des
  habitants. Toujours demander à l'humain « qu'est-ce qui fait venir du monde ici ? » et chercher
  l'équipement dans Sirene (établissements de la commune par effectif). Les chiffres de
  fréquentation viennent de l'exploitant ou de la presse spécialisée : les citer avec leur
  source, et écrire « non vérifié » quand on n'en a que le récit.

## Effet d'une infrastructure de transport
Pour une gare ou une ligne nouvelle : comparer le prix médian DVF dans un rayon autour de la station,
avant l'annonce, après l'annonce et après la mise en service, au prix de la commune entière. Écart
qui s'ouvre = effet anticipé déjà dans les prix ; pas d'écart = potentiel restant ou effet absent.
Toujours le présenter comme une **mesure**, pas une prévision.

## Zone de confort du marchand (préférence, pas limite)
Sud-ouest parisien, là où il vit et connaît le terrain : axe Versailles–Rambouillet (N10, N12),
plateau de Saclay, Vélizy, Saint-Cloud, Vallée de Chevreuse, Grand Paris 78. Y appliquer la même
grille, en ajoutant la connaissance de terrain de l'humain.

Ailleurs, les villes recherchées (exemples cités : Biarritz, Bordeaux, Cannes, Deauville) passent la
grille comme les autres. **Monaco n'est ni en France ni dans l'Union européenne** : aucune donnée
data.gouv, droit et fiscalité propres — un partenaire local s'impose.
