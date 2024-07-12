
# PROPOSITION BUGSZERO KATA MARWEN MAALEL 

## 1. Class GameRunner
    On peu changer la façon comment ajouter de joueurs et surtout utiliser la méthode isPlayable : 
    
    
    Game aGame = new Game("P1", "P2");
    Game aGame = new Game("P1", "P2", "P3");
    // ....
    Game aGame = new Game("P1", "P2", "P3", "P4", "P5", "P6");
    
    Pour gérer le nombre des joueurs.
    Un exemple de constructeur à 3 joueurs qui utilise le constructeur à 2 joueurs :

    public Game(String joueur1, String joueur2, String joueur3) {
        this(joueur1, joueur2);
        this.add(joueur3);
    }

    Il faut aussi rendre la méthode add privée, puisque c'est nos constructeurs qui se chargent de l'ajout de joueurs.
    Je propose d'utiliser cette méthode avant de "roll" pour pouvoir arrêter le jeu si le nombre de joueurs minimum n'est pas le bon.


## 2. Class Game : 
### 2.1. La méthode wronganswer() : 
    La méthode wronganswer(), retourne toujours un true.
    Il faut se baser sur un traitement, pour retourner un false ou un true.

### 2.2. La méthode didPlayerWin() :
    La méthode didPlayerWin(), elle doit nous retourner si le joueur à 6 pièces dans son sac,
    Dans ce cas : return !(purses[currentPlayer] == 6, si le joueur à 6 pièces elle va nous retourner false, alors la condition est inversée.

### 2.3. Nombre maximum de joueurs :
    On a dit que le nombre maximum des joueurs est 8 (exemple, ou 6), 
    Dans les deux cas, la méthode "howManyPlayers()" retourne la taille de l'ArrayList contenant les joueurs, dans notre cas places, alors quand on ajouter le 6ème joueur cette même méthode renvoie 6, 
    mais places[6] n'existe pas (index de 0 à 5), alors -> IndexOutOfBoundException.

    Je propose également d'inclure une condition dans la méthode "isPlayable" pour vérifier le nombre maximum de joueurs avant de lancer le jeu.
    Il faut également revoir toutes les parties du code où "howManyPlayers()" est utilisé comme indice d'un tableau.

### 2.4. Couplage propriétés :
    Je propose d'encapsuler dans un objet Player, les listes : places, purse et inPenaltyBox.
    Parce qu'on peut, ne pas faire attention est oublier la modification d'une de ces propriétés dans une des méthodes qui les utilise, ce qui va générer un bug.

### 2.5. Redondance dans currentCategory
    La méthode currentCategory répète le même code plusieurs fois. 
    Il serait préférable d'utiliser des structures de données plus efficaces comme une liste ou un tableau associatif pour éviter les répétitions.

### 2.6. La méthode currentCategory() :
    La méthode currentCategory() est appelé plusieurs fois pour la même vérification. 
    Il serait plus efficace de stocker le résultat dans une variable et de l'utiliser.

### 9. Absence de vérification des limites pour les listes de questions
    Les listes de questions peuvent être vides après plusieurs tours, ce qui entraînera une exception lorsque removeFirst() sera appelé sur une liste vide.


### 2.5. Autres : 
    a- Formatter le code sur les deux classes Game et GameRunner, avec CTRL + ALT + L.
    b- La méthode "isPlayable" n'est pas utiliser.
    c- Les trois premières catégories de questions sont ajoutées directement, avec addLast, alors que pour la dernière on utilise la méthode "createRockQuestion", faut faire pareil pour toutes les lignes. 
       En plus, la gestion des questions peut également être améliorée, on peu créer un Objet Question qui contient toutes les questions, avec le titre et le type de la question,
    e- L'utilisation de plusieurs if dans les méthodes "askQuestion" et "currentCategory", va être alerter par Sonar, en plus pas très lisible, alors je propose d'utiliser un switch au lieu du if.
    f- La comparaison des String se fait avec un equals et non == comme ici : currentCategory() == "Pop"
