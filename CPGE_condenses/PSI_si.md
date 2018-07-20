---
lang: fr-FR
papersize: a4
geometry: margin=1.8cm
classoption: twocolumn,twoside
numbersections: yes
title: Condensé de cours de SI de PSI
toc: yes
keywords: S2I,SI,PSI,cours,condensé,asservissement,mécanique,logique
---

\vspace{24pt}

![](assets/PSI_si_dessin)

\newpage

# Asservissement

## Rappels de première année

### Les transformations

Soit $f$ une fonction du temps telle que $\forall t < 0, f(t)=0$. <!-- -->
La transformée de *Laplace* de $f$ est
$$ \mathcal{L}(f):p \mapsto \int_{0^-}^\infty f(t)\,e^{-pt}\,\mathrm{d}t $$

Soit $f$ une fonction du temps.
La transformée de *Fourier* (hors programme) de $f$ est
$$ \mathcal{F}(f):\omega \mapsto \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{+\infty}
f(t)\,\mathrm{e}^{-{\rm{j}}\omega t}\,\mathrm{d}t $$

Soit $s$ une fonction discrète du temps.
La transformée en Z (hors programme) de $f$ est
$$ \mathcal{Z}(s): z \mapsto \sum_{n=-\infty}^{+\infty} s(n)\,z^{-n} $$

### Formulaire des transformées de *Laplace*

Dans les pays anglo-saxons, $p$ se note $s$.

$u$ est la fonction d'Heaviside.

#### Théorème de la valeur finale

$$\underset{t \rightarrow +\infty}{\mathrm{lim}} ~ f(t) =
\underset{p \rightarrow 0}{\mathrm{lim}} ~ p\,F(p)$$
(valeur initiale : $p \rightarrow +\infty$)

#### Dérivation (intégration par partie)

$$\frac{\mathrm{d}f(t)}{\mathrm{d}t}u(t) \underset{\mathcal{L}}{\longrightarrow}
p\,F(p)-f(t=0^+)$$

#### Intégration

$$\int_a^t f(x)\,u(x)\,\mathrm{d}x  \underset{\mathcal{L}}{\longrightarrow}
\frac{F(p)}{p}+\frac{1}{p} \int_a^0 f(x)\,\mathrm{d}x$$

#### Translation (changement de variable)

$$f(t-\tau)\,u(t-\tau) \underset{\mathcal{L}}{\longrightarrow}
e^{-\tau\,p}\,F(p)$$

#### Homothétie (changement de variable)

$$f(a\,t)\,u(t) \underset{\mathcal{L}}{\longrightarrow}
\frac{1}{a}\,F\left(\frac{p}{a}\right)$$

#### Multiplication par $e^{-a\,t}$

$$e^{-a\,t}\,f(t)\,u(t) \underset{\mathcal{L}}{\longrightarrow} F(p+a)$$

#### Dirac

$$\delta (t) \underset{\mathcal{L}}{\longrightarrow} 1$$

#### Heaviside, Rampe...

$$\forall n\in\mathbb{N},\quad t^n\,u(t) \underset{\mathcal{L}}{\longrightarrow}
\frac{n!}{p^{n+1}}$$

#### Oscillations

$$\sin(\omega t)\,u(t) \underset{\mathcal{L}}{\longrightarrow}
\frac{\omega}{p^2+\omega^2}$$
$$\cos(\omega t)\,u(t) \underset{\mathcal{L}}{\longrightarrow}
\frac{p}{p^2+\omega^2}$$

### Dépassement d'un second ordre

Lors de la réponse d'un second ordre à un échelon, le $k$-ième dépassement
vaut (pourcentage relatif à la consigne)
$$ D_k = \exp \left({\frac{-k \xi \pi}{\sqrt{1-\xi^2}}}\right) $$

### Identifier un second ordre

On cherche à identifier un second ordre avec la réponse temporelle à un échelon.

$$ H(p)=\frac{K}{1+\frac{2\xi}{\omega_0}p+\frac{p^2}{\omega_0^2}} $$

Déjà on a **le gain $K$** en régime établi (rapport de la sortie sur l'entrée).

On cherche ensuite **le coefficient d'amortissement $\xi$**.
On mesure le 1er dépassement $D$ et on utilise cette formule
$$ D = \exp \left({\frac{-\xi \pi}{\sqrt{1-\xi^2}}}\right) $$

On cherche enfin **la pulsation propre du système $\omega_0$**.
Pour cela on mesure la pseudo période $T$ et on utilise
$$ \frac{2\pi}{T} = \omega = \omega_0 \sqrt{1-\xi^2} $$

<!-- TODO Rappeler la méthode de Black -->
<!-- TODO Rappeler la décomposition en elmts simples -->
<!-- TODO Rappeler différence système bouclé/dynamique et qu'est ce qu'est
un système asservi -->

\newpage

## Précision des systèmes bouclés

### Classe d'une fonction de transfert

Une fonction de transfert de classe $\alpha$ s'écrit canoniquement
$$G(p)=\frac{K}{p^\alpha} \times \frac{1+b_1 p+...}{1+a_1 p+...}$$

### En régime permanent en poursuite

Soit $\alpha$ la classe généralisée de $H_{BO}(p)$.

-   Pour $\alpha = 0$, $\epsilon_{statique} = \frac{X_0}{1+K_{BO}}$

-   Pour $\alpha = 1$, $\epsilon_{statique} = 0$ et
    $\epsilon_{trainage} = \frac{V}{K_{BO}}$

-   Pour $\alpha = 2$, $\epsilon_{statique} = \epsilon_{trainage} = 0$ et
    $\epsilon_{acceleration} = \frac{a}{K_{BO}}$

Donc l'erreur en régime permanent diminue si le gain $K_{BO}$ ou la classe
$\alpha$ augmentent.

*Démonstration.* On applique le théorème de la valeur final sur le signal
d'erreur $\epsilon(p)$ (après le comparateur) avec en entrée un échelon, une
rampe puis une parabole.

### En régime permanent en régulation

L'erreur due à une perturbation en régulation diminue si le gain ou le nombre
d'intégrateur en amont de cette perturbation augmentent.

*Démonstration.* Comme la démonstration précédente mais on considère la consigne
nulle et une perturbation.

### En régime harmonique en poursuite

Plus la bande passante d'un système bouclé est grande, plus le système est
précis en régime sinusoïdal sur une grande plage de fréquence.

*Démonstration.* L'expression du gain de la BF avec $H_{BO}(p)$ montre qu'il
existe une pulsation de coupure que l'on souhaite maximiser pour être précis en
hautes fréquences.

### En régime harmonique en régulation

Plus la bande passante des composants en amont de la perturbation est grande,
plus le système est précis vis-à-vis d'une perturbation harmonique de
haute fréquence.

*Démonstration.* Comme la démonstration précédente mais on considère la consigne
nulle et une perturbation.

### Cas de non linéarité

Les modèles utilisés sont des approximations linéaires autour de points de
fonctionnement. Pour rester réaliste il faut éviter les phénomènes non linéaires
tels que

* **Une saturation** (ex : tension max d'un hacheur),
* **Une zone morte** (ex : tension min d'un MCC).

\newpage

## Stabilité des systèmes asservis

### Stabilité

Un système stable est un système qui revient vers sa position d'équilibre
après perturbation.

### Conditions de stabilité {#condstab}

Un système stable est un système qui admet une fonction de transfert $H(p)$
telle que
$$ \forall \text{pôles~}p_i\text{~de~}H(p),\quad\mathrm{Re}(p_i) < 0 $$ <!-- -->

*Démonstration.* Se ramener à la forme des pôles de la fonction de transfert :
$p_i = -a_i \pm j\Omega_i$. La décomposition en élément simple mène au résultat.

Une seule étude de stabilité est nécessaire qu'il y ait perturbation ou
pas.

*Démonstration.* Le dénominateur de la fonction de transfert en régulation et 
en poursuite est le même.

Donc un système est stable en boucle fermée si seulement si $1+H_{BO}(p)=0$ n'a
que des solutions à partie réelle $<0$. <!-- -->

*Démonstration.* Les racines de $1+H_{BO}$ sont les pôles de $H_{BF}$.

![Représentation des pôles](assets/PSI_si_asservissement-poles){#fig:f1}

### Critère de Routh (hors programme)

Ce critère ne marche pas sur un système comportant un retard. On
considère un système de fonction de transfert $H(p)$ de dénominateur
$$ D(p) = a_n\,p^n+a_{n-1}\,p^{n-1}+...+a_1\,p+a_0 $$

Le système est stable si seulement si

* Tous les coefficients $a_i$ soient de même signe et $\neq 0$,
* Tous les termes de la première colonne du tableau (voir cours)
  soient de même signe et non nuls.

Le nombre de racine à partie réelle strictement positive est donné par
le nombre de changement de signe dans la première colonne.

### Théorème de Cauchy (hors programme) {#thmcauchy}

Si un point $M$ d'affixe $p$ décrit dans le plan complexe un contour
fermé $(C)$ dans le sens inverse trigonométrique, à l'intérieur duquel
se trouve $P$ pôles et $Z$ zéros d'une fonction $F(p)$, alors l'image de
$(C)$ par $F(p)$ décrit une courbe $(\Gamma)$ qui fait autour de l'origine
$(Z-P)$ tours.

*Démonstration.* La variation de l'argument de $F(p)$ pour un tour de $M$ sur
$(C)$ est $(-2\pi) \times (Z-P)$.

### Critère de Nyquist (hors programme) {#crinyquist}

Un système bouclé est stable en boucle fermée si seulement si le lieu de
Nyquist de $H_{BO}$ complété et parcouru dans le sens des $\omega$
croissants

* Ne passe pas par le point critique $-1$,
* Fasse autour du point critique $-1$, $N$ tours dans le sens trigonométrique
  égal au nombre de pôles de $H_{BO}$ à partie réelle strictement positive.

*Démonstration.* Par [la condition de stabilité](#condstab) ainsi que
[le théorème de Cauchy](#thmcauchy) en considérant la courbe englobant
la partie réelle positive du plan complexe.
Le point critique est en $-1$ car on se rapporte à $1+H_{BO}$.

### Critère du Revers

Un système bouclé est stable en boucle fermée si et seulement si le point
critique $-1$ reste à gauche en parcourant le lieu de Nyquist de $H_{BO}$ dans
le sens des $\omega$ croissants.

Valable que si $H_{BO}$ n'a pas de pôle à partie réelle positive.

*Démonstration.* Cas particulier du [critère de Nyquist](#crinyquist).

### Marge de phase et de gain

Soit $\omega_c$ la pulsation de coupure, i.e. $|H_{BO}(j\,\omega_c)|=1$.
Alors la marge de phase est
$$M_\varphi = \varphi(\omega_c) - (-180^\circ)$$

Soit $\omega_1$ tel que $\varphi(\omega_1)=-180^\circ$.
Alors la marge de gain est
$$M_G = -20 \times \log|H_{BO}(\rm{j}\,\omega_1)|$$

En pratique, il y a stabilité pour $M_\varphi \geq 45^\circ$ et
$M_G \geq 6\,\mathrm{dB}$.

![Marge de Gain et de Phase sur un Nyquist et
Bode](assets/PSI_si_asservissement-mphasegain)

### Facteur de résonance

Il y a résonance en $\omega_r=\omega_0 \sqrt{1-2 \xi^2}$.
Le facteur de résonance est
$$Q = 20 \times \log \left( \frac{1}{2 \xi \sqrt{1-\xi^2}} \right)$$

*À savoir faire.* Lire $Q$ sur un diagramme de Bode (la parallèle à l'asymptote 
en BF passant par le maximum).

En pratique, il y a stabilité pour $Q \leq 2.3\,\mathrm{dB}$.

### Abaque de Black-Nichols

L'abaque est consitué d'un réseau de courbes isophases et isomodules en boucle
fermée par retour unitaire.

En traçant un lieu de $H_{BO}$ on trouve

* Le facteur de qualité $Q$ par l'isomodule tangeant.
* La marge de phase $M_\varphi$ et de gain $M_G$ (voir +@fig:f3). 

*À faire au moins une fois dans sa vie.* Utiliser le module Control Design de
MatLab-Simulink pour régler un correcteur via un abaque de Black-Nichols.

![Abaque de Black-Nichols avec le lieu d'une
$H_{BO}$](assets/PSI_si_asservissement-abaque){#fig:f3}

### Modes et Pôles dominants

Voir +@fig:f1. On peut approximer une fonction de transfert avec ses
pôles dominants (les plus proches de l'origine) après le début du régime
transitoire.

\newpage

## Correcteurs (Régulateurs)

Pour améliorer la stabilité, précision et la rapidité d'un système asservi on
peut ajouter et régler un correcteur.

![Visualisation des critères sur le Bode de
$H_{BO}$](assets/PSI_si_asservissement-perf_bode)

### Les correcteurs en parallèle

* Retour avec une grandeur physique intermédiaire,
* **La compensation** en mesurant la perturbation,
* **Chaîne d'anticipation** (feedforward) avec l'entrée.

### Les correcteurs en série

Mise en place plus simple qu'en parallèle, très utilisés.

* **Correction proportionnelle (P)** :
  meilleures rapidité et précision mais la stabilité diminue ($\omega_c$ 
  augmente donc $M_\varphi$ diminue).
  $C(p)=K$

* **Correction intégrale (I)** :
  meilleure précision mais la stabilité diminue ($-90^\circ$ pour $M_\varphi$).
  $C(p)=\frac{1}{T_i\,p}$

* **Correction dérivée (D)** :
  meilleure rapidité et stabilité ($+90^\circ$ pour $M_\varphi$) mais la
  précision diminue et risque de bruit en hautes fréquences.
  $C(p)=T_D\,p$

### Les correcteurs classiques

#### Le correcteur PI

Améliore la précision en ajoutant un intégrateur.
$$ C(p) = K \left( 1+\frac{1}{T_i\,p} \right) $$

*Méthode de réglage*.

1. Choisir la pulsation de coupure $\omega_c$ en réglant $K$.
2. Choisir la marge de phase $M_\varphi$ en réglant $T_i<\omega_c$.

#### Le correcteur à retard de phase

Pour éviter l'instabilité due à l'intégrateur du PI, on utilise
$$ C(p) = K \frac{1+T\,p}{1+a\,T\,p} \quad\text{avec } a > 1 $$

*Utilisation*.

* Règle la précision (placé dans les basses fréquences),
* Règle la marge de phase (placé dans les hautes fréquences).

*Point d'inflexion* en $\omega_m = \frac{1}{T\sqrt{a}}$ où
$\sin(\varphi_m) = \frac{1-a}{1+a}$

![Diagramme de Bode du PI et retard de
phase](assets/PSI_si_asservissement-bode_pi)

<!-- TODO Ajouter retard de phase sur schéma -->
<!-- TODO Je me suis arrêté là -->

\newpage

#### Le correcteur PD

Analogie du correcteur PI.

Le correcteur PD n'est pas physique
$$C(p) = K \left( 1+T_d\,p \right)$$

On bloque donc les BF avec $\tau << T_d$ <!-- -->
$$C(p) = K \left( 1 + \frac{T_d\,p}{1+\tau\,p} \right)
\approx K \frac{1+T_d\,p}{1+\tau\,p}$$

#### Le correcteur à avance de phase

Analogie du correcteur à retard de phase.
$$C(p) = K \frac{1+T\,p}{1+a\,T\,p} \quad\text{avec } a < 1$$ <!-- -->

![](assets/PSI_si_asservissement-correction)

#### Le correcteur PID

$$C(p) = K \left( 1 + \frac{1}{\tau_i\,p} + \tau_d\,p \right)$$

\newpage

# Mécanique

## Rappels de première année

### Formule de Willis

<!-- TODO Mettre un schéma -->

À savoir retrouver très rapidement, soit en repartant du roulement sans
glissement (méthode longue), soit directement en se plaçant sur le
porte-sattelites.

Par exemple :
$$\frac{\omega_{1/ps}}{\omega_{3/ps}} = - \frac{Z_3}{Z_1} \frac{Z_2}{Z_2}$$

### Formule de la base mobile

La formule de la base mobile, aussi appelée **formule de Bour**, est une
relation entre les dérivées temporelles d'un vecteur par rapport à deux
référentiels distincts.

$$ \left.\frac{\mathrm{d}\vec{u}}{\mathrm{d}t}\right|_{R_0} =
\left.\frac{\mathrm{d}\vec{u}}{\mathrm{d}t}\right|_R
+ \overrightarrow{\Omega}_{R/R_0} \wedge \vec{u} $$

### Théorème de Varignon {#varignon}

Chaque torseur est composé d'**une résultante** et d'**un moment** (dépendant du
point). Le théorème de Varignon permet de déplacer le point d'écriture du
torseur.

Par exemple pour [le torseur cinématique](#torseurs), on obtient la
formule de Varignon
$$ \overrightarrow{V}_{B,~S/R} = \overrightarrow{V}_{A,~S/R} +
\overrightarrow{BA} \wedge \overrightarrow{\Omega}_{S/R} $$

*Pour retenir.* « BABAR »

*Démonstration.* Avec la formule de la base mobile sur $\frac{\mathrm{d}
\overrightarrow{AB}}{\mathrm{d}t}$ puis une relation de Chasles
$\overrightarrow{AB}=-\overrightarrow{OA}+\overrightarrow{OB}$.

### Modélisation des actions mécaniques

On distingue :

* Les actions volumiques : l'action exercée sur pour un volume élémentaire
  $\mathrm{d}\tau$ est
  $$ \mathrm{d}\vec{f}(M) = \vec{f}_v(M)\,\mathrm{d}\tau $$

* Les actions surfaciques : l'action exercée sur pour une surface élémentaire
  $\mathrm{d}S$ est
  $$ \mathrm{d}\vec{f}(M) = \vec{f}_s(M)\,\mathrm{d}S $$

Ainsi l'action appliqué à une particule infinitésimale de masse $\mathrm{d}m$,
de volume $\mathrm{d}V$ et de surface $\mathrm{d}S$ est
$$ \mathrm{d}\vec{f} = \vec{f}_v(M)\,\mathrm{d}V + \vec{f}_s(M)\,\mathrm{d}S $$

### Formule de Gibbs

$$\vec{u} \wedge (\vec{v} \wedge \vec{w})
= (\vec{u}\cdot\vec{w})\vec{v} - (\vec{u}\cdot\vec{v})\vec{w}$$

\newpage

## Dynamique des solides

On se limite à des **solides indéformables** et à **masse conservative**.

### Les torseurs utilisés {#torseurs}

**Le torseur cinématique**
$$ \{ \mathcal{V}_{S/R} \}
= \left\{ \begin{array}{l}
\overrightarrow{\Omega}_{S/R} \\
\overrightarrow{V}_{A,~S/R}
\end{array} \right\}_{A} $$

**Le torseur des actions mécaniques**
$$ \{ \mathcal{T}_{\overline{E}/E} \}
= \left\{ \begin{array}{l}
\overrightarrow{R}_{\overline{E}/E} \\
\overrightarrow{M}_{A,~\overline{E}/E}
\end{array} \right\}_{A}
= \left\{ \begin{array}{l}
\displaystyle\int_E \mathrm{d}\vec{f} \\
\displaystyle\int_E \overrightarrow{AM}\wedge\mathrm{d}\vec{f}
\end{array} \right\}_{A} $$

**Le torseur cinétique**
$$ \{ \mathcal{C}_{E/R} \}
= \left\{ \begin{array}{l}
\overrightarrow{R_C}_{(E/R)} \\
\overrightarrow{\sigma}_{A,E/R}
\end{array} \right\}_{A}
= \left\{ \begin{array}{l}
\displaystyle\int_E \overrightarrow{V}_{M,~E/R}\,\mathrm{d}m \\
\displaystyle\int_E \overrightarrow{AM}\wedge\overrightarrow{V}_{M,~E/R}
\,\mathrm{d}m
\end{array} \right\}_{A} $$

**Le torseur dynamique**
$$ \{ \mathcal{D}_{E/R} \}
= \left\{ \begin{array}{l}
\overrightarrow{R_D}_{(E/R)} \\
\overrightarrow{\delta}_{A,E/R}
\end{array} \right\}_{A}
= \left\{ \begin{array}{l}
\displaystyle\int_E \overrightarrow{a}_{M/R}\,\mathrm{d}m \\
\displaystyle\int_E \overrightarrow{AM}\wedge\overrightarrow{a}_{M/R}
\,\mathrm{d}m
\end{array} \right\}_{A} $$

### Propriétés de ces torseurs

$$ \overrightarrow{R_C}_{(E/R)} = m\,\overrightarrow{V}_{G,~E/R} $$
$$ \overrightarrow{R_D}_{(E/R)}
= \left.\frac{\mathrm{d}\overrightarrow{R_C}_{(E/R)}}{\mathrm{d}t} \right|_R
= m\,\vec{a}_{G,~E/R} $$ 
$$ \vec{\delta}_{A,E/R}
= \left.\frac{\mathrm{d}\vec{\sigma}_{A,E/R}}{\mathrm{d}t} \right|_R
+ m\left.\frac{\mathrm{d}\overrightarrow{OA}}{\mathrm{d}t} \right|_R \wedge
\vec{V}_{G,~E/R}$$

*Démonstration.* Avec [la définition des torseurs](#torseurs).

### Théorème des actions réciproques

$$\{ \mathcal{T}_{E2/E1} \} = -\{ \mathcal{T}_{E1/E2} \}$$

### Théorèmes généraux de la mécanique

Le principe fondamental de la dynamique dit qu'il existe au moins un référentiel
$R$ (dit galiléen) tel que
$$ \mathrm{d}\vec{f}(M) = \overrightarrow{a}_{M/R}\,\mathrm{d}m $$

*Démonstration.* Voir le cours de Physique.

On obtient le théorème de la résultante et du moment :
$$\{ \mathcal{T}_{\overline{E}/E} \} = \{ \mathcal{D}_{E/R} \}$$

*Démonstration.* On utilise la relation précédente avec
[la définition des torseurs](#torseurs).

### Un peu d'algèbre linéaire {#algebre}

On considère le plan euclidien.
Soit le vecteur $\overrightarrow{AG}$ de coordonnées $(x, y, z)$ dans la base
canonique.

Soit $M$ la matrice canoniquement associée à l'application linéaire
$f: \overrightarrow{u} \mapsto
\overrightarrow{AM} \wedge (\overrightarrow{u} \wedge \overrightarrow{AM})$ :

$$M = \left( \begin{array}{ccc}
 y^2+z^2 & - x y & - x z \\
 - x y & x^2+z^2 & - y z \\
 - x z & - y z & x^2+y^2
\end{array} \right)$$

*Démonstration.* Voir le cours de Mathématiques.

### Opérateur d'inertie

$\mathcal{I}(A,S)$ est l'opérateur d'inertie du solide $S$ exprimé en $A$.
$$ \mathcal{I}(A,S):\overrightarrow{u}\mapsto\int_S\overrightarrow{AM}\wedge
(\vec{u}\wedge\overrightarrow{AM})\,\mathrm{d}m $$

Alors on a la **propriété importante**
$$ \vec{\sigma}_{A,~S/R} = \mathcal{I}(A,S) \overrightarrow{\Omega}_{S/R}
+ m\,\overrightarrow{AG} \wedge \overrightarrow{V}_{A,~S/R} $$

### Matrice d'inertie

La matrice d'inertie est la matrice associée à l'opérateur d'inertie.
Elle est symétrique réelle donc il existe une **base principale d'inertie**
où elle est diagonale et ses valeurs propres sont les **moments principaux 
d'inertie**.

Par [ce qui précède](#algebre)
$$\mathcal{I}(A,S) = \int_S M \, \mathrm{d}m$$

*À savoir faire.* Trouver la matrice d'inertie d'objets rudimentaires dans une
base bien choisie.

### Théorème de Huyghens {#huyghens}

Le théorème de Huyghens s'écrit
$$ \mathcal{I}(A, S)\vec{u} = \mathcal{I}(G, S)\vec{u}
+ m\,\overrightarrow{AG} \wedge (\vec{u} \wedge \overrightarrow{AG}) $$

Donc avec [ce qui précède](#algebre) avec
$\overrightarrow{AM}=\overrightarrow{AG}$
$$ \mathcal{I}(A, S) = \mathcal{I}(G, S) + m\,M $$

*Démonstration.* $\overrightarrow{AM} = \overrightarrow{AG}+\overrightarrow{GM}$
dans $\mathcal{I}(A, S)$.

### Moment d'inertie par rapport à une droite

On note $d$ la distance entre deux objets dans l'espace.

Le moment d'inertie par rapport à une droite $\Delta$ de vecteur directeur
$\vec{u}$ passant par $O$ est
$$ J_{(S/\Delta)}=\int_S \left(d(M,\Delta)\right)^2\,\mathrm{d}m =
\vec{u}\cdot\mathcal{I}(O, S)\vec{u} $$

Le théorème de Huyghens implique que
$$ J_{(S/\Delta)} = J_{(S/\Delta')} + m\,\left(d(\Delta,\Delta')\right)^2 $$

### Caractéristiques d'inertie

Les caractéristiques d'inertie du solide indéformable $S$ sont

* Sa masse $m$,
* Son centre d'inertie $G$,
* Son opérateur d'inertie $\mathcal{I}(\cdot,S)$.

### Méthode de résolution d'un problème

Pour trouver les paramètres du mouvement (cinématique du solide S par rapport à
R) :

* Résultante :

  * La résultante vaut $\displaystyle m\,\vec{a}_{G,\,S/R} = m\,\left.
    \frac{\mathrm{d}^2 \overrightarrow{OG}}{\mathrm{d}t^2}\right|_R$

* Moment $\vec{\delta}_{A,\,S/R}$ :

  * Si on a l'opérateur d'intertie en $G$, 
  
    1. $\displaystyle \vec{\delta}_{A,\,S/R} =
       \vec{\delta}_{G,\,S/R} + m\,\overrightarrow{AG} \wedge \vec{a}_{G,\,S/R}$
       
    2. $\displaystyle \vec{\delta}_{G,\,S/R}
       = \left. \frac{\mathrm{d}\vec{\sigma}_{G,\,S/R}}{\mathrm{d}t} \right|_R$
       
    3. $\displaystyle \vec{\sigma}_{G,\,S/R} =
       \mathcal{I}(G,S) \vec{\Omega}_{S/R}$

  * Sinon,
  
    1. $\displaystyle \vec{\delta}_{A,\,S/R}
       = \left. \frac{\mathrm{d}\vec{\sigma}_{A,\,S/R}}{\mathrm{d}t} \right|_R
       + m\,\left.\frac{\mathrm{d}\overrightarrow{OA}}{\mathrm{d}t}\right|_R
       \wedge\vec{V}_{G,\,S/R}$
       
    2. $\displaystyle \vec{\sigma}_{A,\,S/R}
       = \mathcal{I}(A,S) \vec{\Omega}_{S/R}
       + m\,\overrightarrow{AG} \wedge \vec{V}_{A,\,S/R}$

### Théorèmes de Guldin (hors programme)

<!-- TODO Peut-on dire "solide homogène" ? -->
<!-- TODO Figure -->

**Pour trouver une aire par révolution d'un arc.**
Soit $(AB)$ un arc plan dans $(O,\vec{x},\vec{y})$ de longueur $L$ et de
centre d'inertie $G$.
$$\mathcal{A} = L \times \mathrm{longueur~du~cercle~decrit~par~G}$$

*Démonstration.*
Partir de $\mathcal{A} = 2 \pi \int_{(AB)} x\, \mathrm{d}L$ et introduire la
masse linéique $\rho$.

**Pour trouver un volume par révolution d'une surface.**
Soit une surface dans $(O,\vec{x},\vec{y})$ d'aire $\mathcal{A}$ et de
centre d'inertie $G$.
$$\mathcal{V} = \mathcal{A} \times \mathrm{longueur~du~cercle~decrit~par~G}$$

*Démonstration.*
Partir de $\mathcal{V} = 2 \pi \int_{S} x\, \mathrm{d}S$ et introduire la masse
linéique $\rho$.

### Cas dans un référentiel non Galiléen (hors programme)

Ce référentiel non galiléen se déplace par rapport à un référentiel galiléen.

Ainsi il faut prendre en compte les forces d'entrainement et la force de
Coriolis.

Pour plus de détail : [Introduction à la mécanique du
point](http://films-lab.univ-lille1.fr/michael/michael/Teaching_files/C2.pdf)

\newpage

## Théorème de l'énergie cinétique

### Énergie cinétique de S par rapport à R {#energiecin}

L'énergie cinétique de S par rapport à R est
$$ T(S/R) = \frac{1}{2} \int_S \overrightarrow{V}_{M,~S/R}^2 \, dm $$

### Puissance des efforts extérieurs

La puissance des efforts extérieurs sur le solide $S$ est
$${P_{e}}_{(\overline{S}\rightarrow S/R)}
= \{ \mathcal{T}_{\overline{S}/S} \}_A \otimes \{ \mathcal{V}_{S/R} \}_A$$

### Puissance des efforts intérieurs

La puissance des efforts intérieurs de l'ensemble de solide $E$ est
$$ P_{int(E)}
= \sum_{i\neq j} \{\mathcal{T}_{i/j}\}_A \otimes \{\mathcal{V}_{j/i}\}_A $$

Pour une liaison parfaite cette puissance est nulle sinon négative.

### Puissance des quantités d'accélération

La puissance des quantités d'accélération du solide $S$ est
$$ {P_{a}}_{(S/R)} = \{\mathcal{D}_{S/R}\}_B \otimes \{\mathcal{V}_{S/R}\}_B $$

Donc
$$ {P_{a}}_{(S/R)} = \frac{d T(S/R)}{dt}$$

*Démonstration.* Par le calcul en utilisant
[la définition des torseurs](#torseurs) et
[de l'énergie cinétique](#energiecin).

### Théorème de l'énergie cinétique

Aussi appelé « théorème de l'énergie/puissance » par le programme.

Pour un ensemble $E$ de solides
$$\frac{d T(E/R)}{dt} = {P_{e}}_{(\overline{E}\rightarrow E/R)} + P_{int(E)}$$

*Démonstration.*
Le PFD donne ${P_{e}}_{(\overline{S}\rightarrow S/R)} = {P_{a}}_{(S/R)}$
pour un solide. On généralise ensuite pour un ensemble de solides.

### Expression de l'énergie cinétique

$$\begin{array}{rcl}
T(S/R) & = & \frac{1}{2} m \overrightarrow{V}_{A,~S/R}^2 \\
 & & + \frac{1}{2} \vec{\Omega}_{S/R}.\mathcal{I}(A,S)\vec{\Omega}_{S/R} \\
 & & + (m \overrightarrow{AG}, \vec{V}_{A,~S/R}, \vec{\Omega}_{S/R})
\end{array}$$

*Démonstration (à savoir faire).* À partir de la définition de $T(S/R)$ et avec
[la formule de Varignon](#varignon).

*Remarque.* Le choix du point $A$ n'est important que pour le calcul. Il faut
donc le choisir astucieusement.

Il est plus astucieux parfois d'utiliser cette expression qui se montre par
calcul à partir de la définition des torseurs.
$$ T(S/R)=\frac{1}{2} \{\mathcal{C}_{S/R}\} \otimes \{\mathcal{V}_{S/R}\} $$

### Utilisation du théorème de l'énergie cinétique

#### Posologie

Théorème à utiliser sur un système régit par un seul paramètre de mouvement.
À éviter s'il existe des frottements que l'on ne souhaite pas déterminer.

#### Calcul d'une inertie équivalente

Pour calculer l'inertie équivalente de $E=1+2+3$, on écrit
$$ T(E/R)=T(1/R)+T(2/R)+T(3/R)=\frac{1}{2} I_{eq} \omega_1^2 $$

\newpage

## Mobilité, hyperstaticité

### Nombre cyclomatique

On note $\nu$ le nombre de cycles indépendants d'une chaîne fermée
complexe. Pour $L$ liaisons et $(N-1)$ pièces autres que le bâti
$$\nu = L-(N-1)$$

### Analyse cinématique

Dans le plan on peut écrire $E_c=3 \nu$ équations par la fermeture de
chaîne cinématique et dans l'espace : $$E_c=6 \nu$$

Le nombre d'inconnues cinématiques est :
$$I_c=\sum_{\mathrm{liaisons}} DDL$$

Dans le plan, $DDL_{\mathrm{liaison}} \leq 3$.

### Analyse statique

Le nombre d'équations de statique que l'on peut écrire dans l'espace est :
$$E_s = 6(N-1)$$

Le nombre d'inconnues d'effort est :
$$I_s = \sum_{\mathrm{liaison}} (6-I_{c~\mathrm{liaison}})$$

### Mobilité cinématique

Soit $r_c$ le rang du système $\{ \mathcal{V}_{S_i/S_i} \} = \{ 0 \}$.
Ainsi la mobilité cinématique est : $$m_c = I_c - r_c$$

On remarque que : $m_c = m_{\mathrm{utile}} + m_{\mathrm{interne}}$

### Déterminant caractéristique

On note $r_s$ le rang du système
$\{ \mathcal{T}_{ext/S_i} \} = \{ 0 \}$.

$E_s-r_s$ conditions doivent être vérifiées pour que le mécanisme soit
en équilibre.

### Hyperstaticité

On note $h$ l'hyperstaticité : $$h = I_s - r_s$$

En étude statique, c'est le nombre d'inconnues de liaisons en trop pour
résoudre le système.

En étude cinématique, dans une base bien choisie, c'est le nombre
d'équations $0=0$ obtenues.

Si $h=0$, alors le système est **isostatique**.

### Formule de mobilité

$$m_c - h = I_c - E_c = E_s - I_s$$

Le plus souvent $m_c$ est évident et alors la méthode cinématique est directe :
$$h = m_c - (I_c - E_c)$$

*Démonstration.*
Voir le cours.

## Équilibrage

### Solide équilibré

Un solide en rotation autour d'un axe fixe est dit équilibré si les
actions qu'il exerce sur le bâti qui le supporte sont constantes au
cours du temps.

### Théorème

Un solide en rotation autour d'un axe fixe est équilibré si seulement si :

-   Équilibrage statique : centre d'inertie $G \in$ axe rotation,

-   Équilibrage dynamique : l'axe de rotation est un axe principal
    d'inertie.

### Question de cours

On peut équilibrer avec une unique masse si la bonne
composante de la matrice d'inertie est nulle. Savoir refaire pour
équilibrer avec deux masses.

\newpage

# Logique séquentielle

## Circuits logiques

### Bascule RS

![Exemple de réalisation : Déclenchement
prioritaire](assets/PSI_si_logique-bascule_RS_declenchement_prio)

![Exemple de réalisation : Enclenchement
prioritaire](assets/PSI_si_logique-bascule_RS_enclenchement_prio)

\newpage
## Diagrammes SysML

<!--
Un diagramme des séquences montre l'enchaînement séquentiel des différentes
interactions.
Il contient **des lignes de vie** et des flèches représentant les
interactions, ainsi que **des fragments combinés**.

Un diagramme d'états peut contenir des états composites. Il faut accéder à tous
les points de terminaison pour sortir de l'état composite.


![Diagramme d'états, stm](assets/PSI_si_logique-diagramme_etats.png)

![Diagramme d'états avec un état
composite](assets/PSI_si_logique-diagramme_etats_composite.png)

![Diagramme des séquences, sd](assets/PSI_si_logique-diagramme_sequences.png)

\newpage

![](assets/PSI_si_logique-sysml)

\newpage
-->

### Architecture des systèmes

![Diagramme des blocs internes (ibd)](assets/PSI_si_logique-sysml-ibd)

![Chaîne d'information et d'énergie
(à savoir faire)](assets/PSI_si_logique-chaine_info)

Le diagramme de blocs internes se compose de flux de matière, d'énergie et
d'information.

Voici quelques exemples classiques d'architectures :

* Pour un système utilisant un moteur Courant-Continu :
  1. **Alimenter** : batterie ou { transformateur, redresseur (pont de diodes)
     et filtrage },
  2. **Distribuer** : pont en H,
  3. **Convertir** : moteur CC,
  4. **Transmettre** : réducteur, poulie-couroie...
  5. **Agir** : déplacement du robot...

* Pour un système pneumatique :
  1. **Alimenter** : tête de ligne qui reçoit l'énergie pneumatique d'un
     compresseur,
  2. **Distribuer** : distributeur ou électrovanne,
  3. **Adapter** : réducteur de débit, bloqueur...
  4. **Convertir** : actionneur pneumatique comme un vérin, une ventouse...
  5. **Agir** : aspiration, mouvement...

\newpage

# Hydraulique et pneumatique de puissance

Ce chapitre est hors programme en PSI mais permet de comprendre le
fonctionnement de certains systèmes.

## Pneumatique de puissance

### Distribution de l'énergie

Avant chaque système il y a une tête de ligne, aussi appelée une unitée de
conditionnement de l'air FRL. Il est composé de :

<!-- TODO Mettre des figures pour illustrer chaque composant -->

* **Un filtre** : assèche l'air et filtre les impuretés, 
* **Un manomètre régulateur** : régule/règle la pression,
* **Un lubrificateur** : évite la corrosion et améliore le glissement.

<!-- TODO À finir -->


