# service du preparation des données

ce service a pour l'objective de preparer les données necessaire pour analyser les transaction et detecter les fraudes

la modelisation initial consiste a configurer les sources de données a recuperer pour analyser les transactions

Cette approche implique de configurer le système pour récupérer les données pertinentes à l'analyse à partir de sources externes, telles que des systèmes bancaires ou des bases de données externes. Voici les avantages et les inconvénients de cette approche :

un exemple comme notre system de detection de fraude revecoir un evenement d'authentification notre service de preparation de donnée doit extraire dans une base de donnée les derniers session de l'utilisateur (les addresses ip, les dispositive utilisé)

cette approche presente plusieurs avantages

Flexibilité : En récupérant les données depuis des sources externes, le système peut s'adapter à différents formats de données et à des sources variées, offrant ainsi une plus grande flexibilité.

Réduction du Besoin de Stockage de Données : En récupérant les données directement depuis les sources externes au moment de leur utilisation, cela réduit le besoin de stockage de données à long terme, ce qui peut réduire les coûts d'infrastructure associés.

Compatibilité avec les Petites Applications : Cette approche permet au système de fonctionner efficacement même pour des applications de petite taille, car il n'est pas nécessaire de stocker de grandes quantités de données localement.

mais il faut prendre en consideration quelque aspect

Dépendance aux Sources Externes : Cette approche rend le système dépendant des sources externes pour la disponibilité et l'intégrité des données, ce qui peut entraîner des risques en cas de panne ou de problème avec les sources de données externes.

Latence Potentielle : La récupération des données depuis des sources externes peut entraîner une certaine latence, en particulier si les sources de données sont situées sur des systèmes distants ou si les volumes de données sont importants.

Complexité de Configuration : Configurer le système pour récupérer efficacement les données depuis des sources externes peut nécessiter une certaine complexité de configuration, en particulier avec des sources de données variées et des formats de données différents.

*Qualité de Traitement :* Les formats de données dans les bases de données des systèmes bancaires sont souvent transactionnels et doivent être transformés en temps réel pour être utilisés dans un contexte d'analyse. Cela peut entraîner des défis supplémentaires en termes de qualité de traitement des données.

Approche de Stockage des Transactions
Stockage de Toutes les Transactions dans une Base de Données Propriétaire
Cette approche implique de stocker toutes les transactions reçues par le système dans une base de données propriétaire. Voici les avantages et les inconvénients de cette approche :

Avantages :
Analyse Complète des Transactions : En stockant toutes les transactions dans notre propre base de données, nous avons accès à l'ensemble des données nécessaires à l'analyse et à la détection de fraudes, permettant une analyse complète des schémas de fraude.
Adaptabilité : En utilisant notre propre base de données, nous avons le contrôle total sur la structure et le fonctionnement de la base de données, ce qui nous permet de l'adapter spécifiquement à nos besoins en matière de détection de fraudes.
Utilisation de Bases de Données Graphes : En optant pour une base de données orientée graphe, nous pouvons visualiser les différentes entités et leurs relations de manière plus intuitive, ce qui facilite la détection des schémas de fraudes complexes.
Inconvénients :
Coût de Stockage : Stocker toutes les transactions dans notre propre base de données peut entraîner des coûts de stockage significatifs, en particulier pour les volumes de données importants.
Complexité de Configuration : Configurer et gérer une base de données propriétaire peut nécessiter une expertise technique supplémentaire et une gestion plus complexe par rapport à l'utilisation de bases de données transactionnelles standard.
Maintenance Continue : Une fois la base de données configurée, elle nécessitera une maintenance continue pour assurer sa disponibilité, sa performance et sa sécurité.
Choix de la Base de Données
Pour cette approche, le choix de la base de données est crucial. Il est recommandé d'utiliser une base de données orientée graphe, qui offre une haute adaptabilité, des performances élevées et une capacité à gérer des volumes de données importants sans compromettre la disponibilité du système. Les bases de données graphes telles que Neo4j ou Amazon Neptune peuvent être envisagées en fonction des besoins spécifiques du projet.