# Document de cadrage — Cas D : Galvaplus Industries (maintenance prédictive)

> **Livrable principal.** Lisible par le persona client (pas un dev). Renomme en
> `document_cadrage.md`. Les analyses (besoin, données, risques, KPI) se font
> **directement ici** : pas de fichiers séparés. Le schéma vit dans
> `schema_archi_cible.md`, tes notes dans `notes_entretien.md`.
> **3 pages est un plafond** : phrases courtes, tableaux, pas de remplissage.

## 1. Synthèse exécutive (5-6 lignes — rédigée EN DERNIER)

Galvaplus exploite quatre bains de galvanisation à chaud dont les arrêts non planifiés coûtent environ 30 000 € chacun. L'entreprise dispose déjà de deux ans d'historique de capteurs (température, pH, niveau) et d'un journal de maintenance recensant une cinquantaine de pannes. Le besoin réel n'est pas de disposer de nouveaux tableaux de bord mais d'anticiper les dérives annonciatrices de panne afin de permettre une intervention préventive. Une solution de maintenance prédictive basée sur l'analyse des séries temporelles est recommandée, avec maintien d'une validation humaine des décisions. La recommandation est de démarrer par un pilote sur un bain avant généralisation aux quatre bains. Les indicateurs clés retenus sont : détection d'au moins 70 % des pannes 48 heures avant leur survenue, réduction du nombre d'arrêts non planifiés et diminution des coûts associés.

> **Imprévu client (14h30) — ce que ça change** : aucune nouvelle contrainte n'a été communiquée durant l'entretien. Les sections données, risques, architecture et KPI restent cohérentes avec les éléments recueillis.

## 2. Besoin métier et contexte (1 paragraphe)

La demande exprimée par le client est : « On voudrait être prévenus 48 heures avant. » Le besoin réel est de réduire les pertes liées aux arrêts non planifiés des bains de galvanisation en exploitant les données historiques déjà disponibles afin de détecter suffisamment tôt les dérives annonciatrices de panne et permettre une intervention préventive. L'activité repose sur quatre bains de zinc fonctionnant en 3×8. L'entreprise dispose d'une supervision industrielle avec alarmes, mais celles-ci interviennent lorsque la situation est déjà critique. L'atelier est isolé d'Internet et le responsable production souhaite conserver une validation humaine des décisions.

## 3. Données — mini-cours `02`

| Donnée | Existante / à acquérir | Volume, qualité estimée | Personnelle ? |
|---|---|---|---|
| Température des bains | Existante | Historique 2 ans, mesure horaire, qualité apparente bonne | Non |
| pH du bain de préparation | Existante | Historique 2 ans, mesure horaire, qualité apparente bonne | Non |
| Niveau de zinc | Existante | Historique 2 ans, mesure horaire, qualité apparente bonne | Non |
| Journal de maintenance | Existante | ~50 pannes sur 2 ans, qualité moyenne des libellés | Oui (nom technicien) |
| Causes de panne normalisées | À acquérir | Incomplètes, saisie libre des techniciens | Non |
| Historique des interventions préventives | À confirmer | Non demandé explicitement | À confirmer |

Constats sur l'extrait transmis :

- Les données sont horodatées, structurées et sans valeurs manquantes visibles.
- Une dérive progressive du pH, de la température et du niveau est observable sur les 48 heures fournies, ce qui suggère la présence possible de signaux précurseurs.

## 4. Risques et conformité — mini-cours `04` et `07`

**Usage réel**

Le système sera utilisé par le responsable production et les équipes de quart pour recevoir une alerte de risque de panne. La décision d'arrêter ou non un bain reste humaine. L'alerte ne déclenche aucune action automatique dans le périmètre actuel.

**Qualification AI Act**

Le cas d'usage correspond à une aide à la décision pour la maintenance industrielle. Aucun traitement de texte ou système génératif n'est prévu. La qualification est considérée comme faible à ce stade. Une réévaluation sera nécessaire si l'entreprise souhaite automatiser l'arrêt des bains sans validation humaine.

**RGPD**

Les données de capteurs ne sont pas des données personnelles. Le journal de maintenance contient cependant le nom du technicien de quart. La base légale retenue serait l'intérêt légitime de l'entreprise pour la maintenance des équipements. Les noms des techniciens ne sont pas nécessaires au modèle et devront être exclus ou pseudonymisés. Il n'y a ni profilage des salariés, ni décision automatisée produisant des effets juridiques au sens de l'article 22.

| Risque (éthique, métier, conformité) | 🔴/🟠/🟡 | Obligation ou raison | Traitement dans l'archi |
|---|---|---|---|
| Panne non détectée | 🔴 | Impact financier élevé (30 k€) | Validation humaine + suivi des performances |
| Perte de vigilance des équipes | 🔴 | Risque explicitement signalé par le client | Maintien des contrôles humains |
| Qualité insuffisante du journal de maintenance | 🟠 | Labels imprécis | Validation et normalisation des causes |
| Utilisation des données nominatives | 🟠 | RGPD | Pseudonymisation ou suppression |
| Dépendance excessive au système | 🟡 | Risque d'usage | Communication claire sur le rôle d'assistance |

**Sécurité du modèle** — selon l'**exposition** de ton archi : 2 menaces
plausibles minimum, les autres écartées en 1 ligne. Mitiger ≠ supprimer.

| Menace | Plausibilité sur CE cas | Mitigation proposée | Risque résiduel |
|---|---|---|---|
| Altération des données de capteurs | Élevée | Contrôles d'intégrité, journalisation, séparation OT/IT | Faible à moyen |
| Accès non autorisé au système d'alerte | Élevée | Authentification, gestion des accès, journalisation | Moyen |
| Vol de modèle | Faible | Modèle déployé localement | Faible |
| Prompt injection | Non applicable | Aucun LLM utilisé | Négligeable |

## 5. Architecture cible et sobriété — mini-cours `05`

Voir `schema_archi_cible.md`.

La solution recommandée repose sur une approche de maintenance prédictive basée sur l'analyse de séries temporelles (machine learning classique ou détection d'anomalies). Les données disponibles sont numériques, structurées et historisées ; elles ne justifient pas l'utilisation d'un LLM. Un agent conversationnel ou un système génératif augmenterait les coûts, la complexité et les risques sans apporter de valeur métier démontrée. La solution devra fonctionner sans connexion Internet vers l'atelier et conserver une validation humaine des décisions.

## 6. Indicateurs, seuils, questions ouvertes — mini-cours `03`

| Indicateur | Cible | Seuil d'acceptabilité | Comment on le mesure |
|---|---|---|---|
| Pannes détectées 48 h avant | ≥ 70 % | ≥ 60 % | Comparaison avec le journal de maintenance |
| Horizon moyen d'anticipation | 48 h | ≥ 24 h | Différence entre alerte et panne |
| Réduction des arrêts non planifiés | Amélioration mesurable | ≥ 20 % | Comparaison avant/après pilote |
| Réduction des coûts d'arrêt | Amélioration mesurable | Tendance positive | Coût des arrêts évités |
| Disponibilité du système | ≥ 99 % | ≥ 95 % | Journal d'exploitation |

**Prochaines étapes**

1. Évaluer en détail la qualité du journal de maintenance et normaliser les causes de panne.
2. Réaliser un pilote sur un bain avant l'arrêt technique annuel.
3. Mesurer les KPI sur plusieurs semaines avant décision de généralisation.

**Questions ouvertes**

- Combien de fausses alertes par mois sont acceptables pour les équipes ?
- Quelles actions préventives sont réellement possibles dans les 48 heures précédant une panne ?
- Quel budget est disponible pour le projet ?
- Les quatre bains présentent-ils des comportements similaires ou nécessitent-ils un modèle spécifique ?
- Les causes de panne peuvent-elles être normalisées à partir des historiques existants ?