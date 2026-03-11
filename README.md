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
|- output/                   # resultats exportes
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
- `FAST_TOPIC_UMAP.ipynb`

Autres baselines presentes :
- `DVAE.ipynb`
- `ETM_correct.ipynb`
- `HYPERMINER.ipynb`
- `K-Means.ipynb`
- `LDA.ipynb`
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
- WeTe : `https://github.com/BoChenGroup/WeTe`
- HyperMiner : `https://github.com/NoviceStone/HyperMiner`
- DVAE : `https://github.com/sophieburkhardt/dirichlet-vae-topic-models`
- WLDA : `https://github.com/jinmang2/W-LDA` 
- LDA : `https://github.com/akashii99/Topic-Modelling-with-Latent-Dirichlet-Allocation`
- Kmeans  `https://aclanthology.org/2020.emnlp-main.135/` présence d'un lien vers un zip 

## Remarques
- Le dossier actif pour les experiences courantes est `notebook/baselines/`.


## Citations

Les references suivantes renvoient directement vers les pages officielles des revues, proceedings ou archives scientifiques.

### Modeles principaux

- `ECRTM` : Wu, X. et al. *Effective Neural Topic Modeling with Embedding Clustering Regularization*. [arXiv 2306.04217](https://arxiv.org/abs/2306.04217)
- `FASTopic` : Wu, X. et al. *FASTopic: A Fast, Adaptive, Stable and Transferable Topic Modeling Paradigm*. [arXiv 2405.17978](https://arxiv.org/abs/2405.17978)

### Baselines

- `DVAE` : Burkhardt, S. and Kramer, S. *Decoupling Sparsity and Smoothness in the Dirichlet Variational Autoencoder Topic Model*. Journal of Machine Learning Research, 2019. [Article officiel](https://jmlr.org/papers/v20/18-569.html)
- `LDA` : Blei, D. M., Ng, A. Y. and Jordan, M. I. *Latent Dirichlet Allocation*. Journal of Machine Learning Research, 2003. [Article officiel](https://www.jmlr.org/papers/v3/blei03a.html)
- `K-Means topics` : Sia, S., Dalmia, A. and Mielke, S. J. *Tired of Topic Models? Clusters of Pretrained Word Embeddings Make for Fast and Good Topics too!*. EMNLP 2020. [Article officiel](https://aclanthology.org/2020.emnlp-main.135/)
- `WLDA` : Nan, F., Ding, R., Nallapati, R. and Xiang, B. *Topic Modeling with Wasserstein Autoencoders*. ACL 2019. [Article officiel](https://aclanthology.org/P19-1640/)
- `ETM` : Dieng, A. B., Ruiz, F. J. R. and Blei, D. M. *Topic Modeling in Embedding Spaces*. Transactions of the Association for Computational Linguistics, 2020. [Article officiel](https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00325/96463/Topic-Modeling-in-Embedding-Spaces)
- `HyperMiner` : Xu, Y., Wang, D., Chen, B., Lu, R., Duan, Z. and Zhou, M. *HyperMiner: Topic Taxonomy Mining with Hyperbolic Embedding*. NeurIPS 2022. [Article officiel](https://proceedings.neurips.cc/paper_files/paper/2022/file/cc7e4c6e6c8ef1e2fc4dadaf1f78cc50-Paper-Conference.pdf)
- `NSTM` : Zhao, H., Phung, D., Huynh, V., Le, T. and Buntine, W. *Neural Topic Model via Optimal Transport*. arXiv 2020. [Article officiel](https://arxiv.org/abs/2008.13537)
- `WeTe` : Wang, D., Guo, D., Zhao, H., Zheng, H., Tanwisuth, K., Chen, B. and Zhou, M. *Representing Mixtures of Word Embeddings with Mixtures of Topic Embeddings*. arXiv 2022. [Article officiel](https://arxiv.org/abs/2203.01570)

### BibTeX minimal

```bibtex
@article{burkhardt2019decoupling,
  title={Decoupling Sparsity and Smoothness in the Dirichlet Variational Autoencoder Topic Model},
  author={Burkhardt, Sophie and Kramer, Stefan},
  journal={Journal of Machine Learning Research},
  volume={20},
  number={131},
  pages={1--27},
  year={2019}
}

@article{blei2003latent,
  title={Latent Dirichlet Allocation},
  author={Blei, David M. and Ng, Andrew Y. and Jordan, Michael I.},
  journal={Journal of Machine Learning Research},
  volume={3},
  pages={993--1022},
  year={2003}
}

@inproceedings{sia2020tired,
  title={Tired of Topic Models? Clusters of Pretrained Word Embeddings Make for Fast and Good Topics too!},
  author={Sia, Suzanna and Dalmia, Ayush and Mielke, Sabrina J.},
  booktitle={Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP)},
  pages={1728--1736},
  year={2020}
}

@inproceedings{nan2019topic,
  title={Topic Modeling with Wasserstein Autoencoders},
  author={Nan, Feng and Ding, Ran and Nallapati, Ramesh and Xiang, Bing},
  booktitle={Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics},
  pages={6345--6381},
  year={2019}
}

@article{dieng2020topic,
  title={Topic Modeling in Embedding Spaces},
  author={Dieng, Adji B. and Ruiz, Francisco J. R. and Blei, David M.},
  journal={Transactions of the Association for Computational Linguistics},
  volume={8},
  pages={439--453},
  year={2020}
}

@inproceedings{xu2022hyperminer,
  title={HyperMiner: Topic Taxonomy Mining with Hyperbolic Embedding},
  author={Xu, Yi and Wang, Dongsheng and Chen, Bo and Lu, Ruiying and Duan, Zhibin and Zhou, Mingyuan},
  booktitle={Advances in Neural Information Processing Systems},
  volume={35},
  pages={31557--31570},
  year={2022}
}

@article{zhao2020neural,
  title={Neural Topic Model via Optimal Transport},
  author={Zhao, He and Phung, Dinh and Huynh, Viet and Le, Trung and Buntine, Wray},
  journal={arXiv preprint arXiv:2008.13537},
  year={2020}
}

@article{wang2022representing,
  title={Representing Mixtures of Word Embeddings with Mixtures of Topic Embeddings},
  author={Wang, Dongsheng and Guo, Dandan and Zhao, He and Zheng, Huangjie and Tanwisuth, Korawat and Chen, Bo and Zhou, Mingyuan},
  journal={arXiv preprint arXiv:2203.01570},
  year={2022}
}
```
