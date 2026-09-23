# Labo 1 - Introduction

But du labo : à la fin, votre ordinateur compile du C++, vous savez
travailler à deux sur un dépôt Git avec des branches et des pull requests,
et vous avez écrit et testé vos premiers programmes.

Ce labo se fait en **binôme**, dans ce dépôt. Il n'est pas noté, mais il
est **vérifié** : nous regardons ce qui est sur GitHub à la date indiquée
dans Roster.

Guides d'accompagnement :
[Installation](https://heigvd-prg-b-26.github.io/guides/installation.html),
[Git en pratique](https://heigvd-prg-b-26.github.io/guides/git.html),
[Assertions et premiers tests](https://heigvd-prg-b-26.github.io/guides/assertions.html).

## Gestion du temps

Vous avez deux séances de deux périodes. Budget conseillé :

| Partie | Étapes | Budget |
|---|---|---|
| Partie 1 : outils, Git et premier programme | 0 à 5 | 1 séance (90 min) |
| Partie 2 : exercices et premiers tests | 6 à 8 | 1 séance (90 min) |

Dans la partie 1, l'**étape 3** (branches et pull requests) est la plus
importante : faites-la en classe. Si le temps manque, terminez l'étape 4 à
la maison. Dans la partie 2, faites les exercices dans l'ordre : trois
exercices finis et commités valent mieux que six à moitié faits.

Dans la suite, **A** est le membre du binôme dont le nom de famille vient
en premier dans l'ordre alphabétique, **B** est l'autre.

---

## Partie 1 : outils, Git et premier programme

### Étape 0 : ordinateur prêt (10 min)

Chacun passe la
[liste de contrôle](https://heigvd-prg-b-26.github.io/guides/installation.html#liste-de-contrôle)
du guide d'installation : compilateur, Git configuré, clé SSH, compte
GitHub, CLion. Si une ligne ne passe pas, appelez-nous tout de suite.

### Étape 1 : récupérer le dépôt (15 min)

Chacun sur son ordinateur :

1. Acceptez l'assignment sur Roster. Le premier du binôme crée le dépôt,
   le deuxième le rejoint.
2. Clonez le dépôt dans CLion avec l'URL **SSH** : suivez
   [Cloner un dépôt de laboratoire](https://heigvd-prg-b-26.github.io/guides/git.html#git-dans-clion).
3. Lancez la cible `presentation` (bouton **Run**). La console affiche
   `Bonjour PRG`.

Ouvrez `CMakeLists.txt` : c'est le modèle du cours, quatre lignes utiles
et le bloc des avertissements. Vous le réutiliserez tel quel dans vos
projets.

### Étape 2 : premier commit, premier push (15 min)

**A** seulement :

1. Dans `main.cpp`, complétez l'en-tête : les deux adresses e-mail du
   binôme dans `Auteur`, la date, et le nom de votre compilateur dans
   `Compilateur` (par exemple `MinGW GCC 13` ou `Apple clang 17`).
2. Remplacez `Bonjour PRG` par un titre de votre choix, par exemple
   `Labo 1 - Prenom et Prenom se presentent`.
3. Lancez le programme pour vérifier, puis commitez et poussez :
   **Git > Commit**, message `Compléter l'en-tête et le titre`, puis
   **Git > Push** (ou `git add`, `git commit`, `git push` dans le terminal).

**B** ensuite : **Git > Pull** (ou `git pull`). B reçoit le fichier
modifié par A. Vérifiez sur GitHub que le commit de A est dans
l'historique.

### Étape 3 : une branche, une pull request, un conflit (30 min)

Chacun ajoute sa propre présentation dans `main.cpp`, en suivant pas à pas
[Une branche par personne ou par fonctionnalité](https://heigvd-prg-b-26.github.io/guides/git.html#une-branche-par-personne-ou-par-fonctionnalité)
du guide Git.

1. Créez votre branche `presentation-<prenom>`.
2. Juste sous la ligne `// --- Présentations ---`, ajoutez votre
   présentation, un `cout` par ligne, avec au minimum :
   - votre nom et prénom,
   - votre expérience en programmation (jamais programmé, un peu, un langage
     que vous connaissez, ...),
   - vos loisirs,
   - à votre avis, à quoi sert la programmation : quels types de programmes,
     pour quels buts.

   Lancez le programme : l'affichage doit être lisible, une information par
   ligne. Vous pouvez décorer l'affichage. Évitez les accents dans les
   messages : la console les affiche souvent mal.
3. Commitez et poussez la branche, puis ouvrez la **pull request** sur
   GitHub. Écrivez une description en trois lignes (quoi, pourquoi, à
   vérifier) et choisissez votre binôme comme *reviewer*.
4. Le binôme relit dans **Files changed**, écrit au moins un commentaire
   (une question, une remarque, un compliment), puis **Approve**.
5. La **première** pull request fusionne sans problème : **Squash and
   merge**, puis **Delete branch**.
6. La **deuxième** ne peut pas fusionner : GitHub affiche
   *This branch has conflicts that must be resolved*. C'est normal, vous
   avez tous les deux écrit sous la même ligne. Celui dont la pull request
   est bloquée résout le conflit sur son ordinateur :

   ```sh
   git checkout main
   git pull                          # récupère la présentation déjà fusionnée
   git checkout presentation-<prenom>
   git merge main                    # s'arrête sur le conflit dans main.cpp
   ```

   Résolvez avec l'outil de CLion (fenêtre *Conflicts*, bouton **Merge**)
   ou en éditant les marqueurs, voir
   [Conflits](https://heigvd-prg-b-26.github.io/guides/git.html#conflits).
   Résultat attendu : **les deux présentations**, l'une après l'autre.
   Lancez le programme pour vérifier, puis terminez la fusion :

   ```sh
   git add main.cpp
   git commit                        # termine la fusion
   git push
   ```

   La pull request peut maintenant être fusionnée : **Squash and merge**,
   **Delete branch**.
7. Tous les deux : `git checkout main` puis `git pull`. Vous avez le même
   `main.cpp` avec les deux présentations. Regardez l'historique sur GitHub :
   chaque pull request est devenue **un seul commit** dans `main`, et le
   commit de fusion de l'étape 6 a disparu. C'est l'effet du *squash*.

### Étape 4 : le push refusé (10 min)

Tous les deux sur `main`, en même temps, sans vous mettre d'accord :

- **A** ajoute une ligne dans `Remarque` de l'en-tête (par exemple
  `Labo fait en binome`).
- **B** ajoute, juste avant `return EXIT_SUCCESS;`, un
  `cout << "Fin du labo 1" << endl;`.

Chacun commit, puis pousse. Le deuxième push est **refusé**. Suivez
[Tout le monde sur main, et le push refusé](https://heigvd-prg-b-26.github.io/guides/git.html#tout-le-monde-sur-main-et-le-push-refusé) :
configuration de `pull.rebase`, `git pull`, `git push`. Vous avez modifié
des lignes différentes, donc pas de conflit cette fois. L'autre membre fait
ensuite `git pull`.

### Étape 5 : vérification (5 min)

Sur GitHub, le dépôt doit montrer :

- [ ] `main.cpp` avec l'en-tête complété et les deux présentations ;
- [ ] dans l'historique de `main` : le commit de A (étape 2), un commit
      par pull request (étape 3), les deux commits de l'étape 4 ;
- [ ] deux pull requests fermées, avec au moins un commentaire de relecture
      chacune ;
- [ ] aucune autre branche que `main`.

---

## Partie 2 : exercices et premiers tests

Dans cette partie, chaque exercice est un fichier `exercices/<nom>.cpp` et
un exécutable du même nom. Travaillez sur `main`, chacun sur ses fichiers,
avec un `git pull` avant chaque `git push`. **Un exercice terminé = un
commit**, avec un message qui nomme l'exercice.

### Étape 6 : un exécutable par exercice (10 min)

Remplacez le contenu de `CMakeLists.txt` par celui-ci. Il crée
automatiquement une cible pour chaque fichier `exercices/*.cpp` et garde la
cible `presentation` :

```cmake
cmake_minimum_required(VERSION 3.28)
project(labo01 CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Avertissements du cours : on les lit, on les corrige.
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -Wpedantic -Wconversion)
endif()

add_executable(presentation main.cpp)

# Un exécutable par fichier exercices/*.cpp : ajouter un fichier suffit,
# CLion propose la cible correspondante dans la liste de lancement.
file(GLOB EXERCICES CONFIGURE_DEPENDS exercices/*.cpp)
foreach(src ${EXERCICES})
    get_filename_component(name ${src} NAME_WE)
    add_executable(${name} ${src})
endforeach()
```

Rechargez le projet CMake (bandeau *Reload CMake project*), puis commitez
et poussez : `Passer à un exécutable par exercice`.

### Étape 7 : erreurs de compilation et d'exécution (30 min)

Exercices du
[chapitre 1 du recueil](https://github.com/HEIGVD-PRG1/PRG1_Recueil_Exercices/tree/main/01%20-%20Introduction%20Git%20IA%20IDE%20debug),
un fichier par exercice. Chaque fichier commence par
l'[en-tête de fichier du cours](https://heigvd-prg-b-26.github.io/ressources/index.html#en-tête-de-fichier).

| Exercice du recueil | Fichier | À rendre |
|---|---|---|
| 03 - erreur de compilation | `exercices/ch01_ex03.cpp` | le programme corrigé, qui compile **sans avertissement** |
| 04 - segmentation fault | `exercices/ch01_ex04.cpp` | le programme tel quel, plus un commentaire en tête : le message obtenu et une phrase sur sa cause |
| 05 - uncaught exception | `exercices/ch01_ex05.cpp` | le programme tel quel, plus un commentaire en tête : la valeur de `i` au moment du plantage, trouvée **avec le débogueur** |

Faites l'exercice 03 à deux, puis partagez-vous 04 et 05. Regardez la
solution du recueil seulement après avoir commité la vôtre.

### Étape 8 : prédire, puis vérifier avec des assertions (40 min)

Lisez [Assertions et premiers tests](https://heigvd-prg-b-26.github.io/guides/assertions.html).
Une assertion vérifie qu'une condition est vraie, et arrête le programme
si elle est fausse. Vous allez l'utiliser pour **tester vos prédictions**
sur les expressions du chapitre 2.

Créez `exercices/ch02_expressions.cpp`. Pour chaque expression des
exercices
[11 - division entière et réelle](https://github.com/HEIGVD-PRG1/PRG1_Recueil_Exercices/tree/main/02%20-%20Types%20references%20arithmetique),
12 - modulo et 14 - priorité des opérateurs du recueil :

1. **Avant** de lancer le programme, écrivez votre prédiction sous forme
   d'assertion :

   ```cpp
   assert(7 / 2 == 3);            // division entière : je prédis 3
   assert(7 % 2 == 1);
   assert(7.0 / 2 == 3.5);
   ```

2. Lancez le programme en **Debug**. Si une assertion échoue, votre
   prédiction était fausse : cherchez pourquoi (cours, chapitre 2), puis
   corrigez la **prédiction**, jamais l'expression. Notez en commentaire
   ce qui vous a surpris.
3. Le programme se termine par `cout << "Toutes les predictions sont justes"`.

Minimum : **quinze assertions**, réparties sur les trois exercices, dont
au moins trois qui vous ont surpris au premier essai (le commentaire le
dit). Un commit par exercice du recueil.

Si vous avez le temps : même méthode avec
16 - Evaluation d'expressions (2) dans `exercices/ch02_ex16.cpp`.

---

## Avant de rendre

- [ ] `git status` ne montre rien et `git pull` ne ramène rien : vous
      êtes à jour tous les deux.
- [ ] Le dépôt sur GitHub contient `main.cpp`, le `CMakeLists.txt` de
      l'étape 6 et les fichiers `exercices/ch01_ex03.cpp`, `ch01_ex04.cpp`,
      `ch01_ex05.cpp` et `ch02_expressions.cpp`, chacun avec l'en-tête du
      cours.
- [ ] Tout compile sans avertissement et chaque exécutable se lance.
- [ ] Aucun dossier `cmake-build-*` ni `.idea` dans le dépôt (ils sont dans
      le `.gitignore`).
