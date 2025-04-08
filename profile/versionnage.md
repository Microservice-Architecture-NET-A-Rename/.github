# **Trunk Based Development dans la vraie vie : Une approche hybride**

Le **Trunk Based Development (TBD)** est un principe fondamental dans les pratiques modernes de développement logiciel, où les équipes cherchent à fusionner leurs modifications sur la branche principale (trunk) aussi fréquemment que possible. Cela permet de garantir une **intégration continue**, un suivi rapide des erreurs, et de minimiser le risque de conflits lors des fusions. Cependant, appliquer le TBD dans la vraie vie peut parfois entraîner des problèmes, notamment une instabilité du code sur la branche principale. C'est pourquoi une approche hybride est souvent nécessaire pour répondre aux exigences spécifiques des équipes tout en maintenant les bénéfices de TBD.

### **1. Trunk Based Development pur : un équilibre délicat**

Dans un contexte de développement rapide et d'intégration continue, les développeurs sont censés fusionner fréquemment leur travail sur la branche principale. Cependant, le **Trunk Based Development pur** peut entraîner une instabilité trop fréquente du code sur la branche principale, notamment lorsque plusieurs développeurs travaillent simultanément sur des fonctionnalités complexes. Cela peut aussi rendre plus difficile de tester des fonctionnalités en développement, car des modifications fréquentes peuvent affecter la stabilité de l’application.

Afin de **conserver la stabilité du code tout en appliquant les principes du Trunk Based Development**, il est important d'adopter une approche plus **contrôlée** et **hybride**.

### **2. Une approche hybride : Fusionner régulièrement, mais avec prudence**

#### **Branches Feature et User Stories**
Dans cette approche hybride, chaque **feature** doit idéalement être divisée en plusieurs **user stories**. Une branche feature peut contenir plusieurs commits correspondant à différentes tâches ou fonctionnalités, mais ces branches doivent être **fusionnées dans la branche principale toutes les 2 à 3 jours**. Cette pratique permet de **réduire les conflits** et de faciliter l'intégration continue.

- **Raison principale** : Fusionner fréquemment permet de récupérer rapidement les modifications des autres équipes, réduisant ainsi le risque de conflits complexes. Si l'on attend trop longtemps pour fusionner, la gestion des conflits à la fin devient de plus en plus difficile et peut entraîner des régressions importantes dans le code, ce qui ralentit la livraison.

#### **Gestion du Changelog et des Merges**
Lors de la fusion des branches dans la branche principale, il est crucial de **ne pas inclure ces changements dans le changelog** jusqu'à ce que la fonctionnalité soit prête à être mise en production. Cela permet de travailler sur des fonctionnalités tout en gardant la branche principale stable et propre pour la livraison. Cela empêche également l’exposition prématurée des fonctionnalités en développement.

- **Exemple** : Si une fonctionnalité est en développement et fusionnée dans la branche principale, elle peut être cachée des utilisateurs en utilisant des **features flags**. Cependant, cette fonctionnalité ne doit pas apparaître dans les changelogs tant qu'elle n'est pas prête pour être activée en production.

#### **Gestion des Conflits**
Les conflits de fusion sont inévitables, mais pour les minimiser, il est recommandé de **rebaser fréquemment** pour récupérer les dernières modifications effectuées par les autres équipes. Cela permet de s'assurer que les modifications restent alignées avec la branche principale, réduisant ainsi les risques de régressions importantes et facilitant la gestion des conflits au fur et à mesure.

### **3. Utilisation des Features Flags : Maîtriser les fonctionnalités en développement**

Pour maintenir la stabilité de l’application tout en permettant aux équipes de travailler sur de nouvelles fonctionnalités, l’utilisation de **features flags** est essentielle. Ces flags permettent de cacher les fonctionnalités en développement des utilisateurs tout en continuant à livrer le code sous-jacent.

- **Avantage** : Le code de la fonctionnalité peut être fusionné dans la branche principale et prêt pour la production, tout en étant **désactivé** par un feature flag jusqu’à ce que la fonctionnalité soit complète et prête à être utilisée par les utilisateurs finaux.
  
- **Conseil supplémentaire** : Il est crucial de **penser à l’avenir** et d'implémenter une nomenclature claire pour les feature flags. Lors de recherches dans le code, il doit être facile de trouver et de supprimer ces flags, idéalement d'un seul coup, pour éviter l'accumulation de code inutile.

### **4. Les Features ne doivent pas être trop grandes ni trop complexes**

Une caractéristique fondamentale du Trunk Based Development est la **petite taille des features**. Pour éviter une surcharge de travail sur de longues périodes et minimiser le risque de régressions, il est important que les fonctionnalités développées soient relativement petites. Cela permet de les livrer rapidement, de réduire les risques et d’améliorer la prévisibilité du projet.

- **Conseil pratique** : Lorsque les fonctionnalités sont petites et modifiées fréquemment, elles sont plus faciles à intégrer dans la branche principale. Il est donc préférable d'éviter de développer des fonctionnalités trop complexes qui nécessitent des mois de travail. Idéalement, chaque fonctionnalité doit pouvoir être livrée dans un **court délai**.

### **5. Tagger les Fonctionnalités et Commits Intermédiaires**

Si le besoin de **conserver l’historique des fonctionnalités** existe, par exemple pour des raisons de traçabilité, de gestion de versions ou de suivi des correctifs, tu peux utiliser des **tags** dans Git, non seulement sur le commit final mais aussi sur les **commits intermédiaires**.

#### **Tag sur les commits intermédiaires :**
- Il est possible de **taguer un commit intermédiaire** dans la branche principale pour marquer l'achèvement d'une étape significative d'une fonctionnalité avant sa finalisation.
- **Avantage** : Cette approche permet de conserver une trace détaillée de l'évolution de la fonctionnalité tout au long de son développement. Chaque étape peut être ainsi suivie et vérifiée indépendamment. Par exemple, si un certain aspect d'une fonctionnalité a été terminé et validé dans le code, un tag peut être ajouté pour marquer ce point.
- **Pratique** : Lorsqu'un commit intermédiaire est tagué, ce tag sert de référence pour le suivi de cette partie de la fonctionnalité dans l'historique. Les tags peuvent être utilisés dans des processus comme les revues de code, le suivi des livraisons, ou la documentation des versions intermédiaires d'une fonctionnalité.

#### **Tag sur un commit final** :
Une fois qu'une fonctionnalité est terminée et prête à être mise en production, un **tag peut être ajouté** sur le commit final. Ce tag ne modifie pas l'historique des commits ni les associations avec les **user stories/WITs**.
  
- **WITs associés** : Tant que chaque commit est correctement lié à un **WIT** (par exemple, via un ID de ticket dans le message du commit), l'historique des fonctionnalités restera tracé. Les WITs (user stories) continueront à être associés aux **commits individuels** et **au commit final** via le tag. Cela permet de conserver une référence claire à l’évolution de chaque fonctionnalité.

### **6. Conclusion : Trouver un équilibre entre stabilité et agilité**

Le Trunk Based Development dans la vraie vie nécessite une approche hybride pour éviter les instabilités qui peuvent découler d’un développement trop rapide sur la branche principale. En suivant ces bonnes pratiques, l’équipe peut bénéficier de l’intégration continue tout en préservant la **stabilité du code**, en **réduisant les risques de régression**, et en **améliorant la collaboration** entre les équipes.

**En résumé :**
- **Fusionner fréquemment (tous les 2-3 jours)** pour récupérer les dernières modifications des autres équipes.
- **Utiliser des features flags** pour cacher le code en développement aux utilisateurs tout en livrant des modifications fréquentes.
- **Appliquer une nomenclature claire** pour les feature flags afin de faciliter la maintenance à long terme.
- **Rebaser régulièrement** pour minimiser les conflits.
- **Tagger les commits intermédiaires** pour conserver l’historique des modifications et permettre le suivi détaillé de l’évolution de chaque fonctionnalité.
- **Tagger également les commits finaux** pour marquer les étapes finales de la fonctionnalité avant sa mise en production.

Ce processus hybride permet de tirer parti des avantages du Trunk Based Development tout en atténuant les risques liés à l’instabilité du code et à la gestion de fonctionnalités complexes.

