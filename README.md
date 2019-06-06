Afin de reproduire le fonctionnement de vecteurs de C++ avec des
templates, tout va se jouer dans un grand "#define" que nous
appellerons dans le code afin d'obtenir le type que l'on souhaite.

Ce define nous allons l’appeler par convention :
#define define_vector(type)



Ce qui est important de noter c'est ce type qui agiras comme une
variable que l'ont donne en paramètre a une fonction.

Maintenant afin de reproduire le fonctionnement basique d'un
vecteur, il va falloir faire une structure.

```C
#define define_vector(type)\
    typedef struct vector_##type {\
        type *items;\
        int size;\
        int capacity;\
    } vector_##type;\
 ```

Pensez toujours a mettre un '\' a la fin de vos lignes, cela
permet de conserver le 1er #define en une seule ligne.



Notre structure étant prête, nous pouvons maintenant penser
à créer notre vecteur.
Pour ce faire, rien de plus simple, une bête fonction
"new_vector".
Afin d'éviter les erreurs lors de la compilation, on va déclarer
le prototype de la fonction juste au dessus de celle-ci.

```C
vector(type) *new_vector_##type(int capacity);\
\
vector(type) *new_vector_##type(int capacity)\
{\
    vector_##type *v;\
    v->items;\
    v->size;\
    v->capacity;\
    return (v);\
}\
```

(je vous laisse le loisir d’assigner correctement les variables)
Note : Cette fonction devras toujours être la dernière dans le
define car c'est ici que l'on assigneras les fptr de la structure.



Maintenant essayez de réaliser une 1ère fonction de base pour
votre vector, la fonction "push_back" afin d'obtenir la structure
suivante.
(Si vous n'en connaissez pas le fonctionnement, allez regarder
sur "C++ reference vector")

```C
typedef struct vector_##type {\
    type *items;\
    int size;\
    int capacity;\
    void (*push_back)(struct vector_##type *, type);\
} vector_##type;\
```


Si vous souhaitez tester votre code, il faut d'abord créer le
template en appellant le define en haut de votre fichier .c
comme les .h

```C
define_vector(int);
```

et ensuite le créer la où vous le souhaitez

```C
vector_int *v_int = new_vector_int(1);
```

Important : Le code étnt fait dans un ".h", les erreurs et bugs
sont très difficile a tracker et valgrind n'auras aucun effet.
Je vous recommande donc d'abord de coder dans un .c avant de les
intégrer au ".h".


Maintenant amusez vous à reproduire le plus fidèlement les
fonctions déjà existante sur es vectors de C++
