# Test technique Backend Folhomee

## Contexte

Les buts de ce test technique sont les suivants :

- Nous permettre de voir votre niveau technique
- Essayer de déterminer vos capacités concernant la résolution de problèmes
- Voir si vous pourriez vous intégrer au sein de notre équipe technique

L'objectif de ce test technique est de créer un moteur de résolution de bataille (le jeu de carte)

Il est important de respecter les consignes suivantes :

- Ne sautez pas un exercice, il faut respecter l'ordre
- Vous n'avez pas besoin d'utiliser un service externe pour les exercices
- Il est très facile de trouver des résolutions/solutions de ce test en ligne, aussi vous serez jugé sur votre capacité de structurer votre code

## Livrables

Les livrables minimum sont les suivants :

- Un **nouveau repo github privé** auquel vous aurez donné accès au CTO de Folhomee (username github : [milanito](https://github.com/milanito))
- Un ensemble de dossiers/fichiers selon une nomenclature claires
- Pour chacun des exercices, le temps que vous avez mis à le réaliser au travers d'un README que vous essayerez de détailler (le markdown est recommandé), de préférences individuellement pour chaque partie

Nous vous demanderons en plus de respecter les contraintes technique suivantes :

- Le code devra être écrit en javascript et tourner sur node LTS (v12 au moment de l'écriture de ce test)
- Le code devra respecter la coding style de l'entreprise, à savoir [standardjs](https://standardjs.com/)

Pour le reste, vous êtes libre de vos choix technique quand il n'est pas explicitement dit dans l'exercice le choix à faire

## Exercices


La bataille est un jeu de cartes qui oppose deux joueurs. Au début de chaque partie, on sépare aléatoirement les 52 cartes du jeu en deux paquets de même taille attribués à chacun des deux adversaires.
L'issue d'une partie est entièrement déterminée par la répartition initiale des cartes. C'est donc un jeu sans intérêt mais qui, en contrepartie, peut être entièrement automatisé.

Le but de ce test est d'écrire un programme qui mélange les cartes et décide, en fonction d'une répartition initiale, si la partie se termine et quel est le gagnant dans ce cas.

En particulier le programme devra être capable de simuler une partie.

Lors de ce test, nous vous demandons de créer un module nodejs à la racine de votre repo :

- Un dossier `src` qui regroupera les fichiers source de votre application serveur :
- n'oubliez pas de l'initialiser avec `npm init` ou `yarn init`, vous êtes libre du choix du gestionnaire de paquet
- Vous êtes libre d'utiliser, ou non, un module bundler ou un compiler javascript

### Fonction de résolution de partie

Le but est de créer une fonction qui va simuler une partie et renvoyer le vainqueur de la partie, dans un dossier `src/services`

#### Début de partie

Pour commencer la partie, vous devez créer un paquet de carte (52 cartes) et le diviser de manière aléatoire entre les deux joueurs

Un jeu de cartes standard contient 52 cartes, chacune étant caractérisée par

- sa couleur ∈ {♠,♥,♣,♦} et
- sa valeur ∈ {1 < . . . < 10 < Valet < Dame < Roi}.

> Vous êtes libre sur le modèle de données que vous voulez utiliser, n'oubliez pas que la couleur n'a aucune importance

#### Déroulement d'un pli

On simule un pli comme ceci :

1) chaque joueur tire une carte et la met dans le pli,
2) le joueur ayant retourné la carte la plus forte remporte le pli,
3) en cas d'égalité il y a « bataille » :
  - chaque joueur tire une première carte et l'ajoute au pli (ces cartes ne sont pas comparées, c'est à cette occasion que les cartes de grande valeur peuvent changer de main)
  - chaque joueur tire une seconde carte et l'ajoute au pli
  - on retourne à l'étape 2

#### Bonus

- Des tests, des tests, des tests !
- Faire renvoyer à votre fonction, si on lui donne en entrée un numéro de tour, l'état du plateau (ie les cartes des deux joueurs) au tour donnés
- Pouvoir déterminer si une partie est infinie (ie ne se finira jamais), regardez du côté de l'algorithme du lièvre et de la tortue, dû à Floyd.

### Route de résolution de partie

Le but de cette partie est de créer un [serveur express](https://expressjs.com/) pour nous permettre de faire une petite API pour simuler des parties de batailles

#### Serveur express

Vous devrez créer un [serveur express](https://expressjs.com/) à la racine de `src`

- Vous êtes libre sur l'implémentation, vous serez jugé sur l'architecture de votre code
  - N'oubliez pas la [sécurité](https://expressjs.com/en/advanced/best-practice-security.html) et la [performance](https://expressjs.com/en/advanced/best-practice-performance.html)
- Vous êtes libre sur votre utilisation des middlewares et du logging

#### Simulation de partie

Vous devez créer une route qui permet d'utiliser votre fonction préalablement réalisée dans `src/services` pour simuler la résolution d'une partie

- La fonction doit renvoyer json indiquant le joueur vainqueur, vous pouvez utiliser le format suivant :

```
{
  winner: 1
}
```

Mais vous êtes plutôt libre d'utiliser le format que vous voulez

#### Bonus

- Des tests, des tests, des tests !
- Faire renvoyer à votre API, si on lui donne en query un numéro de tour, l'état du plateau (ie les cartes des deux joueurs) au tour donnés (même bonus que précédemment)
- Pouvoir renvoyer par l'API si une partie est infinie (même bonus que précédemment)

## Bonus

Une fois l'intégralité des exercices précédents réalisés, vous pouvez réaliser les tâches suivantes en bonus :

- Proposer un hébergement en ligne pour les applications
- Avoir la possibilité d'ajouter plus de joueurs
- Nous impressionner avec n'importe quoi que vous trouverez pertinent
