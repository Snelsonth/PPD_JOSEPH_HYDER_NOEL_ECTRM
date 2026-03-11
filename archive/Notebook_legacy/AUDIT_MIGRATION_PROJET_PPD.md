# Audit migration notebook -> Gensim C_V

## Resultat global
- Migration realisee sur les notebooks modeles (`Projet_PPD/Projet_PPD/notebook` + notebooks modeles de `notebook_tester`).
- Dependance Palmetto/Java supprimee des notebooks modeles actifs.
- Chemins absolus Windows remplaces par detection dynamique de `PROJECT_ROOT` (compat local + Kaggle).

## Etat detaille
| Notebook | Palmetto refs | Gensim C_V refs | Hardcoded paths | Java/subprocess | Statut |
|---|---:|---:|---:|---:|---|
| `Projet_PPD/Projet_PPD/notebook/DVAE.ipynb` | 0 | 3 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/ECRTM.ipynb` | 0 | 3 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/ETM.ipynb` | 0 | 3 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/HYPERMINER.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/K-Means.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/NSTM.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/WeTe.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |
| `Projet_PPD/Projet_PPD/notebook/WLDA.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |
| `notebook_tester/code 20NG.ipynb` | 19 | 0 | 21 | 3 | Legacy a migrer (archive) |
| `notebook_tester/code AG NEWS.ipynb` | 16 | 0 | 24 | 3 | Legacy a migrer (archive) |
| `notebook_tester/code IMDB.ipynb` | 17 | 0 | 22 | 3 | Legacy a migrer (archive) |
| `notebook_tester/code YahooAnswer.ipynb` | 16 | 0 | 24 | 3 | Legacy a migrer (archive) |
| `notebook_tester/DVAE_correct (1).ipynb` | 0 | 3 | 0 | 0 | Nettoye (Gensim) |
| `notebook_tester/ETM_correct.ipynb` | 0 | 3 | 0 | 0 | Nettoye (Gensim) |
| `notebook_tester/nb-fastopic-ppd-v2.ipynb` | 0 | 0 | 0 | 0 | Partiellement nettoye |
| `notebook_tester/WeTe.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |
| `notebook_tester/WLDA.ipynb` | 0 | 4 | 0 | 0 | Nettoye (Gensim) |

## Decision operationnelle
1. Executer en priorite les notebooks de `Projet_PPD/Projet_PPD/notebook` (base principale).
2. Utiliser `notebook_tester` uniquement pour `DVAE_correct (1)`, `ETM_correct`, `WeTe`, `WLDA`, `nb-fastopic-ppd-v2`.
3. Laisser `notebook_tester/code 20NG|AG NEWS|IMDB|YahooAnswer` en archive, ou migrer plus tard si necessaire.
