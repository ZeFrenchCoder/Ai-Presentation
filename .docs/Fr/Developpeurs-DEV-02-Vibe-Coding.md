# Vibe Coding : coder en collaboration avec une AI

**ID:** DEV-02  
**Plateforme:** GitHub Enterprise + Vibe Coding  

## Type d'audience
Développeurs

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Intermédiaire

## Résumé Technique
Utiliser GitHub Copilot comme partenaire de code pour accélérer le développement et améliorer la lisibilité.

## Contenu

### 🧠 Introduction – Le Vibe Coding avec GitHub Enterprise

Le **Vibe Coding** transforme ta façon de coder en créant un dialogue continu avec GitHub Copilot Enterprise. Au lieu de coder directement, tu décris tes intentions dans des fichiers de travail, puis tu collabores avec l'AI pour exécuter tes idées étape par étape.

Cette approche permet de :
- **Clarifier tes objectifs** avant de commencer
- **Décomposer les tâches complexes** automatiquement
- **Valider ton travail** avec l'aide de l'AI
- **Maintenir une trace** de ton processus de développement

### 🧪 Démonstration 1 — Créer un fichier de planification (todo.txt)

#### 🎯 But
Apprendre à exprimer clairement tes intentions de développement dans un format que Copilot Enterprise peut analyser et décomposer.

#### ⚙️ Étapes techniques

1. **Crée un fichier `todo.txt`** dans ton projet

2. **Décris ton objectif principal** en langage naturel :
```markdown
# Objectif : Créer une API REST pour gérer des utilisateurs

## Fonctionnalités souhaitées :
- Endpoint GET /users pour lister tous les utilisateurs
- Endpoint POST /users pour créer un nouvel utilisateur
- Endpoint PUT /users/{id} pour modifier un utilisateur existant
- Endpoint DELETE /users/{id} pour supprimer un utilisateur
- Validation des données d'entrée
- Gestion d'erreurs appropriée
- Tests unitaires pour chaque endpoint

## Contraintes techniques :
- Utiliser Node.js avec Express
- Base de données MongoDB
- Authentification JWT
- Documentation OpenAPI
```

#### 💡 À souligner
- Sois **spécifique** sur les fonctionnalités attendues
- Inclus les **contraintes techniques** dès le départ
- Pense aux **aspects qualité** (tests, gestion d'erreurs)

### 🧪 Démonstration 2 — Analyser avec Copilot Enterprise (TodoAI.md)

#### 🎯 But
Utiliser Copilot Enterprise pour analyser ton fichier todo.txt et générer un plan d'exécution structuré.

#### ⚙️ Étapes techniques

1. **Ouvre Copilot Chat** dans VS Code

2. **Sélectionne le contenu** de ton fichier `todo.txt`

3. **Demande à Copilot** d'analyser et de créer un plan :
```
Analyse le contenu de todo.txt et crée un fichier TodoAI.md avec :
- Un plan étape par étape
- Titre, statut et résumé pour chaque tâche
- Ordre d'exécution recommandé
- Estimation de temps pour chaque étape
```

4. **Copilot génère** un fichier `TodoAI.md` structuré :
```markdown
# Plan d'exécution - API Utilisateurs

## Étape 1: Configuration du projet
**Statut:** 🔄 À faire  
**Résumé:** Initialiser le projet Node.js avec les dépendances nécessaires  
**Temps estimé:** 30 minutes

### Tâches détaillées:
- npm init -y
- Installation d'Express, MongoDB, JWT, Jest
- Configuration de la structure des dossiers

## Étape 2: Modèle utilisateur
**Statut:** 🔄 À faire  
**Résumé:** Créer le schéma MongoDB pour les utilisateurs  
**Temps estimé:** 45 minutes

### Tâches détaillées:
- Définir le schéma utilisateur (nom, email, mot de passe)
- Validation des champs
- Méthodes de hachage de mot de passe

## Étape 3: Endpoints CRUD
**Statut:** 🔄 À faire  
**Résumé:** Implémenter les 4 endpoints principaux  
**Temps estimé:** 2 heures

### Tâches détaillées:
- GET /users (avec pagination)
- POST /users (avec validation)
- PUT /users/{id}
- DELETE /users/{id}
```

#### 💡 À souligner
- Copilot **décompose automatiquement** les tâches complexes
- Il propose un **ordre logique** d'exécution
- Les **estimations de temps** aident à planifier

### 🧪 Démonstration 3 — Exécution étape par étape

#### 🎯 But
Collaborer avec Copilot pour exécuter chaque étape du plan en demandant du code spécifique.

#### ⚙️ Étapes techniques

1. **Pour chaque étape** du TodoAI.md, utilise Copilot Chat :

```
Exécute l'Étape 1 du TodoAI.md : 
Génère les commandes et le code nécessaire pour configurer le projet Node.js
```

2. **Copilot répond** avec du code concret :
```bash
# Commandes à exécuter
npm init -y
npm install express mongoose bcryptjs jsonwebtoken jest supertest
npm install -D nodemon

# Structure des dossiers
mkdir src controllers models routes middleware tests
```

3. **Demande le code** pour chaque composant :
```
Génère le fichier server.js pour l'Étape 1
```

4. **Marque l'étape comme terminée** dans TodoAI.md :
```markdown
## Étape 1: Configuration du projet
**Statut:** ✅ Terminé  
**Temps réel:** 25 minutes
```

#### 💡 À souligner
- **Une étape à la fois** pour maintenir la qualité
- **Dialogue constant** avec Copilot pour ajuster
- **Mise à jour du statut** pour suivre l'avancement

### 🧪 Démonstration 4 — Validation avec l'AI (validation.md)

#### 🎯 But
Créer un processus de validation assisté par l'AI pour vérifier la qualité du travail accompli.

#### ⚙️ Étapes techniques

1. **Demande à Copilot** de créer un plan de validation :
```
Crée un fichier validation.md pour valider que l'API respecte :
- Les exigences du todo.txt original
- Les bonnes pratiques de sécurité
- La qualité du code
- La couverture de tests
```

2. **Copilot génère** un fichier `validation.md` :
```markdown
# Validation de l'API Utilisateurs

## ✅ Checklist des exigences fonctionnelles
- [ ] GET /users retourne la liste des utilisateurs
- [ ] POST /users crée un nouvel utilisateur
- [ ] PUT /users/{id} modifie un utilisateur
- [ ] DELETE /users/{id} supprime un utilisateur
- [ ] Validation des données d'entrée
- [ ] Gestion d'erreurs appropriée

## 🔒 Checklist sécurité
- [ ] Mots de passe hachés avec bcrypt
- [ ] Authentification JWT fonctionnelle
- [ ] Validation des entrées utilisateur
- [ ] Protection contre les injections

## 🧪 Checklist tests
- [ ] Tests unitaires pour chaque endpoint
- [ ] Couverture > 80%
- [ ] Tests d'intégration
- [ ] Tests de validation des erreurs

## 📋 Checklist qualité code
- [ ] Code commenté et lisible
- [ ] Structure des dossiers cohérente
- [ ] Gestion des erreurs centralisée
- [ ] Documentation API (OpenAPI)
```

3. **Exécute la validation** étape par étape avec Copilot :
```
Aide-moi à vérifier le premier point : teste l'endpoint GET /users
Génère un test unitaire complet
```

#### 💡 À souligner
- La **validation automatisée** garantit la qualité
- Copilot aide à **identifier les manques**
- Le processus est **reproductible** pour d'autres projets

## Résumé

Le **Vibe Coding** révolutionne le développement en créant un flux de travail collaboratif entre le développeur et GitHub Copilot Enterprise.

**Processus en 4 étapes :**
1. **📝 Planning** : Expression des objectifs dans `todo.txt` 
2. **🤖 Analyse** : Génération automatique du plan détaillé dans `TodoAI.md`
3. **⚡ Exécution** : Développement étape par étape avec assistance Copilot
4. **✅ Validation** : Vérification qualité via `validation.md`

**Bénéfices clés :**
- **Clarté des objectifs** avant de commencer à coder
- **Décomposition automatique** des tâches complexes
- **Traçabilité complète** du processus de développement
- **Qualité garantie** par la validation assistée

**Résultat :** Une méthode de développement plus structurée, collaborative et qualitative qui transforme Copilot en véritable partenaire de code.

## Résumé

_À compléter..._

## Résumé

_À compléter..._