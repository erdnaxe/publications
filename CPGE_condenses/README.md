# Condensés de cours de PSI en CPGE

Ce projet contient le code source pour générer les condensés de cours écrits par 
Alexandre IOOSS.

Elles correspondent au cours de PCSI-PSI exigible au concours 2017-2018 des
écoles d'ingénieurs françaises.

Ces fiches ont été écrites par un étudiant donc des erreurs sont probablement
présentes. Si c'est le cas vous pouvez ouvrir un rapport d'erreur.

## Sources

La structure du cours correspond le plus souvent à l'ordre chronologique des
cours au fur et à mesure de l'année. Mais le contenu a été travaillé à partir de
ces différentes sources :

* [Le programme officiel](http://eduscol.education.fr/sti/sites/eduscol.education.fr.sti/files/textes/977-programme-pcsi-si.pdf)

* [WikiMéca](https://wikimeca.org/),
  * [Abaque de Black-Nichols](https://wikimeca.org/index.php?title=Fichier:Abaque_de_Black-Nichols.svg),

* Des articles présents sur [Wikipédia](https://www.wikipedia.org/) et
  [Wikiversity](https://www.wikiversity.org/).

* UNIVERSITE DES SCIENCES ET TECHNOLOGIES DE LILLE
  * [Chapitre 2 : Introduction à la mécanique du point](http://films-lab.univ-lille1.fr/michael/michael/Teaching_files/C2.pdf)
  * [Chapitre 3 : Rappels de cinématique du solide](http://films-lab.univ-lille1.fr/michael/michael/Teaching_files/C3.pdf)

* L'extrait gratuit du livre de cours *Sciences industrielles de l'ingénieur
  MPSI-PCSI-PTSI* de *VUIBERT PRÉPAS*.

Toutes les illustrations ont été redessinées sur l'outil
[Inkscape](https://inkscape.org/) pour être vectorielles.

Si vous constatez un problème d'attribution ou une violation de licence,
veuillez me contacter et je supprimerai le contenu en faute si c'est le cas.

## Comment compiler ?

Dépendances nécessaires :

* [Pandoc](https://pandoc.org/),
* [pandoc-fignos](https://github.com/tomduck/pandoc-fignos),
* Une installation LaTeX avec de préférence **XeTeX**.

### Sous Linux

Sur une distribution basée sur Ubuntu/Debian vous pouvez installer les
dépendances avec les commandes suivantes.

```bash
sudo apt install pandoc poppler-utils make texlive-xetex
pip install pandoc-fignos
```

Pour compiler les fiches, placez-vous dans le dossier et exécutez `make`.
Les fichiers générés sont dans le dossier *build*.

Si vous rencontrez des difficultés je vous recommande d'utiliser le binaire
officiel de Pandoc (compilé en statique) qui est plus récent.

## Licences

La police de caractère **TeX Gyre Pagella** est sous licence
[GUST Font Source Li­cense (GFSL)](https://ctan.org/license/gfsl).

Ces fiches sont sous licence [Creative Common BY-SA 4.0](LICENCE.md).

