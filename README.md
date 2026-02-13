# 📊 Prévision de la Facture Électrique Résidentielle (Québec)

## 🧠 Description du projet

Ce projet vise à prédire le montant mensuel de la facture d’électricité résidentielle à partir de données historiques de consommation par région.

Le pipeline couvre l’ensemble du cycle machine learning :

- Chargement et nettoyage des données  
- Feature engineering temporel  
- Split temporel (train/test)  
- Pipelines de prétraitement  
- Entraînement de plusieurs modèles  
- Optimisation d’hyperparamètres  
- Suivi des expériences  
- Comparaison des performances  
- Sauvegarde du meilleur modèle  

---

## 🚀 Technologies utilisées

- Python 3.12  
- NumPy  
- Pandas  
- scikit-learn  
- MLflow  
- Optuna  
- Matplotlib  
- Seaborn  
- Joblib  

---

## 📁 Structure du projet

```text
.
├── historique-consommation-secteur-activite-ra-mois.csv
├── modele_final_gradientboosting.pkl
├── mae_comparaison_base.png
├── comparaison_MAE.png
├── comparaison_RMSE.png
├── comparaison_R².png
├── notebook.ipynb
└── README.md
⚙️ Installation
pip install -U scikit-learn numpy scipy pandas mlflow optuna matplotlib seaborn joblib
📥 Données
Le fichier CSV contient :

Région administrative

Date (année/mois)

Secteur d’activité

Consommation totale (kWh)

Seul le secteur résidentiel est conservé.

🛠 Feature Engineering
Variables temporelles
mois

année

saison_froide

Historique consommation
lag1 (M-1)

lag3 (M-3)

roll3 (moyenne mobile 3 mois)

Variables synthétiques
Température moyenne simulée

Tarif saisonnier

Interaction consommation × température

Variable cible
Montant_facture = Consommation_kWh × Tarif
🔄 Split temporel
Train : avant janvier 2023

Test : janvier 2023 et après

Cela simule un scénario réel de prédiction future.

🧩 Préprocessing
Pipeline :

StandardScaler → variables numériques

OneHotEncoder → régions

Le tout encapsulé dans un ColumnTransformer.

🤖 Modèles évalués
Régression linéaire

Ridge Regression

Random Forest Regressor

Histogram Gradient Boosting Regressor

Chaque modèle est intégré dans un Pipeline complet :

Préprocessing → Modèle
📈 Métriques
MAE

RMSE

R²

📊 Résultats initiaux
Modèle	MAE
Linear	~1.56M
Ridge	~1.63M
RandomForest	~735k
GradientBoosting	~936k
RandomForest et GradientBoosting sont retenus pour optimisation.

🔍 Optimisation
RandomForest (GridSearchCV)
n_estimators

max_depth

min_samples_split

GradientBoosting (Optuna)
max_iter

learning_rate

max_depth

🏆 Performances finales
Modèle	Version	MAE
RandomForest	Base	735k
RandomForest	Optimisé	735k
GradientBoosting	Base	936k
GradientBoosting	Optimisé	918k
Le GradientBoosting optimisé est sélectionné comme modèle final.

💾 Sauvegarde du modèle
Le modèle final est sauvegardé :

modele_final_gradientboosting.pkl
Chargement :

import joblib
model = joblib.load("modele_final_gradientboosting.pkl")
📉 Visualisations
Comparaison MAE / RMSE / R²

Prédictions vs Réalité

Résidus

Ces graphiques permettent l’analyse des erreurs et la validation visuelle.

🧪 Tracking MLflow
Chaque run enregistre :

hyperparamètres

métriques

graphiques

modèle

Objectifs :

reproductibilité

audit ML

comparaison d’expériences

📌 Conclusion
Pipeline ML complet orienté séries temporelles avec :

Feature engineering avancé

Pipelines sklearn propres

Optimisation automatique

Tracking MLflow

Le modèle final atteint un R² ≈ 0.9986.

👤 Créateur
Latrous Akram
📧 latrousakram@gmail.com
