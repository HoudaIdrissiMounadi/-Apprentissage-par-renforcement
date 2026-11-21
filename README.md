# Apprentissage par renforcement

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/HoudaIdrissiMounadi/-Apprentissage-par-renforcement/blob/main/RL.ipynb)

Travaux pratiques du module **Technologies IA** (ENSA Fès, ILIA2) : TP4, apprentissage par renforcement (RL) sur l'environnement `CartPole-v1`.

## Contenu du dépôt

| Fichier | Description |
|---|---|
| `RL.ipynb` | Notebook Google Colab exécuté (code, sorties, graphiques, vidéos) |
| `Rapport_TP4_RL.docx` | Rapport du TP : méthodes, résultats, discussion, conclusion |
| `README.md` | Ce fichier |

## Outils

- Python, Google Colab
- Gymnasium (environnement `CartPole-v1`)
- Stable-Baselines3 : PPO, A2C, DQN
- Ray RLlib : PPO avec 1 worker

## Ce que fait le notebook

1. Découverte de Gymnasium et agent aléatoire (référence).
2. Exemple 1 du sujet : PPO sur 10 000 pas, test sur un épisode.
3. Exemple 2 du sujet : test sur 5 épisodes avec courbe des récompenses.
4. Évaluation sur 20 épisodes et courbe d'apprentissage (50 000 pas).
5. Effet du nombre de pas d'entraînement.
6. Comparaison PPO / A2C / DQN.
7. Entraînement avec Ray RLlib.
8. Comparaison conceptuelle des frameworks (SB3, RLlib, Coach, Dopamine) et réponse à la question du TP.

Sur Colab, il n'y a pas d'écran : `render_mode="human"` est remplacé par `render_mode="rgb_array"` avec enregistrement de vidéos affichées dans le notebook.

## Résultats principaux

Une seule graine (`seed=42`) par configuration. Le score maximal de CartPole-v1 est 500.

| Expérience | Récompense |
|---|---|
| Agent aléatoire (20 épisodes) | 19,4 ± 9,6 |
| Exemple 1 : PPO 10 000 pas, 1 épisode de test | 500 |
| Exemple 2 : PPO 10 000 pas, 5 épisodes de test | 190, 500, 500, 500, 500 |
| PPO 50 000 pas, évaluation sur 20 épisodes | 500 ± 0 |

**Effet du budget d'entraînement (PPO, évaluation sur 20 épisodes)**

| Pas | Récompense moyenne |
|---|---|
| 5 000 | 354,7 ± 178,0 |
| 10 000 | 413,6 ± 104,4 |
| 25 000 | 500 ± 0 |
| 50 000 | 500 ± 0 |
| 100 000 | 500 ± 0 |

**Comparaison des algorithmes (50 000 pas)**

| Algorithme | Récompense moyenne | Temps |
|---|---|---|
| PPO | 500 ± 0 | 63 s |
| A2C | 500 ± 0 | 73 s |
| DQN | 159,5 ± 42,8 | 47 s |

**RLlib (PPO, 1 worker)** : la récompense moyenne passe de 22,1 à 476,3 en 10 itérations.

## Conclusions

- PPO atteint le score maximal avec 25 000 pas ou plus ; A2C l'atteint de façon moins stable ; DQN n'a pas convergé avec ses hyperparamètres par défaut sur 50 000 pas.
- La récompense mesurée pendant l'entraînement (politique stochastique) diffère de celle mesurée à l'évaluation (politique déterministe) : il faut évaluer sur plusieurs épisodes.
- Limite : chaque expérience n'a été lancée qu'avec une seule graine.

## Exécution

Cliquer sur le badge « Open In Colab » ci-dessus, puis **Exécution > Tout exécuter**. Compter une dizaine de minutes au total (les cellules les plus longues sont la comparaison de budgets, la comparaison d'algorithmes et RLlib).
