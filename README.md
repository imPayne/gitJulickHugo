# Exercices sur git

Il existe plusieurs outils permettant le versionning de fichiers. 
Il s'avère qu'aujourd'hui, l'outil le plus utilisé est git.

Voici quelques exercices permettant de découvrir quelques subtilisés de git.

## Exercice N°1

> Le but de cet exercice est de découvrir les conflits de merge. 

Askip faut le faire en duo et moi j'ai bien faire chier donc je suis chiant.
Après avoir forké ce dépôt, définissez votre dépôt en privé et attribuez à votre binôme les droits afin de contribuer ensemble au sein de ce dépôt. 
Clonez ce dépôts sur vos machines respectives. 

Sur chaque machine, modifiez le fichier `README.md` afin d'y ajouter vos propres messages. 
Assurez-vous de bien travailler en même temps sur le fichier et d'y saisir des informations différentes. L'objectif étant que vous vous retrouviez à modifier simultanément les mêmes lignes d'un fichier. 

Puis, une fois satisfaits, réalisez un `git add` puis `git commit` puis un `git push`.
La première personne à envoyer le code ne devrait pas avoir de problème, le second oui. Résolvez ensemble le conflit de merge par le biais de la ligne de commande.

## Exercice N°2

> Découverte de ce qui ne génère pas de conflit

Toujours au sein du même dépôt, et toujours en binômes. 
Ajoutez simultanément un fichier ayant le même nom, "fichier1.txt" au sein du dossier. Laissez tous les deux ce fichier vide.
Puis, une fois satisfaits, réalisez un `git add` puis `git commit` puis un `git push`.
Vous ne devriez pas rencontrer de problème.

Ajoutez simultanément un fichier ayant le même nom, "fichier2.txt" au sein du dossier. Ecrivez tous les deux le même texte dans le fichier.
Puis, une fois satisfaits, réalisez un `git add` puis `git commit` puis un `git push`.
Vous ne devriez pas rencontrer de problème.

Il vous est possible de continuer à voir le travail en collaboration par le biais de `git log`. 
Vous avez aussi probablement une vue intéressant au sein de votre IDE .

## Exercice 3

> Découverte des limites de git et de sa gestion des conflits

Au sein d'un des dépôts, créez un fichier `why_pijul.txt` contenant deux lignes : 
```
A
B
```
Par le biais de push pull assurez de l'avoir sur vos deux ordinateurs. 

Sur le premier  ordinateur, modifiez le fichier pour qu'il soit comme ceci : 
```
A
X
B
```

Sur l'autre ordinateur, modifiez le fichier : 
```
G
A
B
```
Puis continuez à rajouter une ligne en haut du fichier : 
```
B
G
A
B
```
Puis encore une fois
```
A
B
G
A
B
```
Réalisez vos push pull habituels et observez le résultat.
Git lui-même s'emmêle un peu les pinceaux, et en fonction de ce que vous avez avez réalisé précisément, git peut même ne pas détecter d'incohérence et ne pas générer de conflit de merge.
Vous trouverez une explication [ici](https://pijul.org/manual/why_pijul.html).


## Exercice 4

> La gestion du stash
ALORS JE MODIFIE LE README EN PREMIER

Au sein d'un ordinateur, reprenez la rédaction du fichier `README.md` et réalisez votre commit, push. 
Au sein de l'autre machine, editez également le fichier `README.md` et faites un `git pull`afin de récupérer les modifications apportées par votre binôme. 
Votre système devrait refuser le pull et vous demander de commiter ou remiser votre travail. 
Réalisez un git stash puis reprenez le pull. 

Votre travail n'a pas pour autant été perdu mais mis dans le stashed. Un espace tampon dans lequel vous pouvez stocker (sans pour autant commiter) vos modifications. 

Vous pouvez les voir en réalisant : 
`git stash list`

puis 
`git show stash@{0}`

Et l'appliquer en réalisant `git stash pop` ou encore `git stash apply`. 
Quelle est la différence entre ces deux méthodes ?

## Exercice 5

> La gestion du squash

Regardez tout l'historique de votre dépôt git  `git log`.
Parfois il est intéressant de vouloir fusionner plusieurs commits afin de conserver un dépôt et une histoire propre. Cette manipulation est de préférence à réaliser sur des commits qui n'ont pas encore été poussés en ligne. Tout simplement car si d'autres développeurs sont en train de travailler en même temps sur votre dépôt, celà risque de poser des problèmes lors des fusions. 

### Consignes
Au sein de votre dossier réaliser : 
`git rebase -i HEAD~3 `

Remplacez tous les `pick` par des `squash`.
Modifiez le nom du commit
Puis réaliser un `git push -f`.

Au sein du second dépôt, réalisez un git pull. Vous ne verrez plus du tout l'historique. 

## Exercice 6
> La gestion des branches. 

Voici des commandes qui pourront vous être utiles afin de pouvoir suivre les consignes de l'exercice. 

Créer une branche
`git branch nom-branch`

Switch sur la branche 
`git checkout nom-branch`

Fusionner des branches 
`git checkout main && git merge nom-branch`

Créer une branch et switch dessus d'un seul coup
`git checkout -b nom-branch`

Déplacer la branche actuelle afin d'intégrer les derniers commits de la branche parente
`git rebase main`

### Consignes

Dans un contexte professionnel, le travail est souvent scindé en petites taches. Et il est d'usage de créer une branche par tache. 
A partir de votre dépôt actuel, je vous demande de créer une tache "Générer une page phpinfo". 
Les instructions à réaliser sont donc :
 - Créez une branche `feature-phpinfo`
 - Travaillez dans cette branche et créez le fichier: `echo "<?php phpinfo()" > index.php`
 - Réalisez votre commit. 

 Si vous retournez sur la branche `main`, vous verrez que le fichier n'existe pas. 

 - Vous réalisez que vous avez oublié un `;` dans le fichier php car vous avez eu le bon reflexe de tester le fichier  `php -S localhost:`.
 - Corrigez l'erreur et faites en sorte de n'avoir qu'un seul commit.

 Fusionnez votre branche dans la branche main. 
 N'oubliez pas, votre IDE et `git status` peuvent beaucoup vous servir pour visualiser ce qui se trame dans git. 

## Exercice 7
> git log en ligne de commande

Loggez l'ensemble des commits de la branche 
`git log`

Loggez l'ensemble des commits, d'une manière concise afin de ne voir qu'une ligne par commit
`git log --oneline`

Loggez l'ensemble des commits afin d'y voir les branches et leurs hierarchies
`git log --graph`


## Exercice 8
> La gestion des remote

Prenons pour exemple que vous souhaitez partir d'une base d'un projet existant sur git mais que vous souhaitez contribuer au sein d'un autre dépôt.

Vous pouvez lister les dépôts distants connus
`git remote -v`

Vous pouvez avoir plusieurs remote : 
`git remote add <alias> <url>`

Vous pouvez changer le dépôt existant
`git remote set-url origin <url>`

Vous pouvez supprimer une référence vers un dépôt distant
`git remote remove origin`


### Consignes
Définissez un nouveau remote, hébergé au sein de profil github de votre binôme.
Et synchronisez les deux comptes git. 

Il est toujours bon de comprendre un concept quand on le découvre. Ainsi prenez le temps de comprendre ainsi les commandes `git push origin main` et autres.

## Exercice 9
> Le git --bare

Il vous est possible de générer des dépots distants aussi sans `working directory` mais avec uniquement les fichiers internes de git. 

Faites donc un `git clone --bare` de votre dépôt.
Et définissez ce dossier en tant que remote

Exemple : 
```shell
git clone <url> repository
git clone --bare <url> bare-repository.git
cd repository
git remote add hello-world ../bare-repository.git
```

Ce qui peut vous servir de backup ou permettre de stocker vos dépôts ailleurs que chez gitlab, github, framagit, bitbucket ...