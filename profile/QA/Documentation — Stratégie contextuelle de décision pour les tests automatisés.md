# Documentation — Stratégie contextuelle de décision pour les tests automatisés

## Objectif

Cette documentation définit une méthode pragmatique pour décider **quoi tester**, **quand**, et **pourquoi** dans un projet logiciel.

Le principe central : il n’existe pas de priorité universelle. La valeur d’un test dépend toujours du contexte technique, métier et architectural.

L’objectif n’est pas de tester tout le code immédiatement, mais de maximiser rapidement :

* la réduction du risque,
* la stabilité du produit,
* la vitesse de développement,
* la sécurité des refactors.

---

# 1. Pourquoi contextualiser les tests ?

Dans un projet réel, le temps de développement est limité.
Écrire des tests sur l’ensemble du code dès le départ est rarement rentable.

Le problème n’est pas seulement :

> Faut-il écrire des tests ?

Mais plutôt :

> Quel risque veut-on réduire maintenant ?

Une bonne priorisation permet de :

* détecter les bugs critiques plus tôt,
* sécuriser les zones sensibles,
* réduire les régressions,
* automatiser les tâches répétitives.

---

# 2. Axe structurel : fréquence d’utilisation et centralité

## Perspective systémique

La fréquence d’utilisation et la centralité ne servent pas uniquement à réduire le risque de bug.

Elles servent aussi à stabiliser l’ensemble du système.

Une primitive centrale fiable améliore :

* la prédictibilité globale,
* la fiabilité des modules dépendants,
* la qualité des tests d’intégration,
* la vitesse de diagnostic.

Lorsqu’une fonction centrale est testée et stable :

* les tests d’intégration deviennent plus fiables,
* les erreurs sont plus localisables,
* le bruit de test diminue,
* le coût de debugging baisse.

Principe :

Plus une fonction est centrale, plus sa stabilité réduit l’incertitude globale du système.

Formule utile :

```text
Valeur structurelle = stabilité × réutilisation × propagation évitée
```

## Perspective économique

Le principe est simple :

Plus une fonction est utilisée, plus son comportement influence le système global.

Si une fonction est appelée partout dans le projet, une erreur dans celle-ci aura des effets en cascade.

---

## Méthode : construire un graphe d’appels

Un graphe d’appels (Call Graph) permet de visualiser :

* quelles fonctions appellent quelles fonctions,
* quelles fonctions sont centrales,
* quelles fonctions sont des dépendances majeures.

Exemple :

```text
API Controller
   ↓
Service Layer
   ↓
Business Logic
   ↓
Validation
   ↓
Utils
```

Plus une fonction est proche du centre et réutilisée, plus elle est prioritaire.

---

## Critères de priorité haute

Tester d’abord :

* fonctions cœur métier,
* fonctions utilitaires globales,
* fonctions de validation,
* fonctions de calcul.

---

## Pourquoi ?

Une fonction utilisée 200 fois est plus risquée qu’une fonction utilisée 2 fois.

Le coût d’un bug est proportionnel à sa propagation.

Formule simplifiée :

```text
Impact du bug = fréquence × dépendances × criticité
```

---

# 3. Axe économique : complexité et coût du test manuel

## Concept

Le code complexe produit plus de bugs, mais il coûte aussi plus cher à tester manuellement.

Plus la logique est complexe :

* plus il y a de branches,
* plus il y a de cas limites,
* plus les erreurs sont probables.

---

## Signaux de complexité

Code à tester rapidement :

* algorithmes,
* transformations de données,
* calculs métier,
* systèmes de règles,
* parsing,
* mapping complexe.

---

## Pourquoi automatiser cela ?

L’automatisation transforme un coût variable en coût fixe.

Sans automatisation :

chaque exécution du test coûte du temps humain.

Avec automatisation :

le coût principal est payé une seule fois, puis amorti.

Le test manuel est mauvais pour :

* la répétition,
* la précision,
* la couverture des cas limites.

Le test automatisé est meilleur pour :

* la reproductibilité,
* la vitesse,
* la fiabilité.

---

# 4. Troisième axe : Pénibilité du test manuel

## Concept

Si tester une fonctionnalité manuellement est long, frustrant ou coûteux :

elle doit être automatisée.

---

## Exemples

### Cas typiques

* remplir 15 champs à chaque test,
* reproduire plusieurs états,
* créer des jeux de données complexes,
* tester beaucoup de combinaisons.

---

## Règle simple

Si un test manuel prend plus de temps que son automatisation sur le long terme :

automatiser.

---

# 5. Axe métier : criticité fonctionnelle

## Concept

Tous les bugs n’ont pas le même coût.

Un bug sur une fonctionnalité critique doit être couvert avant le reste.

---

## Exemples de zones critiques

* authentification,
* paiement,
* permissions,
* sécurité,
* sauvegarde de données,
* facturation.

---

## Question à poser

Si cette fonctionnalité casse :

Quel est l’impact ?

* faible,
* moyen,
* élevé,
* critique.

---

# 6. Cinquième axe : Fréquence de modification

## Concept

Le code qui change souvent casse souvent.

Tester ces zones réduit le risque de régression.

---

## Zones concernées

* fonctionnalités en développement actif,
* modules souvent refactorés,
* zones de dette technique.

---

# 7. Matrice contextuelle de décision

Utiliser cette matrice comme aide à la décision, pas comme règle absolue :

| Complexité |  Usage | Priorité |
| ---------- | -----: | -------- |
| Faible     | Faible | Basse    |
| Faible     |  Haute | Moyenne  |
| Haute      | Faible | Moyenne  |
| Haute      |  Haute | Maximale |

Ajouter :

* criticité métier,
* instabilité.

---

# 8. Système de scoring

Attribuer un score à chaque fonction.

## Critères

### Usage

0 à 5

### Complexité

0 à 5

### Criticité

0 à 5

### Difficulté manuelle

0 à 5

### Instabilité

0 à 5

---

## Formule

```text
Priorité = Usage + Complexité + Criticité + Difficulté + Instabilité
```

---

## Exemple

Fonction : calculateInvoice()

Usage : 5
Complexité : 4
Criticité : 5
Difficulté manuelle : 4
Instabilité : 3

Total = 21/25

Priorité très haute.

---

# 9. Ordre recommandé de mise en place

## Niveau 1 — Tests critiques

Commencer par :

* règles métier,
* validations,
* sécurité.

---

## Niveau 2 — Tests complexes

Continuer avec :

* algorithmes,
* transformations,
* calculs.

---

## Niveau 3 — Fonctions centrales

Puis :

* utilitaires communs,
* services partagés.

---

## Niveau 4 — Cas limites

Ensuite :

* erreurs,
* exceptions,
* edge cases.

---

## Niveau 5 — Régression

Enfin :

* bugs corrigés,
* scénarios historiques.

---

# 10. Ce qu’il ne faut pas tester en premier

Éviter de commencer par :

* getters simples,
* setters simples,
* code trivial,
* wrappers sans logique.

Pourquoi ?

Faible valeur.

---

# 11. Types de tests recommandés

## Unit tests

Pour :

* logique métier,
* calculs,
* fonctions isolées.

---

## Integration tests

Pour :

* interaction entre modules,
* base de données,
* APIs.

---

## End-to-end tests

Pour :

* parcours utilisateur critiques.

---

# 12. Workflow recommandé

Étape 1 : cartographier le code

Étape 2 : identifier les fonctions centrales

Étape 3 : scorer chaque fonction

Étape 4 : prioriser

Étape 5 : écrire les tests

Étape 6 : intégrer au CI/CD

Étape 7 : maintenir les tests

---

# 13. Checklist pratique

Avant d’écrire un test :

* Cette fonction est-elle souvent utilisée ?
* Est-elle complexe ?
* Est-elle critique ?
* Est-elle pénible à tester à la main ?
* Change-t-elle souvent ?

Si oui sur plusieurs points : priorité haute.

---

# 14. Règle de décision finale

La meilleure stratégie de test repose sur l’analyse du contexte.

Une formule plus réaliste :

```text
Valeur du test = surface de propagation × risque × coût de détection × criticité contextuelle
```

En pratique :

Tester d’abord ce qui :

* casse fort,
* casse souvent,
* est difficile à vérifier manuellement,
* évolue régulièrement.

---

# 15. Modèle de valeur d’un test

La valeur d’un test peut être évaluée selon trois dimensions :

## Valeur structurelle

Réduction de l’incertitude système.

Mesurée par :

* centralité,
* fréquence d’usage,
* surface de propagation.

## Valeur économique

Réduction du coût opérationnel.

Mesurée par :

* temps de test manuel,
* répétition,
* difficulté de reproduction.

## Valeur métier

Réduction du risque business.

Mesurée par :

* impact utilisateur,
* impact financier,
* impact sécurité.

Formule globale :

```text
Valeur du test = valeur structurelle + valeur économique + valeur métier
```

---

# Conclusion

Une bonne stratégie de test n’est pas basée sur la quantité de tests, mais sur leur valeur.

L’objectif est de protéger le maximum de comportement critique avec le minimum d’effort initial.

Principe clé :

Tester selon le contexte avant de tester selon une règle fixe.

Un test unitaire sur une primitive structurelle peut être plus important qu’un test d’intégration sur une feature métier si cette primitive conditionne la prédictibilité globale du système.
