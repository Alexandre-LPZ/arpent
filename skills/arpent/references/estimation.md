# Estimation et dossier de prix juste

## Méthode par comparables (DVF)
1. Identifier la commune (code Insee) et, si possible, la section cadastrale du bien.
2. Extraire les ventes DVF du même **type** (maison / appartement / terrain), sur **24 mois** par
   défaut, dans la commune puis, si moins de 10 ventes, dans les communes voisines.
3. Calculer le **prix au m²** de chaque vente (valeur foncière / surface réelle bâtie ; terrain : au m²
   de terrain). Écarter les ventes aberrantes (lots multiples, dépendances seules, valeurs nulles).
   Règles de nettoyage, à appliquer telles quelles pour que deux calculs donnent le même chiffre :
   - grouper les lignes par `id_mutation` (une vente = plusieurs lignes : logement, cave, parking) ;
   - garder `nature_mutation = Vente` seulement (écarter VEFA, échange, adjudication, expropriation :
     les dire à part, la VEFA est un autre marché) ;
   - garder les ventes qui contiennent **exactement un** logement (Appartement ou Maison) ; les
     dépendances qui l'accompagnent restent incluses dans le prix (usage DVF courant, à dire) ;
   - écarter valeur nulle et surface bâtie < 9 m² ;
   - toujours afficher **combien de ventes ont été écartées et pourquoi**.
   Procédure d'extraction : `sources.md`, section « Extraire les ventes d'une commune ».
4. Donner **médiane, 1er et 3e quartile**, nombre de ventes — jamais une moyenne seule. Sous 30
   ventes, prévenir que la médiane bouge beaucoup d'un semestre à l'autre ; ne pas tirer de
   « tendance » d'une variation de médiane inférieure à l'écart interquartile.
5. Comparer, quand on la trouve, à une source d'un autre type (notaires, portails) en disant sa
   méthode : un **prix moyen** d'annonces ou d'estimations n'est pas une **médiane de ventes signées**.
   Les annonces ne sont jamais des comparables ; et une médiane DVF a plusieurs mois de retard
   (compromis → acte → publication). Voir `vendeur.md`.
6. Ajuster qualitativement (état, étage, DPE, extérieur, vue, nuisances) en le disant ; l'ajustement
   est une **opinion**, la médiane est un **fait**.

## Dossier de prix juste (à archiver dans le dossier de chaque achat)
Document daté, en Markdown, contenant :
- le bien (adresse, type, surface, parcelle) ;
- la liste des comparables DVF utilisés (date, type, surface, prix, prix au m²), sans aucune donnée
  sur les personnes ;
- la médiane et les quartiles ;
- le prix d'achat convenu et **l'écart en % à la médiane**.

But : prouver, si un vendeur ou un héritier conteste plus tard, que le prix était conforme au
marché du moment. Alerte automatique si le prix d'achat est sous **75 %** de la médiane : l'écart
doit alors être expliqué par écrit (travaux, occupation, servitude) — voir la lésion dans
`reglementation.md`.
