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
| 3 | 1 | Risques métier | Qu'est-ce qui vous ferait considérer l'outil comme suffisamment fiable pour envisager une coupure automatique ? |
| 4 | 1 | Données | Depuis quand enregistrez-vous les mesures de température, de pH et de niveau ? |
| 5 | 1 | Données | Combien de pannes sont enregistrées dans votre historique et comment sont-elles identifiées aujourd'hui ? |
| 6 | 1 | Données | Pouvez-vous nous transmettre un extrait représentatif des mesures capteurs et du journal de maintenance associé à quelques pannes ? |
| 7 | 1 | Succès | Qu'est-ce qui vous ferait dire que le projet est réussi dans un an ? |
| 8 | 2 | Données personnelles | Les données sont-elles associées à des opérateurs ou à des techniciens identifiables ? |
| 9 | 2 | SI / hébergement | Quelles contraintes d'hébergement, d'accès au réseau industriel ou de cybersécurité devons-nous impérativement respecter ? |
| 10 | 2 | Existant | Quelle action réalisez-vous concrètement lorsqu'une dérive est détectée ?? |
| 11 | 3 | Processus métier | Lorsqu'une dérive est détectée suffisamment tôt, quelles actions pouvez-vous mettre en œuvre pour éviter l'arrêt du bain ?? |
| 12 | 3 | Déploiement | Préféreriez-vous commencer par un pilote sur un seul bain ou déployer directement la solution sur les quatre bains ? |
| R1 | réserve | Budget | Quel budget avez-vous prévu pour ce projet ? |
| R2 | réserve | Délai | Quelle échéance souhaitez-vous pour une première mise en production ? |

## 2. Pendant le rendez-vous — dit / interprété

| Question posée (telle quelle) | Ce que le client a **dit** (citation) | Ce que j'en **interprète** |
|---|---|---|
| Quand vous dites qu'un bain « tombe en panne », quel événement concret se produit ? | « Nos bains tombent en panne deux à trois fois par mois : résistance qui lâche, dérive de température, problème de niveau. Chaque arrêt non prévu nous coûte environ 30 000 euros : production perdue, zinc à refondre, clients livrés en retard. On voudrait être prévenus 48 heures avant. » | Trois types de défaillances sont identifiés. Chaque arrêt a un impact financier important. Le besoin exprimé est d'obtenir une anticipation de 48 h. |
| Comment détectez-vous aujourd'hui qu'un bain commence à dériver ? | « Le chef d'équipe de quart et moi. C'est moi qui décide d'arrêter ou pas, après avoir regardé. Mais la direction m'a demandé : si l'outil est fiable, est-ce qu'il ne pourrait pas couper le bain tout seul la nuit ? » | La détection actuelle est humaine. La décision d'arrêt est réalisée par le responsable production. Une automatisation future est envisagée mais soulève des questions de confiance et de responsabilité. |
| Qu'est-ce qui vous ferait considérer l'outil comme suffisamment fiable pour envisager une coupure automatique ? | « Une panne ratée, c'est ce qu'on vit aujourd'hui : 30 000 euros et une équipe en pompier. Donc ce n'est pas pire qu'avant. Mais si on dit aux gars “l'outil surveille” et qu'il rate la panne, ils vont arrêter de surveiller eux-mêmes, et ça, ça m'inquiète. » | Le principal risque perçu est la perte de vigilance humaine. Le client souhaite conserver une supervision humaine même en présence d'un système prédictif. |
| Depuis quand enregistrez-vous les mesures de température, de pH et de niveau ? | « Chaque bain a des capteurs : température, pH du bain de préparation et niveau de zinc. Ils remontent dans notre supervision toutes les heures. On garde tout depuis deux ans, mais personne ne regarde vraiment, sauf quand il y a une alarme. » | Les données existent, sont historisées sur deux ans et collectées toutes les heures. Le fonctionnement actuel est réactif et non prédictif. |
| Combien de pannes sont enregistrées dans votre historique et comment sont-elles identifiées aujourd'hui ? | « Oui, la maintenance tient un journal : date et heure de l'arrêt, bain concerné, cause supposée. Sur deux ans, ça fait une cinquantaine de pannes. Les causes, c'est ce que le technicien a écrit, pas toujours très précis. » | Un historique exploitable existe (~50 pannes). La qualité des causes renseignées devra être vérifiée et probablement normalisée. |
| Pouvez-vous nous transmettre un extrait représentatif des mesures capteurs et du journal de maintenance associé à quelques pannes ? | « Je vous envoie 48 heures de relevés d'un bain, exportées de la supervision. Vous me direz si vous y voyez quelque chose. » | Un extrait réel a été fourni. Il permettra d'évaluer la structure et la qualité des données disponibles. |
| Qu'est-ce qui vous ferait dire que le projet est réussi dans un an ? | « Si on détecte au moins 70 % des pannes 48 heures avant, c'est déjà énorme. Aujourd'hui, on en détecte zéro. » | KPI métier clairement défini : détecter au moins 70 % des pannes avec un préavis de 48 h. |
| Les données sont-elles associées à des opérateurs ou à des techniciens identifiables ? | « Des données personnelles ? Non, ce sont des températures et des niveaux. Enfin… le journal de maintenance a le nom du technicien de quart. » | Les mesures industrielles ne sont pas des données personnelles mais le journal de maintenance contient des informations nominatives. |
| Quelles contraintes d'hébergement, d'accès au réseau industriel ou de cybersécurité devons-nous impérativement respecter ? | L'atelier n'est pas connecté à internet, et l'automaticien ne veut pas qu'il le soit. Les bureaux, oui.| | Quelles contraintes d'hébergement, d'accès au réseau industriel ou de cybersécurité devons-nous impérativement respecter ? | L'atelier n'est pas connecté à internet, et l'automaticien ne veut pas qu'il le soit. Les bureaux, oui.|
| Lorsqu'une dérive est détectée suffisamment tôt, quelles actions pouvez-vous mettre en œuvre pour éviter l'arrêt du bain ? | Il y a des seuils d'alarme dans la supervision : si la température passe 470, ça sonne. Mais quand ça sonne, c'est déjà trop tard. Un stagiaire a fait des graphiques Excel une fois, c'était joli mais ça n'a servi à rien. | Le site dispose déjà d'alarmes et de visualisations. Le besoin réel n'est pas un nouveau tableau de bord mais une capacité d'anticipation.  |
| Préféreriez-vous commencer par un pilote sur un seul bain ou déployer directement la solution sur les quatre bains ? | « On a un arrêt technique annuel en février. Si on peut tester quelque chose avant, sur un bain, ce serait bien. » | Le client privilégie une expérimentation progressive sur un bain avant généralisation aux quatre bains. |

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
| Besoin réel (≠ demande exprimée) | 🟢 | 1, 10 |
| Processus actuel | 🟢 | 2 |
| Données : existence | 🟢 | 4 |
| Données : volume | 🟢 | 4, 5 |
| Données : qualité | 🟠 | 5, 6 |
| Données : extrait obtenu | 🟢 | 6 |
| Données personnelles / confidentialité | 🟢 | 8 |
| Critère de succès chiffré | 🟢 | 7 |
| Coût d'une erreur | 🟢 | 1, 3 |
| Erreurs tolérées (chiffre : fausses alertes, mauvais routage…) | 🔴 | |
| Utilisateurs | 🟢 | 2 |
| Validation humaine / qui décide | 🟢 | 2 |
| SI / hébergement | 🟢 | 9 |
| Budget | ⬜ | |
| Délai | 🟠 | 12 |
| Ce qui a déjà été essayé | 🟢 | 10 |

## 3. Après — ce que je n'ai pas pu demander → questions ouvertes

| Je n'ai pas pu demander / pas eu de réponse claire | Pourquoi c'est important | → §6 du cadrage |
|---|---|---|
| Nombre maximum de fausses alertes acceptable par mois | Permet de définir les seuils métier d'acceptabilité | KPI et risques |
| Actions de maintenance réellement réalisables dans les 48 h | Permet de vérifier que la détection apporte une valeur opérationnelle | Architecture et processus cible |
| Budget prévu pour le projet | Influence le périmètre et la trajectoire de mise en œuvre | Questions ouvertes |
| Qualité réelle du journal de maintenance | Conditionne la faisabilité d'un apprentissage supervisé | Données à qualifier |
| Similarité des comportements entre les 4 bains | Influence la généralisation du pilote aux autres équipements | Architecture et feuille de route |