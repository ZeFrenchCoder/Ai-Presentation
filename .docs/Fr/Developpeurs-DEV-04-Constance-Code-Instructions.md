# Constance du code et fichier Instruction

**ID:** DEV-04  
**Plateforme:** GitHub Enterprise + Setup  

## Type d'audience
Développeurs

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Intermédiaire

## Résumé Technique
Utiliser les fichiers d'instruction du répertoire .github pour maintenir la cohérence du code et guider l'AI dans la génération de code conforme aux standards de l'équipe.

## Contenu

Excellente question 👏 — tu touches ici à une partie **avancée et peu connue de GitHub Copilot Enterprise**, liée à la **personnalisation du comportement de Copilot** grâce à des fichiers d’instructions dans le dépôt `.github`.

Voici une explication claire et technique de chaque fichier :

---

## 🧩 **1. `.github/copilot-instructions.md`**

### 📘 **But :**

C’est **le fichier maître d’instructions globales** pour GitHub Copilot dans un dépôt.
Il permet d’**influencer la façon dont Copilot génère du code, commente, ou documente**, pour toute l’équipe.

### ⚙️ **Comment ça marche :**

* Copilot lit ce fichier **au moment de suggérer du code** ou de répondre dans Copilot Chat.
* Le contenu agit comme une **couche de contexte permanente**, un peu comme des *Custom Instructions* dans ChatGPT.

### 🧠 **Utilisation typique :**

Tu y définis :

* Les **standards de code** (langage, style, docstring, format des commentaires).
* Les **règles de nommage** (variables, fonctions, fichiers).
* Les **bonnes pratiques spécifiques à l’équipe ou au projet**.
* Les **comportements à éviter** (ex. “ne pas proposer de code non typé”, “éviter print() dans les libs”).

### 💡 **Exemple concret :**

```markdown
# .github/copilot-instructions.md

## Style de code
- Utiliser des fonctions en snake_case.
- Toujours inclure un docstring au format Google.
- Utiliser des f-strings pour les logs.

## Tests
- Suggérer des tests unitaires avec pytest.
- Préférer la librairie unittest pour les tests intégrés.

## Sécurité
- Ne jamais inclure de mot de passe, clé API, ou token dans le code généré.
```

🧩 **Résultat :**
Copilot ajuste ses suggestions automatiquement selon ces directives dans **tous les fichiers du repo**.
C’est idéal pour **standardiser les pratiques entre plusieurs développeurs.**

---

## 🧩 **2. `.github/instructions/**/NAME.instructions.md`**

### 📘 **But :**

Ces fichiers servent à **définir des instructions contextuelles spécifiques** pour des **domaines précis** du projet.

Ils sont plus **granulaires** que le fichier principal, et permettent d’adapter les comportements à des sous-dossiers, modules ou types de tâches.

### 🧠 **Structure typique :**

* Le dossier `instructions/` peut contenir plusieurs sous-répertoires (ex. `frontend/`, `backend/`, `devops/`).
* Chaque fichier `.instructions.md` porte un **nom clair** (ex. `api.instructions.md`, `tests.instructions.md`).

### 💡 **Exemple concret :**

```
.github/instructions/backend/api.instructions.md
```

Contenu :

```markdown
# API Instructions
- Utiliser FastAPI pour les endpoints.
- Les fonctions doivent retourner un objet JSON.
- Préférer async/await pour toutes les routes.
- Ajouter une docstring avec le schéma de réponse.
```

✅ **Effet :**
Quand tu codes dans `/backend/`, Copilot **priorise ces directives** plutôt que celles du fichier global.

Cela permet d’avoir :

* Un style différent pour le backend vs frontend.
* Des conventions adaptées aux technologies (React vs Python, etc.).
* Des règles distinctes selon les modules.

---

## 🧩 **3. `.github/<agent>`**

### 📘 **But :**

Ce répertoire concerne les **Copilot Agents** — des assistants spécialisés intégrés à GitHub Copilot Chat (introduits avec Copilot Enterprise).

Chaque “agent” agit comme un **rôle AI personnalisé** :

* `copilot`, `security`, `docs`, `tests`, etc.

Ces agents peuvent être configurés pour répondre différemment selon leur mission.

### ⚙️ **Exemple de structure :**

```
.github/
 ├── copilot-instructions.md
 ├── instructions/
 │    └── backend/api.instructions.md
 └── agents/
      ├── security/
      │    └── security.instructions.md
      ├── docs/
      │    └── docs.instructions.md
```

### 💡 **Exemples d’usage d’agent :**

#### `.github/agents/security/security.instructions.md`

```markdown
# Agent de sécurité Copilot
- Prioriser la détection des vulnérabilités.
- Ne jamais ignorer les alertes de dépendances critiques.
- Préférer l'utilisation de la librairie "secrets" pour les clés.
```

#### `.github/agents/docs/docs.instructions.md`

```markdown
# Agent documentation
- Générer des README au format Markdown.
- Utiliser un ton professionnel, concis et clair.
- Ajouter un exemple d’usage minimal pour chaque fonction publique.
```

### 🚀 **Effet :**

Quand un utilisateur discute avec Copilot Chat et appelle un agent (ex. `/security` ou `/docs`),
Copilot **lit automatiquement les instructions correspondantes** pour ajuster son comportement.

---

## 🔐 **Résumé global**

| **Emplacement**                                | **Portée**                          | **Utilité principale**                                       |
| ---------------------------------------------- | ----------------------------------- | ------------------------------------------------------------ |
| `.github/copilot-instructions.md`              | Globale (tout le repo)              | Standardiser les pratiques de code et de style.              |
| `.github/instructions/**/NAME.instructions.md` | Contextuelle (par module / dossier) | Adapter Copilot à des zones spécifiques du projet.           |
| `.github/agents/**/NAME.instructions.md`       | Agent Copilot Chat (rôle dédié)     | Spécialiser des assistants AI (docs, sécurité, tests, etc.). |

---

Souhaites-tu que je te fasse un **exemple complet de structure .github/** avec tous ces fichiers (et leur contenu minimal) pour ton dépôt de démo GitHub Enterprise ?
👉 Je pourrais le générer sous forme de **zippé (.zip)** prêt à déposer dans un repo.

## Résumé

_À compléter..._