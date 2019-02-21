---
title: Les classes en Python / Arbres
---

## Les classes

Python est un langage orienté-objet. Dans ce type de langage, absolument tout est objet : une chaîne de caractères, un entier, une liste, un dictionnaire, ou encore une fonction. Un **objet** est une entité qu'on crée par *instantiation* à partir d'une classe. Une **classe** est un type permettant de regrouper dans la même structure les *informations* (champs, propriétés, attributs) relatives à une entité ainsi que les *fonctions*, qu'on appelle **méthodes** permettant de les manipuler. Les champs et les méthodes constituent les *membres* de la classe.

La création d'un objet se fait en deux étapes. On décrit d'abord à quoi ressemble notre objet et on demande ensuite à l’ordinateur d’utiliser cette description pour le fabriquer. Créons une classe `Etudiant`.

~~~python
class Etudiant:
    def __init__(self, nom, prenom, numero_etudiant, age):
        self.nom = nom
        self.prenom = prenom
        self.numero_etudiant = numero_etudiant
        self.age = age
~~~

La classe `Etudiant` modélise l'entité *étudiant* et décrit ses caractéristiques principales à travers ses *champs*.

* Le mot `class` est un mot-clé utilisé lorsqu'on définit une nouvelle classe.
* `Etudiant` est le nom de la classe. Par convention, le nom de la classe commence par une lettre majuscule et ne comporte pas d'espaces. On écrit par exemple : `NomDeLaClasse`.
* `__init__` est une méthode spéciale, appelée **constructeur**, qui permet de construire et personnaliser des objets. Le constructeur, lorsqu'il est appelé, crée et renvoie un objet du type voulu et contenant ce qui est passé en paramètre. Contrairement à d'autres langages orientés-objet, le constructeur en Python porte toujours le même nom.
* Le mot `self` (soi) fait référence à une instance de la classe (celle que nous sommes en train de créer ou de manipuler). C'est l'équivalent de `this` en Java ou d'autres langages.
* Notre classe `Etudiant` comporte quatre attributs ou champs. À la création d'un nouvel objet, on initialise ses champs  à l'aide des valeurs qu'on passe comme arguments au constructeur.

Créons maintenant un objet `Etudiant`.

~~~python
unEtudiant = Etudiant("Dupont", "Marcel", 2110012, 23)
~~~

Nous allons maintenant voir comment définir les *méthodes d'instance* d'une classe. Ce sont des méthodes (fonctions) qui s'appliquent directement aux objets, instances de la classe. Vous avez déjà utilisé des méthodes d'instance plusieurs fois sans vous en rendre probablement compte. Par exemple, lorsque vous écrivez

~~~python
>>> liste = list([1, 2, 3])
>>> liste.append(4)
>>> liste
[1, 2, 3, 4]
~~~

vous appelez la *méthode* `append()` de la classe `list` sur l'objet `liste` qui est une instantiation de la classe `list`. D'ailleurs, en écrivant `liste = list([1, 2, 3])` vous êtes en train d'appeler un constructeur de la classe `list`.

Voici alors quelques méthodes que nous pouvons définir dans notre classe `Etudiant`.

~~~python
class Etudiant:
    def __init__(self, nom, prenom, numero_etudiant, age):
        self.nom = nom
        self.prenom = prenom
        self.numero_etudiant = numero_etudiant
        self.age = age

    def getNom(self):
        return self.nom

    def getPrenom(self):
        return self.prenom

    def estPlusAgeQue(self, age):
        if self.age > age:
            return True
        else:
            return False
~~~

* Toutes les méthodes d'instance prennent `self` comme premier argument. L'utilisation d'une méthode d'instance est très simple. Il suffit d'écrire le nom de l'objet, suivi par un '`.`' et suivi ensuite par le nom de la méthode.

~~~python
>>> unEtudiant.getNom()
Dupont
>>> unEtudiant.getPrenom()
Marcel
>>> unEtudiant.estPlusAgeQue(30)
False
~~~

## Une classe Ville

Téléchargez dans votre serveur Jupyter le fichier [villes.txt](villes.txt). Ce fichier contient la liste des 200 plus grandes villes de France dans un ordre aléatoire. Chaque ligne de ce fichier contient les 5 informations suivantes :

* Nom de la ville
* Numéro du département
* Nombre d'habitants
* Superficie (en km²)
* Rang au niveau national (critère : nombre d'habitants)

Voici à quoi ressemblent les deux premières lignes de ce fichier :

~~~
Saint-Priest 69 40944 29.7 155
Versailles 78 85761 26.2 46
~~~

**:**{:.exercise} 

Créez une classe `Ville` ayant 5 champs : chacun de ces champs doit correspondre aux 5 informations concernant une ville comme décrit ci-dessus (nom, numéro de département, population, superficie, rang). Le constructeur prendra en paramètre une liste `liste`, et initialisera les 5 champs avec les 5 premières cases de la liste (`liste[0], liste[1]`) etc.

Ajoutez ensuite les 3 méthodes suivantes à votre classe :

* Une méthode `getRang(self)` qui renvoie la valeur du champ *rang*,

* Une méthode `getSuperficie(self)` qui renvoie la valeur du champ *superficie*,

* Une méthode `afficherNom(self)` qui affiche la valeur du champ *nom*, en utilisant la commande `print`,

* Une méthode `afficherVille(self)` qui affiche les valeurs des quatre premiers champs, en utilisant la commande `print`.

Testez votre classe en tapant :

~~~python

>>> liste = ["Maisons-Alfort", 94, 51091, 5.4, 100]
>>> ville = Ville(liste)
>>> ville.getRang()
100
>>> ville.getSuperficie()
5.4
>>> ville.afficherVille()
Maisons-Alfort 94 51091 5.4
~~~

Vous devez maintenant parcourir le fichier et créer un nouvel objet ville à partir des informations contenues dans chaque ligne du fichier. Pour cela, il vous suffit de copier-coller le code ci-dessous :

~~~python
with open("villes.txt", "r") as fichier:
	for ligne in fichier:
		liste = ligne.rsplit(" ")
		ville = Ville(liste)
~~~

La première ligne indique que nous allons ouvrir le fichier `villes.txt` en mode *lecture* (d'où, le `"r"`, faisant référence à *read*). Nous pouvons ensuite parcourir le fichier ligne par ligne. La variable `ligne` contient à chaque itération la ligne que nous sommes en train de lire, vue comme une chaîne de caractères. 

La méthode `rsplit` de la classe `String` nous permet de *couper* une chaîne de caractères en mots. Cette méthode retourne une liste contenant les mots de la ligne. Dans notre cas, la taille de la liste créé est 5 pour chaque ligne. Vérifiez-le.

## Construire un arbre binaire de recherche

Notre but maintenant est d'insérer toutes ces villes dans un arbre binaire de recherche. Les noeuds de l'arbre seront les objets de la classe `Ville`. Dans un premier temps, la valeur qui nous permettra de créer un *ordre*, sera l'attribue rang. Ceci veut dire qu'on va comparer les villes selon leur rang. Par exemple on va dire que `Meulon < Paris`.

Commencez par créer une classe `Noeud` ayant le constructeur suivant :

~~~python
class Noeud:
   def __init__(self,liste):
       self.gauche = None
       self.droite = None
       self.ville = Ville(liste)
~~~

Cette classe a donc trois attributs (comme attendu pour un ABR) : un fils gauche, un fils droite, et une *valeur* pouvant être comparée (ou ayant des champs pouvant être comparés), qui est ici un objet de type `Ville`.

**:**{:.exercise} 

Dotez votre classe `Noeud` d'une méthode `inserer(self, liste)` qui prendra comme argument une liste (de longueur 5 dans notre cas) et insérera l'objet `Ville` construit à partir de cette liste, dans l'arbre. Vous pouvez utiliser l'algorithme d'insertion vu en cours.

**:**{:.exercise} 

Écrivez une méthode  `afficherArbre(self)` qui affichera les noms des villes sauvegardées dans l'arbre en suivant un **parcours infixe**.

Testez votre code :

~~~python
liste = ["Maisons-Alfort", 94, 51091, 5.4, 100]
noeud = Noeud(liste)
with open("villes.txt", "r") as fichier:
	for ligne in fichier:
		liste = ligne.rsplit(" ")
		noeud.inserer(liste)

noeud.afficherArbre()
~~~

Vous devez obtenir l'affichage suivant :

~~~
Paris
Marseille
Lyon
Toulouse
Nice
Nantes
Strasbourg
Montpellier
Bordeaux
...
~~~

**:**{:.exercise} 

Modifiez la méthode `afficherArbre(self)`afin qu'elle affiche le nom, le numéro de département et la population de chaque ville.


~~~
Paris 75 2125851 105.4
Marseille 13 797491 240.6
Lyon 69 445274 47.9
Toulouse 31 390301 118.3
Nice 6 343123 71.9
Nantes 44 270343 65.2
Strasbourg 67 263941 78.3
Montpellier 34 225511 56.9
Bordeaux 33 215374 49.4
...
~~~

**:**{:.exercise} 

Nous avons maintenant besoin d'une méthode qui permet de rechercher une ville dans l'arbre à partir de son rang. Écrivez une méthode `rechercher(self, rang)` qui prend en entrée un entier correspondant au rang de la ville recherchée et qui renvoie l'objet contentant la ville (noeud) en question correspondant. Si l'objet n'est pas trouvé, la méthode doit renvoyer `None`.

Testez votre code :

~~~python
unNoeud = noeud.rechercher(130)
if unNoeud is not None:
   unNoeud.ville.afficherNom()
else:
   print("Non trouvé")
~~~

~~~
Saint-Brieuc
~~~

**:**{:.exercise} 

Écrivez une méthode `compterEnfants(self)` qui compte le nombre d'enfants (0, 1 ou 2) d'un noeud de l'arbre.

Testez votre code :

~~~python
>>> unNoeud = noeud.rechercher(130)
>>> unNoeud.compterEnfants()
1
>>> unNoeud = noeud.rechercher(100)
>>> unNoeud.compterEnfants()
2
>>> unNoeud = noeud.rechercher(200)
>>> unNoeud.compterEnfants()
0
~~~

**:**{:.exercise} 

Modifiez la construction de votre arbre, afin que la comparaison se fasse maintenant à partir de la superficie d'une ville.

**:**{:.exercise} 

En utilisant cette nouvelle construction, écrivez une méthode `rechercheMax(self)` qui renvoie la ville ayant la plus grande superficie.
