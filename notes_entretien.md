# Notes d'entretien — Cas D : Galvaplus Industries (maintenance prédictive)

> Mini-cours `01`. Ce fichier sert d'abord à **toi** ; il est aussi lu pour
> évaluer ta préparation. Renomme en `notes_entretien.md`.

## 1. Avant le rendez-vous — 12 questions + 3 de réserve

> Le client accorde **12 réponses**. **Une question à la fois**. Classe par
> priorité : si tu n'en poses que 8, ce doivent être les 8 plus utiles.
> Catégories à couvrir : besoin · processus actuel · données (existence, volume,
> qualité, **extrait**) · données personnelles / confidentialité · critère de
> succès chiffré · coût d'une erreur · utilisateurs · SI / hébergement · budget / délai.

| # | Priorité (1-3) | Catégorie | Question |
|---|---|---|---|
| 1 | 1 | Besoin | Quand vous dites qu'un bain « tombe en panne », quel événement concret se produit ? |
| 2 | 1 | Processus actuel | Comment détectez-vous aujourd'hui qu'un bain commence à dériver ? |
| 3 | 1 | Besoin réel | Qu'est-ce qui vous fait perdre le plus de temps ou d'argent aujourd'hui avec ces bains ? |
| 4 | 1 | Succès | Qu'est-ce qui vous ferait dire que ce projet est une réussite dans un an ? |
| 5 | 1 | Coût d'une erreur | Quelle erreur serait la plus pénalisante : manquer une panne ou générer une fausse alerte ? |
| 6 | 1 | Données | Depuis quand les mesures de température, pH et niveau sont-elles enregistrées ? |
| 7 | 1 | Données | Combien de pannes sont enregistrées dans votre historique et comment sont-elles identifiées aujourd'hui ? |
| 8 | 1 | Données | Pouvez-vous nous transmettre un extrait représentatif des données et incidents ? |
| 9 | 2 | Utilisateurs | Qui utilise aujourd'hui les informations de supervision et qui décide d'arrêter un bain ? |
| 10 | 2 | Données personnelles | Les données utilisées sont-elles associées à des opérateurs ou techniciens identifiables ? |
| 11 | 2 | SI / hébergement | Quelles contraintes d'hébergement ou de cybersécurité devons-nous respecter ? |
| 12 | 3 | Déploiement | Préféreriez-vous commencer par un pilote sur un bain ou viser directement les quatre bains ? |
| R1 | réserve | Processus métier | Lorsqu'une dérive est détectée suffisamment tôt, quelles actions pouvez-vous mettre en œuvre pour éviter l'arrêt ? |
| R2 | réserve | Périmètre | Combien de bains sont concernés au total ? |
| R3 | réserve | Budget / délai | Quel budget et quelle échéance avez-vous en tête pour ce projet ? |

## 2. Pendant le rendez-vous — dit / interprété

| Question posée (telle quelle) | Ce que le client a **dit** (citation) | Ce que j'en **interprète** |
|---|---|---|
| Quand vous dites qu'un bain « tombe en panne », quel événement concret se produit ? | « Nos bains tombent en panne deux à trois fois par mois : résistance qui lâche, dérive de température, problème de niveau. Chaque arrêt non prévu nous coûte environ 30 000 euros. » | Trois familles de défaillance sont identifiées. Le coût métier est élevé. L'objectif est de réduire les arrêts non planifiés. |
| Qui utilise aujourd'hui les informations de supervision et qui décide d'arrêter un bain ? | « Le chef d'équipe de quart et moi. C'est moi qui décide d'arrêter ou pas. » | La décision est aujourd'hui entièrement humaine. |
| Relance : pourquoi évoquer l'automatisation ? | « La direction m'a demandé : si l'outil est fiable, est-ce qu'il ne pourrait pas couper le bain tout seul la nuit ? » | Une automatisation future est envisagée mais ne fait pas partie du fonctionnement actuel. C'est un point de vigilance AI Act et sécurité industrielle. |
| Quelle erreur serait la plus pénalisante ? | « Une panne ratée, c'est ce qu'on vit aujourd'hui. Mais si on dit aux gars que l'outil surveille, ils vont arrêter de surveiller eux-mêmes. » | Le principal risque métier est la surconfiance dans l'outil et la perte de vigilance humaine. |
| Depuis quand les mesures sont-elles enregistrées ? | « Chaque bain a des capteurs : température, pH et niveau. Ils remontent dans notre supervision toutes les heures. On garde tout depuis deux ans. » | Les données existent, sont historisées et potentiellement exploitables pour une étude prédictive. |
| Combien de pannes sont enregistrées dans votre historique et comment sont-elles identifiées ? | « La maintenance tient un journal : date, heure, bain concerné, cause supposée. Sur deux ans, ça fait une cinquantaine de pannes. » | Existence d'une cible exploitable. Les labels sont présents mais leur qualité doit être vérifiée. |
| Pouvez-vous transmettre un extrait des données ? | « Je vous envoie 48 heures de relevés d'un bain exportés de la supervision. » | Un extrait réel a été obtenu pour évaluer la qualité des données. |
| Qu'est-ce qui vous ferait dire que le projet est une réussite dans un an ? | « Si on détecte au moins 70 % des pannes 48 heures avant, c'est déjà énorme. Aujourd'hui, on en détecte zéro. » | KPI métier explicite et mesurable. |
| Les données sont-elles associées à des techniciens identifiables ? | « Les températures et niveaux non. Le journal de maintenance contient le nom du technicien de quart. » | Présence limitée de données personnelles. Une minimisation ou pseudonymisation sera nécessaire. |
| Quelles contraintes d'hébergement ou de cybersécurité devons-nous respecter ? | « L'atelier n'est pas connecté à internet, et l'automaticien ne veut pas qu'il le soit. Les bureaux, oui. » | Forte séparation OT/IT. Une architecture locale ou hybride sera privilégiée. |
| Existe-t-il déjà des seuils ou règles d'alarme ? | « Si la température passe 470, ça sonne. Mais quand ça sonne, c'est déjà trop tard. » | Les alarmes existent déjà. Le besoin est l'anticipation, pas la supervision ou la visualisation. |
| Préféreriez-vous commencer par un pilote ou un déploiement global ? | « On a un arrêt technique annuel en février. Si on peut tester quelque chose avant, sur un bain, ce serait bien. » | Le client est favorable à une expérimentation sur un bain avant généralisation. |
| Relance complémentaire | « Un stagiaire a fait des graphiques Excel une fois, c'était joli mais ça n'a servi à rien. » | Le client ne cherche pas un tableau de bord mais une aide décisionnelle opérationnelle. |
| Relance complémentaire | « Quatre bains, qui tournent en 3×8. » | Le périmètre du projet couvre quatre équipements critiques exploités en continu. |

_Relance non prévue ? Note-la aussi, avec la raison (« réponse surprenante sur… »)._

### Boussole — ce que j'ai déjà obtenu

> Mets-la à jour **après chaque réponse**. Elle suit des **informations**, pas
> tes questions : une réponse peut en remplir plusieurs, une autre aucune.
> Quand il te reste 3-4 questions, regarde les 🔴 : lequel manquera le plus à
> ton cadrage ? C'est à toi de formuler la question.
>
> 🟢 obtenu · 🟠 partiel / à vérifier · 🔴 à obtenir · ⬜ pas demandé (→ §3)

| Information | Statut | Réponse n° |
|---|---|---|
| Besoin réel (≠ demande exprimée) | 🟢 | 1, 11 |
| Processus actuel | 🟢 | 2 |
| Données : existence | 🟢 | 5 |
| Données : volume | 🟢 | 5, 6 |
| Données : qualité | 🟠 | 6, 7 |
| Données : extrait obtenu | 🟢 | 7 |
| Données personnelles / confidentialité | 🟢 | 9 |
| Critère de succès chiffré | 🟢 | 8 |
| Coût d'une erreur | 🟢 | 1, 4 |
| Erreurs tolérées (chiffre : fausses alertes, mauvais routage…) | 🔴 | |
| Utilisateurs | 🟢 | 2 |
| Validation humaine / qui décide | 🟢 | 2 |
| SI / hébergement | 🟢 | 10 |
| Budget | ⬜ | |
| Délai | 🟠 | 12 |
| Ce qui a déjà été essayé | 🟢 | 11, relance |

## 3. Après — ce que je n'ai pas pu demander → questions ouvertes

| Je n'ai pas pu demander / pas eu de réponse claire | Pourquoi c'est important | → §6 du cadrage |
|---|---|---|
| Nombre de fausses alertes acceptable par mois | Permet de définir les seuils métier et l'équilibre précision/rappel | KPI et risques |
| Actions préventives réalisables dans les 48 h | Vérifier que la détection génère réellement une valeur métier | Architecture et processus cible |
| Budget disponible pour le projet | Conditionne le périmètre et la trajectoire de déploiement | Questions ouvertes |
| Niveau de qualité réel du journal de maintenance | Peut limiter l'apprentissage supervisé | Données à qualifier |
| Similarité des comportements entre les 4 bains | Influence la généralisation du pilote | Architecture et feuille de route |