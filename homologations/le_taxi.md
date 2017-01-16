# Dossier d'homologation : Le Taxi

## Décision d'homologation

Le Directeur Interministériel du Numérique, des Systèmes d'Information et de Communication

  - vu le Référentiel Général de Sécurité version 2.0 approuvé par arrêté du 13 juin 2014
  - vu le [Guide de l'Homologation de Sécurité de l'ANSSI](https://www.ssi.gouv.fr/uploads/2014/06/guide_homologation_de_securite_en_9_etapes.pdf), version 1.0 d'Août 2014
  - vue la Politique de Sécurité S.I. de l'Incubateur de la DINSIC, https://github.com/sgmap/beta.ssi/ dans sa version du XX janvier 2017
  - vu le Décret n° 2016-335 du 21 mars 2016 relatif au registre national de disponibilité des taxis
  - vu les éléments du "Dossier d'homologation : Le Taxi", ci-après ou inclus par référence

décide l'homologation du système constituant le registre national de disponibilité des taxis, aux conditions prévues ci-après.

## Commission d'homologation

La commission d'homologation est constituée de

  - V.B.
  - V.L.
  - L.V.
  - L.B.

## Périmètre

L'homologation couvre le système constituant le registre national de disponibilité des taxis, c'est à dire le serveur hébergeant l'API Taxi Exchange Point (TXP), les bases de données, les procédures et opérateurs affectés à son exploitation; ce périmètre exclut tout système ou application, mobile ou non, susceptible d'être connecté à l'API.

![Diagramme de composants logiques](https://cdn.rawgit.com/openmaraude/APITaxi_front/588acd56562385ca02e1de3aba0fb8635480e4e9/APITaxi_front/static/images/overview.svg)

## Durée et conditions de l'homologation

La décision d'homologation est temporaire, pour une durée maximale de 24 mois, et soumise à des conditions de volumétrie d'usage du service : elle n'est valable, et les risques résiduels considérés comme acceptables, que pour un volume de courses journalier inférieur à 500. En cas de dépassement de ce seuil, une nouvelle homologation doit être prononcée sous un délai de 3 mois.

## Démarche

La démarche retenue est une démarche autonome _a minima_ ("Pianissimo"), conforme également au Guide d'Analyse des Risques et au Guide d'Homologation visant les équipes dites "Agiles" (ouvrages en cours de réalisation par l'ANSSI conjointement avec la DINSIC).

## Suivi

Pendant la durée de l'homologation, la Commission est réunie si une modification substantielle de l'architecture du service, de nature a altérer l'analyse des risques, est envisagée ou implémentée.

## Analyse des risques

Cette analyse recense

  - les biens essentiels ("valeurs métier")
  - les sources de menaces
  - les composants du SI
  - les événements redoutés
  - les scénarios de menace
  - les mesures de sécurité existantes
  - les risques résiduels

Incorporée par référence: https://github.com/openmaraude/le.taxi/wiki/Anayse-des-risques dans sa version du XX janvier 2017 (page accessible publiquement)

## Recensement des composants du système

Composants physiques:

  - un serveur hébergé par OVH, identifiant technique ns376081

Composants logiques:

  - recensés sur https://github.com/openmaraude

## Procédures d'exploitations sécurisées

### Contrôles d’accès physique

Le serveur est hébergé par OVH, unique exploitant du centre de données. 
Seuls les salariés accrédités peuvent accéder physiquement aux serveurs informatiques.
L'accès est contrôlés par badge, surveillance vidéo et gardiennage 24/7.

### Standards pour les mots de passe

Les mots de passe des utilisateurs leur sont attribués par les opérateurs affectés à l'exploitation du Taxi Exchange Point (TXP).
Ils sont générés à l'aide d'un générateur de mots de passe utilisant les réglages suivants :

  - 10 caractères
  - Majuscules, minuscules, chiffres et symboles

### Gestion et réponse aux incidents

Les opérateurs affectés à l'exploitation du Taxi Exchange Point (TXP) sont seuls accrédités à intervenir sur le Taxi Exchange Point (TXP).
L'authentification des opérateurs affectés à l'exploitation du Taxi Exchange Point (TXP) est individuelle, multifacteurs (HOTP) et loguée.

### Sauvegardes 

Les différents éléments sauvegardés sont :

 - les sources : publiquement sur https://github.com/openmaraude
 - la configuration : sur un gitlab privé
 - les données : sauvegardes périodiques chiffrées (GPG) exportées vers un stockage distant

### Chiffrement des données et des communications

Toutes les communications entre le Taxi Exchange Point (TXP) et le monde extérieur sont chiffrées par SSL.
Seule exception, les datagrammes UDP remontant des opérateurs de taxis vers le Taxi Exchange Point (TXP) sont en clair (signés mais pas chiffrés), mais ce canal est unidirectionnel.

### Tests de la sécurité

Des tests réguliers de sécurité sont effectués avec des scanners de vulnérabilité (Qualys SSL Labs, AsafaWeb).
Les résultats de certains de ces tests sont publiquement consultables sur https://verif.site/#api.taxi

### Surveillance en continu

La disponibilité est surveillée en continu et publiquement consultable sur http://opendatataxi.fr/status/
Les opérateurs affectés à l'exploitation du Taxi Exchange Point (TXP) sont automatiquement alertés par e-mail en cas d'incident.


## Signature

Paris, le XX janvier 2017
