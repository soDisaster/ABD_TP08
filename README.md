ABD - TP 08
===========

Auteurs
-------

- Anne-Sophie Saint-Omer
- Thomas Bernard

Exercice 1
----------

#### 1. Toutes les modifications sont propagées à la base de données avant l'écriture de Commit sur le fichier log (et donc, avant le commit).

__Faux__. Principe de Write-Ahead Logging, c'est à dire que les modifications doivent être d'abord ajoutées au fichier de log, avant d'être réellement effectuées sur la base de données.

#### 2. Toutes les modifications sont propagées à la base de données après l'écriture de Commit sur le fichier log (et donc, après le commit).

__Vrai__. Principe de Write-Ahead Logging, c'est à dire que les modifications doivent être d'abord ajoutées au fichier de log, avant d'être réellement effectuées sur la base de données.

#### 3. Toutes les modifications peuvent être propagées à la base de données soit avant soit après l'écriture de Commit sur le fichier log (et donc, soit avant soit après le commit).


#### 4. Les modifications de données sont propagées à la base de données avant de stocker de façon permanente le valeur précèdent des données dans le fichier log.


#### 5. Les modifications de données sont propagées à la base de données après le stockage permanent du valeur précèdent des données dans le fichier log.


#### 6. Les modifications de données sont propagées à la base de données soit avant soit après le stockage permanent du valeur précèdent des données dans le fichier log.

Exercice 2
----------

Algorithme undo-redo pour la gestion des  échecs de transactions, dans le cas de :

1. Ecriture

2. Commit

3. Abort

4. Restart

Exercice 3
----------

Fichier log de transactions gérées par la technique de undo-redo.  
Les enregistrements du fichier log ont le format (W, Tid, Variable, Old, New).  

```
1.  (BEGIN T1)
2.  (W, T1, A, 25, 50)
3.  (W, T1, B, 25, 250)
4.  (BEGIN T2)
5.  (W, T1, A, 50, 75)
6.  (W, T2, C, 25, 55)
7.  (COMMIT T1)
8.  (BEGIN T3)
9.  (W, T3, E, 25, 65)
10. (W, T2, D, 25, 35)
11. (CKP T2,T3)
12. (W, T2, C, 55, 45)
13. (COMMIT T2)
14. (BEGIN T4)
15. (W, T4, F, 25, 120)
16. (COMMIT T3)
17. (W, T4, F, 120, 150)
18. (COMMIT T4)
```

1. Restart à cause d'un malfonctionnement avant d'écrire l'enregistrement 10 dans le disque.

```
9.  (W, T3, E, 25, 65)
======== CRASH ========
10. (W, T2, D, 25, 35)
```

Variable A :
Variable B :
Variable C :
Variable D :
Variable E :
Variable F :

2. Restart à cause d'un malfonctionnement avant d'écrire l'enregistrement 13 dans le disque.

```
12. (W, T2, C, 55, 45)
======== CRASH ========
13. (COMMIT T2)
```

Variable A :
Variable B :
Variable C :
Variable D :
Variable E :
Variable F :

3. Restart à cause d'un malfonctionnement avant d'écrire l'enregistrement 14 dans le disque.

```
13. (COMMIT T2)
======== CRASH ========
14. (BEGIN T4)
```

Variable A :
Variable B :
Variable C :
Variable D :
Variable E :
Variable F :

4. Restart à cause d'un malfonctionnement avant d'écrire l'enregistrement 18 dans le disque.

```
17. (W, T4, F, 120, 150)
======== CRASH ========
18. (COMMIT T4)
```

Variable A :
Variable B :
Variable C :
Variable D :
Variable E :
Variable F :

5. Restart à cause d'un malfonctionnement après avoir écrit l'enregistrement 18 dans le disque.

```
18. (COMMIT T4)
======== CRASH ========
```

Variable A :
Variable B :
Variable C :
Variable D :
Variable E :
Variable F :

Exercice 4
----------
