# 🎵 Détection d'anomalies sonores par autoencodeurs

Ce projet utilise des techniques d'apprentissage profond non supervisé pour détecter des sons anormaux dans un environnement industriel, en particulier pour des machines à rails coulissants. Nous avons implémenté et comparé deux modèles : un **autoencodeur (AE) classique** et un **autoencodeur variationnel (VAE)**, atteignant un **AUC de 0.89** pour le VAE.

---

## 📋 Table des matières
1. [Introduction](#Introduction)
2. [Dataset](#Dataset)
3. [Méthodologie](#Méthodologie)
4. [Résultats](#Résultats)
5. [Discussion](#Discussion)
6. [Conclusion](#Conclusion)
7. [Contributeurs](#Contributeurs)
8. [Références](#Références)

---

## 📖 Introduction

Les défaillances et pannes de machines entraînent des coûts substantiels pour les entreprises. Pour atténuer ces dépenses, les industries investissent dans des capteurs et l'intelligence artificielle afin d'améliorer la détection d'anomalies et réduire les coûts de maintenance. Notre approche utilise des autoencodeurs pour analyser les spectrogrammes des sons de machines, avec un focus particulier sur les autoencodeurs variationnels (VAE) qui ont démontré des performances supérieures dans l'identification de sons anormaux.

---

## 📊 Dataset

Le dataset utilisé est dérivé du dataset MIMII, focalisé sur les machines à rails coulissants.

- **Composition** :
  - 2370 enregistrements normaux pour l'entraînement
  - 1101 enregistrements de test (300 normaux, 801 anormaux)
- **Caractéristiques** :
  - Fichiers audio mono-canal de 10 secondes
  - Échantillonnage à 16 kHz
  - Sons provenant de trois rails coulissants (IDs 00, 02, et 04)

## 🧠 Méthodologie

### Prétraitement des données
- Conversion des signaux audio en spectrogrammes pour une analyse visuelle
- Normalisation et redimensionnement des spectrogrammes

### Architecture des modèles

#### Autoencodeur (AE)
- 3 couches denses pour l'encodeur et le décodeur
- Activation ReLU
- 50 760 paramètres entraînables

#### Autoencodeur Variationnel (VAE)
- Couches fully connected avec batch normalization
- Activation ReLU
- 861 480 paramètres entraînables

### Entraînement
- Optimiseur : Adam
- Fonction de perte : MSE pour AE, MSE + KL divergence pour VAE
- Batch size : 128 pour AE, 512 pour VAE
- Nombre d'époques : 100

---

## 🏆 Résultats

### Performances du VAE

| Slider ID | AUC | pAUC |
|-----------|-----|------|
| 00 | 0.950449 | 0.759462 |
| 02 | 0.783333 | 0.646757 |
| 04 | 0.932416 | 0.675931 |
| **Moyenne** | **0.888733** | **0.694050** |

### Performances de l'AE

| Métrique | Valeur |
|----------|--------|
| Précision | 52.7% |
| Rappel | 62.0% |
| Exactitude | 78.3% |
| Score F1 | 56.9% |
| AUC | 0.7662 |

- Le VAE surpasse l'AE classique avec un AUC moyen de 0.89 contre 0.7662
- La complexité accrue du VAE (861 000 paramètres vs 50 760 pour l'AE) se traduit par de meilleures performances
- Limitations : nécessité d'une grande quantité de données normales pour l'entraînement

---

## 🎓 Conclusion

Notre étude démontre l'efficacité des autoencodeurs, en particulier des VAE, pour la détection d'anomalies sonores dans un contexte industriel. Le VAE, grâce à sa nature probabiliste et son architecture avancée, offre une précision et une robustesse supérieures dans l'identification des sons anormaux.

---

## 🤝 Contributeurs

Ce projet a été réalisé par :
- Victor Mayaud
- Elliot Bouchy
- Aymeric Legros
- Naveen Johnson Vallavanatt

Sous la supervision du Professeur Pietro Michiardi, EURECOM, France.

---

## 📚 Références

1. Harsh Purohit et al., MIMII Dataset: Sound Dataset for Malfunctioning Industrial Machine Investigation and Inspection[1].
2. Ian Goodfellow et al., Deep Learning[2].
3. Geoffrey E. Hinton and Ruslan R. Salakhutdinov, Reducing the dimensionality of data with neural networks.
4. Mana Sakurada and Takehisa Yairi, Anomaly detection using autoencoders with nonlinear dimensionality reduction.
