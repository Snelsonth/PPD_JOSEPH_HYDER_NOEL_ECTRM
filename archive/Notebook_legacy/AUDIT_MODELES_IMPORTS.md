# Audit modeles + imports (PPD_2026)

## 1) Modeles detectes dans le repo

- `ECTRM_source` (ECRTM, papier cible ICML 2023)
- `ETM_source` (Embedded Topic Model)
- `NSTM_source` (Neural Sinkhorn Topic Model)
- `DVAE_source` (Dirichlet VAE variants)
- `HyperMiner_source` (HyperMiner / hyperbolic topic modeling)
- `Notebook/nb-fastopic-ppd.ipynb` (FASTopic, deja integre cote notebook)

## 2) Norme observee dans tes notebooks (`Notebook/`)

Pattern a garder pour chaque nouveau notebook modele:

1. Cell `Install` (pip minimal, Kaggle-safe, sans casser torch/cuda si possible).
2. Cell `Imports + versions + GPU check`.
3. Cell `Detection environnement` (`IS_KAGGLE`, `PROJECT_ROOT`).
4. Cell `Config globale` (`TARGET_DATASETS`, `K_LIST`, `RANDOM_SEED`, hyperparams modele).
5. Cell `Resolution des paths` (datasets + sortie).
6. Cell `Verification pre-run` (presence des fichiers requis).
7. Cell `Training loop` sur dataset x K.
8. Cell `Export .mat harmonise`.
9. Cell `Recap fichiers` + (optionnel) metriques TD/Purity/NMI + topics texte.

Schema `.mat` cible (commun):

```python
scipy.io.savemat(
    out_path,
    {
        "beta": beta.astype(np.float32),
        "train_theta": train_theta.astype(np.float32),
        "test_theta": test_theta.astype(np.float32),
    },
)
```

## 3) Reference par modele

### ECRTM (`ECTRM_source/ECRTM`)

- Entree training: `ECTRM_source/ECRTM/run.py`
- Configs: `ECTRM_source/ECRTM/configs/model/ECRTM_*.yaml`
- Data attendue: `train_bow.npz`, `test_bow.npz`, `train_labels.txt`, `test_labels.txt`, `vocab.txt`, `word_embeddings.npz`
- Sortie native: `*_params.mat` avec `beta`, `train_theta`, `test_theta`

Imports notebook (recommandes):

```python
import os
import random
from types import SimpleNamespace

import numpy as np
import scipy.io
import scipy.sparse as sp
import torch
import yaml
from torch.utils.data import DataLoader, TensorDataset

from models.ECRTM import ECRTM
from models.ECR import ECR
```

Packages clefs:
- `torch`
- `numpy`
- `scipy`
- `pyyaml`
- `scikit-learn` (eval)
- `gensim` (preprocess)

### ETM (`ETM_source`)

- Entree training: `ETM_source/main.py`
- Classe modele: `ETM_source/etm.py`
- Data utilitaire: `ETM_source/data.py`
- Sortie native: checkpoint torch (pas de `.mat` harmonise direct)

Imports notebook (recommandes):

```python
import os
import random
from pathlib import Path

import numpy as np
import scipy.io
import torch
from torch import nn, optim
from torch.nn import functional as F

import data
from etm import ETM
from utils import nearest_neighbors, get_topic_coherence, get_topic_diversity
```

Optionnel (si embeddings FastText):

```python
from gensim.models.fasttext import FastText as FT_gensim
```

Packages clefs:
- `torch`
- `numpy`
- `scipy`
- `gensim`
- `scikit-learn`
- `matplotlib`
- `tqdm`

Note adaptation:
- Ajouter une cellule d'export `.mat` (extraire `beta=model.get_beta()`, inferer `train_theta/test_theta` par batch).

### NSTM (`NSTM_source`)

- Entree training: `NSTM_source/nstm.py`
- Data attendue: `datasets/<name>/data.mat` avec `wordsTrain`, `wordsTest`, `labelsTrain`, `labelsTest`, `vocabulary`, `embeddings`
- Sortie native: `save.mat` avec `phi`, `train_theta`, `test_theta`

Imports notebook (recommandes):

```python
import os
import sys
import glob
import time
import subprocess
from pathlib import Path

import numpy as np
import scipy.io
import scipy.sparse as sp
import tensorflow as tf
from tqdm import tqdm
```

Si execution interne du code NSTM (pas juste subprocess):

```python
from auto_diff_sinkhorn import sinkhorn_tf
from utils import load_data, batch_indices, print_topics, set_logger, save_flags, get_doc_topic
```

Packages clefs:
- `tensorflow==1.15.*` (ou patch compat TF2)
- `numpy<=1.19.5` (contrainte mentionnee par le repo)
- `scipy`
- `tqdm`

Note adaptation:
- Normaliser la sortie via `beta = phi` puis sauvegarder `.mat` harmonise.

### DVAE (`DVAE_source`)

- Entrees training: `nvdm_dirichlet_rsvi.py`, `nvdm_dirichlet_invCDF.py`, `nvdm_dirichlet_weibull.py`, `nvdm_dirichlet_implicitGradients.py`
- Data attendue: format `.feat` + `vocab.new` (ex: `DVAE_source/data/20news`)
- Sortie native: checkpoints TF (`models/improved_model*`), pas de `.mat` harmonise direct

Imports notebook (recommandes):

```python
import os
import sys
import math
import argparse
import pickle

import numpy as np
import scipy.io
import tensorflow as tf

import utils as utils
```

Specifique variante implicite:

```python
import tensorflow_probability as tfp
```

Packages clefs:
- `tensorflow==1.15.*`
- `numpy` compatible TF1
- `tensorflow-probability` (uniquement implicit gradients)

Note adaptation:
- Ajouter extraction de `phi` + inference theta train/test, puis `savemat` harmonise.

### HyperMiner (`HyperMiner_source`)

- Entrees training: `train_clustering.py` et `train_quality.py`
- Configs args: `HyperMiner_source/config.py`
- Data attendue: dataset pickle (default: `./data/20NG/20news_groups.pkl`)
- Sortie native: checkpoints `.pth` + logs/topics, pas de `.mat` harmonise direct

Imports notebook (recommandes):

```python
import os
import time
import datetime
import logging
import pickle

import numpy as np
import scipy.io
import scipy.sparse as sp
import torch

from config import parser
from models.etm import ETM
from models.sawetm import SawETM
from models.hyperminer import HyperETM, HyperMiner, HyperMinerKG
from utils.data_util import get_data_loader
from utils.train_util import get_dir_name, convert_to_coo_adj, load_glove_embeddings, visualize_topics
from utils.eval_util import text_clustering, topic_diversity, topic_coherence
```

Packages clefs:
- `torch`
- `numpy`
- `scipy`
- `scikit-learn`
- `networkx` (utils/hyperbolicity)
- `nltk` (utils/build_graph)

Note adaptation:
- Construire `beta` depuis `model.get_phi()` (ou produit cumulatif des couches selon protocole) + inference theta par document, puis export `.mat` harmonise.

### FASTopic (deja present dans `Notebook/nb-fastopic-ppd.ipynb`)

Imports notebook utilises:

```python
import os
import random
import numpy as np
import torch
import scipy.io
import scipy.sparse as sp
import yaml

from fastopic import FASTopic
```

Packages clefs:
- `fastopic`
- `topmost`
- `torch`
- `numpy`
- `scipy`
- `pyyaml`

## 4) Etat actuel pour la reproduction article + export `.mat`

- Pret directement: `ECTRM`, `NSTM`, `FASTopic` (notebooks deja bien avances).
- A harmoniser pour comparaison finale: `ETM`, `DVAE`, `HyperMiner` (ajouter cellule export `.mat` standard).

## 5) Ordre recommande pour la suite (sans GPU local)

1. Finaliser notebooks `ETM`, `DVAE`, `HyperMiner` avec meme norme que `nb-nstm-ppd.ipynb`.
2. Verifier generation de `.mat` standard pour K = 20, 50, 100.
3. Lancer sur Kaggle (un notebook par modele), puis centraliser dans `Sortie_mat`.
4. Faire notebook final de fusion des resultats et metriques comparatives.
