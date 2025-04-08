# **Trunk Based Development dans la vraie vie : Une approche hybride**

Le **Trunk Based Development (TBD)** est un principe fondamental dans les pratiques modernes de d�veloppement logiciel, o� les �quipes cherchent � fusionner leurs modifications sur la branche principale (trunk) aussi fr�quemment que possible. Cela permet de garantir une **int�gration continue**, un suivi rapide des erreurs, et de minimiser le risque de conflits lors des fusions. Cependant, appliquer le TBD dans la vraie vie peut parfois entra�ner des probl�mes, notamment une instabilit� du code sur la branche principale. C'est pourquoi une approche hybride est souvent n�cessaire pour r�pondre aux exigences sp�cifiques des �quipes tout en maintenant les b�n�fices de TBD.

### **1. Trunk Based Development pur : un �quilibre d�licat**

Dans un contexte de d�veloppement rapide et d'int�gration continue, les d�veloppeurs sont cens�s fusionner fr�quemment leur travail sur la branche principale. Cependant, le **Trunk Based Development pur** peut entra�ner une instabilit� trop fr�quente du code sur la branche principale, notamment lorsque plusieurs d�veloppeurs travaillent simultan�ment sur des fonctionnalit�s complexes. Cela peut aussi rendre plus difficile de tester des fonctionnalit�s en d�veloppement, car des modifications fr�quentes peuvent affecter la stabilit� de l�application.

Afin de **conserver la stabilit� du code tout en appliquant les principes du Trunk Based Development**, il est important d'adopter une approche plus **contr�l�e** et **hybride**.

### **2. Une approche hybride : Fusionner r�guli�rement, mais avec prudence**

#### **Branches Feature et User Stories**
Dans cette approche hybride, chaque **feature** doit id�alement �tre divis�e en plusieurs **user stories**. Une branche feature peut contenir plusieurs commits correspondant � diff�rentes t�ches ou fonctionnalit�s, mais ces branches doivent �tre **fusionn�es dans la branche principale toutes les 2 � 3 jours**. Cette pratique permet de **r�duire les conflits** et de faciliter l'int�gration continue.

- **Raison principale** : Fusionner fr�quemment permet de r�cup�rer rapidement les modifications des autres �quipes, r�duisant ainsi le risque de conflits complexes. Si l'on attend trop longtemps pour fusionner, la gestion des conflits � la fin devient de plus en plus difficile et peut entra�ner des r�gressions importantes dans le code, ce qui ralentit la livraison.

#### **Gestion du Changelog et des Merges**
Lors de la fusion des branches dans la branche principale, il est crucial de **ne pas inclure ces changements dans le changelog** jusqu'� ce que la fonctionnalit� soit pr�te � �tre mise en production. Cela permet de travailler sur des fonctionnalit�s tout en gardant la branche principale stable et propre pour la livraison. Cela emp�che �galement l�exposition pr�matur�e des fonctionnalit�s en d�veloppement.

- **Exemple** : Si une fonctionnalit� est en d�veloppement et fusionn�e dans la branche principale, elle peut �tre cach�e des utilisateurs en utilisant des **features flags**. Cependant, cette fonctionnalit� ne doit pas appara�tre dans les changelogs tant qu'elle n'est pas pr�te pour �tre activ�e en production.

#### **Gestion des Conflits**
Les conflits de fusion sont in�vitables, mais pour les minimiser, il est recommand� de **rebaser fr�quemment** pour r�cup�rer les derni�res modifications effectu�es par les autres �quipes. Cela permet de s'assurer que les modifications restent align�es avec la branche principale, r�duisant ainsi les risques de r�gressions importantes et facilitant la gestion des conflits au fur et � mesure.

### **3. Utilisation des Features Flags : Ma�triser les fonctionnalit�s en d�veloppement**

Pour maintenir la stabilit� de l�application tout en permettant aux �quipes de travailler sur de nouvelles fonctionnalit�s, l�utilisation de **features flags** est essentielle. Ces flags permettent de cacher les fonctionnalit�s en d�veloppement des utilisateurs tout en continuant � livrer le code sous-jacent.

- **Avantage** : Le code de la fonctionnalit� peut �tre fusionn� dans la branche principale et pr�t pour la production, tout en �tant **d�sactiv�** par un feature flag jusqu�� ce que la fonctionnalit� soit compl�te et pr�te � �tre utilis�e par les utilisateurs finaux.
  
- **Conseil suppl�mentaire** : Il est crucial de **penser � l�avenir** et d'impl�menter une nomenclature claire pour les feature flags. Lors de recherches dans le code, il doit �tre facile de trouver et de supprimer ces flags, id�alement d'un seul coup, pour �viter l'accumulation de code inutile.

### **4. Les Features ne doivent pas �tre trop grandes ni trop complexes**

Une caract�ristique fondamentale du Trunk Based Development est la **petite taille des features**. Pour �viter une surcharge de travail sur de longues p�riodes et minimiser le risque de r�gressions, il est important que les fonctionnalit�s d�velopp�es soient relativement petites. Cela permet de les livrer rapidement, de r�duire les risques et d�am�liorer la pr�visibilit� du projet.

- **Conseil pratique** : Lorsque les fonctionnalit�s sont petites et modifi�es fr�quemment, elles sont plus faciles � int�grer dans la branche principale. Il est donc pr�f�rable d'�viter de d�velopper des fonctionnalit�s trop complexes qui n�cessitent des mois de travail. Id�alement, chaque fonctionnalit� doit pouvoir �tre livr�e dans un **court d�lai**.

### **5. Tagger les Fonctionnalit�s et Commits Interm�diaires**

Si le besoin de **conserver l�historique des fonctionnalit�s** existe, par exemple pour des raisons de tra�abilit�, de gestion de versions ou de suivi des correctifs, tu peux utiliser des **tags** dans Git, non seulement sur le commit final mais aussi sur les **commits interm�diaires**.

#### **Tag sur les commits interm�diaires :**
- Il est possible de **taguer un commit interm�diaire** dans la branche principale pour marquer l'ach�vement d'une �tape significative d'une fonctionnalit� avant sa finalisation.
- **Avantage** : Cette approche permet de conserver une trace d�taill�e de l'�volution de la fonctionnalit� tout au long de son d�veloppement. Chaque �tape peut �tre ainsi suivie et v�rifi�e ind�pendamment. Par exemple, si un certain aspect d'une fonctionnalit� a �t� termin� et valid� dans le code, un tag peut �tre ajout� pour marquer ce point.
- **Pratique** : Lorsqu'un commit interm�diaire est tagu�, ce tag sert de r�f�rence pour le suivi de cette partie de la fonctionnalit� dans l'historique. Les tags peuvent �tre utilis�s dans des processus comme les revues de code, le suivi des livraisons, ou la documentation des versions interm�diaires d'une fonctionnalit�.

#### **Tag sur un commit final** :
Une fois qu'une fonctionnalit� est termin�e et pr�te � �tre mise en production, un **tag peut �tre ajout�** sur le commit final. Ce tag ne modifie pas l'historique des commits ni les associations avec les **user stories/WITs**.
  
- **WITs associ�s** : Tant que chaque commit est correctement li� � un **WIT** (par exemple, via un ID de ticket dans le message du commit), l'historique des fonctionnalit�s restera trac�. Les WITs (user stories) continueront � �tre associ�s aux **commits individuels** et **au commit final** via le tag. Cela permet de conserver une r�f�rence claire � l��volution de chaque fonctionnalit�.

### **6. Conclusion : Trouver un �quilibre entre stabilit� et agilit�**

Le Trunk Based Development dans la vraie vie n�cessite une approche hybride pour �viter les instabilit�s qui peuvent d�couler d�un d�veloppement trop rapide sur la branche principale. En suivant ces bonnes pratiques, l��quipe peut b�n�ficier de l�int�gration continue tout en pr�servant la **stabilit� du code**, en **r�duisant les risques de r�gression**, et en **am�liorant la collaboration** entre les �quipes.

**En r�sum� :**
- **Fusionner fr�quemment (tous les 2-3 jours)** pour r�cup�rer les derni�res modifications des autres �quipes.
- **Utiliser des features flags** pour cacher le code en d�veloppement aux utilisateurs tout en livrant des modifications fr�quentes.
- **Appliquer une nomenclature claire** pour les feature flags afin de faciliter la maintenance � long terme.
- **Rebaser r�guli�rement** pour minimiser les conflits.
- **Tagger les commits interm�diaires** pour conserver l�historique des modifications et permettre le suivi d�taill� de l��volution de chaque fonctionnalit�.
- **Tagger �galement les commits finaux** pour marquer les �tapes finales de la fonctionnalit� avant sa mise en production.

Ce processus hybride permet de tirer parti des avantages du Trunk Based Development tout en att�nuant les risques li�s � l�instabilit� du code et � la gestion de fonctionnalit�s complexes.

