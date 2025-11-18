# Créer des Unit Tests automatiquement (version QA)

**ID:** QA-02  
**Plateforme:** GitHub Enterprise + Copilot  

## Type d'audience
QA / Testeurs

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Débutant

## Résumé Technique
Permet de créer ou valider des tests unitaires cohérents avec les spécifications fonctionnelles et générer des cas de test manuels détaillés.

## Contenu

### Démonstration : Analyse de code et génération de cas de test manuels

#### Étape 1 : Analyser le code source

Supposons que nous ayons une fonction de calcul de prix avec remise :

```javascript
function calculatePrice(basePrice, discountPercent, customerType, quantity) {
    // Validation des paramètres
    if (basePrice <= 0) {
        throw new Error("Le prix de base doit être positif");
    }
    
    if (discountPercent < 0 || discountPercent > 100) {
        throw new Error("Le pourcentage de remise doit être entre 0 et 100");
    }
    
    if (quantity <= 0) {
        throw new Error("La quantité doit être positive");
    }
    
    // Calcul du prix avec remise
    let discountAmount = (basePrice * discountPercent) / 100;
    let discountedPrice = basePrice - discountAmount;
    
    // Remise supplémentaire selon le type de client
    if (customerType === "VIP") {
        discountedPrice *= 0.95; // 5% de remise supplémentaire
    } else if (customerType === "PREMIUM") {
        discountedPrice *= 0.97; // 3% de remise supplémentaire
    }
    
    // Remise en volume
    if (quantity >= 10) {
        discountedPrice *= 0.92; // 8% de remise supplémentaire
    } else if (quantity >= 5) {
        discountedPrice *= 0.95; // 5% de remise supplémentaire
    }
    
    return Math.round(discountedPrice * 100) / 100; // Arrondi à 2 décimales
}
```

#### Étape 2 : Demander à l'IA d'analyser et générer les cas de test

**Prompt pour l'IA :**
```
Analysez cette fonction calculatePrice et générez une liste complète de cas de test manuels. 
Pour chaque cas de test, fournissez :
1. Le nom du test
2. Les données d'entrée
3. Le résultat attendu
4. Les étapes de test détaillées
5. La catégorie du test (nominal, limite, erreur)

Exportez les résultats en format JSON et Markdown.
```

#### Étape 3 : Réponse de l'IA - Cas de test générés

##### Format JSON

```json
{
  "testSuite": "calculatePrice Function Tests",
  "version": "1.0",
  "generatedDate": "2024-10-14",
  "testCases": [
    {
      "id": "TC001",
      "name": "Test calcul prix normal client standard",
      "category": "Nominal",
      "priority": "High",
      "input": {
        "basePrice": 100,
        "discountPercent": 10,
        "customerType": "STANDARD",
        "quantity": 1
      },
      "expectedOutput": 90,
      "steps": [
        "1. Appeler calculatePrice(100, 10, 'STANDARD', 1)",
        "2. Vérifier que le résultat est 90",
        "3. Valider que le calcul applique 10% de remise",
        "4. Confirmer qu'aucune remise supplémentaire n'est appliquée"
      ]
    },
    {
      "id": "TC002",
      "name": "Test calcul prix client VIP",
      "category": "Nominal",
      "priority": "High",
      "input": {
        "basePrice": 100,
        "discountPercent": 10,
        "customerType": "VIP",
        "quantity": 1
      },
      "expectedOutput": 85.5,
      "steps": [
        "1. Appeler calculatePrice(100, 10, 'VIP', 1)",
        "2. Vérifier que le résultat est 85.5",
        "3. Valider la remise de base (10%) : 100 -> 90",
        "4. Valider la remise VIP (5%) : 90 -> 85.5"
      ]
    },
    {
      "id": "TC003",
      "name": "Test calcul prix client PREMIUM",
      "category": "Nominal",
      "priority": "High",
      "input": {
        "basePrice": 100,
        "discountPercent": 15,
        "customerType": "PREMIUM",
        "quantity": 1
      },
      "expectedOutput": 82.45,
      "steps": [
        "1. Appeler calculatePrice(100, 15, 'PREMIUM', 1)",
        "2. Vérifier que le résultat est 82.45",
        "3. Valider la remise de base (15%) : 100 -> 85",
        "4. Valider la remise PREMIUM (3%) : 85 -> 82.45"
      ]
    },
    {
      "id": "TC004",
      "name": "Test remise en volume 5-9 articles",
      "category": "Nominal",
      "priority": "Medium",
      "input": {
        "basePrice": 100,
        "discountPercent": 0,
        "customerType": "STANDARD",
        "quantity": 7
      },
      "expectedOutput": 95,
      "steps": [
        "1. Appeler calculatePrice(100, 0, 'STANDARD', 7)",
        "2. Vérifier que le résultat est 95",
        "3. Valider qu'aucune remise de base n'est appliquée",
        "4. Valider la remise volume (5%) : 100 -> 95"
      ]
    },
    {
      "id": "TC005",
      "name": "Test remise en volume 10+ articles",
      "category": "Nominal",
      "priority": "Medium",
      "input": {
        "basePrice": 100,
        "discountPercent": 0,
        "customerType": "STANDARD",
        "quantity": 15
      },
      "expectedOutput": 92,
      "steps": [
        "1. Appeler calculatePrice(100, 0, 'STANDARD', 15)",
        "2. Vérifier que le résultat est 92",
        "3. Valider qu'aucune remise de base n'est appliquée",
        "4. Valider la remise volume (8%) : 100 -> 92"
      ]
    },
    {
      "id": "TC006",
      "name": "Test cas limite - prix zéro",
      "category": "Boundary",
      "priority": "High",
      "input": {
        "basePrice": 0,
        "discountPercent": 10,
        "customerType": "STANDARD",
        "quantity": 1
      },
      "expectedOutput": "Error: Le prix de base doit être positif",
      "steps": [
        "1. Appeler calculatePrice(0, 10, 'STANDARD', 1)",
        "2. Vérifier qu'une exception est levée",
        "3. Valider le message d'erreur exact",
        "4. Confirmer que le traitement s'arrête"
      ]
    },
    {
      "id": "TC007",
      "name": "Test cas limite - remise 101%",
      "category": "Boundary",
      "priority": "High",
      "input": {
        "basePrice": 100,
        "discountPercent": 101,
        "customerType": "STANDARD",
        "quantity": 1
      },
      "expectedOutput": "Error: Le pourcentage de remise doit être entre 0 et 100",
      "steps": [
        "1. Appeler calculatePrice(100, 101, 'STANDARD', 1)",
        "2. Vérifier qu'une exception est levée",
        "3. Valider le message d'erreur exact",
        "4. Confirmer que le traitement s'arrête"
      ]
    },
    {
      "id": "TC008",
      "name": "Test cas limite - quantité négative",
      "category": "Boundary",
      "priority": "High",
      "input": {
        "basePrice": 100,
        "discountPercent": 10,
        "customerType": "STANDARD",
        "quantity": -1
      },
      "expectedOutput": "Error: La quantité doit être positive",
      "steps": [
        "1. Appeler calculatePrice(100, 10, 'STANDARD', -1)",
        "2. Vérifier qu'une exception est levée",
        "3. Valider le message d'erreur exact",
        "4. Confirmer que le traitement s'arrête"
      ]
    },
    {
      "id": "TC009",
      "name": "Test combinaison VIP + volume important",
      "category": "Complex",
      "priority": "Medium",
      "input": {
        "basePrice": 200,
        "discountPercent": 20,
        "customerType": "VIP",
        "quantity": 12
      },
      "expectedOutput": 140.16,
      "steps": [
        "1. Appeler calculatePrice(200, 20, 'VIP', 12)",
        "2. Vérifier que le résultat est 140.16",
        "3. Valider remise de base (20%) : 200 -> 160",
        "4. Valider remise VIP (5%) : 160 -> 152",
        "5. Valider remise volume (8%) : 152 -> 140.16"
      ]
    },
    {
      "id": "TC010",
      "name": "Test arrondi décimal",
      "category": "Precision",
      "priority": "Medium",
      "input": {
        "basePrice": 99.99,
        "discountPercent": 33.33,
        "customerType": "STANDARD",
        "quantity": 1
      },
      "expectedOutput": 66.66,
      "steps": [
        "1. Appeler calculatePrice(99.99, 33.33, 'STANDARD', 1)",
        "2. Vérifier que le résultat est exactement 66.66",
        "3. Valider l'arrondi à 2 décimales",
        "4. Confirmer la précision du calcul"
      ]
    }
  ]
}
```

##### Format Markdown

```markdown
# Plan de Test Manuel : Fonction calculatePrice

## Informations Générales
- **Fonction testée :** calculatePrice
- **Date de génération :** 14 octobre 2024
- **Version :** 1.0
- **Testeur assigné :** [À définir]

## Cas de Test

### TC001 - Test calcul prix normal client standard
**Catégorie :** Nominal | **Priorité :** Haute

**Données d'entrée :**
- Prix de base : 100
- Pourcentage remise : 10
- Type client : STANDARD
- Quantité : 1

**Résultat attendu :** 90

**Étapes de test :**
1. Appeler calculatePrice(100, 10, 'STANDARD', 1)
2. Vérifier que le résultat est 90
3. Valider que le calcul applique 10% de remise
4. Confirmer qu'aucune remise supplémentaire n'est appliquée

**Critères de succès :** ✅ Le prix calculé est exactement 90

---

### TC002 - Test calcul prix client VIP
**Catégorie :** Nominal | **Priorité :** Haute

**Données d'entrée :**
- Prix de base : 100
- Pourcentage remise : 10
- Type client : VIP
- Quantité : 1

**Résultat attendu :** 85.5

**Étapes de test :**
1. Appeler calculatePrice(100, 10, 'VIP', 1)
2. Vérifier que le résultat est 85.5
3. Valider la remise de base (10%) : 100 → 90
4. Valider la remise VIP (5%) : 90 → 85.5

**Critères de succès :** ✅ Le prix calculé inclut la remise VIP

---

### TC006 - Test cas limite - prix zéro
**Catégorie :** Boundary | **Priorité :** Haute

**Données d'entrée :**
- Prix de base : 0
- Pourcentage remise : 10
- Type client : STANDARD
- Quantité : 1

**Résultat attendu :** Exception "Le prix de base doit être positif"

**Étapes de test :**
1. Appeler calculatePrice(0, 10, 'STANDARD', 1)
2. Vérifier qu'une exception est levée
3. Valider le message d'erreur exact
4. Confirmer que le traitement s'arrête

**Critères de succès :** ❌ Une exception appropriée est levée

---

## Matrice de Couverture

| Scénario | Couvert | ID Test |
|----------|---------|---------|
| Calcul nominal | ✅ | TC001 |
| Client VIP | ✅ | TC002 |
| Client PREMIUM | ✅ | TC003 |
| Remise volume 5-9 | ✅ | TC004 |
| Remise volume 10+ | ✅ | TC005 |
| Prix invalide | ✅ | TC006 |
| Remise invalide | ✅ | TC007 |
| Quantité invalide | ✅ | TC008 |
| Combinaisons complexes | ✅ | TC009 |
| Précision décimale | ✅ | TC010 |

## Métriques Estimées
- **Nombre total de tests :** 10
- **Temps d'exécution estimé :** 45 minutes
- **Tests priorité haute :** 5
- **Tests priorité moyenne :** 5
```

#### Étape 4 : Instructions pour le QA

1. **Utilisation du JSON :**
   - Importable dans des outils de gestion de tests
   - Facilite la traçabilité et le reporting
   - Permet l'automatisation partielle

2. **Utilisation du Markdown :**
   - Documentation lisible pour l'équipe
   - Intégration facile dans la documentation projet
   - Format idéal pour les revues de test

3. **Validation des résultats :**
   - Exécuter manuellement chaque cas de test
   - Vérifier la logique de calcul
   - Documenter les écarts trouvés

## Bonnes Pratiques

### Prompts efficaces pour l'analyse de code

1. **Soyez spécifique :**
   ```
   "Analysez cette fonction et générez 15 cas de test couvrant :
   - Les cas nominaux (5 tests)
   - Les cas limites (5 tests) 
   - Les cas d'erreur (5 tests)"
   ```

2. **Demandez des formats structurés :**
   ```
   "Exportez en JSON avec les champs : id, name, input, expected, steps, category"
   ```

3. **Incluez des critères de qualité :**
   ```
   "Assurez-vous que les tests couvrent 100% des branches de code"
   ```

### Vérification des cas de test générés

- ✅ Couverture complète des branches
- ✅ Tests des valeurs limites
- ✅ Gestion des erreurs
- ✅ Combinaisons de paramètres
- ✅ Précision des calculs

## Résumé

Cette approche permet aux testeurs QA de :
- **Automatiser** la génération de cas de test manuels
- **Standardiser** le format de documentation
- **Accélérer** la phase de planification des tests
- **Améliorer** la couverture de test
- **Faciliter** la maintenance des suites de test

L'IA devient un assistant puissant pour identifier les scénarios critiques souvent oubliés lors de la création manuelle de cas de test.