# Documentation – Évolution des Procédures Stockées vers les Microservices

---

## Introduction

Avant l'émergence des architectures à base de microservices, les applications informatiques étaient majoritairement conçues sous forme de monolithes. Dans ce contexte, les **procédures stockées** et les **fonctions SQL** jouaient un rôle central pour encapsuler la logique métier directement au niveau de la base de données.

Avec l'évolution vers les microservices, la gestion de la logique métier a changé de paradigme. Ce document présente cette évolution et les bonnes pratiques à adopter lors d'une transition vers une architecture distribuée.

---

## 1. Rôle des Procédures Stockées dans les Architectures Monolithiques

### 1.1 Centralisation des données

- Utilisation d'une base de données unique pour l'ensemble de l'application.
- La logique métier était centralisée dans des fonctions et procédures SQL.

### 1.2 Avantages

- **Réutilisabilité** : Éviter la duplication de code.
- **Performance** : Réduction des allers-retours entre application et BDD.
- **Sécurité** : Contrôle d'accès à travers des interfaces définies.
- **Maintenance** : Mise à jour unique de la logique pour toutes les applications utilisatrices.
- **Intégrité des données** : Garantir l'application cohérente des règles métier au niveau de la base de données.

### 1.3 Limites

- Forte dépendance à la base de données.
- Difficulté à évoluer vers des architectures modulaires.

---

## 2. Évolution vers l'Architecture Microservices

### 2.1 Principes Clés

- **Décentralisation** : Chaque service gère ses propres données.
- **Souveraineté des données** : Accès via APIs, pas directement à la BDD.
- **Polyglot Persistence** : Choix de différentes technologies de stockage selon les besoins (SQL, NoSQL, etc.).

### 2.2 Impacts sur les Procédures Stockées

- Diminution de l'utilisation de procédures partagées.
- Externalisation de la logique métier dans des microservices exposant des APIs.

---

## 3. Strégie de Migration Progressive

### 3.1 Centralisation Initiale

- Regrouper et documenter les procédures existantes.
- Identifier les fonctionnalités critiques à migrer en priorité.

### 3.2 Extraction et APIƒcation

- Créer des microservices encapsulant la logique extraite.
- Exposer des APIs REST/SOAP pour remplacer les appels directs.

### 3.3 Transition Contrôlée

- Adapter progressivement les applications consommatrices.
- Maintenir la cohérence métier et l'intégrité des données durant la période de coexistence.

### 3.4 Tests et Validation

- Tester chaque fonctionnalité migrée pour assurer l'équivalence fonctionnelle.
- Prévoir des outils d'orchestration (API Gateway, orchestrateurs).

---

## 4. Avantages de la Migration

- **Modularité** : Indépendance des services.
- **Scalabilité** : Possibilité de faire évoluer un service sans impacter les autres.
- **Interopérabilité** : Utilisation facilitée par des systèmes hétérogènes.
- **Résilience** : Un incident isolé n'affecte pas l'ensemble du système.
- **Maintien de l'intégrité des données** : Contrôler les règles métier même dans une architecture distribuée.

---

## 5. Points de Vigilance

- **Complexité de la migration** : Certaines logiques très imbriquées peuvent être difficiles à extraire.
- **Transactions distribuées** : Gestion complexe des opérations atomiques sur plusieurs services.
- **Performance** : Risques d'augmenter la latence si l'orchestration n'est pas optimisée.
- **Garantir l'intégrité des données** : Prévoir des mécanismes de validation et de vérification.

---

## Conclusion

Centraliser la logique métier dans la base de données était une stratégie judicieuse dans les architectures monolithiques. Aujourd'hui, avec la tendance aux microservices, cette logique doit être extraite et externalisée sous forme de services autonomes, exposant leur logique via APIs.

Une approche progressive et méthodique est essentielle pour réussir cette transition tout en garantissant la cohérence fonctionnelle, la performance, et l'intégrité des données du système global.

---

> **Sources & Ressources** :
>
> - [Learn Microsoft - Microservices Data Sovereignty](https://learn.microsoft.com/fr-fr/dotnet/architecture/microservices/architect-microservice-container-applications/data-sovereignty-per-microservice)
> - [Laconsole.dev - Fonctions et Procédures Stockées](https://laconsole.dev/formations/sql/fonctions-procedures-stockees/)
> - [LesMicroservices.com - Introduction aux Microservices](https://www.lesmicroservices.com/2020/05/introduction-microservices-p2.html)

---
