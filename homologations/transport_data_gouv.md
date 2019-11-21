# Dossier d’homologation transport.data.gouv.fr

Le point d’accès national aux données transport permet d’accéder aux données _ouvertes_ destinées à l’information voyageur.

Il n’a pas vocation à héberger des données à caractère privé (données nominatives, ou données à accès restreint).


## Démarche

La démarche retenue est une démarche autonome _a minima_, conforme également au Guide d'Analyse des Risques et au Guide d'Homologation visant les équipes dites « Agiles » (ouvrage réalisé par l’ANSSI conjointement avec la DINSIC et disponible à l’adresse suivante : [https://www.ssi.gouv.fr/uploads/2018/11/guide-securite-numerique-agile-anssi-pa-v1.pdf](https://www.ssi.gouv.fr/uploads/2018/11/guide-securite-numerique-agile-anssi-pa-v1.pdf) ).


## Analyse des risques



*   Modifier les données temps réel
    *   diffusion du mauvais quai de départ générant un mouvement de foule
    *   diffusion de message d’incitation à la haine sur les panneaux d’information
*   Modifier les données théoriques
    *   Introduire un virus dans l’archive zip des horaires
    *   Modifier des horaires sournoisement pour ne plus afficher une partie de l’offre (concurrence, dénigrement en vue d’une campagne électorale…)
*   Faire tomber la plateforme
    *   plus d’information temps réel (vélo libre service, prochains passages…)
    *   impossibilité de télécharger les horaires théorique
*   Intrusion du serveur pour récupérer des identifiants
    *   Faire tomber le serveur de nos partenaires (fournisseurs de données temps réel)
    *   Être un marche-pied pour s’introduire dans les serveur des partenaires (en particulier en ayant un accès en écriture avec des interfaces telles que SOAP pour le temps-réel au format SIRI)
*   Réussir à impersonnifier (en récupérant les accès OAuth de [data.gouv.fr](http://data.gouv.fr))
    *   Publier un jeu de données à la place de quelqu’un d’autre
    *   Utiliser le module de discussion sous le nom de quelqu’un d’autre
*   Modifier le résultat des validation des jeux de données
    *   Discréditer les producteurs de données, partenaires techniques


## Parcours utilisateur

La question que l’on s’est posée ici est de savoir, pour chaque parcours utilisateur l’importance des 4 critères suivants :



*   [D] Disponibilité : la fonctionnalité peut être utilisée au moment voulu ;
*   [I] Intégrité : les données sont exactes et complètes ;
*   [C] Confidentialité : les informations ne sont divulguées qu’aux personnes autorisées ;
*   [P] Preuve : les traces de l’activité du système sont opposables en cas de contestation

<table>
  <tr>
   <td>
<strong>Parcours utilisateur</strong>
   </td>
   <td><strong>[D]</strong>
   </td>
   <td><strong>[I]</strong>
   </td>
   <td><strong>[C]</strong>
   </td>
   <td><strong>[P]</strong>
   </td>
  </tr>
  <tr>
   <td>Une autorité organisatrice publie un jeu de données
   </td>
   <td>●●
   </td>
   <td>●●●
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Un ré-utilisateur télécharge des fichiers statiques d’un producteur tiers
   </td>
   <td>●
   </td>
   <td>●●
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Un ré-utilisateur télécharge un fichier produit par l’équipe
   </td>
   <td>●
   </td>
   <td>●●●
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Utilisation des données temps réel pour une application d’information
   </td>
   <td>●●
   </td>
   <td>●●
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
</table>



        ● Faible	●● Modéré 	●●● Important


## Sources de risques



*   Concurrents des réutilisateurs potentiels : fausses informations pour décrédibiliser
*   Vandales ciblés : modifier les données pour diffuser un virus dans un fichier, diffuser des messages de haine
*   Vandales s’attaquant à tout symbole de l’État, site .gouv.fr
    *   DDOS pour faire tomber la plateforme
    *   défacement de la page d’accueil


## Composants systèmes

Notre unique hébergeur est Clever-Cloud. Leurs mesures de sécurité sont décrites sur leur site : [https://www.clever-cloud.com/fr/security](https://www.clever-cloud.com/fr/security)

Par ailleurs, tous les certificats SSL sont fournis par Clever-Cloud.


### Base de données

Il s’agit de Postgresql hébergé et administré par clever-cloud.


### Temps réel transport en commun

Il s’agit d’une brique écrite en Rust qui télécharge des fichiers d’horaires théoriques (GTFS) et temps réel (GTFS-RT) pour exposer l’information au format SIRI-Lite (API Rest).

Par choix de l’équipe, l’accès à l’API est ouverte et sans authentification.

Ce composant est hébergé seul sur un _scaler_ de Clever-Cloud et n’a aucune clef d’authentification vers d’autres composants.

La configuration du service contient des clés d’api partenaire.

Le code source est ouvert [https://github.com/etalab/transpo-rt](https://github.com/etalab/transpo-rt)


### Validateur

Ce composant écrit en Rust permet de fournir un fichier d’horaires théoriques (GTFS) en passant une URL (requête GET) ou en requête POST et retourne une analyse de qualité de ces horaires ainsi que des métadonnées sur les horaires (période de validité, nombre de lignes, etc.).

Par choix de l’équipe, l’accès à l’API est ouverte et sans authentification.

Ce composant est hébergé seul sur un _scaler_ de Clever-Cloud et n’a aucune clef d’authentification vers d’autres composants.

Le code source est ouvert : [https://github.com/etalab/transport-validator](https://github.com/etalab/transport-validator)


### Site web

Le site web est une application écrite en Elixir avec le framework Phoenix et se compose de plusieurs sous-applications.

L’application a accès à la base de données et au stockage Clever Cloud _Cellar._

Le code source est ouvert : [https://github.com/etalab/transport-site](https://github.com/etalab/transport-site)


#### Front et blog

Il s’agit de la partie visible en arrivant sur [https://transport.data.gouv.fr](https://transport.data.gouv.fr)


#### Vélo libre service

À partir de divers formats selon les réseaux, cette sous-application les ré-expose selon une interface unifiée.


#### Historique des horaires théoriques

Chaque fichier d’horaires de transports en commun est sauvegardée dans le service _Cellar_ de Clever Cloud (clone du service S3 de Amazon Web Services). Ainsi pour chaque autorité organisatrice des mobilités il est possible d’accéder aux anciens horaires.


### [data.gouv.fr](http://data.gouv.fr)

La plateforme transport.data.gouv.fr n’a pas vocation à refaire le travail de data.gouv.fr. Nous ne travaillons pas sur cette brique, ni ne l’hébergeons. Cependant il s’agit d’un composant essentiel à la plateforme. En particulier, nous nous basons sur data.gouv.fr pour :



*   Création des jeux de données et des ressources associées ;
*   Moissonage d’autres plateformes de données ouvertes ;
*   Identification (OAuth) pour l’édition d’une fiche ou participer à une discussion autour d’un jeu de données.


### Gitbook

Ce service sert à rédiger la documentation de [https://doc.transport.data.gouv.fr](https://doc.transport.data.gouv.fr)

Il n’a pas accès au reste de la plateforme.

Des informations sur la sécurité du service : [https://policies.gitbook.com/security-faq](https://policies.gitbook.com/security-faq)


## Mesures déjà mises en place



*   Toutes les données étant publiques et ne gérant aucune donnée nominative, nous n’avons pas de problème de confidentialité.
*   Chaque composant est hébergé sur un _scaler_ Clever Cloud indépendant. Ainsi si un composant est compromis, il ne permet pas d’accéder aux autres composants. Seule le site web a accès à la base de données.
*   Les producteurs de données doivent être validés manuellement par l’équipe pour éviter la diffusion d’un jeu de données en usurpant une identité.
*   Le service de base de données Clever Cloud effectue des _snapshots_ quotidien de la base de données permettant de remettre en place une ancienne version en cas d’altération par un attaquant.
*   Afin d’assurer l’intégrité des jeux de données, le _hash_ sha256 des jeux de données est affichés.


## Risques restants

Nous n’avons pas de mécanisme spécifique destiné à nous protéger d’une attaque de type _déni de service._

Cependant une interruption du service pendant quelque jours ne serait pas très critique.
