# Sourcing — le radar des biens qui vont se vendre

Doctrine de la maison (règle du 26/11/2026). La marge d'un marchand se fait à l'achat, et les
meilleurs achats ne sont pas en annonce. Le radar repère, à partir de **signaux publics**, les biens
dont la vente devient probable avant qu'ils arrivent sur le marché. Il ne dit jamais « achète » :
il dit « va voir », avec le signal, sa source et sa date. C'est l'humain qui va voir.

Le radar part toujours du **bien** ou de la **société** qui le détient. Jamais d'une personne.
C'est la même règle que `contrepartie.md` : la contrepartie, oui ; la vie privée, jamais.

## Le périmètre
- **Zone par défaut** (à adapter à l'utilisateur dans son CLAUDE.md ou en argument) : Yvelines
  (78), Hauts-de-Seine (92), Essonne (91), nord de l'Eure-et-Loir (28 : Maintenon, Épernon,
  autour de Rambouillet). Hors zone, le radar le dit et s'arrête.
- **Types** : résidentiel (maison, appartement, immeuble), professionnel (local d'activité, bureaux,
  commerce), terrain. Le radar note le type ; le bilan viendra après.
- **Seuil d'intérêt** : une opération n'est retenue qu'à **5 % de marge nette avant IS minimum**,
  **20 % visés**. Le radar ne calcule pas la marge (c'est `/bilan`) ; il écarte d'emblée ce qui ne
  peut pas l'atteindre (prix affiché au prix du marché, bien sans décote possible).

## Les signaux — d'où ils viennent, ce qu'ils disent
Chaque signal s'écrit avec sa source et sa date. Un signal n'est pas une preuve : c'est une raison
d'aller voir. Deux signaux concordants sur le même bien valent plus qu'un.

| Signal | Source publique | Ce qu'il révèle | Étiquette |
|---|---|---|---|
| Société propriétaire en procédure collective, dissolution, liquidation amiable ou radiation | BODACC (annonces A et B), Recherche d'entreprises, `sources.md` | une SCI ou une société d'exploitation qui va devoir vendre ses murs | pièce établie |
| Bien issu d'une succession vacante mis en vente par le curateur | `cessions.immobilier-etat.gouv.fr` (site des cessions immobilières de l'État), notaires et agences mandatés | bien sans héritier connu, vendu par appel d'offres, enchères ou gré à gré, ouvert à tous ; droit de préemption de la commune possible | pièce établie |
| Vente judiciaire ou adjudication annoncée | annonces légales, affichage au tribunal judiciaire, sites des ventes aux enchères immobilières des avocats | décote et délai courts, cahier des conditions de vente à lire avant tout | pièce établie |
| Permis de construire ou d'aménager accordé et non commencé depuis plus de deux ans | Sitadel (bases régionales sur data.gouv.fr, `sources.md`), affichage en mairie | un propriétaire qui a renoncé ; terrain ou bâti à reprendre, parfois avec le permis encore valable | indice |
| Copropriété fragile ou sous procédure (administrateur provisoire, plan de sauvegarde, impayés) | Registre national d'immatriculation des copropriétés (ANAH, données ouvertes), arrêtés de péril et d'insalubrité publiés par les mairies | lots à prix décoté, plusieurs vendeurs, travaux votés ou à voter | indice |
| Annonce qui dure (plus de six mois) ou qui disparaît sans vente DVF | relevé **manuel** hebdomadaire des portails, puis DVF six à douze mois après | vendeur fatigué, mandat qui arrive à échéance, prix mal placé | indice |
| Vacance longue de logements ou de locaux dans une commune | LOVAC (données par commune, data.gouv.fr), observation de terrain (volets clos, boîtes aux lettres, enseignes vides) | un stock de biens dont les propriétaires ne font rien ; la donnée publique s'arrête à la commune, le terrain fait le reste | indice |
| Bien détenu par une personne morale, visible au cadastre | Fiche-bien (`/fiche-bien`), propriétaires personnes morales du cadastre | permet d'enchaîner sur les signaux « société » ci-dessus | contexte |

Ce que le radar **ne fait jamais** :
- partir d'un nom de personne physique, chercher un décès, un divorce, une mutation, un âge ;
- croiser avec les réseaux sociaux, les annuaires, les avis d'obsèques ;
- extraire automatiquement les portails d'annonces (leurs conditions d'utilisation l'interdisent) :
  le relevé est manuel, une liste courte tenue à la main ;
- utiliser les données des logements vacants à l'adresse (réservées aux collectivités par la loi) ;
- conserver une fiche au-delà du dossier, ni publier le radar.

## La fiche radar — format de sortie
Une fiche par bien, courte, datée. Le radar hebdomadaire est la liste de ces fiches, triée par
priorité.

```
RADAR · [commune] · [adresse ou parcelle] · [type]
Signal(s) : [signal — source — date — étiquette]
Priorité : A / B / C
  A = vente contrainte probable sous six mois (procédure, succession vacante, adjudication)
  B = signal sérieux mais sans échéance (permis dormant, copropriété fragile, annonce qui dure)
  C = à surveiller (vacance, détention par personne morale sans autre signal)
Action proposée : [visite extérieure / courrier au gérant de la société / appel du notaire ou du
  curateur / lecture du cahier des conditions de vente / passage sur place]
Ce qui manque pour confirmer : [pièce, personne à joindre, donnée à vérifier]
Suite Arpent : /fiche-bien → /contrepartie (si une acquisition se dessine) → /bilan
```

Règles de la fiche :
- une seule ligne par signal, avec sa source et sa date ; rien d'inventé pour « remplir » ;
- sans pièce, jamais A : un A repose sur une publication (BODACC, cession de l'État, annonce
  d'adjudication) ;
- une fiche sans action proposée n'est pas une fiche ;
- l'ordre des suites ne change pas : d'abord le bien, puis la contrepartie si une acquisition se
  dessine, puis le bilan. Le prix maximal du bilan ne se règle jamais sur l'enthousiasme du radar.

## Le rythme
- **Hebdomadaire** : BODACC sur la zone (procédures, dissolutions, radiations), cessions de l'État,
  annonces d'adjudication, relevé manuel des annonces qui durent.
- **Mensuel** : permis dormants, registre des copropriétés, LOVAC (données annuelles, à relire
  quand elles sortent).
- Chaque radar remplace le précédent ; les fiches closes (bien vendu, signal éteint, hors seuil)
  sortent de la liste avec un mot de raison.

## Ce qui tue un signal
- Le bien est déjà en annonce au prix du marché : pas de décote, pas d'opération.
- La société en procédure ne détient pas le bien (vérifier au cadastre : propriétaire personne
  morale, et à défaut l'état hypothécaire chez le notaire).
- La commune a un droit de préemption qu'elle exerce souvent sur ce type de bien.
- Le signal a plus d'un an sans suite : il s'éteint, sauf nouveau fait.

## Ce que le radar ne remplace pas
Le réseau. Les notaires, les syndics, les artisans, les voisins, les bénévoles d'un quartier savent
avant les registres. Le radar sert à arriver avec une raison de frapper à la porte, pas à remplacer
la porte.
