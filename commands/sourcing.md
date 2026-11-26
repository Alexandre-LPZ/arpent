---
description: Radar hebdomadaire des biens qui vont probablement se vendre avant l'annonce, dans une zone donnée, à partir de signaux publics (procédures collectives, successions vacantes, adjudications, permis dormants, copropriétés fragiles, annonces qui durent, vacance). Fiches A/B/C, action proposée, enchaînement vers /fiche-bien, /contrepartie, /bilan. Part du bien ou de la société, jamais d'une personne.
---
Avec le skill `arpent`, lis `references/sourcing.md`, `references/sources.md` et
`references/terrain-regles.md`, puis établis le radar pour : $ARGUMENTS

Argument attendu : une zone (départements ou communes) et, si l'utilisateur le précise, un type de
bien et une période. Sans zone, utiliser celle du CLAUDE.md du projet ; sans rien, demander la zone
et s'arrêter. Hors de la zone, ne rien chercher et le dire.

Ordre de travail : BODACC sur la zone (procédures collectives, dissolutions, radiations de sociétés
dont l'activité ou le nom désigne de l'immobilier), cessions immobilières de l'État (successions
vacantes), annonces d'adjudication, puis les signaux lents (permis dormants, registre des
copropriétés, LOVAC par commune). Pour chaque bien repéré, vérifier au cadastre que la société
détient bien le bien avant de l'écrire. Les annonces qui durent se relèvent à la main, jamais par
extraction automatique.

Jamais : partir d'un nom de personne physique, chercher un décès ou une situation familiale, croiser
avec les réseaux sociaux ou les avis d'obsèques, utiliser des données réservées aux collectivités,
conserver ou publier le radar au-delà du dossier. Chaque signal avec sa source, sa date et son
étiquette ; sans pièce publiée, jamais A.

Sortie : la liste des fiches radar au format de `sourcing.md`, triée A puis B puis C, avec pour
chacune l'action proposée et ce qui manque pour confirmer ; en tête, la zone, la date du radar et
les sources effectivement consultées (et celles qui n'ont pas répondu). Rappeler que le seuil de
marge (5 % net avant IS minimum, 20 % visés) se vérifie avec `/bilan`, jamais à ce stade.
