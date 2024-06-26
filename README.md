# Sitourisme (PACA-API)

Passerelle permettant d'importer automatiquement des itinéraires depuis l'API d'instances Geotrek-admin vers Apidae (par API).

- Fonctionnement et correspondance des champs : https://geotrek.ecrins-parcnational.fr/ressources/technique/2022-04-Geotrek-Apidae-v2.pdf
- Présentation aux rencontres Geotrek 2021 : https://geotrek.ecrins-parcnational.fr/rencontres/2021/presentations/09-geotrek-apidae.pdf

Afin de mettre en place la passerelle, il est nécessaire (voir PDF sur le Github):
- côte Apidae : s'abonner au projet multi-membre n°7421 
- côté Geotrek : fournir les éléments suivants :
  - URL du flux API Geotrek
  - Pour chaque identifiant de structure Geotrek, fournir l'identifiant de l'ENT correspondant dans Apidae 

Version 1 financée par la [Région Sud](https://www.maregionsud.fr), développée par [IDfr](https://www.idfr.net) et [MEDIACTEURS](https://mediacteurs.net).

Depuis 2023, l'[agence WebSenso](https://www.websenso.com) héberge la plateforme qui synchronise quotidiennement Geotrek avec Apidae et prépare la version 1.1 de la passerelle.
Mars 2024, l'[agence WebSenso](https://www.websenso.com) publie la version 2.1 de la passerelle.

## Installation

Outils nécessaires :

- NodeJS 15+
- Docker et Docker-compose
- MongoDB 4.4.6

Créer la structure de dossier :

```
├── Sitourisme (PACA-API)
└── var
    └── data
        └── report
```

Dans le projet effectuer les commandes d'installation : 

```
$ docker-compose up -d
```
Le container Docker de MongoDB est ainsi créé.

Ensuite pour générer l'application :

```
$ npm install
```

Environnement de développement, connecté à apidae.cooking sur un projet en écriture / multimembre
```
$ npm run dev 
```

Environnement de production, connecté à apidae.com 
```

$ npm run prod
```

## Usage

L'import des données est effectué automatiquement toutes les nuits via la commande : 

```
$ curl "URL/api/products/import?type=geotrek-api"
```

# Changelog

## 2.1 - WebSenso
- Fix picture'author recording to author record in place of description
- Library classes refactoring
- Server controller refactoring
- Models classes, entity model, entity factory & generic import refactoring
- Removing old unused method
- Product & Event Schema updated

## 1.1 - 1.2  - WebSenso
- EVO Write on Apidae Multimember project
- EVO New Geotrek configuration file with Axios renew connection
- EVO New Geotrek configuration file to customize activities depending of Geotrek instance
- EVO Config/Apidae - Json Activity from Apidae
- EVO FO removing auto inscription and unused views
- EVO FO listing products - Adding status / ID Geotrek - Apidae / Errors
- Class ImportGenericGeotrekApi refactored with deprecated Util.inherits removed by ES6 extends Geotrek import class
- Depcheck install & clean dependencies modules from npm project (async, elasticsearch, json2csv, mongodb, q, slug, xml2json)
- Tests Lint Done
- Removing unused routes & methods from controller / models
- Removing old Geotrek import 
- Removing old RegionDo import
- Removing unused ElasticSearch on Api Geotrek import
- Removing Ecosystem / PM2 old hosting configuration

## 1.0
- FO Angular 1.4.14 managed by Bower
- MongoDB 4.4.6
- ElasticSearch
- Geotrek / Geotrek API / RegioDo

## To prepare
- Update to Mangoose 7.1.x - Methods no CB allowed > refact to do 
- Fix middleware Passeport on product api, Guest GET allowed
- Remove Swig module - Engine templating refactoring needed
