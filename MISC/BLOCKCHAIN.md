## TP-BLOCKCHAIN-SMARTCONTRACT
## 🎯 Objectif général

Créer une **blockchain simplifiée** avec **FastAPI en Python**, qui permet d'assurer la **traçabilité des produits dans une Supply Chain**. Le système devra simuler des **smart contracts** pour automatiser certaines vérifications métiers (comme le contrôle de température des vaccins).

---

## 🔧 Stack technique

- **Langage** : Python 3.11+
- **Framework** : [FastAPI](https://fastapi.tiangolo.com/)
- **Librairies** :
  - `uvicorn` (serveur ASGI)
  - `hashlib` (hashing)
  - `datetime`, `uuid`, `typing`
  - `pydantic` (modèles de données)
  - `requests` (si communication inter-nœuds)
  - `sqlite3` ou `json` (si stockage)

---

## 📦 Cas d’usage

### Suivi d’un **lot de vaccins** sensible à la température :

#### Acteurs :
- **Fabricant**
- **Transporteur**
- **Distributeur**
- **Pharmacie**

À chaque étape, un acteur enregistre une **transaction** dans la blockchain : lieu, état du produit, température, horodatage.

Si la température dépasse **-18°C**, un **smart contract simulé** déclenche une alerte.

---

## 🏗️ Architecture du projet

### 1. `blockchain.py` — Classe principale

- Gère la chaîne, les transactions, le minage, le proof-of-work
- Contient :
  - `Blockchain`
  - `Block`
  - `Transaction`

### 2. `smart_contracts.py` — Règles métiers

- Contient les règles automatisées simulant un "smart contract"
  - Exemple : `check_temperature`

### 3. `main.py` — FastAPI app

- Déclare toutes les routes :
  - `/transactions/new`
  - `/mine`
  - `/chain`
  - `/validate`
  - `/alerts`

---

## 📚 Fonctionnalités à implémenter

### ✅ Transactions

#### Route :
`POST /transactions/new`

```json
{
  "product_id": "VAC123",
  "actor": "Transporteur",
  "location": "Lyon",
  "temperature": -17.5,
  "status": "En transit"
}
```

Enregistre une transaction en mémoire.

---

### ✅ Minage d’un bloc

#### Route :
`GET /mine`

- Agrège les transactions en attente
- Applique un **proof of work**
- Vérifie les smart contracts (alertes, anomalies)
- Génère un nouveau bloc dans la blockchain

---

### ✅ Consultation de la blockchain

#### Route :
`GET /chain`

Affiche la blockchain entière.

---

### ✅ Validation de la chaîne

#### Route :
`GET /validate`

Vérifie si la chaîne est intacte :
- chaque bloc pointe bien vers le précédent via son hash
- recalcul des hash cohérents

---

### ✅ Smart Contracts (simulés)

Fichier `smart_contracts.py` :

```python
def check_temperature(transaction: dict) -> str:
    if transaction["temperature"] > -18:
        return f"ALERTE: Produit {transaction['product_id']} non conforme à {transaction['temperature']}°C"
    return "OK"
```

Chaque fois qu’un bloc est miné, toutes les transactions sont analysées par ces règles.

---

## ✨ Bonus optionnels

- Ajout de logs/alertes (`GET /alerts`)
- Enregistrement dans un fichier `.json` ou base SQLite
- Authentification simple des acteurs (JWT ou clé API)
- Simulation multi-noeuds FastAPI (avec `/nodes/register` et `/nodes/resolve`)
- Interface Web simple avec `Jinja2` ou `React + FastAPI`

---

## 📌 Étapes du projet à rendre

1. **Documentation du code**
2. **Capture des appels API via Postman ou Swagger**
3. **Diagramme de fonctionnement**
4. **Analyse : Comment la blockchain améliore la Supply Chain ?**
5. **Perspectives : passage à Ethereum, sécurité, authentification, chiffrement**

---

## 🧪 Exemple pédagogique

- L’étudiant développe le backend
- Il simule 4 transactions (acteur par acteur)
- Il tente une transaction invalide (température trop élevée)
- Il vérifie que le système **détecte l’anomalie automatiquement**

---

## 🗂️ Structure finale recommandée du projet

```
/supplychain_blockchain/
│
├── main.py                  ← Application FastAPI
├── blockchain.py            ← Classe Blockchain, Block, Transaction
├── smart_contracts.py       ← Fonctions de vérification métier
├── models.py                ← Schémas Pydantic pour validation
├── database.json            ← (optionnel) stockage persistant
├── README.md                ← Documentation du projet
└── requirements.txt         ← Dépendances
```

## CORRECTION : 

Parfait ! Voici un **projet complet FastAPI en Python** pour créer une **blockchain simplifiée** avec **smart contracts simulés** dans le contexte de la **Supply Chain**.

---

## 🗂️ Structure du projet

```
supplychain_blockchain/
├── main.py
├── blockchain.py
├── smart_contracts.py
├── models.py
├── database.json           ← (facultatif pour persister)
├── requirements.txt
└── README.md
```

---

## 1. 📄 `requirements.txt`

```txt
fastapi
uvicorn
pydantic
```

Installe les dépendances avec :

```bash
pip install -r requirements.txt
```

---

## 2. 📄 `models.py` (validation des données)

```python
from pydantic import BaseModel
from typing import Optional


class TransactionModel(BaseModel):
    product_id: str
    actor: str
    location: str
    temperature: float
    status: str


class BlockModel(BaseModel):
    index: int
    timestamp: str
    transactions: list
    previous_hash: str
    nonce: int
    hash: str
```

---

## 3. 📄 `smart_contracts.py` (logique métier)

```python
def check_temperature(transaction: dict) -> str:
    if transaction["temperature"] > -18:
        return f"ALERTE : Produit {transaction['product_id']} a dépassé la température limite : {transaction['temperature']}°C"
    return "OK"
```

---

## 4. 📄 `blockchain.py` (moteur de la blockchain)

```python
import hashlib
import json
from time import time
from typing import List, Dict
from uuid import uuid4
from smart_contracts import check_temperature


class Blockchain:
    def __init__(self):
        self.chain: List[Dict] = []
        self.pending_transactions: List[Dict] = []
        self.alerts: List[str] = []

        # Création du bloc Genesis
        self.create_block(nonce=1, previous_hash='0')

    def create_block(self, nonce, previous_hash):
        block = {
            'index': len(self.chain) + 1,
            'timestamp': time(),
            'transactions': self.pending_transactions,
            'nonce': nonce,
            'previous_hash': previous_hash,
        }
        block['hash'] = self.hash(block)
        self.chain.append(block)

        # Vérification des transactions via les smart contracts
        for tx in self.pending_transactions:
            result = check_temperature(tx)
            if result != "OK":
                self.alerts.append(result)

        self.pending_transactions = []
        return block

    def add_transaction(self, transaction: Dict):
        self.pending_transactions.append(transaction)
        return self.last_block['index'] + 1

    def proof_of_work(self, previous_hash):
        nonce = 0
        while True:
            block = {
                'index': len(self.chain) + 1,
                'timestamp': time(),
                'transactions': self.pending_transactions,
                'nonce': nonce,
                'previous_hash': previous_hash
            }
            hash_block = self.hash(block)
            if hash_block[:4] == '0000':
                return nonce
            nonce += 1

    def hash(self, block: Dict):
        block_copy = block.copy()
        block_copy.pop("hash", None)
        encoded_block = json.dumps(block_copy, sort_keys=True).encode()
        return hashlib.sha256(encoded_block).hexdigest()

    @property
    def last_block(self):
        return self.chain[-1]

    def is_valid_chain(self):
        for i in range(1, len(self.chain)):
            prev = self.chain[i - 1]
            current = self.chain[i]

            if current['previous_hash'] != prev['hash']:
                return False
            if self.hash(current) != current['hash']:
                return False
        return True
```

---

## 5. 📄 `main.py` (API FastAPI)

```python
from fastapi import FastAPI
from blockchain import Blockchain
from models import TransactionModel
from typing import List

app = FastAPI(title="Supply Chain Blockchain")
blockchain = Blockchain()


@app.get("/")
def home():
    return {"message": "Bienvenue sur la Blockchain Supply Chain API !"}


@app.post("/transactions/new")
def create_transaction(tx: TransactionModel):
    index = blockchain.add_transaction(tx.dict())
    return {"message": f"Transaction ajoutée pour le bloc {index}"}


@app.get("/mine")
def mine_block():
    previous_hash = blockchain.last_block['hash']
    nonce = blockchain.proof_of_work(previous_hash)
    block = blockchain.create_block(nonce, previous_hash)
    return {
        "message": "Bloc miné avec succès",
        "index": block['index'],
        "hash": block['hash'],
        "transactions": block['transactions'],
        "alerts": blockchain.alerts[-len(block['transactions']):]  # alertes du bloc actuel
    }


@app.get("/chain")
def get_chain():
    return {
        "length": len(blockchain.chain),
        "chain": blockchain.chain
    }


@app.get("/validate")
def validate_chain():
    is_valid = blockchain.is_valid_chain()
    return {"valid": is_valid}


@app.get("/alerts")
def get_alerts():
    return {"alerts": blockchain.alerts}
```

---

## ▶️ Lancement du projet

### Étapes :

1. Crée un dossier `supplychain_blockchain`
2. Place tous les fichiers ci-dessus dedans
3. Dans un terminal :

```bash
cd supplychain_blockchain
python -m venv venv
source venv/bin/activate  # ou venv\Scripts\activate sur Windows
pip install -r requirements.txt
uvicorn main:app --reload
```

4. Ouvre ton navigateur sur 👉 `http://127.0.0.1:8000/docs`  
   → Tu accèdes à Swagger UI pour tester les routes.

---

## 🔍 Exemple de test via Swagger

1. `POST /transactions/new`

```json
{
  "product_id": "VAC123",
  "actor": "Transporteur",
  "location": "Lyon",
  "temperature": -17.5,
  "status": "En transit"
}
```

2. `GET /mine` → crée un bloc

3. `GET /chain` → affiche tous les blocs

4. `GET /alerts` → alerte si température trop élevée

---

## ✅ Résultat attendu

- Blockchain fonctionnelle avec PoW
- Ajout sécurisé de transactions
- Vérification automatique des anomalies
- API REST complète avec documentation interactive

---
