# co-aff-align

Script d'alignement des affiliations Conditor avec le RNSR.

## Installation

```bash
npm i
```

## Configuration

> :warning: Attention, comme dans toute utilisation de
> [@ezs/conditor](https://inist-cnrs.github.io/ezs/#/plugin-conditor), il faut
> créer dans le répertoire d'où le script est lancé (ou plus vers la racine) un
> fichier `.env`.
>
> Seuls les scripts utilisant la commande
> [`conditorScroll`](https://inist-cnrs.github.io/ezs/#/plugin-conditor?id=conditorscroll)
> doivent y placer une variable `CONDITOR_TOKEN` contenant un token Conditor
> valide.

### Usage

#### affAlign.ini

```bash
npx ezs scripts/affAlign.ini < data/10-notices-conditor-hal.json
```

Ce script prend un tableau JSON de documents Conditor, et ajoute une clé
`[].authors[].affiliations[].conditorRnsr[]`, contenant les identifiants RNSR
repérés grâce au champ `address` d'une affiliation d'auteur et à l'année de
publication du document, `xPublicationDate`.

#### computeRecall.ini

```bash
$ npx ezs scripts/computeRecall.ini < data/10-notices-conditor-hal.json
[{
    "correct": 8,
    "total": 11,
    "recall": 0.7272727272727273
}]
```

Ce script fait la même chose que [affAlign.ini](#affalignini), et compte le nombre
d'identifiants RNSR déjà fourni dans la clé `rnsr` qui sont aussi retrouvés dans
`conditorRnsr`, le nombre total d'éléments retrouvés dans `conditorRnsr`, et
fournit le taux de rappel dans `recall`.
