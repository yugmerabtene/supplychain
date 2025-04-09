## Exercice – Analyse de performance Supply Chain basée sur les KPI

### 🎯 Objectif général :
Vous êtes analyste logistique dans une entreprise de distribution. Votre mission est de réaliser une **analyse de performance de la Supply Chain** à partir de plusieurs **KPI critiques** et de proposer des pistes d’amélioration pour soutenir la prise de décision stratégique.

---

### 🗂️ Contexte :
Le directeur logistique souhaite un **rapport décisionnel** basé sur les données de l’année écoulée. Vous disposez de données brutes (commandes, ventes, stock, transport, etc.) à partir desquelles vous devez :

1. **Calculer les principaux KPI** logistiques.
2. **Identifier les points de faiblesse ou d’alerte.**
3. **Proposer des recommandations concrètes.**
4. **Présenter les résultats avec des visualisations claires** (graphiques, tableaux de bord).

---

### 📌 KPI à analyser :

- **Livraison à l’heure des commandes clients (Ponctualité)**
- **Ratio Stock / Ventes (ISR - Inventory to Sales Ratio)**
- **Coût de possession du stock**
- **Ponctualité des livraisons fournisseurs**
- **DSI – Durée moyenne de rotation des stocks**
- **Coût de transport par tonne expédiée**
- **Taux de commandes parfaites (Perfect Order Rate)**

---

### 📋 Travail à réaliser :

1. **Extraire et structurer les données nécessaires**.
2. **Calculer chaque KPI avec la formule adaptée**.
3. **Comparer les résultats aux seuils acceptables du secteur**.
4. **Identifier les indicateurs critiques à améliorer**.
5. **Créer des visualisations pertinentes** (diagrammes en barres, radar, etc.).
6. **Formuler des recommandations pour améliorer la performance logistique**.

---

### 💡 Indications supplémentaires :
- Vous pouvez simuler les données si elles ne sont pas fournies.
- Soyez rigoureux dans l’application des formules.
- Justifiez vos recommandations par une analyse factuelle.
- La clarté des graphiques est essentielle pour la communication avec les parties prenantes non techniques.
-----
Voici un **exercice complet en Python** autour des **KPI Supply Chain** que tu as listés. Il inclut :

1. Un **énoncé clair** pour des étudiants ou professionnels,
2. Un **script de correction** avec calculs et visualisation via `matplotlib` et `seaborn`,
3. Une logique de **prise de décision** à partir des KPI.

---

## 🧠 Énoncé de l'exercice : "Analyse de performance Supply Chain"

### Contexte :
Vous êtes analyste Supply Chain dans une entreprise de distribution. Le directeur logistique vous demande un **rapport décisionnel** sur la performance des opérations logistiques de l’année écoulée, basé sur plusieurs **KPI critiques** :

- Livraison à l’heure (Ponctualité)
- Ratio Stock / Ventes
- Coût de possession du stock
- Suivi des commandes d’achat
- DSI (rotation moyenne)
- Coût de transport par tonne
- Taux de commandes parfaites
- Livraison à l’heure des fournisseurs

### Objectifs :
1. Calculer les KPI à partir des données.
2. Identifier les points d’amélioration.
3. Visualiser les tendances avec des **graphiques**.
4. Fournir une recommandation sur la stratégie logistique à adopter.

---

### 📁 Données fournies :

Voici un échantillon des données (à simuler en Python) :

```python
data = {
    'commandes': 500,
    'commandes_livrees_a_temps': 420,
    'stock_moyen': 120000,  # en €
    'ventes_net': 600000,   # en €
    'cout_biens_vendus': 450000,
    'taux_possession': 0.25,
    'commandes_parfaites': 385,
    'cout_total_transport': 75000,  # en €
    'tonnage_total': 1500,  # en tonnes
    'delais_livraisons_fournisseurs': [True, True, False, True, False, True, True, True, False, True],
}
```

