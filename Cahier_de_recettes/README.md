# Mon cahier de recettes

Ce projet contient le code source pour générer le cahier de recettes écrit par 
Alexandre IOOSS.

Des erreurs sont probablement présentes.
Si c'est le cas vous pouvez ouvrir un rapport d'erreur.

## Comment compiler ?

Dépendances nécessaires :

* [Pandoc](https://pandoc.org/),
* Une installation LaTeX avec de préférence **XeTeX**.

### Sous Linux

Sur une distribution basée sur Ubuntu/Debian vous pouvez installer les
dépendances avec les commandes suivantes.

```bash
sudo apt install pandoc poppler-utils make texlive-xetex
```

Pour compiler les fiches, placez-vous dans le dossier et exécutez `make`.
Les fichiers générés sont dans le dossier *build*.

Si vous rencontrez des difficultés je vous recommande d'utiliser le binaire
officiel de Pandoc (compilé en statique) qui est plus récent.

## Licences

La police de caractère **TeX Gyre Bonum** est sous licence
[GUST Font Source Li­cense (GFSL)](https://ctan.org/license/gfsl).

Ces fiches sont sous licence [Creative Common BY-SA 4.0](LICENCE.md).

