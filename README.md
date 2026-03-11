# PPD_2026_ECRTM

Projet universitaire de comparaison et de reproduction de modeles de topic modeling, avec un focus principal sur ECRTM.

## Objectif

Le depot sert a :
- reproduire les resultats du modele ECRTM ;
- comparer ECRTM a plusieurs baselines du domaine ;
- tester des variantes experimentales comme AMP et UMAP ;
- centraliser les notebooks, les sorties et les references utiles au rapport.

## Structure du projet

```text
PPD_2026_ECRTM/
|- Article/                  # papiers et references PDF
|- data/                     # jeux de donnees
|- models/                   # composants modeles annexes
|- notebook/
|  |- baselines/             # notebooks actifs
|  |- legacy_palmetto/       # anciens notebooks conserves
|- output/                   # resultats exportes
|- Projet_PPD/               # ancien espace de travail conserve
|- tools/                    # scripts utilitaires
|- .gitignore
`- README.md
```

## Dossier de travail principal

Les notebooks actifs sont dans `notebook/baselines/`.

Notebooks principaux :
- `ECRTM.ipynb`
- `ECTRM_AMP.ipynb`
- `ECTRM_UMAP.ipynb`
- `Fastopic.ipynb`
- `Fast_topic_avec_UMAP.ipynb`

Autres baselines presentes :
- `DVAE.ipynb`
- `ETM_correct.ipynb`
- `HYPERMINER.ipynb`
- `K-Means.ipynb`
- `LDA_V2.ipynb`
- `NSTM.ipynb`
- `WeTe.ipynb`
- `WLDA.ipynb`

## Jeux de donnees

Les jeux de donnees principaux sont stockes dans `data/` :
- `20NG`
- `AGNews`
- `IMDB`
- `YahooAnswer`

Selon le notebook, on retrouve generalement :
- `train_bow.npz`
- `test_bow.npz`
- `train_labels.txt`
- `test_labels.txt`
- `vocab.txt`
- `word_embeddings.npz`

## Resultats

Les sorties des notebooks sont enregistrees dans `output/`, avec un sous-dossier par modele.

Exemples :
- `output/ECRTM/`
- `output/ECTRM_AMP/`
- `output/Umap_ECTRM/`
- `output/ETM/`
- `output/NSTM/`

On y trouve en general :
- des fichiers `.mat` ;
- des CSV de metriques ;
- des CSV de temps d'execution ;
- des fichiers intermediaires pour le calcul de `C_V`.

## Execution locale

1. Verifier que les donnees sont presentes dans `data/`.
2. Ouvrir le notebook voulu dans `notebook/baselines/`.
3. Executer les cellules dans l'ordre.
4. Recuperer les sorties dans `output/`.

## Execution sur Kaggle

1. Importer le notebook souhaite depuis `notebook/baselines/`.
2. Ajouter les datasets necessaires comme inputs.
3. Activer Internet si le notebook doit cloner automatiquement un depot source.
4. Executer les cellules dans l'ordre.
5. Recuperer les fichiers exportes dans `/kaggle/working/Sortie_mat/`.

## Depots sources utiles

- ECRTM : `https://github.com/bobxwu/ecrtm`
- FASTopic : `https://github.com/bobxwu/FASTopic`
- ETM : `https://github.com/adjidieng/ETM`
- NSTM : `https://github.com/ethanhezhao/NeuralSinkhornTopicModel`
- WeTe : `https://github.com/wds2014/WeTe`
- HyperMiner : `https://github.com/NoviceStone/HyperMiner`
- DVAE : `https://github.com/sophieburkhardt/dirichlet-vae-topic-models`

## Remarques

- `notebook/legacy_palmetto/` contient des versions anciennes conservees pour reference.
- `Projet_PPD/` est garde comme archive de travail.
- Le dossier actif pour les experiences courantes est `notebook/baselines/`.
