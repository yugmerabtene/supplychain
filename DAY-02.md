# 📅 **Jour 2 : Systèmes d'Information pour la Supply Chain**

---

## 🎯 Objectifs pédagogiques

- Comprendre l’**architecture des systèmes d’information (SI)** dans la Supply Chain  
- Identifier les **solutions logicielles** utilisées pour la planification, la gestion des entrepôts, du transport et des commandes  
- Relier les **outils SI aux processus métier**  
- Appréhender l'**interopérabilité** des systèmes

---

## 1. 🧠 **Pourquoi des SI dans la Supply Chain ?**

Les SI permettent de :
- **Planifier** efficacement les besoins et les ressources  
- **Piloter** les opérations en temps réel  
- **Optimiser** les coûts et les délais  
- **Tracer** les flux logistiques et financiers  
- **Communiquer** entre les maillons internes et externes de la chaîne

---

## 2. 🏛️ **Architecture globale des SI en Supply Chain**

```
            +------------+      +------------+      +------------+
            |   ERP      |<---->|   CRM      |<---->|   E-commerce|
            +------------+      +------------+      +------------+
                 |
        +--------+--------+
        |                 |
  +-----------+    +------------+    +------------+    +--------+
  |   APS     |    |    WMS     |    |    TMS     |    |  OMS   |
  +-----------+    +------------+    +------------+    +--------+
```

---

## 3. 🧩 **Présentation des principaux systèmes**

### 3.1 **ERP (Enterprise Resource Planning)**
- Cœur du système d’information de l’entreprise
- Intègre les fonctions : finance, RH, achats, logistique, production
- Exemples : SAP, Oracle, Microsoft Dynamics

### 3.2 **APS (Advanced Planning System)**
- Outils d’aide à la planification stratégique et tactique  
- Gèrent les prévisions, le calcul des besoins, la planification des capacités  
- Exemples : SAP APO, Kinaxis, Quintiq

### 3.3 **WMS (Warehouse Management System)**
- Gère les **entrepôts** : emplacements, mouvements de stock, préparation de commandes  
- Optimise les flux internes  
- Exemples : Reflex, Manhattan, Generix WMS

### 3.4 **TMS (Transport Management System)**
- Planifie et suit les **livraisons**, optimise les tournées  
- Intègre les coûts, les délais, les capacités de transport  
- Exemples : Transwide, Akanea, Oracle TMS

### 3.5 **OMS (Order Management System)**
- Gère l'ensemble du **cycle de la commande** : réception, traitement, affectation, expédition  
- Interface entre les canaux de vente et la logistique

### 3.6 **CRM (Customer Relationship Management)**
- Gère la **relation client**, la satisfaction, les réclamations  
- Apporte une vision 360° du client

---

## 4. 🔗 **Intégration & communication entre les SI**

### 4.1 Communication inter-systèmes :
- Utilisation de **bus applicatifs**, **API**, **EDI**, **connecteurs**
- Objectif : permettre un **échange fluide et sécurisé** de données

### 4.2 Exemple de scénario :
> Une commande est passée en ligne → OMS l’enregistre → vérifie le stock via le WMS → le TMS planifie l’envoi → le CRM informe le client → les données sont centralisées dans l’ERP

---

## 5. 📈 **Bénéfices des SI dans la Supply Chain**

| Bénéfice                         | Description |
|----------------------------------|-------------|
| Réduction des délais             | Meilleure coordination des processus |
| Amélioration du taux de service | Fiabilité des livraisons |
| Réduction des coûts              | Optimisation des stocks et transports |
| Traçabilité                      | Historique des mouvements et données |
| Agilité                          | Adaptation rapide aux changements |

---

## 🛠️ **Travaux Pratiques (TP) – Cartographie des SI de la Supply Chain**

### Objectif :
Analyser un **cas d’entreprise** et associer les bons systèmes d’information aux différentes **étapes de la chaîne logistique**.

### Modalité :
- Étude d’un scénario fourni ou d’une entreprise choisie par les participants  
- Remplir une **table de correspondance** entre processus métier et système SI :

| **Processus métier**         | **SI associé** | **Rôle du système**                         |
|-----------------------------|----------------|---------------------------------------------|
| Prévision de la demande     | APS            | Calcul de la demande future                |
| Réception des commandes     | OMS            | Centralisation et suivi des commandes      |
| Gestion des stocks entrepôt | WMS            | Suivi des mouvements de stock              |
| Livraison client             | TMS            | Planification et optimisation des tournées |
| Suivi de satisfaction        | CRM            | Gestion de la relation client              |

### Restitution :
- Présentation orale de chaque groupe avec justification des choix
