# Dette organisationnelle : quand les conflits techniques ne sont que le symptôme d'un manque de gouvernance

## Introduction

Dans de nombreuses équipes de développement, les conflits sont souvent attribués aux individus : développeurs difficiles, ego surdimensionnés, manque de communication ou problèmes d'attitude.

Pourtant, cette lecture est souvent incomplète.

Une part importante des tensions techniques trouve son origine dans des défaillances organisationnelles. Lorsque les règles du jeu ne sont pas définies, les développeurs sont contraints de les inventer eux-mêmes. Les décisions deviennent alors des négociations permanentes, et les désaccords techniques finissent progressivement par se transformer en conflits humains.

Autrement dit, ce que l'on perçoit comme un problème de personnes est fréquemment le symptôme d'un problème de gouvernance.

---

# Le vide organisationnel est rarement neutre

Une organisation ne peut pas fonctionner durablement sans cadre.

Lorsqu'il n'existe pas de règles communes, la nature a horreur du vide. Ce vide est alors rempli par :

* des préférences personnelles ;
* des habitudes individuelles ;
* des rapports de force ;
* des interprétations contradictoires ;
* du micro-management technique.

Plus l'organisation laisse de zones grises, plus les décisions deviennent politiques au lieu d'être techniques.

---

# Exemple classique : la Pull Request interminable

Prenons une situation très courante.

Un développeur ouvre une Pull Request.

Au lieu de recevoir des commentaires sur :

* la logique métier ;
* la sécurité ;
* les performances ;
* la maintenabilité ;
* les tests ;

il reçoit une multitude de remarques telles que :

* « Je préfère ce nom de variable. »
* « Mets plutôt cette accolade sur la ligne suivante. »
* « J'aurais utilisé une autre syntaxe. »
* « Je n'aime pas cette façon d'écrire. »
* « Chez moi je fais autrement. »

Au bout de cinquante commentaires, rien n'a réellement amélioré le produit.

Pourquoi ?

Parce qu'aucune convention n'avait été définie avant.

Le problème n'est pas que les développeurs discutent.

Le problème est que l'organisation leur demande implicitement de redécider les mêmes sujets à chaque revue de code.

Un simple formatter, un linter et quelques conventions auraient supprimé automatiquement 90 % de ces discussions.

---

# La loi de la futilité (Bikeshedding)

Ce phénomène est connu sous le nom de **loi de la futilité** (*Bike Shedding*).

Plus un sujet est simple, plus tout le monde se sent légitime pour donner son avis.

À l'inverse, les sujets complexes sont souvent moins débattus.

Sans gouvernance technique, les équipes passent alors davantage de temps à discuter :

* de l'indentation ;
* du nom d'une variable ;
* du placement d'une accolade ;

que :

* de la qualité du produit ;
* des performances ;
* de la sécurité ;
* de la dette technique ;
* des besoins métiers.

L'intelligence collective est consommée sur des sujets qui auraient pu être automatisés.

---

# Les conventions de code ne sont pas là pour faire joli

Les conventions de code poursuivent plusieurs objectifs :

* homogénéiser le code ;
* faciliter la lecture ;
* accélérer les revues de code ;
* réduire les débats inutiles ;
* permettre aux nouveaux arrivants de comprendre rapidement le projet.

Elles ne limitent pas la créativité.

Elles déplacent simplement la créativité vers les sujets qui créent réellement de la valeur.

---

# L'architecture est également une responsabilité collective

Le même raisonnement s'applique à l'architecture.

Lorsqu'une évolution importante est envisagée, elle devrait être discutée avec les personnes responsables de l'architecture ou avec le Lead Tech.

À l'inverse, lorsqu'un développeur ne sait plus où placer son code dans un projet existant, plusieurs situations sont possibles :

* l'architecture n'existe pas réellement ;
* elle n'a jamais été documentée ;
* elle a évolué sans coordination ;
* elle est devenue incohérente au fil du temps.

Dans ce cas, il est difficile de reprocher aux développeurs leurs hésitations.

Ils ne peuvent pas appliquer des règles qui n'ont jamais été clairement définies.

---

# La dette organisationnelle

On parle souvent de dette technique.

Mais il existe également une dette organisationnelle.

Elle comprend notamment :

* l'absence de conventions ;
* une architecture peu claire ;
* des responsabilités mal définies ;
* une documentation insuffisante ;
* des décisions implicites ;
* un manque d'arbitrage technique.

Comme toute dette, elle paraît faire gagner du temps au début.

Mais elle produit des intérêts.

Chaque nouveau développeur doit réapprendre les règles.

Chaque Pull Request rediscute les mêmes sujets.

Chaque évolution devient plus coûteuse.

La productivité diminue progressivement.

---

# Le coût caché

Le coût n'est pas uniquement technique.

Il est également humain.

Lorsqu'il n'existe pas de gouvernance :

* chacun développe ses propres habitudes ;
* chacun défend son territoire ;
* chacun devient propriétaire de sa façon de faire.

Les discussions cessent progressivement de porter sur les idées.

Elles portent sur les personnes.

On entend alors :

> « Il refuse toujours mes Pull Requests. »

> « Il veut imposer sa manière de coder. »

> « Avec lui on ne peut jamais travailler. »

Alors que, bien souvent, personne n'a défini les règles communes.

---

# Le rôle du Lead Tech

Le rôle d'un Lead Tech n'est pas de gagner tous les débats techniques.

Son rôle est surtout de réduire l'incertitude.

Il doit notamment :

* définir les conventions ;
* arbitrer lorsqu'un consensus n'émerge pas ;
* documenter les décisions importantes ;
* maintenir une architecture cohérente ;
* éviter que les mêmes discussions reviennent continuellement.

Chaque décision documentée est une discussion de moins demain.

---

# L'organisation influence les comportements

Les comportements individuels ne naissent pas dans le vide.

Ils sont influencés par :

* les règles ;
* les responsabilités ;
* les objectifs ;
* les incitations ;
* la culture de l'entreprise.

Une mauvaise gouvernance favorise les conflits.

Une bonne gouvernance favorise la coopération.

Cela ne signifie pas que tous les conflits sont organisationnels.

Les personnalités, les compétences et la communication jouent également un rôle.

En revanche, une organisation solide réduit fortement la probabilité que des désaccords techniques deviennent des conflits personnels.

---

# L'illusion du "livrer vite"

Certaines organisations pensent gagner du temps en évitant :

* la documentation ;
* les conventions ;
* la clarification de l'architecture ;
* les arbitrages techniques.

En réalité, elles déplacent simplement ce coût.

Le temps économisé aujourd'hui est payé plusieurs fois demain :

* en revues de code interminables ;
* en incompréhensions ;
* en refactorings ;
* en conflits ;
* en ralentissements.

Le coût n'a pas disparu.

Il a simplement été reporté sur les équipes.

---

# Conclusion

Une équipe performante n'est pas celle où tout le monde pense de la même manière.

C'est une équipe où les règles communes permettent de concentrer les débats sur les décisions importantes.

Les conventions de code, une architecture claire, des responsabilités définies et une gouvernance technique efficace ne servent pas uniquement à produire un code plus propre.

Elles permettent surtout de préserver l'intelligence collective.

Moins les développeurs doivent débattre de sujets triviaux, plus ils peuvent consacrer leur énergie à ce qui crée réellement de la valeur : le produit, son évolution, la qualité logicielle, les tests, la performance, la dette technique et l'amélioration continue.

En définitive, de nombreux conflits attribués aux individus sont en réalité les manifestations visibles d'une dette organisationnelle devenue trop importante. Investir dans la gouvernance technique n'est donc pas une dépense administrative : c'est un investissement qui améliore durablement la qualité du logiciel, la collaboration entre les équipes et la performance globale de l'organisation.
