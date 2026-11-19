# Fiche de terrain — classe 1 : habitation (maison ou appartement à rénover et revendre)

Dictée par le marchand de biens le 19/11/2026. Ce que les données publiques ne voient pas, c'est
le professionnel qui le dit : état, configuration, occupation, défauts, calendrier. Arpent prend ses
réponses, les étiquette, et les fait entrer dans le calcul. Il ne note pas, il ne moyenne pas : une
seule réponse éliminatoire suffit à bloquer, quelle que soit la qualité du reste.

## Comment la fiche se remplit
- **Avant** : le professionnel colle ses huit réponses (lettre + un mot) dans le premier message.
  Ex. « Q1 B, Q2 C (toiture + électricité, devis 180 k€), Q3 A, Q4 B (copro, ravalement voté 12 k€),
  Q5 A, Q6 C (rez-de-chaussée sur rue), Q7 B, visite du 15/11 ».
- **Après** : si la fiche manque, Arpent fait le bilan avec les données publiques et le termine par
  les questions **sans réponse**, chacune avec ce qu'une réponse défavorable change (« si Q2 = C :
  −150 à −250 k€ sur le prix maximal et +6 mois »). Il ne remplit jamais une réponse à la place du
  professionnel.

## Les quatre étiquettes (obligatoires sur chaque ligne du bilan)
| Étiquette | Sens | Exemple |
|---|---|---|
| **pièce vérifiée** | un document lu : acte, PV d'AG, devis signé, certificat d'urbanisme, diagnostic | « ravalement voté, PV d'AG du 12/03/2026 » |
| **déclaré** | ce que le professionnel dit avoir vu ou su, daté | « rénovation lourde, visite du 15/11/2026 » |
| **hypothèse** | un montant ou un délai posé pour calculer, à remplacer | « frais de revente 6 %, hypothèse » |
| **manquant** | ni pièce, ni déclaration, ni hypothèse acceptable : le calcul s'arrête là | « solde de l'emprunt du vendeur : manquant » |
Une date de visite ne transforme pas une déclaration en pièce vérifiée. Les chiffres publics (DVF,
cadastre, GPU) gardent leur étiquette habituelle : source et date.

## Les huit questions

### Q1. À combien puis-je réellement revendre ce bien, une fois terminé ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | prix confirmé par plusieurs ventes comparables récentes, secteur et prestations équivalents | **base de calcul** : médiane des comparables DVF |
| B | prix plausible, comparables imparfaits | **scénario prudent** : premier quartile des comparables, ou médiane − 5 % |
| C | prix fondé surtout sur les annonces ou l'estimation du vendeur | **vérification obligatoire avant offre** : Arpent refait les comparables (`estimation.md`) ; tant que ce n'est pas fait, pas de prix maximal, seulement une fourchette |
| D | produit difficile à comparer, marché étroit, faible demande | **forte décote** (prix prudent − 10 à 15 %) **ou NO GO** si la sortie reste incertaine |
Règle : prix affichés ≠ prix signés (`vendeur.md`). Le prix de revente du calcul est **HT**, selon le
régime fiscal réel de l'opération ; il ne se déduit pas mécaniquement d'un prix TTC affiché.

### Q2. Quel est l'état réel du bien, et quelle enveloppe de travaux ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | coup de frais : peintures, sols, embellissement | travaux **par devis** ; imprévus 5 % ; délai court |
| B | rénovation classique : cuisine, salles d'eau, électricité, plomberie, menuiseries | devis ; imprévus 10 % ; délai moyen |
| C | rénovation lourde : redistribution, réseaux complets, isolation, toiture | devis détaillés ; imprévus 15 à 20 % ; délai long ; autorisations probables (Q3, Q4) |
| D | risque structurel : fondations, fissures évolutives, planchers, humidité profonde, désordres non maîtrisés | **expertise technique et chiffrage avant tout engagement** ; **NO GO si le risque ne peut pas être borné** |
Règle : les travaux se chiffrent avec des entreprises, pas seulement au m². Un ratio au m² n'est
qu'une **hypothèse** en attendant le devis, et il est écrit comme tel.

### Q3. Puis-je revendre dans la configuration actuelle, ou dois-je transformer ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | configuration conservée | rien |
| B | redistribution intérieure sans structure | travaux Q2 ; en copropriété, vérifier que les parties touchées sont privatives |
| C | agrandissement, surélévation, aménagement de surfaces existantes (combles, sous-sol) | **étude d'urbanisme préalable** (PLU : emprise, hauteur, reculs ; ABF : `fiche-bien.md`), autorisation, délai, coût ; la surface créée n'entre dans le prix de revente **que si l'autorisation est acquise** |
| D | division en plusieurs logements ou lots | idem, plus : règles de division du PLU, servitude de mixité sociale, copropriété à créer, diagnostics par lot ; **le lot hypothétique ne se valorise pas** tant qu'il n'existe pas |
Règle : on ne valorise jamais une surface ou un lot comme si sa création était acquise.

### Q4. Existe-t-il un obstacle juridique, urbanistique ou de copropriété ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | situation régulière, propriété et consistance vérifiées | rien |
| B | contraintes connues, financièrement maîtrisables | **ajustement du prix** du montant connu (ex. travaux votés) |
| C | autorisation, régularisation ou accord nécessaire | **condition préalable** dans la promesse, coût et délai en plus (Q7) |
| D | blocage juridique ou administratif, droit de propriété mal sécurisé | **NO GO tant que le blocage n'est pas levé** |
Appartement : règlement de copropriété, PV des trois dernières AG, travaux votés, charges,
procédures. Maison : servitudes, accès, limites (bornage), règles d'urbanisme. Les documents lus
sont des **pièces vérifiées** ; ce que le vendeur en dit reste **déclaré**.

### Q5. Quelle est la situation d'occupation, et quand puis-je disposer du bien ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | libre à l'acte | calendrier standard |
| B | occupé, libération contractualisée et sécurisée | **marge de sécurité** sur le délai (Q7) |
| C | loué : bail et droits du locataire à analyser | **recalcul du scénario de sortie** (vente occupée = décote, ou attente de la fin du bail = portage) |
| D | occupation litigieuse ou libération incertaine | **NO GO** pour une opération qui exige un bien libre, sauf résolution juridiquement sécurisée |
Règle : le délai de libération conditionne le financement, les travaux et la commercialisation.

### Q6. Quels défauts pénalisent la revente, même après rénovation ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | aucun défaut rédhibitoire | rien |
| B | corrigeables : décoration, distribution, luminosité améliorable | **budget correctif** (dans Q2) |
| C | permanents : nuisances, vis-à-vis, étage défavorable, pas d'extérieur ou de stationnement selon le marché | **décote sur le prix de sortie** de **5 à 10 %** (hypothèse, afficher les deux bornes) et délai de commercialisation allongé (Q7) |
| D | majeurs : accès problématique, environnement dégradé, exposition forte à un risque, produit difficilement commercialisable | **forte décote ou NO GO** |
Règle : un bien magnifiquement rénové reste un bien mal situé si l'emplacement est mauvais. Les
données publiques aident ici (`fiche-bien.md` : antennes, bruit, risques, usage passé du site) ; le
reste est déclaré après visite.

### Q7. Quel est mon calendrier réel, de l'acquisition à l'encaissement de la revente ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | travaux simples, autorisations acquises ou inutiles, commercialisation prévisible | portage court |
| B | travaux classiques, plusieurs entreprises à coordonner | portage moyen |
| C | travaux lourds ou autorisations nécessaires | portage long : intérêts, assurances, charges, fiscalité récurrente, trésorerie |
| D | délais dépendant d'événements incertains ou de tiers | **NO GO si le délai ne peut pas être raisonnablement encadré** |
Règle : on compte **jusqu'à l'encaissement chez le notaire**, pas jusqu'à la fin du chantier
(`vendeur.md` : compromis → acte, 1 à 4 mois).

### Q8. Après tous les coûts, quelle marge reste-t-il, et quel capital dois-je immobiliser ?
| | Réponse | Ce que ça change |
|---|---|---|
| A | marge et trésorerie conformes à mes critères, **même en scénario prudent** | **GO** sous réserve des vérifications |
| B | marge acceptable seulement dans le scénario central | **renégociation ou sécurisation** complémentaire |
| C | marge insuffisante au prix demandé, négociation possible | **offre plafonnée au prix d'achat maximal** calculé |
| D | marge négative, risque disproportionné, financement non sécurisé | **NO GO** |
Règle : la marge est définie **en euros**, avec sa base de calcul et son niveau (avant ou après impôt
sur les bénéfices) ; **Q8 se donne donc en euros, et la lettre se déduit du calcul** : Arpent ne la
choisit pas à la place du professionnel, il dit « le calcul tombe en C / en D ». Pas de pourcentage universel sans connaître le risque et la durée ; la cible
maison de `marchand.md` (5 à 15 %) sert de **contrôle**, pas de règle.

## Le calcul à rebours, rendu opérationnel
Prix d'achat maximal = prix de revente prudent HT − frais d'acquisition − travaux et imprévus HT −
portage et commercialisation − fiscalité non récupérable ou applicable − marge cible.

Les flux TTC, la TVA immobilière applicable (sur marge ou sur le prix total), sa récupération
éventuelle, les coûts financiers et le besoin de trésorerie sont traités **séparément** et montrés.

| Ligne | Montant | Étiquette | Origine (formule, pièce, date) | Question |
|---|---|---|---|---|
| Prix de revente prudent HT | | pièce / hypothèse | comparables DVF (médiane ou Q1 selon Q1), régime de TVA | Q1, Q6 |
| − Frais d'acquisition | | hypothèse / pièce | droits + notaire + intermédiaire, formule écrite | Q4 |
| − Travaux HT | | pièce (devis) / déclaré / hypothèse | devis signés ; sinon ratio **étiqueté hypothèse** | Q2, Q3 |
| − Imprévus | | hypothèse | 5 / 10 / 15–20 % selon Q2 | Q2 |
| − Autorisations, études, régularisations | | pièce / hypothèse | architecte, géomètre, CU, diagnostics | Q3, Q4 |
| − Portage | | hypothèse | intérêts × durée Q7, assurances, charges, taxe foncière | Q5, Q7 |
| − Commercialisation | | hypothèse | % du prix de revente, formule écrite | Q1 |
| − Fiscalité applicable | | hypothèse, « à valider » | TVA sur marge ou totale, IS, formule écrite | — |
| − Marge cible | | **déclaré** | montant en €, base et niveau précisés par le marchand | Q8 |
| **= Prix d'achat maximal** | | | | |
| Écart avec le prix demandé | | | | Q8 |
| Capital immobilisé (pointe de trésorerie) | | hypothèse | achat + travaux − financement, mois par mois | Q7, Q8 |
Deux colonnes de scénario quand Q1 = B ou Q8 = B : **central** et **prudent**. Le verdict se lit sur
le prudent.

## Grille de décision finale
Pas de moyenne. On lit les réponses dans l'ordre et on s'arrête à la première qui bloque. Règles
communes et quatre verdicts (dont **NO GO en l'état**, réexaminable après pièce, expertise ou
régularisation, distinct du **NO GO définitif**) : `terrain-regles.md`.

| Si… | Verdict |
|---|---|
| Q2 = D (risque structurel non borné), Q4 = D (blocage juridique), Q5 = D (occupation litigieuse, bien libre requis), Q7 = D (délai non encadrable), Q8 = D (marge négative ou financement non sécurisé), ou Q1 = D / Q6 = D avec sortie incertaine | **NO GO** |
| Au moins un C (Q1, Q3, Q4, Q5, Q7, Q8) ou un B sur Q8, sans aucun D bloquant | **À SÉCURISER / RENÉGOCIER** : lister les conditions (vérification des comparables, autorisation, devis, libération, financement) et le prix maximal qui les rend acceptables |
| Que des A et B, et Q8 = A | **GO**, sous réserve des pièces à vérifier listées |
| Une question sans réponse | pas de verdict sur cette question : « **manquant** », avec ce qu'une réponse défavorable changerait |

Le verdict s'écrit en une ligne, en tête du bilan, suivi de la question qui l'a décidé. Une baisse
de prix consentie par le vendeur ne rend pas une opération bonne : elle le devient quand prix
d'achat, risque et délai sont cohérents avec une sortie réaliste.
