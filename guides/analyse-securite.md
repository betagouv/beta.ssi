# Intégration de la sécurité dans une démarche agile

## Pour qui et quels projets ?

- Les clients, les maîtrises d’ouvrage
- Les concepteurs / développeurs / exploitants de produits informatiques : matériels, logiciels, infrastructure
- Les producteurs de services publics et privés.
  - Les contraintes d’homologation spécifiques aux acteurs publics sont __soulignées__ ainsi tout au long de ce manuel
- Les projets développés selon la démarche agile
  - Développement itératif, incrémental et adaptatif ou le produit se construit dans le temps. La prise en compte de la sécurité se fait au fur et à mesure.
  - DevOps – regroupement du développement (Build) et de la mise en production (Run) dans la seule démarche Agile.
- Les projets développés selon tout autre démarche / méthode

## Pourquoi ?

- Pour obtenir le niveau de sécurité correspondant aux enjeux du produit
- Pour traiter les risques de manière (plus) exhaustive :
  - Les objectifs de sécurité sont réajustés en permanence tout au long du développement du produit ;
  - Le niveau de granularité étudié est celui des sprints ;
  - Les mesures de sécurité sont définies sur les composants déployés.
- Contractualiser l’intégration de la sécurité.
  - L’apparition de nouveaux risques peut être pris en compte sans renégociation contractuelle.
- Appliquer une méthode reconnue (EBIOS de l’ANSSI).
- Répondre à une contrainte règlementaire d’homologation.

## Quand ?

- A toutes les étapes du développement
- Sprint 0 : Définir les grands scénarios de risques et les principaux éléments de l’infrastructure de sécurité.
- En début de projet : homologation temporaire  (si nécessaire).
- Dans chaque sprint : analyser et traiter les risques de chaque user story.
- Lors d'un Sprint de sécurité, si nécessaire : traiter les risques communs et les interactions entre plusieurs itérations.
- Lors d'une Release: homologation ferme.

# Comment ?

- Planification de Sprint :
 - analyser les risques de chaque _user story_.
 - décrire les risques les plus critiques sous la forme d’_abuser stories_.
 - tracer les risques résiduels dans un outil collaboratif (Github, Trello, etc.)
- Développement :
 - traiter les risques et prévenir les régressions par des tests automatisés.
 - tracer les risques traités dans un outil collaboratif.
- Démo :
 - démontrer l’efficacité des mesures implémentées grâce aux tests.
- Mise en production:
 - obtenir (si cela est pertinent) une homologation temporaire

# Quoi ?

- L'étendue fonctionnelle du sprint ; en Sprint 0 (ou au démarrage), toute l'étendue fonctionnelle pressentie
- Les interactions des éléments périphériques avec le produit mais pas les éléments eux-mêmes :
  - donc si j’utilise une API : ma connexion à cette API, pas l’API elle-même
- Tous les éléments permettant la mise en production du produit :
 - Donc en DevOps : supervision, administration, suivi d’exploitation…

# Identification, traitement et évaluation des risques

## Quelles finalités ?

### Protéger la valeur métier...

Un *besoin de sécurité* est un niveau d'exigences opérationnelles relatives à un élément de *valeur métier* pour un critère de sécurité donné :
- Disponibilité : propriété d'accessibilité au moment voulu par les personnes autorisées
- Intégrité : propriété d'exactitude et de complétude
- Confidentialité : propriété de n'être accessible qu'aux personnes autorisées
- Preuve : élément pouvant être opposé en cas de problème

Exemple : L’application « Le TAXI », c’est la garantie d’un chauffeur professionnel (intégrité) et d’applications agréées respectueuses de la vie privée (confidentialité).

### Par l'identification de risques...

L’identification des mesures de sécurité à appliquer résulte d’un processus d’identification et d’évaluation des *risques*.

Exemple : En tant qu’attaquant, je divulgue des données personnelles que j’ai récupérées en compromettant la base de données de l’application utilisateurs.

### Et la mise en place de mesures...

La mise en place de *mesures de sécurité* lors du développement du produit va permettre  de répondre à ces besoins de sécurité.

Exemple : L’utilisation de HTTPS entre l’application mobile du client et le serveur central garantit l’authentification et la confidentialité de l’échange sur Internet.

### Reconnues par l'homologation

L’*homologation de sécurité* est l’engagement par lequel une autorité atteste que le produit a bien été protégé des risques identifiés pendant son développement, à l'exception des risques résiduels documentés.

## Qu'est-ce qu'un risque ?

### Définition

Un risque est un scénario combinant un *événement redouté* sur une *valeur métier* et un ou plusieurs *scénarios de menaces* visant des *composants du SI* présentant des *vulnérabilités*. On lui associe une criticité qui correspond à l'estimation de sa gravité et de sa vraisemblance.

### Représentation

Dans une démarche Agile, un risque est représenté par une « Abuser Story » décrivant
- la réalisation d’un scénario de menaces
  - provoquant un évènement redouté
    - sur une valeur métier ayant
      - des besoins sécurité et
      - des impacts engendrés en cas de non respect de ces besoins,
  - en exploitant une vulnérabilité d’un composant du produit.

Exemple : En tant qu’attaquant, j’empêche les clients de demander un taxi en inondant le serveur applicatif par un attaque DOS.

### Actions associées

Un risque peut être traité (mise en place de mesures de sécurité), transféré (assurance, produit complémentaire) ou accepté (résiduel). En dernier recours, un risque peut également être évité (refus ou suspension d’une évolution).

## Identification et évaluation d'un risque

La méthode EBIOS (ANSSI) formalise un processus d’identification et d’évaluation des risques.

# Les outils

## Organisation

Comme dans toutes les démarches projets, les développeurs sont formés à la sécurité et éventuellement épaulés par un expert sécurité.

## Outils

Le choix des outils utilisés est libre mais conforme aux exigences de sécurité du product backlog. Par exemple :
- Réunions sous forme d’ateliers où l’usage de post-its est courant,
- Utilisation d’outils collaboratifs pour tracer les évènements.

Le traitement de la sécurité se fait à l’aide de ces outils tant qu’ils garantissent qu’*il n’y aura pas de concession sur le niveau de sécurité*.

## Atelier d'analyse des risques

L'atelier se déroule dans les conditions usuelles pour des équipes agiles:
- le format est présentiel
- toute l'équipe est présente, et seulement l'équipe (éventuellement renforcée d'un animateur ou expert sécurité)
- la durée est limitée, quitte à programmer plusieurs ateliers ; une durée d'une heure environ est appropriée

Le support consiste en une feuille au format paperboard ou Post-It géant, structurée en "canevas", avec les rubriques suivantes:
- Valeurs métier et besoins en sécurité
- Sources de menaces
- Evenements redoutés
- Composants SI et leurs vulnérabilités
- Mesures de sécurité existantes
- Scénarios de menace

Chaque participant proposer sur un Post-It un item destiné à l'une de ces rubriques. Les Post-It sont ajoutés au canevas au fur et à mesure.

#### Valeurs métier

Pour cette rubrique, recenser les principaux processus, fonctions et données sensibles du produit et à identifier et estimer leurs besoins de sécurité (DICP).

#### Sources de menaces

Réfléchir aux origines des risques : qui ou quoi pourrait porter atteinte aux besoins de sécurité exprimés (sources humaines, environnementales, internes, externes, …)

#### Evénements redoutés

A partir des besoins de sécurité exprimés sur les valeurs métiers, estimer les impacts (sur les missions, sur la sécurité des personnes, financiers, juridiques, sur l'image, sur l'environnement, sur les tiers et autres…) en cas de non-respect de ces besoins. Ces impacts associés aux sources de menaces susceptibles d'en être à l'origine permettent de formuler les événements redoutés.

#### Composants SI et leurs vulnérabilités

Prendre connaissance des composants du système d'information, qu'il s'agisse de biens techniques ou non techniques, supports aux valeurs métiers précédemment identifiées. On note que ces composants SI possèdent des vulnérabilités que des sources de menaces pourront exploiter, portant ainsi atteinte aux valeurs métier.

#### Mesures de sécurité existantes

Pour chaque composant SI identifié, il convient de s'interroger sur l'existence de mesures de sécurité déjà existantes ou d'ores et déjà prévues. Ces mesures peuvent être techniques ou non techniques (produit de sécurité logique ou physique, configuration particulière, mesures organisationnelles ou humaines, règles, procédures…).

#### Scénarios de menace

Identifier et estimer les scénarios qui peuvent engendrer les événements redoutés, et ainsi composer des risques. Pour ce faire, sont étudiées les menaces que les sources de menaces peuvent générer et les vulnérabilités exploitables.

### Exploitation

A l'issue de l'atelier, mettre en évidence les risques qui pèsent sur le produit en confrontant les événements redoutés aux scénarios de menaces. Estimer et évaluer également ces risques et identifier les mesures de sécurité qu'il faudra implémenter pour les traiter. Traiter les risques en spécifiant les mesures de sécurité à mettre en œuvre et en planifiant la mise en œuvre de ces mesures.

Cette étape se traduit par la rédaction et la planification des *Abuser Stories*. Leur implémentation, mise en évidence par des tests automatisés, est priorisée par le Product Owner de l'équipe Agile comme le sont les autres User Stories.

## Travail collaboratif sur les risques

Un outil de travail collaboratif (ex : wiki, redmine, github) pour garder « juste ce qu’il faut » comme traces des traitements des risques :
- Accessible suivant le contexte (privé/public) par tous les développeurs du produit et/ou les internautes. Dans tous les cas, les besoins de filtrage des données sur la sécurité seront vérifiés (ex : risques résiduels)
- Déjà utilisé pour conserver la mémoire des évènements, la description du produit et les codes sources, son utilisation est étendue à la sécurité.
- De même que des rubriques sont déjà définies pour l’implémentation, les sources, les bugs, etc., une rubrique « sécurité » est créée.
- L’outil collaboratif est renseigné à partir des post-its (couper/coller) quand il apparait que leur contenu n’évolue plus et qu’il semble nécessaire d’en garder une trace (ex : scénario de risque identifié et mesures de sécurité retenues et implémentées pour le traiter).
- L’outil collaboratif est renseigné au fil de l’eau, quand des issues (évènements, observations, problèmes potentiels) de sécurité surgissent.
- Les mesures de sécurité sont exprimées sous la forme de tâches ou backlog item.
- Aucune contrainte de forme n’est imposée pour renseigner l’outil collaboratif (texte, tableau, schéma, etc.).
- Il doit être possible d’extraire l’ensemble des points relatifs à la sécurité grâce à la balise « sécurité » afin de créer un document qui sera présenté pour une homologation de sécurité.

Exemple: https://github.com/openmaraude/le.taxi/wiki/Anayse-des-risques

## Bases de connaissances

Des bases de connaissances sont mises à disposition en annexe de ce document pour faciliter les démarches d’analyses des risques :
- Types de composants du système d’information (biens supports)
- Types d’impacts
- Types de sources de menaces
- Menaces et vulnérabilités génériques
- Mesures de sécurité applicables

## Glossaire

- *Abuser story* : Brève description d’un scénario de risque qui sera utilisé pour déterminer les mesures de sécurité à implémenter et réaliser les tests de couverture du risque.
- *Analyse des risques* : Sous-processus de la gestion des risques visant à identifier, analyser et à évaluer les risques.
- *Besoin de sécurité* : Définition précise et non ambiguë du niveau d'exigences opérationnelles relatives à une valeur métier pour un critère de sécurité donné (disponibilité, confidentialité, intégrité…).
- *Valeur métier (Bien essentiel)* :  Information ou processus jugé comme important pour l'organisme. On appréciera ses besoins de sécurité mais pas ses vulnérabilités.
- *Composant du SI (Bien support)* : Bien sur lequel reposent des valeurs métiers. On distingue notamment les systèmes informatiques, les organisations et les locaux. On appréciera ses vulnérabilités mais pas ses besoins de sécurité. La notion de composant SI peut être aussi abordée en début de projet sous la forme de grosse briques fonctionnelles : réseau LAN bureautique, réseau WAN de transit, réseau d'administration AD, applicatifs métiers éventuellement en mode saas, bases de données localisées ou distantes voire en Cloud.
- *Événement redouté* : Situation crainte par l'organisme. Il s'exprime par la combinaison des sources de menaces susceptibles d'en être à l'origine, d'une valeur métier, du besoin de sécurité concerné et des impacts potentiels.
- *Homologation de sécurité* :  Validation par une autorité dite d’homologation, que le niveau de sécurité est conforme aux attentes.
- *Impact* :  Conséquence directe ou indirecte de l'insatisfaction des besoins de sécurité sur l'organisme et/ou sur son environnement.
- *Mesure de sécurité* :  Moyen de traiter un risque de sécurité de l'information.
- *Risque résiduel* : Risque subsistant après le traitement du risque.
- *Scénario de menace* : Scénario décrivant des modes opératoires. Il combine les sources de menaces susceptibles d'en être à l'origine, un composant du SI, un besoin de sécurité, des menaces et les vulnérabilités exploitables pour qu'elles se réalisent.
- *Source de menace* :  Chose ou personne à l'origine de menaces.
- *Vulnérabilité* : Caractéristique d'un composant du SI qui peut constituer une faiblesse ou une faille au regard de la sécurité des systèmes d'information.
