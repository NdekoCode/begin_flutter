# Apprendre Flutter en 2 minutes

## Afficher du text

La premiere chose que l'on apprend dans un language c'est comment afficher `Hello World` et pour faire cela avec flutter on utilise le Widget `Text()` et pour y mettre du texte vous n'avez qu'à le lui passer en parametre car le constructeur de ce Widget prend en premier parametre le texte à afficher, par exemple: `Text("Hello World")` et si vous voulez afficher une variable vous faite par exemple `Text("Hello World: $LeNomDeLaVariableAafficher")`.
Ce widget prend les parametres suivant dont à partir du deuxieme sont optionnel

- text: Qui est le texte à afficher
- style: Pour mettre des styles sur les textes, ce meme parametre prend un Widget en parametre qui est `TextStyle()` et ce Widget Prend aussi plusieurs parametre comme
                - fontFamily : La police à utiliser sur le texte, prealablement chargement dans le fichier `pubspec.yaml`
                - color: La couleur du texte,
                - fontSize: La taille du texte,
                - fontWeight: La graisseur du texte,
                - decoration: pour la decoration du texte, soit en underline, overline, outline,...
                - letterSpacing: Pour les espaces entre les lettres,
                - wordSpacing: Pour les espaces entre les mots,
                - shadows: Qui est un tableau contenant les ombres à utiliser sur le texte mais generalement ce tableau contient un Widget qui `Shadow()` qui prend different parametre comme `color` la couleur de l'ombre, `offset` prend les dispositions de l'ombre par `x` et `y` ie `offet: Offet(x,y)`, le `blurRadius` qui gère le flou sur l'ombre du texte
- textAlign: Pour disposer le texte soit à gauche,à droite, au centre ou en bas

Par exemple:

```{DART}


    var nbrVues = 315;
    var date = DateTime.now();
    ...
    child: Text("Hello World: $nbrVues à ${date.hour}H",
        style: TextStyle(
            fontFamily: 'SF UI Display',
            decoration: TextDecoration.underline,
            decorationColor: Colors.blue,
            fontWeight: FontWeight.bold,
            fontSize: 25,
            color: Colors.red,
            letterSpacing: 3,
            wordSpacing: 15,
            shadows: [
                Shadow(
                    color: Colors.redAccent,
                    offset: Offset(5.0, 5.0),
                    blurRadius: 10.0)
            ]),
        textAlign: TextAlign.center)

```

![Faire un hello World avec flutter](./assets/images/Learn-%20HelloWorld%20in%20flutter.PNG)

## Le Widget de type Bouton càd Les boutons

 Flutter a déjà créer plusieurs type de boutons pour nous faciliter la vie et dans ces types on a:

### FlatButton

Qui est utiliser par exemple dans les popUp ou card, etant donnée qu'il a été deprecier il est recommandé d'utiliser le `TextButton`

exemple:

```{DART}
// Le remplacant de FlatButton
TextButton(
    child: Text("Ok"),
    onPressed: () {
    print("Vous avez cliquer sur OKAY");
    })
```

![Le bouton TextButton ressemblant à du texte simple](./assets/images/Learn-%20TextButton.PNG)

### RaisedButton(ElevedButton) et OutlineButton(OutlinedButton)

Sont exactement comme le `TextButton` ou le `FlatButton`(Deprecier) mais le `RaisedButton` permet d'avoir un impacte visuel très important en mettant un background grise sur son bouton mais il a été aussi déprécier et il est recommander d'utiliser le `ElevatedButton` quand au `OutlineButton` il a une bordure grise mais pas de background grise mais il permet aussi d'avoir un impact visuel important, lui aussi il est deprecier et il est recommander l'Utiliser `OutlinedButton`

exemple:

```{DART}
// Le remplacant de RaisedButton
ElevatedButton(
    child: Text("Raised"),
    onPressed: () {
    print("Vous avez cliquer sur Raised");
    })


    // Le remplacant de OutlineButton
OutlinedButton(
    child: Text("Outline"),
    onPressed: () {
    print("Vous avez cliquer sur Outline");
    })

```

Le bouton ElevatedButton ressemblant à un bouton à fond du theme ![Le bouton ElevatedButton ressemblant à un bouton à fond du theme](./assets/images/Learn%20-%20ElevatedButton.PNG)

Le bouton OutlinedButton ressemblant à un bouton à fond du theme ![Le bouton OutlinedButton ressemblant à un bouton à fond du theme](./assets/images/Learn-%20OutlineButton.PNG)

### ButtonBar

Il est utile si vous souhaiter aligner Horizontalement deux element de type Button à droite
comme par exemple dans une `PopUp` de confirmation avec un `Ok` et un `cancel`
il prend en parametre un `children` qui va contenir une liste de `Widget` et type `Button` que vous souhaiter `afficher`
par exemple:

```{DART}
return Scaffold(
        body: Center(
            child: Container(
                child: ButtonBar(
                    alignment: MainAxisAlignment.center,
                    children: <Widget>[
          OutlinedButton(
              child: Text("Ok"),
              onPressed: () {
                print("Vous avez cliquer sur OKAY");
              }),
          ElevatedButton(
              child: Text("Cancel"),
              onPressed: () {
                print("Vous avez appuyer sur `Annuler`");
              })
        ]))));

```

![ButtonBar](./assets/images/Learn-%20Button%20Bar.PNG)

### PopupMenuButton

Ce widget porte bien son nom, c'est une icon à 3 points vertical qui affiche un menu, il peut etre utiliser dans une `AppBar` par exemple pour etre rediriger vers d'autres ecrans.
il prend comme parametre:

- itemBuilder: Qui va etre une fonction qui retourne une liste(Tableau) contenant par indice un `PopupMenuItem` et ce `PopupMenuItem` contient deux parametre principale qui sont `child` et `value`, `value` est un entier qui est considerer un peu comme en quelques sorte l'ordre avec lequel on va afficher le menu dans le `Popup`
par exemple:

```{DART}
return Scaffold(
    body: Center(
        child: Container(
            child: PopupMenuButton(
                itemBuilder: (ctx) => [
                        PopupMenuItem(value: 1, child: Text("Setting")),
                        PopupMenuItem(value: 2, child: Text("Profile"))
                    ]))));
```

![PopupMenuButton](./assets/images/Learn-%20PopupMenuButton%20-1.PNG)
![PopupMenuButton](./assets/images/Learn-%20PopupMenuButton%20-2.PNG)

### IconButton

Si vous souhaiter avoir une icon Clickable, c'est très simple il suffit d'utiliser les Widget `IconButton` il prend les parametres suivant, `icon` qui est l'Icon que l'on souhaite utiliser souvant on les tires dans le Widget `Icons.IconAUtiliser` et le parametre onPressed qui est l'action qui survient lors de l'Appui sur ce boutton

![PopupMenuButton](./assets/images/Learn-%20IconButton.PNG)

### DropdownButton

Pour ce bouton vous devez etre dans un `StatefulWidget` car en dehors d'un `StatefulWidget` il genera une erreur.
Le `DropdownButton` peut etre très utile pour afficher une liste avec un seul element à selectionner comme par exemple le choix d'une option.
Ce widget prend plusieurs parametres qui sont:

- `value`: qui est la valeur de depart du `DropdownButton` et cette valeur correspond à la valeur d'un de ces items.
- `items`:Qui correspond à une liste de Widget `DropdownMenuItem` qui est la liste des items disponible dans le button `DropdownButton` ce Widget aussi prend deux parametre necessaire qui sont `child` contenant la description de cet item et `value` la valeur correspondante à l'item, cette valeur est utiliser pour selectionner un `item` dans `DropdownButton`
- onChanged: Qui est une action qui est executer quand on change d'item dans le Widget `DropdownButton`

Pour utiliser ce `DropdownButton` vous aurez besoin d'un `setState()` pour permettre à votre application de `rebuild` avec les nouvelles données du `Widget` et ici c'est le Widget `DropdownMenuItem`  qui a une value correspondant à celle du Widget Parent, ce parametre contiendra une fonction qui prendra en parametre la nouvelle valeur de l'item selectionner qui sera transferer de maniere implicite.
Par exemple on a:

```{DART}
return Scaffold(
        body: Center(
            child: Container(
                child: DropdownButton(
                    value: _value,
                    items: [
                      DropdownMenuItem(value: 1, child: Text("Select 1")),
                      DropdownMenuItem(value: 2, child: Text("Select 2"))
                    ],
                    onChanged: (int? value) {
                      setState(() {
                        _value = value!;
                        print(value);
                      });
                    }))));
```

PopupMenuButton ![PopupMenuButton](./assets/images/Learn-%20DropdownButton%20-1.PNG)

PopupMenuButton ![PopupMenuButton](./assets/images/Learn-%20DropdownButton%20-2.PNG)

### FloatinActionButton

Qui est generalement utiliser comme action principale de la page, ou action principale de l'application
pour envoyer un message ou ajouter un colis par exemple
il prend le parametre `child` qui va contenir un peu le contenu de ce bouton en generale c'est une icon et `onPressed` qui est l'action qui suit l'appuis sur ce bouton
par exemple:

```{DART}
return Scaffold(
        body: Center(
            child: Container(
                child: FloatingActionButton(
                    child: Icon(Icons.add),
                    onPressed: () {
                      print("Vous avez ajouter un element");
                    }))))
```

![PopupMenuButton](./assets/images/Learn-%20FloatingActionButton.PNG)

### Recaputulatif

 On peut styliser un button en lui ajoutant le parametre `style` et le widget `ButtonStyle`

 ```{DART}
    style: ButtonStyle(
                        backgroundColor: MaterialStateProperty.all(Colors.red))
 ```

![PopupMenuButton](./assets/images/Learn-%20All%20button%20Widget.PNG)

## Row et Column

Permet d'afficher plusieurs elements aligner selon les ligne et les colonnes
Au sein d'une `Row` et `Column` nous avons la possibilité d'aligner sur l'axe des X avec mainAxisAlignment et sur l'axe des Y avec crossAxisAlignement
![Alignement vertical et Horizontal des Widget](./assets/images/Learn-%20Alignement%20Horizontale%20et%20vertical%20des%20widget.PNG)

### Row

Permet d'aligner horizontalement

### Column

Permet d'aligner verticalement
Il prend en parametre `children` qui est une liste des Widget à utiliser dans la Ligne et aussi `mainAxisAlignment` (axe des X) pour l'alignement horizontal et `crossAxisAlignement`(axe des Y) pour l'alignment vertical

### Exemple de row Et column

Il prend en parametre `children` qui est une liste des Widget à utiliser dans la Colonne et aussi `mainAxisAlignment` (axe des X) pour l'alignement horizontal et `crossAxisAlignement`(axe des Y) pour l'alignment vertical

![Exemple d'une implementation des Row et Column](./assets/images/Learn-%20Example%20de%20Row%20et%20Column%20dans%20Flutter.PNG)

## Container

Le `Container` est de base invisible mais il est très utile pour styliser un widget enfant, de base le `Container` prend toute la place disponible mais en lui rajoutant un enfant ie `child` qui peut etre de plusieurs type comme de type `Text` par exemple alors dans ce cas il s'adapte il s'adapte à celui-ci
Ce `Container` une couleur peut prendre plusieur parametres dont:

- child: Qui est l'enfant que contient le container
- color: Si on veut donner une coleur de fond au `Container`
- width: La largeur du `Container` qui se fait en entier
- height: La longeur du `Container` qui se fait en entier
- padding: La marge interieur du `Container` ie l'espace entre les bords du `Container` et son Widget enfant, qui est notre Texte et pour cela on utilise `padding: const EdgeInsets.all(NombreQueVousDonner)` avec par exemple `padding: const EdgeInsets.all(20)` ou `padding: const EdgeInsets.only(left: 10,right: 5, top: 10,bottom: 30)` ou encore le symetrique ie `padding:const EdgeInsets.symetric(horizontal: 10, vertical: 30)`
- margin:La marge exterieur du `Container` il nous permet de definit l'espace minimum entre notre `Container` et son parent, il est definis de la meme maniere que le padding mais avec des Effets visuel differents càd `margin: const EdgeInsets.all(NombreQueVousDonner)` avec par exemple `margin: const EdgeInsets.all(10)` ou `margin: const EdgeInsets.only(top: 20)` ou encore le symetrique ie `margin: const EdgeInsets.symetric(horizontal: 10, vertical: 30)`
- alignment: Permet d'aligner l'enfant (`child`) par rapport au parent par exemple en Haut à droite `alignment: Alignement.topRight` et comme il n'a pas de taille fixe, alors pour l'alignement il se refere au Widget parent on peut fixer la taille du container en lui definisant une `largeur` et une `hauteur` et dans ce cas l'aligment se faira par rapport à la taille du container
- transform: en faisant de la transformation de notre `Container` avec des `translation` ou `rotation` suivant les 3 axes X, Y et Z par exemple une rotation `transform: Matrix4.rotationZ(0.5)`
- decoration: nous permet de styliser ou de decorer notre `Container`, pour utiliser une decoration de fond on doit pour cela retirer l'attribut `color` du `Container` car cela sera definit dans la decoration, On a plusieurs sorte de decoration comme en utilisant le widget `ShapeDecoration` ou `BoxDecoration`, `ShapeDecoration` permet d'avoir une ou plusieurs bordure par exemple une double bordure rouge et blanche et `BoxDecoration` permet de jouer sur les formes de bordure ie comme le `border-radius` en CSS et `BoxDecoration` peut choisir specifiquement sur quel partie du bordure il peut mettre ses courbes ou sur mettre ses courbes de bordure sur tous les cotés et pour faire cela on utilise le code suivant:

```{DART}
// Le cas du ShapeDecoration
decoration: const ShapeDecoration(
                        color: Colors.red, 
                        shape: Border.all(
                                    color: Colors.white,
                                    width: 8
                                    ) + Border.all(
                                    color: Colors.red,
                                    width: 8
                                )
                        )

```

Dans ce code d'en haut on vient dire que notre `Container` aura comme decoration une couleur de font rouge, qu'il aura deux bordure dont chacun fait 8px et dont le premier a une couleur `Blanche` et la seconde a une couleur `Rouge`

```{DART}
// Le cas du ShapeDecoration sur le coté haut droit et bas droit
decoration: const BoxDecoration(
    color: Colors.red,
    borderRadius: BorderRadius.only(
        topRight: Radius.circular(20),
        bottomRight: Ridius.Circular(20)
    )
)

// Le cas du ShapeDecoration sur tous les cotés
decoration: const BoxDecoration(
    color: Colors.red,
    borderRadius: BorderRadius.circular(20)
)

```

## TextField

Le Widget TextField nous permet d'afficher un champ pour que l'utilisateur rentre du texte
elle prend plusieurs parametre comme:

- onChanged : c'est un parametre qui va contenir une fonction qui sera appeler dès que le texte à l'interieur du champ est modifie ie `onChanged: (text) { print(text) }`

Pour recuperer un texte dans une variable et la printer dès l'appuis sur un bouton on doit assigner la variable dans la methode `onChange` et donc par exemple on a

```{DART}
 String value ='';
 ...
 TextField(
     onChanged: (text) {
         value = text;
     }
 )
```

On peux egalement recuperer la donnée d'un TextField grace au `TextEditingController` est une classe de flutter auquel on va linker à notre `TextField(controller: avecUneInstanceDeTextEditingController)` et dans le button qui execute l'action dans le parametre `onPressed` sa fonction peut acceder au contenus de `TextField` avec l'instance de `TextEditingController` ainsi que le parametre `text` càd `instance.text`

```{DART}
 Column(
    children: [
     TextField(onChanged: (text) {
        _textValue = text;
        print(_textValue);
    }),
     TextField(controller: myController),
     ElevatedButton(
        child: Text("Get Text"),
        onPressed: () {
            print('Vous avez taper ${myController.text}');
        },
        style: ButtonStyle(
            backgroundColor:
                MaterialStateProperty.all(Colors.green)))
    ],
)
```

Comment passer le focus sur un deuxieme `TextField` depuis le premier et pour cela on va avoir besoin de l'instance de la classe `focusNode` de flutter et ainsi dans notre deuxieme `TextField` càd celui à qui on veut mettre le focus à partir du premier `focus` on lui ajoute le parametre `focusNode` et ce parametre prendra en parametre l'instance de la classe `FocusNode`, puis sur le premier qui va mettre le second en mode `focus` on va lui ajouter le parametre `textInputAction` qui aura comme valeur `TextInputAction.next` qui veut dire `"quand tu tape dans ce champ passe directement au champ suivant"` et aussi on lui donne le parametre `onSubmitted` qui est une action qui est appeler quand ce boutton `textInputAction` est presser et cette action est une fonction qui fait passer le focus sur deuxieme `TextField` avec `secondEditText.requestFocus()`

On peux changer le type du clavier avec le parametre `keyboardType` qui prendra comme valeur `TextInputType.phone` ainsi le type de clavier sera entierement numerique

Quand on veut créer un champ mot de passe ie qui cache les donnée du formulaire on utilise le parametre `obscureText` et on le met à `true`

On peux egalement decorer notre `TextInput` avec le parametre `decoration` qui prend comme valeur un `InputDecoration` qui peut contenir une `icone` representant le champ

## Scaffold

Le scaffold permet d'avoir une page de type `Material Design`, le `Scaffold` permet de definir par exemple:

- Une `"AppBar"`: Considerer comme le navbar d'une application mobile
- Un `"Drawer"`: Considerer comme le sidebar d'une application Mobile
- Un `"Body"`: Consider comme l'element `<body></body>` d'une application mobile
- Un `"FloatingActionBottom"`: Est considerer comme le boutton principale d'une application Mobile
-Un `BottomNavigationBar`: Consider comme le footer d'une application Mobile, il contient souvent quelques boutons essentiel de l'application permettant d'aller sur une page quelconque ou de delencher une fonctionnalité ou une action quelconque qui est tres important dans l'application

### AppBar

Voyons quelques parametres de l'element `AppBar` de `Scaffold`

- Dans `AppBar` on a en premier le parametre **`title`** qui contient souvent une `Widget` de type `Text` ou `Icon` ou **meme les deux**, representant le titre de notre application ou de la page où on se trouve.
- Par defaut le **`title`** est placer à gaucher met on peut le center avec le parametre **`centerTitle`** de `AppBar` qui prend comme valeur un booleen *`true`* si on veut center le titre et *`false`* si on veut qu'il reste à gauche
- C'est dans `AppBar` que l'on peut definir les differents actions accessible depuis l`AppBar` comme le *reglage* ou *la deconnection* tous ça avec le parametre **`actions`** qui prend comme valeur une liste des `Widget` càd `<Widget>`, souvent dans **`actions`** on y met un `PopupMenuButton` pour afficher le bouton à3 puces permettant de pouvoir selectionner une serie d'option dans une liste flottante Cfr partie `Button Widget`

## Drawer

Le `Drawer` permet d'afficher le menu d'application, souvent pour construire un `Drawer` on le met dans une liste, le `Drawer` a un parametre `child` dans lequel comme exemple on y definit souvent un Widget `ListView` qui n'a pas de padding et dont les enfants qui sont definis avec son parametre `children` qui prend en parametre une liste de `Widget` le plus souvent de type `DrawerHeader` pour commencer et `ListTile`
