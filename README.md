# Conversational Agents - Master's Course Workshop (Université Côte d’Azur)

This repository contains the practical materials I designed and taught for the **Conversational Agents AI Course** at Université Côte d’Azur (M2 - Master in Artificial Intelligence, Dec 2024 – Jan 2025).

## 🧠 Course Overview

- **Duration**: 2 months, 7 workshops
- **Audience**: Master’s students in Artificial Intelligence
- **Focus**: Design and implementation of Conversational Agents using **Large Language Models**, **FastAPI**, and **Langchain**

## 🛠️ Technologies

- Python 3.11+
- FastAPI
- Langchain

## 📚 Content Summary

| Workshop | Topics |
|----------|--------|
| 1        | Introduction to LLMs and Chatbots |
| 2        | APIs and REST principles |
| 3        | FastAPI fundamentals |
| 4        | Langchain Chains & Tools |
| 5        | Function Calling with LLMs |
| 6        | Evaluation & Prompt Engineering |
| 7        | Group Projects & Demo Day |

## ✍️ About the Instructor

This course was designed and taught by [Nathan Rihet](https://www.linkedin.com/in/nathan-rihet/?locale=en_US), Full Stack Engineer, as part of an academic collaboration with Université Côte d’Azur.


> Helping students bridge the gap between **AI theory** and **real-world applications** through hands-on LLM-based projects.

---

Feel free to use, adapt, and contribute.

## Architecture

```
C:.
├───api/                    # Gestion des routes et endpoints de l'API
│   ├───endpoints/         # Endpoints spécifiques par fonctionnalité
│   │   └───chat.py       # Endpoint pour les fonctionnalités de chat
│   └───router.py         # Router principal regroupant tous les endpoints
├───core/                  # Configuration et éléments centraux de l'application
├───models/               # Modèles de données Pydantic
│   └───chat.py          # Modèles pour les requêtes/réponses de chat
├───services/            # Services métier
│   └───llm_service.py   # Service d'interaction avec le LLM
├───utils/               # Utilitaires et helpers
└───main.py             # Point d'entrée de l'application
```

## Installation et Configuration

### Prérequis
- Python 3.11+ (ici : https://www.python.org/downloads/release/python-3110/ il faut redémarrer après installation pour avoir le $PATH sur l'OS)
- Visual Studio Code avec l'extension Python
- Une clé OpenAI que je vais vous fournir

### Installation

1. **Cloner le projet**
```bash
git clone <URL_DU_DEPOT>
cd <NOM_DU_PROJET>
```

2. **Créer l'environnement virtuel**
```bash
python -m venv venv
```

3. **Activer l'environnement virtuel**
- Windows :
```bash
.\venv\Scripts\activate
```
- macOS/Linux :
```bash
source venv/bin/activate
```

4. **Installer les dépendances**
```bash
pip install -r requirements.txt
```

5. **Configurer la clé API OpenAI**
Créer un fichier `.env` à la racine du projet :
```
OPENAI_API_KEY=votre-clé-api-openai
```


## Explication des Composants

### 1. Main Application (`main.py`)
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
```
- Point d'entrée de l'application
- Configure FastAPI et les middlewares
- Initialise les routes

### 2. Modèles (`models/chat.py`)
```python
class ChatRequest(BaseModel):
    message: str
```
- Définit la structure des données entrantes/sortantes
- Utilise Pydantic pour la validation des données
- Version simple pour débuter, extensible pour le contexte

### 3. Service LLM (`services/llm_service.py`)
```python
class LLMService:
    def __init__(self):
        self.llm = ChatOpenAI(...)
```
- Gère l'interaction avec le modèle de langage
- Configure le client OpenAI
- Traite les messages et le contexte

### 4. Router API (`api/router.py`)
```python
@router.post("/chat")
async def chat(request: ChatRequest) -> ChatResponse:
```
- Définit les endpoints de l'API
- Gère les requêtes HTTP
- Valide les données entrantes

## Utilisation de l'API

### Version Simple
```bash
curl -X 'POST' \
  'http://localhost:8000/chat/simple' \
  -H 'Content-Type: application/json' \
  -d '{"message": "Bonjour!"}'
```

### Version avec Contexte
```bash
curl -X 'POST' \
  'http://localhost:8000/chat/with-context' \
  -H 'Content-Type: application/json' \
  -d '{
    "message": "Bonjour!",
    "context": [
      {"role": "user", "content": "Comment vas-tu?"},
      {"role": "assistant", "content": "Je vais bien, merci!"}
    ]
  }'
```

## Debugging avec VS Code

1. Ouvrir le projet dans VS Code
2. Aller dans la section "Run and Debug" (Ctrl + Shift + D)
3. Sélectionner la configuration "Python: FastAPI"
4. Appuyer sur F5 ou cliquer sur le bouton Play
5. Démarrer Swagger : http://127.0.0.1:8000/docs

## Structure de l'API

### Endpoints Disponibles

- `/chat/simple` : Version basique sans contexte
- `/chat/with-context` : Version avancée avec gestion du contexte

### Flux de Données

1. La requête arrive sur l'endpoint
2. Les modèles Pydantic valident les données
3. Le service LLM traite la demande
4. La réponse est formatée et renvoyée

## Progression Pédagogique

1. **Démarrer avec la version simple**
   - Comprendre la structure de base
   - Tester les appels API simples

2. **Évoluer vers la version avec contexte**
   - Ajouter la gestion de l'historique
   - Comprendre l'importance du contexte dans les LLM

3. **Explorer les fonctionnalités avancées**
   - Implémenter des prompts personnalisés
   - Gérer différents types de réponses

## Dépannage

### Problèmes Courants

1. **Erreur de clé API**
   - Vérifier le fichier `.env`
   - S'assurer que la clé est valide

2. **Erreurs de dépendances**
   - Vérifier l'activation du venv
   - Réinstaller les requirements

3. **Erreurs de contexte**
   - Vérifier le format du contexte
   - S'assurer que les rôles sont valides

4. **Powershell**
   - Si les droits admin ne sont pas présent : ''Set-ExecutionPolicy Unrestricted -Scope CurrentUser -Force''

## Ressources

- [Documentation FastAPI](https://fastapi.tiangolo.com/)
- [Documentation LangChain](https://python.langchain.com/)
- [API OpenAI](https://platform.openai.com/docs/api-reference)
