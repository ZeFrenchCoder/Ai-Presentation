# Bien démarrer avec l'AI dans GitHub Enterprise

**ID:** DEV-01  
**Plateforme:** GitHub Enterprise + Setup  

## Type d'audience
Développeurs

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Débutant

## Résumé Technique
Configuration et outils AI intégrés à GitHub pour booster la productivité et la qualité du code.

## Contenu

### 🧠 Introduction – Mettre l'AI au service du développeur

Copilot n'est pas une baguette magique : c'est un partenaire de code.
Il comprend ton contexte, anticipe ton intention et te propose du code conforme à ton style.

Copilot Chat devient un "assistant technique" dans ton IDE : il explique, documente et génère des tests à la demande.

Ensemble, ces outils font gagner du temps sans sacrifier la qualité ni la sécurité, car tout reste dans ton environnement GitHub Enterprise.

### 🧪 Démonstration 1 — Créer une fonction avec Copilot

#### 🎯 But
Montrer comment un commentaire clair permet à Copilot de générer du code complet et contextuel.

#### ⚙️ Étapes techniques
1. Ouvre un fichier Python (ou JS, C#, etc.).

2. Écris :
```python
# crée une fonction qui trie une liste de dictionnaires par date
```

3. Observe la complétion automatique proposée par Copilot :
```python
def trier_par_date(liste):
    return sorted(liste, key=lambda x: x['date'])
```

4. Accepte la suggestion, puis modifie légèrement le commentaire pour voir Copilot proposer une nouvelle version.

#### 💡 À souligner
- Plus ton commentaire est précis, plus la suggestion est pertinente.
- Copilot comprend les intents fonctionnels (ex. "tri", "calcul", "validation").

### 🧪 Démonstration 2 — Utiliser Copilot Chat pour expliquer et tester

#### 🎯 But
Montrer comment `/explain` et `/tests` transforment Copilot Chat en mentor et testeur virtuel.

#### ⚙️ Étapes techniques
1. Sélectionne une fonction existante dans ton fichier.

2. Ouvre Copilot Chat et tape :
```
/explain
```

👉 Copilot te donne une explication claire de ce que fait la fonction, ligne par ligne.

3. Ensuite, demande :
```
/tests
```

👉 Copilot propose un ensemble de tests unitaires correspondants à cette fonction.

4. Copie un test et exécute-le localement pour valider le comportement.

#### 💡 À souligner
- `/explain` est parfait pour l'onboarding ou la revue de code.
- `/tests` accélère la couverture unitaire tout en gardant la logique du code existant.
- L'AI ne remplace pas le jugement du dev, elle accélère son itération.

## Résumé

Cet article présente GitHub Copilot comme un **partenaire de développement intelligent** qui comprend le contexte et anticipe les intentions du développeur. 

**Points clés :**
- **Copilot** génère du code à partir de commentaires précis et s'adapte au style existant
- **Copilot Chat** agit comme un assistant technique avec des commandes spécialisées (`/explain`, `/tests`)
- **Gain de productivité** sans compromis sur la qualité grâce à l'intégration native GitHub Enterprise
- **Approche pratique** : deux démonstrations concrètes pour maîtriser les bases

**Résultat :** Les développeurs peuvent immédiatement améliorer leur workflow en utilisant l'AI comme un mentor virtuel qui accélère l'écriture, l'explication et les tests du code.

## Liens Utiles

### 📚 Documentation Officielle
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot) - Guide complet officiel
- [GitHub Copilot Chat](https://docs.github.com/en/copilot/github-copilot-chat) - Documentation Copilot Chat
- [GitHub Copilot for Business](https://docs.github.com/en/copilot/copilot-for-business) - Configuration Enterprise

### 🎓 Formations et Tutoriels
- [GitHub Copilot Fundamentals](https://learn.microsoft.com/en-us/training/paths/copilot/) - Microsoft Learn
- [Getting Started with GitHub Copilot](https://github.blog/2022-06-21-github-copilot-is-generally-available-to-all-developers/) - GitHub Blog
- [Copilot Best Practices](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/) - Techniques avancées

### 🔧 Outils et Extensions
- [GitHub Copilot VS Code Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) - Extension officielle
- [GitHub Copilot Chat Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) - Chat intégré
- [GitHub Copilot for IntelliJ](https://plugins.jetbrains.com/plugin/17718-github-copilot) - Support JetBrains

### 📖 Ressources Complémentaires
- [Awesome GitHub Copilot](https://github.com/sindresorhus/awesome-github-copilot) - Collection de ressources
- [Copilot Patterns](https://github.com/microsoft/copilot-patterns) - Patterns et exemples Microsoft
- [Enterprise Setup Guide](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot-for-business) - Configuration d'entreprise