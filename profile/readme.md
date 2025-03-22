# Introduction

Dans un environnement de développement orienté microservices, la communication et la connectivité entre les différents composants sont essentielles. Cependant, la mise en place d'une infrastructure de test efficace peut rapidement devenir complexe et chronophage.

C'est dans cette optique que notre projet vise à proposer un **template de pipeline** permettant de tester facilement la communication et la connectivité entre plusieurs services. Ce template inclut les éléments suivants :

- Un système de messagerie **RabbitMQ** pour assurer la transmission asynchrone des messages entre services.
- Un **frontend** pour interagir avec l'infrastructure.
- Deux **APIs** distinctes assurant des fonctionnalités spécifiques.
- Une **passerelle API Gateway** pour gérer l'acheminement des requêtes entrantes et sécuriser l'accès aux services.
- Un **load balancing avec Nginx (reverse proxy)** pour assurer une répartition efficace du trafic et garantir une haute disponibilité des services.

## Objectif du projet

L'objectif principal de ce projet est de fournir un **template générique et automatisé** permettant de tester et de valider les interactions entre les différentes composantes d'une architecture microservices **sans complexité excessive**. Ce template inclut tous les éléments nécessaires à une exécution immédiate et reproductible.

Grâce à cette approche, nous visons à **accélérer le développement et la standardisation** des processus de communication entre les services. Ce pipeline simplifie la mise en place d'une infrastructure de test robuste et reproductible, évitant ainsi aux développeurs de perdre du temps sur des configurations récurrentes.

## État actuel et évolutions futures

À ce jour, **Microservice API Template** est en place et sert de base pour la création et l'intégration des APIs dans une architecture microservices. Les prochaines étapes incluront l'ajout des fonctionnalités suivantes :

- **API Gateway** : Point d'entrée unique pour les clients externes avec gestion des authentifications et du routage.
- **RabbitMQ** : Communication asynchrone entre services via un système de messagerie.
- **Load balancing avec Nginx** : Répartition de charge pour améliorer la scalabilité et la résilience.
- **Intégration d'un frontend** pour interagir avec les services de l'infrastructure.

### Évolutions futures pour la tolérance aux pannes et l'atomicité des transactions

Dans le cadre de l'amélioration continue de notre architecture microservices, nous prévoyons d'implémenter les mécanismes suivants :

1. **Utilisation de RabbitMQ et Circuit Breaker pour la tolérance aux pannes** :
   - Mise en place de files d'attente RabbitMQ pour gérer la communication asynchrone entre les services.
   - Implémentation du pattern Circuit Breaker pour prévenir la propagation des pannes et améliorer la résilience du système.
   - Pour plus d'informations, consultez la [documentation Microsoft sur l'utilisation de RabbitMQ dans un environnement de test](https://learn.microsoft.com/fr-fr/dotnet/architecture/microservices/multi-container-microservice-net-applications/rabbitmq-event-bus-development-test-environment).

2. **Transaction Outbox Pattern pour l'atomicité des événements** :
   - Création d'une table persistante pour stocker les événements avant leur publication.
   - En cas de panne générale, les événements non traités seront republiés, assurant ainsi la cohérence des données entre les services.
   - Ce pattern est particulièrement utile pour garantir l'atomicité des opérations impliquant à la fois des mises à jour de base de données et la publication d'événements.
   - Pour plus de détails, voir [le pattern Transactional Outbox](https://microservices.io/patterns/data/transactional-outbox.html).

3. **Considérations sur le pattern SAGA** :
   - Bien que non implémenté dans cette version, le pattern SAGA pourrait être envisagé pour de futures évolutions, particulièrement pour les architectures microservices complexes nécessitant des transactions distribuées.
   - SAGA est particulièrement utile pour gérer des transactions longues et complexes impliquant plusieurs services, mais sa mise en œuvre peut être complexe.
   - Son utilisation est recommandée principalement pour les grandes architectures microservices avec des besoins transactionnels complexes.
   - Pour plus d'informations, consultez la [documentation Microsoft sur le pattern SAGA](https://learn.microsoft.com/fr-fr/azure/architecture/patterns/saga).

Ces évolutions futures permettront d'améliorer significativement la robustesse, la fiabilité et la cohérence des données dans notre architecture microservices, tout en maintenant une approche pragmatique adaptée à la complexité de notre système.

## Architecture et fonctionnement

### API Gateway

L'**API Gateway** joue un rôle central en tant que point d'entrée unique pour les clients externes (applications mobiles, sites web, partenaires). Elle prend en charge :

- **Authentification et autorisation** (OAuth2, JWT)
- **Routage et transformation des requêtes**
- **Gestion des versions d'API**
- **Limitation de débit (rate limiting)**

Exemple : Un client externe appelle `/api/orders` via l'API Gateway pour créer une commande. L'API Gateway valide le token JWT et route la requête vers le microservice "Commandes".

### RabbitMQ

**RabbitMQ** est utilisé pour la communication asynchrone entre microservices internes, notamment pour :

- **L'échange d'événements entre services** (pub/sub)
- **L'orchestration de workflows longs** (exemple : traitement de paiement asynchrone)
- **La persistance des messages** en cas de panne

Exemple : Le microservice "Commandes" publie un événement `OrderCreated` dans RabbitMQ, et le microservice "Facturation" le consomme pour générer une facture.

### API Gateway vs RabbitMQ

| Critère  | API Gateway                      | RabbitMQ                        |
| -------- | -------------------------------- | ------------------------------- |
| Accès    | Externe + Interne (synchrone)    | Interne uniquement (asynchrone) |
| Sécurité | Gérée au niveau HTTP (JWT, etc.) | Credentials + TLS               |
| Latence  | Optimisé pour le temps réel      | Tolère des délais               |
| Couplage | Couplage client-service          | Découplage service-service      |

### Interaction API Gateway et RabbitMQ

Un scénario typique combinant les deux :

1. Un client externe appelle l'API Gateway pour créer une commande.
2. L'API Gateway valide la requête et publie un message dans RabbitMQ.
3. Les microservices internes consomment le message via RabbitMQ pour traiter la commande.

## Avantages

- **Augmentation de la productivité** : En fournissant un environnement prêt à l'emploi, ce projet permet aux équipes de développement de se concentrer sur la conception et l'amélioration de leurs services sans se soucier de la mise en place de l'infrastructure de test.
- **Facilité d'intégration de nouveaux langages** : Dans le futur, il sera simple d'ajouter de nouveaux projets développés dans d'autres langages, grâce à des templates dédiés.
- **Automatisation et standardisation** : Chaque projet généré suivra les mêmes conventions et pratiques recommandées, garantissant une homogénéité et une meilleure maintenabilité du code.
- **Workflows intégrés** : Les templates incluent des workflows GitHub préconfigurés pour la gestion des releases et le déploiement continu, assurant un cycle de développement fluide et optimisé.
- **Load balancing efficace** : L'intégration de **Nginx** comme **reverse proxy** permet une répartition optimale des requêtes entre les services, améliorant ainsi les performances et la scalabilité de l'infrastructure.

## Vision future

Avec cette approche, l'ajout de nouveaux projets ou l'intégration de nouvelles technologies devient beaucoup plus simple. La création de nouveaux templates pour d'autres langages permettra de s'adapter rapidement aux besoins changeants des équipes de développement.

En définitive, ce projet vise à fournir une **base solide et évolutive** pour tester l'infrastructure des architectures microservices en toute simplicité.

**GitHub est et restera la meilleure plateforme pour cela !**
