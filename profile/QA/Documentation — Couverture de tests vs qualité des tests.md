# 📘 Documentation — Couverture de tests vs qualité des tests

## 1. Introduction

La couverture de tests est souvent utilisée comme indicateur de qualité logicielle. Cependant, elle est fréquemment mal interprétée : une forte couverture de code ne garantit ni la qualité des tests, ni la fiabilité du logiciel.

L’objectif de cette documentation est de clarifier la différence entre **couverture de code** et **qualité des tests**, et de proposer une approche plus pertinente du test logiciel.

---

## 2. Qu’est-ce que la couverture de tests ?

La couverture de tests (code coverage) mesure la proportion du code exécutée lors des tests automatisés.

Exemples de métriques :

* lignes de code exécutées
* branches conditionnelles couvertes
* fonctions appelées
* conditions booléennes testées

👉 Exemple :
Un test qui appelle une fonction une seule fois peut suffire à “couvrir” 100% d’une partie du code, même si les cas critiques ne sont pas testés.

---

## 3. Limites de la couverture de code

### 3.1 Une métrique quantitative, pas qualitative

La couverture répond à la question :

> “Quelles parties du code sont exécutées ?”

Mais pas :

> “Le comportement est-il correct ?”

---

### 3.2 Illusion de qualité

Une forte couverture peut donner une impression trompeuse de sécurité :

* tests superficiels
* assertions faibles ou inexistantes
* scénarios irréalistes
* absence de cas limites

👉 Résultat : le code semble “bien testé” mais peut contenir des bugs critiques.

---

### 3.3 Exemple concret

```python
def calcul_prix(prix, reduc):
    return prix - reduc
```

Test possible :

```python
assert calcul_prix(100, 10) == 90
```

➡️ Ce test peut suffire à couvrir la fonction
❌ mais ne teste pas :

* réduction négative
* prix invalide
* comportement métier attendu

---

## 4. Objectif réel des tests

Les tests doivent prioritairement vérifier :

### 4.1 Le comportement métier

* règles fonctionnelles
* logique business
* invariants du domaine

### 4.2 Les cas limites

* entrées invalides
* valeurs extrêmes
* erreurs attendues
* comportements aux frontières

### 4.3 Les scénarios utilisateurs

* parcours complets
* interactions réalistes
* flux critiques

---

## 5. Qualité des tests vs quantité

### ❌ Mauvais objectif

* augmenter la couverture
* multiplier les tests inutiles
* tester du code sans valeur métier

### ✅ Bon objectif

* tester les zones à risque
* valider les règles métier
* couvrir les cas critiques
* écrire des tests lisibles et maintenables

---

## 6. Bonnes pratiques

### 6.1 Tester le métier, pas le code

Un test doit vérifier un **résultat attendu**, pas l’implémentation interne.

---

### 6.2 Prioriser les zones à risque

* logique complexe
* calculs critiques
* sécurité
* paiement
* données sensibles

---

### 6.3 Utiliser la couverture comme indicateur secondaire

La couverture peut aider à :

* détecter du code non testé
* guider les efforts de test

Mais elle ne doit jamais être un objectif principal.

---

### 6.4 Écrire des tests lisibles

Un bon test doit :

* être compréhensible sans contexte technique profond
* expliquer le scénario métier
* être maintenable

---

## 7. Anti-patterns fréquents

* tests écrits uniquement pour “faire monter le pourcentage”
* assertions triviales (`assert true`)
* duplication de tests inutiles
* tests sans lien avec les besoins métier
* obsession du 100% coverage

---

## 8. Conclusion

La couverture de code est un indicateur utile mais limité. Elle ne reflète ni la pertinence, ni la qualité des tests.

👉 La vraie valeur des tests réside dans leur capacité à :

* valider les comportements métier
* détecter les régressions critiques
* sécuriser les zones à risque

> Une bonne suite de tests ne se mesure pas à sa taille ou sa couverture, mais à sa capacité à prévenir des bugs réels.


