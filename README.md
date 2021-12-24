---
title : Guide LaTeX
author : Rémi VAN BOXEM
date: 24 décembre 2021
abstract : Ceci est un guide basique du LaTeX. Réalisez aisément des documents simples et plus propre qu'un logiciel WYSIWYG. Ce guide est fait pour être lu à côté d'un environnement LaTeX opérationnel.
version : 0.0.1
---

- [Introduction](#introduction)
  - [En ligne](#en-ligne)
  - [Sur ma machine](#sur-ma-machine)
    - [macOS](#macos)
    - [Windows](#windows)
    - [Linux](#linux)
- [Comme le bigorneau adhère au bitume](#comme-le-bigorneau-adhère-au-bitume)
  - [Votre premier document](#votre-premier-document)
  - [Document oui, mais...](#document-oui-mais)
    - [Métadonnées](#métadonnées)
    - [Localisation du document](#localisation-du-document)
    - [Section, sous-section, sous-sous-section...](#section-sous-section-sous-sous-section)
  - [Du contenu contenu dans un beau cadre](#du-contenu-contenu-dans-un-beau-cadre)
    - [Encadre-moi ça !](#encadre-moi-ça-)
    - [Des équations](#des-équations)

# Introduction

Dans cette section, vous allez pouvoir choisir comment souhaitez-vous rendre votre document LaTeX. Il faut savoir que LaTeX est un langage compilé, donc il faudra au minima un compilateur LaTeX et un éditeur. Il existe toutefois une solution sans aucune installation en utilisant simplement votre navigateur.

## En ligne

Une solution 100% en ligne est d'utiliser le site **[Overleaf](https://www.overleaf.com/)**. Vous pouvez vous créer gratuitement un compte sur Overleaf. Une fois sur votre espace, cliquez sur le bouton vert **New Project** puis sur **Blank Project**. Choississez un nom pour votre projet et on est parti !

## Sur ma machine

Dans cette sous-section, on va vous installer les outils afin de compiler localement votre fichier. Référez-vous à la partie correspondante à votre système d'exploitation. Dans ce guide (qui est prévu pour les ISEN, bonjour à vous), nous allons utiiser Visual Studio Code comme éditeur de texte (avec l'excellente extension LaTeX Workshop).

Pour installer Visual Studio Code, référez-vous au guide d'installation [suivant](https://code.visualstudio.com/docs/setup/).

### macOS

La distribution LaTeX recommandée est [MacTeX](https://tug.org/mactex/), les détails d'installations sont présents sur la page.

### Windows

La distribution LaTeX recommandée pour Windows est [MiKTeX](https://miktex.org). Vous devez également installer un interpréteur Perl, ma recommendation est [Strawberry Perl](https://strawberryperl.com). C'est un environnement perl pour MS Windows contenant tout ce dont vous avez besoin pour exécuter et développer des applications perl. Il est conçu pour être aussi proche que possible de l'environnement perl des systèmes UNIX.

Redémarrez votre ordinateur. Il n'est pas rare que le compilateur LaTeX MiKTeX soit capricieux sur Windows et nécessite le redémarrage de l'ordinateur pour être correctement inclus dans le `PATH`. 

Ensuite, lors de votre première compilation, il est possible que votre document ne compile juste pas. Soyez à l'affut d'une fenêtre de MiKTeX vous demandant d'installer des paquets.

### Linux

Téléchargez la distribution **TeX Live** depuis votre package manager :

| Distribution | Nom du paquet |
| -------------|---------------|
| Arch Linux | `texlive-most` |
| Debian | `texlive-full`
| Fedora | `texlive-scheme-medium` |
| Gentoo | `app-text/texlive` |
| NixOS | `nixpkgs.texlive.combined.scheme-medium` |
| openSUSE | `texlive-latex` |
| Ubuntu | `texlive-full` |

Une fois TeX Live d'installé, vous n'avez plus rien à faire. Vous êtes opérationnel !

# Comme le bigorneau adhère au bitume

Un drôle de titre, non ? Le principe de cette partie est de poser les premières bases, sans rentrer dans le complexe pour créer un document LaTeX. Vous retrouverez en annexes les différents cas particulier qui seront prochainement annoncés.

## Votre premier document

C'est officiel, vous allez écrire votre premier document LaTeX ! Sortez votre meilleure plume, créez un fichier `main.tex`, ouvrez le répertoire le contenant avec Visual Studio Code et écrivez ce qui suit et compilez votre document. *(Ces lignes vous seront expliqués juste après.)* 

```latex
\documentclass{article}
\begin{document}
Hello World 
\end{document}
```
Vous devriez voir une belle page blanche avec en haut à gauche "Hello World". Si c'est le cas félicitations ! Si ce n'est pas le cas, référez-vous aux procédures d'installation complètes en annexes.

La ligne `\documentclass{article}` présise à votre compilateur quel type de document vous écrivez actuellement. Il en existe un certain nombre de base : `book` un format adapté à la rédaction de gros ouvrages (plusieurs centaines de pages), `report` un format adapté pour des documents de taille modéré et la classe `article` pour des documents extrêmement courts. 

Ces trois formats sont les formats natifs que vous risquez de rencontrer le plus souvent. 

> Il existe aussi d'autres formats plus exotiques tel que `beamer` une classe permettant de faire des présentations, `letter` une classe spéciale pour la rédaction de courrier dans les normes américaines et `lettre` la même chose mais avec les standards européens établis par l'Observatoire de Genève.

Cette ligne doit être impérativement la première de votre fichier `.tex`.

Ensuite vous avez le `\begin{document}` et le `\end{document}`. En écrivant ceci vous dites que tout ce qui est compris entre ces deux balises est dans le document (visuellement parlant). On parle d'environnement de document.

Et enfin, notre "Hello World" est affiché puisqu'il dans l'environnement de document.

## Document oui, mais...

### Métadonnées

En LaTeX, vous avez un ensemble de métadonnées simples : le titre, l'auteur et la date de rédaction/publication du document. *Selon la classe de document choisie, certaines métadonnées supplémentaires peuvent être demandées afin de personnaliser au mieux le document.*

Pour définir ces métadonnées, vous pouvez écrire en haut de votre document :

```latex
\title{Mon super titre}
\author{C'est moi !}
```

Dans votre environnement de document, ajoutez à la première ligne :

```latex
\maketitle
```

Compilez votre document et pouf ! Vous avez un joli titre tout propre ! Mais... La date du jour est en anglais ? Corrigons cela !

### Localisation du document

LaTeX est prévu pour être utilisé dans le monde entier, c'est pour cela qu'on peut préciser la langue et les normes locales qu'on souhaite utiliser. 

Pour choisir cela, juste après votre définition de classe de document, ajoutez : 

```latex
\usepackage[french]{babel} % Normes et traductions
\usepackage[T1]{fontenc} % Usage des caractères spéciaux
```

La première ligne importe le paquet `babel` et lui donne comme option qu'on utilise la langue ***française*** pour notre document. Cela va permettre de traduire "Table of Contents" par "Table des matières", "Abstract" par "Résumé"... et utiliser les normes françaises, notamment pour les dates.

Compilez votre document et découvrez une page de titre bien propre !

### Section, sous-section, sous-sous-section...

Vous pouvez hiérachiser vos informations en faisant des parties. Les trois les plus fréquentes sont `\section` `\subsection` et `\subsubsection`. *Il existe également `\part` `\chapter` mais nécessite la classe de document `book`.* Si ce n'est pas suffisant vous avez aussi des `\paragraph` et des `\subparagraph`.

Ces instructions possèdent tous la même syntaxe : `\typedesection{titre}`. Pour créer une section que j'appelerai Junla, je peux écrire :

```latex
\section{Junla}
```

Pour faire un parallèle avec de la géométrie : La section correspond à un parallélogramme, une sous section correspond à un rectangle ou à un losange et une sous sous section peut être notre carré. Pour représenter cela en LaTeX, vous pouvez écrire : 

```latex
\section{Parallélogramme}
En géométrie, un parallélogramme est un quadrilatère dont les segments diagonaux se coupent en leurs milieux.

\paragraph{Propriété}
Tout parallélogramme a un centre de symétrie : le point d'intersection de ses diagonales.

\subsection{Losange}
Un losange est un parallélogramme ayant au moins deux côtés consécutifs de même longueur. Il est même équilatéral.

\paragraph{Propriété} Les diagonales d'un losange sont les bissectrices de ses angles.

\subsection{Rectangle}
Un rectangle est un parallélogramme ayant au moins un angle droit. Il est même équiangle.

\subsubsection{Carré}
Un carré est un losange rectangle.
```

Compilez et vous avez trié par niveau les différents types de quadrilatères particuliers. 

Pour faire un joli sommaire, ajoutez après `\maketitle` :

```latex
\tableofcontents
```

En suivant la partie précédente, vous devez arriver à ce qui suit :
Code final :
```latex 
\documentclass{article}
\usepackage[french]{babel}
\usepackage[T1]{fontenc}

\title{Mon super titre}
\author{C'est moi !}

\begin{document}
\maketitle
\tableofcontents
Hello World 

\section{Parallélogramme}
En géométrie, un parallélogramme est un quadrilatère dont les segments diagonaux se coupent en leurs milieux.

\paragraph{Propriété}
Tout parallélogramme a un centre de symétrie : le point d'intersection de ses diagonales.

\subsection{Losange}
Un losange est un parallélogramme ayant au moins deux côtés consécutifs de même longueur. Il est même équilatéral.

\paragraph{Propriété} Les diagonales d'un losange sont les bissectrices de ses angles.

\subsection{Rectangle}
Un rectangle est un parallélogramme ayant au moins un angle droit. Il est même équiangle.

\subsubsection{Carré}
Un carré est un losange rectangle.

\end{document}
```

## Du contenu contenu dans un beau cadre
Maintenant qu'on sait comment bien cadrer son contenu, on va apprendre à écrire du contenu en LaTeX.

### Encadre-moi ça !
Ajouter des images, première chose qu'on fait avec un logiciel de traitement de texte. On se bat avec le placement de cette dernière avant d'abandonner et de sortir PowerPoint pour faire son CV.

On va voir comment en LaTeX, on importe une image.

```latex
\documentclass{article}
\usepackage{graphicx}
\graphicspath{ {./images/} }

\begin{document}
L'univers est immense et il semble être homogène, 
à grande échelle, partout où nous regardons.

\includegraphics{universe}

Voici une photo de la galaxie juste au dessus.
\end{document}
```

Et pouf ! L'image est correctement importée ! LaTeX ne peut pas gérer les images par lui-même, nous devons donc utiliser le paquet `graphicx`. Pour l'utiliser, nous incluons la ligne suivante dans le préambule : `\usepackage{graphicx}`.

Il se peut que l'image ne soit pas au bon format. On peut rajouter le paramètre `scale` afin d'affiner la taille de l'image.

```latex
\includegraphics[scale=1.5]{universe} % On aggrandit l'image
```

**Note :** L'extension du fichier peut être incluse, mais c'est une bonne idée de l'omettre. Si l'extension de fichier est omise, LaTeX recherchera tous les formats supportés. 

Plus d'informations sur la gestion du positionnement des images juste [ici](https://www.overleaf.com/learn/latex/Inserting_Images).

### Des équations

Nous devons écrire une équation mathématiques très importante, mais vous n'avez pas envie de scanner un bout de papier car il faut être sérieux ! LaTeX à la solution pour vous !

```\latex
$$E=mc^2$$
```

$$E=mc²$$

Félicitations, vous venez de prouver la formule d'équivalence entre la masse et l'énergie en relativité restreinte ! Voici un cookie.

Cette équation n'a toutefois rien de bien difficile à écrire, un simple E = mc² aurait fait l'affaire. Toutefois, lorsqu'on a des équations plus complexes comme : $\binom{n}{k} = \frac{n!}{k!(n-k)!}$ ou encore $\lim_{h \rightarrow 0 } \frac{f(x+h)-f(x)}{h}$, on est bien content d'avoir un logiciel externe pour !

En LaTeX, pour écrire le paragraph précédent, on a du écrire : 
```latex 
Toutefois, lorsqu'on a des équations plus complexes comme : $\binom{n}{k} = \frac{n!}{k!(n-k)!}$ ou encore $\lim_{h \rightarrow 0 } \frac{f(x+h)-f(x)}{h}$, on est bien content d'avoir un logiciel externe pour !
```

La différence entre le `$math$` et `$$math$$` est que le premier va se contenter de se mettre là où vous l'avez placé tandis que le double `$$` va centrer l'équation au centre de la feuille.

Exemple : 

$\lim_{h \rightarrow 0 } \frac{f(x+h)-f(x)}{h}$

$$\lim_{h \rightarrow 0 } \frac{f(x+h)-f(x)}{h}$$

```latex
$\lim_{h \rightarrow 0 } \frac{f(x+h)-f(x)}{h}$

$$\lim_{h \rightarrow 0 } \frac{f(x+h)-f(x)}{h}$$
```