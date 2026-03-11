# Verification notebooks Kaggle (point-par-point)

Date: 2026-02-19

Objectif: executer les notebooks sur Kaggle avec les 4 datasets (`20NG`, `AGNews`, `IMDB`, `YahooAnswer`) et obtenir des metriques comparables au papier ECRTM.

## Datasets (source unique)

Source retenue pour tous les modeles: `ECTRM_source/data/<dataset>` avec:
- `train_bow.npz`
- `test_bow.npz`
- `train_labels.txt`
- `test_labels.txt`
- `vocab.txt`
- `word_embeddings.npz`

Verification locale:
- 20NG: train `(11314, 5000)`, test `(7532, 5000)`, embeddings `(5000, 200)`
- AGNews: train `(10000, 5000)`, test `(2500, 5000)`, embeddings `(5000, 200)`
- IMDB: train `(25000, 5000)`, test `(25000, 5000)`, embeddings `(5000, 200)`
- YahooAnswer: train `(10000, 5000)`, test `(2500, 5000)`, embeddings `(5000, 200)`

## Notebook checks

### `Notebook/nb-ectrm-ppd.ipynb`
- Statut: corrige pour Kaggle.
- Action: cellules locales hardcodees (`/Users/hydersidra/...`, Palmetto local) desactivees pour eviter les erreurs en `Run all`.
- Architecture: ECRTM officiel via `models/ECRTM.py` + `models/ECR.py`.
- Hyperparams: YAML du repo ECRTM (`ECRTM_*.yaml`).
- Sortie: `.mat` standard (`beta`, `train_theta`, `test_theta`).

### `Notebook/nb-nstm-ppd.ipynb`
- Statut: syntaxe corrigee (cellule metriques tronquee reparée).
- Architecture: NSTM officiel (`nstm.py`) avec conversion auto des datasets vers `data.mat` attendu.
- Hyperparams: alignes NSTM avec options centralisees.
- Sortie normalisee: `phi -> beta`, puis `.mat` standard.
- Metriques: `TD`, `Purity`, `NMI` + CSV.

### `Notebook/nb-fastopic-ppd.ipynb`
- Statut: compatible Kaggle.
- Architecture: API officielle FASTopic.
- Sortie: `.mat` harmonise.

### `Notebook/nb-etm-ppd.ipynb`
- Statut: cree et aligne.
- Architecture: classe `ETM` officielle (`ETM_source/etm.py`).
- Hyperparams:
  - `epochs=100` (default)
  - `epochs_20NG=150` (alignement README ETM)
  - `batch_size=1000`
  - `lr=0.005`
  - `weight_decay=1.2e-6`
- Preprocess: BOW sparse + normalisation document en entree de l'encodeur.
- Sortie: `.mat` standard + fichiers topics texte.
- Metriques: `TD_top25`, `Purity`, `NMI` + CSV.

### `Notebook/nb-wete-ppd.ipynb`
- Statut: cree et aligne.
- Architecture: `WeTe_source/WeTe/model.py` (InferNet + cout transport + terme TM).
- Hyperparams (alignes source WeTe):
  - `epochs=500`
  - `batch_size=500`
  - `lr=1e-2`
  - `beta=0.5`
  - `epsilon=1.0`
- Preprocess: conversion BOW -> liste de tokens (comme le code WeTe original attend).
- Sortie: `phi.T` comme `beta`, + `train_theta`/`test_theta` en `.mat`.
- Metriques: `TD_top25`, `Purity`, `NMI` + CSV.

### `Notebook/nb-hyperminer-ppd.ipynb`
- Statut: cree et aligne pour pipeline unifie.
- Architecture: `HyperMiner_source/models/hyperminer.py` (variant hyperbolique de SawETM).
- Hyperparams (alignes config HyperMiner):
  - `epochs=300`
  - `batch_size=200`
  - `lr=1e-2`
  - `weight_decay=1e-5`
  - `hidden_size=300`
  - `manifold=PoincareBall`, `c=-0.01`
- Preprocess: BOW sparse vers mini-batches torch.
- Sortie: `beta` depuis `phi` couche 1 (`VxK -> KxV`) + theta train/test.
- Metriques: `TD_top25`, `Purity`, `NMI` + CSV.

## Metriques du papier (reference)

Baselines consideres dans le papier (hors ablation DKM):
- LDA, KM, DVAE, WLDA, ETM, HyperMiner, NSTM, WeTe.

References texte:
- `Article/2306.04217v1.txt:676` a `Article/2306.04217v1.txt:693`.

Pour comparaison pratique notebook:
- comparer `TD_top25`, `Purity`, `NMI` par dataset et K (50 / 100 d'abord).
- verifier tendance globale attendue: ECRTM devrait rester meilleur ou parmi les meilleurs.

## Validation technique effectuee

- Verification JSON des notebooks: OK
- Verification syntaxe Python de toutes les cellules code (`nb-*-ppd.ipynb`): OK
- Aucune reinstallation de `torch` ajoutee dans ces notebooks (important Kaggle GPU).

## Limites connues

- Verification "metriques proches du papier" necessite execution complete sur Kaggle (GPU + runtime long).
- Les ecarts mineurs restent possibles selon seed, runtime, version libs et temps d'entrainement.
