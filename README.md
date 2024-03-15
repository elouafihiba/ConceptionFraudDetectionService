# CONCEPTION ET DEVELOPPEMENT D'UN SYSTEME DE DETECTION DES FRAUDES


## 1. Introduction au Projet:

Dans le monde dynamique des services bancaires, la sécurité et l'intégrité des transactions sont primordiales. Afin de garantir la détection précoce et efficace des activités frauduleuses, un système de détection de fraude est essentiel. Notre système de détection de fraude est conçu pour répondre à cette nécessité croissante en offrant une solution robuste et adaptable pour les institutions financières.

### Objectif du Projet

Le système de détection de fraude a pour objectif principal de recevoir, analyser et signaler les événements provenant des systèmes bancaires. Ces événements comprennent une gamme variée de transactions, de mouvements de fonds et d'activités financières. Notre système est conçu pour identifier les schémas et les comportements suspects, permettant ainsi aux institutions financières de réagir rapidement pour prévenir les risques liées à la fraude.

### Flexibilité et Paramétrage

Ce qui distingue notre système, c'est sa capacité à être entièrement paramétrable par l'administrateur du système externe. L'administrateur à la possibilité de définir et de configurer les règles de gestion nécessaire . Cela comprend la paramétrisation des événements à surveiller, des sources de données à intégrer, des traitements à exécuter sur ces données et des résultats attendus de ces traitements. De plus, l'interprétation des résultats en termes de niveaux d'alerte est également configurable, permettant une adaptation précise aux besoins et aux politiques de sécurité de chaque institution.

### Avantages Attendus

En permettant une personnalisation approfondie, notre système offre une flexibilité inégalée pour répondre aux besoins spécifiques de chaque institution financière. En détectant rapidement les activités frauduleuses et en fournissant des alertes en temps réel, notre système aide à réduire les risques et à protéger les comptes des clients. Tout en offrant une interface intuitive et conviviale pour la configuration des règles de détection, notre système facilite la gestion et la maintenance continues, garantissant une efficacité opérationnelle maximale.

## 2. Vue d'Ensemble du Système

Le système de détection de fraude est composé de plusieurs services interconnectés, chacun jouant un rôle crucial dans le processus global de détection et de notification des activités frauduleuses.

![fraud detection system](./diagrammes/vue-ensemble.png)*architecture du système*
### Fraud Detection Service :

Ce service central est responsable de recevoir les événements provenant des systèmes bancaires externes.
Il fonctionne selon deux modes :
- **Mode Push** :Les événements sont envoyés directement par le système externe via un web service.
- **Mode Pull** : Les événements sont consommés à partir d'un courtier (broker) ou d'une file d'attente.
  Le service analyse les événements reçus et génère des alertes en fonction des paramètres configurés.
### Parameter Service :

Ce service est chargé de gérer la configuration globale du système de détection de fraude.
L'administrateur utilise ce service pour configurer :
- **Les événements à analyser**
- **Les traitements à appliquer à ces événements**
- **Les sources de données nécessaires pour effectuer les traitements.**
- **Les différents résultats possibles des traitements.**
- **Les niveaux d'interprétation des résultats en termes d'alertes.**
### Data Preparation Service :

Ce service prépare les données nécessaires à l'analyse des événements.
Il récupère les données pertinentes des sources configurées par le Parameter Service et les prépare pour l'analyse ultérieure.
### Transaction Analysis Service :

Ce service analyse les événements de fraude à l'aide des données préparées par le Data Preparation Service.
Il applique les règles de gestion spécifiques à chaque événement, telles que définies dans les paramètres.
Le service génère des résultats d'analyse détaillés pour chaque événement.
### Alert Service :

Ce service prend les résultats d'analyse générés par le Transaction Analysis Service et les traduit en alertes exploitables.
Il classe les alertes en fonction de leur gravité et de leur urgence, selon les niveaux d'interprétation définis dans les paramètres.
Les alertes sont ensuite transmises aux parties concernées pour appliquer les actions correctives nécessaire.

---
Ce système modulaire et interconnecté permet une gestion efficace des événements de fraude, en garantissant une détection rapide et précise tout en offrant la flexibilité nécessaire pour s'adapter aux besoins spécifiques de chaque institution financière.

## 3. Conception du Systeme:

### Diagramme de use case :

![fraud detection system](./diagrammes/useCase.png)

Ce diagramme de cas d'utilisation représente le processus de détection des fraudes bancaires.
Il met en lumière les interactions entre les différents acteurs et les fonctionnalités clés du système.

#### Acteurs Principaux :

- **Fraud Detection Admin** : Cet acteur est responsable de la définition 
des règles de gestion pour la détection des fraudes. Il a la capacité 
de définir les événements, les sources de données, les traitements 
et les alertes associées à la détection des fraudes. Il configure également 
les règles de gestion avec une relation incluse du cas d'utilisation 
"Validation Workflow".

- **Adria Banking System** : Cette application bancaire agit en tant 
qu'acteur principal dans l'envoi et la gestion des événements liés aux 
transactions bancaires. Elle interagit avec le système de détection 
de fraude en fournissant des données pertinentes pour l'analyse.
Nous avons adopté une approche qui vise 
à garantir la standardisation et l'interopérabilité avec différents systèmes bancaires.


### Diagramme de classe :

![fraud detection system](./diagrammes/class.png)

Ce diagramme de classe représente la structure des entités clés impliquées 
dans notre système de détection de fraude bancaire. Les classes sont conçues 
pour capturer les différents aspects des traitements, règles, sources de données, 
événements et alertes associés à la détection de fraude.

#### Classe TreatmentResult: 
Cette classe comprend les attributs suivants :

- code : Le code de résultat du traitement.
- name : Le nom du traitement.
- description : La description détaillée du traitement.
- severity : L'importance du résultat, représentée par une énumération avec les valeurs "low", "medium" et "high".

#### Classe Treatment : 
Cette classe comprend les attributs suivants :

- id : L'identifiant unique du traitement.
- name : Le nom du traitement.
- type : Le type de traitement, représenté par une énumération avec les valeurs "RESTful", "SOAP", "Serverless", "Broker" ou "Queue".

#### Classe Rule : 
Cette classe comprend les attributs suivants :

- code : Le code de la règle.
- name : Le nom de la règle.
- description : La description détaillée de la règle.
- 
#### Classe DataSource : 
Cette classe comprend les attributs suivants :

- id : L'identifiant unique de la source de données.
- name : Le nom de la source de données.
- type : Le type de la source de données, représenté par une énumération avec les valeurs "SQL Database", "Web Service" ou "Cache Database".

#### Classe Event : 
Cette classe comprend les attributs suivants :

- id : L'identifiant unique de l'événement.
- name : Le nom de l'événement.
- description : La description détaillée de l'événement.
- type : Le type de l'événement.

#### Classe Alert : 
Cette classe comprend les attributs suivants :

- code : Le code de l'alerte.
- body : Le contenu de l'alerte.

#### Classe AlertLevel : 
Cette classe comprend les attributs suivants :

- id : L'identifiant unique du niveau d'alerte.
- name : Le nom du niveau d'alerte.

### Diagramme de communication :

![fraud detection system](./diagrammes/communication.png)

Ce diagramme de communication décrit le flux de données entre 
différents services impliqués dans notre système de détection 
de fraude bancaire. Les interactions entre les services permettent
de traiter les événements, d'analyser les données et de générer 
des alertes en cas de fraude potentielle.

#### Banking System : 
Ce service est responsable de l'envoi d'événements vers 
le service de détection de fraude (Fraud Detection Service) 
et implémente la méthode suivante :

- send(event): Envoie un événement au service de détection de fraude.

#### Fraud Detection Service : 
Ce service est au cœur du processus de détection de fraude
et réalise les opérations suivantes :

- extractEventClassificationParameter(): Extrait les paramètres de
classification d'événement pour le Parameter Service.
-  eventClassification(event, rules): Classe l'événement en fonction
des règles définies.
- extractRulesParameters[eventClass]: Extrait les paramètres 
des règles pour le Parameter Service.
- extractDataSource(rulesParameters[]): Extrait les sources de données pour l'analyse.
- extractTreatment(rulesParameters[]): Extrait les traitements à appliquer.
- extractAlertLevels(rulesParameters[]): Extrait les niveaux d'alerte associés aux règles.
- extractData(datasource, event): Prépare les données pour l'analyse.
- analyse(analysisData, Treatements[]): Effectue l'analyse des transactions pour détecter les fraudes.
- sendAnalysisResults(analysisResult[]): Envoie les résultats de l'analyse au service d'alerte.
- extractAssociations(): Extrait les associations entre les résultats des traitements et les niveaux d'alerte pour le Parameter Service.
- analyseResults(analysisResult[], TreatResult_AlertLevelAssociationParameters[]): Analyse les résultats de l'analyse et génère des alertes.

#### Parameter Service : 
Ce service gère la récupération et le traitement des paramètres nécessaires à l'analyse et à la génération d'alertes.

#### Data Preparation Service : 
Ce service prépare les données pour l'analyse en extrayant les informations pertinentes des sources de données.

#### Transaction Analysis Service : 
Ce service analyse les données des transactions pour détecter les schémas de fraude potentiels.

#### Alert Service : 
Ce service est chargé de la gestion et de la transmission des alertes générées par le système de détection de fraude.

### Diagramme de sequence :

![fraud detection system](./diagrammes/sequence.png)






