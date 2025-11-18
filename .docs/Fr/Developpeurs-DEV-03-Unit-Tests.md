# Créer des Unit Tests automatiquement

**ID:** DEV-03  
**Plateforme:** GitHub Enterprise + Copilot  

## Type d'audience
Développeurs

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Intermédiaire

## Résumé Technique
Génère des tests unitaires cohérents à partir du code source pour éviter les oublis et erreurs manuelles.

## Contenu

### 🧠 Introduction – L'AI pour la qualité du code

GitHub Copilot Enterprise révolutionne la création de tests unitaires en générant automatiquement des scénarios de test complets, y compris les cas d'erreur que les développeurs oublient souvent. Cette approche permet de :

- **Détecter les bugs** avant qu'ils atteignent la production
- **Couvrir tous les cas** y compris les edge cases
- **Accélérer le développement** en automatisant l'écriture des tests
- **Améliorer la qualité** grâce à l'analyse intelligente du code

### 🧪 Démonstration 1 — Créer une fonction avec une erreur

#### 🎯 But
Créer intentionnellement une fonction Python contenant une erreur logique pour démontrer la capacité de l'AI à détecter et corriger les problèmes.

#### ⚙️ Étapes techniques

1. **Crée un fichier `calculator.py`** avec cette fonction :

```python
def calculate_average(numbers):
    """
    Calcule la moyenne d'une liste de nombres.
    
    Args:
        numbers (list): Liste de nombres
        
    Returns:
        float: La moyenne des nombres
    """
    if len(numbers) == 0:
        return 0
    
    total = sum(numbers)
    # ERREUR INTENTIONNELLE : division par la longueur + 1 au lieu de len(numbers)
    average = total / (len(numbers) + 1)
    return average

def divide_numbers(a, b):
    """
    Divise deux nombres.
    
    Args:
        a (float): Le dividende
        b (float): Le diviseur
        
    Returns:
        float: Le résultat de la division
    """
    # ERREUR INTENTIONNELLE : pas de vérification de division par zéro
    return a / b
```

#### 💡 À souligner
- La fonction `calculate_average` a une **erreur de calcul** (+ 1 dans le diviseur)
- La fonction `divide_numbers` manque la **gestion de la division par zéro**
- Ces erreurs sont **subtiles** et courantes dans le développement

### 🧪 Démonstration 2 — Générer des tests unitaires avec l'AI

#### 🎯 But
Utiliser GitHub Copilot pour générer automatiquement des tests unitaires complets qui vont révéler les erreurs dans notre code.

#### ⚙️ Étapes techniques

1. **Sélectionne les fonctions** dans `calculator.py`

2. **Ouvre Copilot Chat** et demande :
```
Génère des tests unitaires complets pour ces fonctions Python.
Inclus des tests pour les cas normaux, les cas limites et les cas d'erreur.
Utilise pytest comme framework de test.
```

3. **Copilot génère** le fichier `test_calculator.py` :

```python
import pytest
from calculator import calculate_average, divide_numbers

class TestCalculateAverage:
    
    def test_calculate_average_normal_case(self):
        """Test avec une liste normale de nombres"""
        numbers = [1, 2, 3, 4, 5]
        result = calculate_average(numbers)
        expected = 3.0  # (1+2+3+4+5) / 5 = 15/5 = 3.0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_calculate_average_single_number(self):
        """Test avec un seul nombre"""
        numbers = [10]
        result = calculate_average(numbers)
        expected = 10.0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_calculate_average_empty_list(self):
        """Test avec une liste vide"""
        numbers = []
        result = calculate_average(numbers)
        expected = 0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_calculate_average_negative_numbers(self):
        """Test avec des nombres négatifs"""
        numbers = [-2, -4, -6]
        result = calculate_average(numbers)
        expected = -4.0  # (-2-4-6) / 3 = -12/3 = -4.0
        assert result == expected, f"Expected {expected}, got {result}"

class TestDivideNumbers:
    
    def test_divide_normal_case(self):
        """Test de division normale"""
        result = divide_numbers(10, 2)
        expected = 5.0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_divide_decimal_result(self):
        """Test avec résultat décimal"""
        result = divide_numbers(7, 3)
        expected = 7/3
        assert abs(result - expected) < 0.0001, f"Expected {expected}, got {result}"
    
    def test_divide_by_zero(self):
        """Test de division par zéro - doit lever une exception"""
        with pytest.raises(ZeroDivisionError):
            divide_numbers(10, 0)
    
    def test_divide_negative_numbers(self):
        """Test avec des nombres négatifs"""
        result = divide_numbers(-10, 2)
        expected = -5.0
        assert result == expected, f"Expected {expected}, got {result}"
```

#### 💡 À souligner
- Copilot génère **automatiquement** des cas de test variés
- Il inclut les **cas d'erreur** comme la division par zéro
- Les tests sont **bien structurés** avec des descriptions claires

### 🧪 Démonstration 3 — Exécuter les tests et identifier les erreurs

#### 🎯 But
Exécuter les tests générés pour révéler les erreurs dans notre code et analyser les résultats avec l'aide de l'AI.

#### ⚙️ Étapes techniques

1. **Installe pytest** si nécessaire :
```bash
pip install pytest
```

2. **Exécute les tests** :
```bash
pytest test_calculator.py -v
```

3. **Observe les échecs** :
```
test_calculator.py::TestCalculateAverage::test_calculate_average_normal_case FAILED
test_calculator.py::TestCalculateAverage::test_calculate_average_single_number FAILED
test_calculator.py::TestCalculateAverage::test_calculate_average_negative_numbers FAILED
test_calculator.py::TestDivideNumbers::test_divide_by_zero FAILED

================================== FAILURES ==================================
______ TestCalculateAverage.test_calculate_average_normal_case ______

    def test_calculate_average_normal_case(self):
        numbers = [1, 2, 3, 4, 5]
        result = calculate_average(numbers)
        expected = 3.0  # (1+2+3+4+5) / 5 = 15/5 = 3.0
>       assert result == expected, f"Expected {expected}, got {result}"
E       AssertionError: Expected 3.0, got 2.5

______ TestDivideNumbers.test_divide_by_zero ______

    def test_divide_by_zero(self):
        with pytest.raises(ZeroDivisionError):
>           divide_numbers(10, 0)
E       ZeroDivisionError: division by zero
```

4. **Demande à Copilot** d'analyser les erreurs :
```
Analyse les résultats de ces tests qui échouent.
Que révèlent-ils sur les erreurs dans calculator.py ?
```

#### 💡 À souligner
- Les tests **révèlent immédiatement** les problèmes
- L'AI aide à **interpréter** les résultats d'échec
- Les messages d'erreur sont **informatifs**

### 🧪 Démonstration 4 — Corriger les erreurs avec l'aide de l'AI

#### 🎯 But
Utiliser Copilot pour identifier et corriger les erreurs détectées par les tests unitaires.

#### ⚙️ Étapes techniques

1. **Montre le code défaillant** à Copilot Chat :
```
Voici ma fonction calculate_average qui échoue aux tests.
Les tests attendaient 3.0 mais ont reçu 2.5 pour [1,2,3,4,5].
Identifie et corrige l'erreur :

[colle le code de la fonction]
```

2. **Copilot identifie l'erreur** et propose la correction :
```python
def calculate_average(numbers):
    """
    Calcule la moyenne d'une liste de nombres.
    
    Args:
        numbers (list): Liste de nombres
        
    Returns:
        float: La moyenne des nombres
    """
    if len(numbers) == 0:
        return 0
    
    total = sum(numbers)
    # CORRECTION : division par len(numbers) au lieu de len(numbers) + 1
    average = total / len(numbers)
    return average
```

3. **Pour la fonction divide_numbers**, demande :
```
Ma fonction divide_numbers doit gérer la division par zéro.
Comment l'améliorer ?
```

4. **Copilot propose** :
```python
def divide_numbers(a, b):
    """
    Divise deux nombres.
    
    Args:
        a (float): Le dividende
        b (float): Le diviseur
        
    Returns:
        float: Le résultat de la division
        
    Raises:
        ZeroDivisionError: Si le diviseur est zéro
    """
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b
```

#### 💡 À souligner
- Copilot **identifie rapidement** les erreurs logiques
- Il propose des **corrections précises**
- Il améliore aussi la **documentation** des fonctions

### 🧪 Démonstration 5 — Validation finale

#### 🎯 But
Vérifier que les corrections sont efficaces en ré-exécutant tous les tests.

#### ⚙️ Étapes techniques

1. **Applique les corrections** au fichier `calculator.py`

2. **Ré-exécute les tests** :
```bash
pytest test_calculator.py -v
```

3. **Observe le succès** :
```
test_calculator.py::TestCalculateAverage::test_calculate_average_normal_case PASSED
test_calculator.py::TestCalculateAverage::test_calculate_average_single_number PASSED
test_calculator.py::TestCalculateAverage::test_calculate_average_empty_list PASSED
test_calculator.py::TestCalculateAverage::test_calculate_average_negative_numbers PASSED
test_calculator.py::TestDivideNumbers::test_divide_normal_case PASSED
test_calculator.py::TestDivideNumbers::test_divide_decimal_result PASSED
test_calculator.py::TestDivideNumbers::test_divide_by_zero PASSED
test_calculator.py::TestDivideNumbers::test_divide_negative_numbers PASSED

======================== 8 passed in 0.03s ========================
```

4. **Demande un rapport de couverture** :
```bash
pytest --cov=calculator test_calculator.py
```

#### 💡 À souligner
- **100% de réussite** après correction
- La **couverture de code** est optimale
- Le processus est **rapide et efficace**

## Résumé

Cet article démontre le **cycle complet de développement assisté par l'AI** pour la création et la validation de tests unitaires automatisés.

**Processus en 5 étapes :**
1. **🐛 Création intentionnelle** d'une fonction avec erreurs logiques
2. **🤖 Génération automatique** de tests unitaires complets par Copilot
3. **🔍 Exécution et analyse** des échecs de tests 
4. **🔧 Correction assistée** des erreurs identifiées par l'AI
5. **✅ Validation finale** avec succès de tous les tests

**Bénéfices démontrés :**
- **Détection automatique** des erreurs subtiles (calcul incorrect, division par zéro)
- **Génération exhaustive** de cas de test (normaux, limites, erreurs)
- **Correction guidée** avec explications claires des problèmes
- **Cycle rapide** de développement-test-correction

**Résultat :** GitHub Copilot Enterprise transforme la création de tests unitaires d'une corvée en un processus collaboratif intelligent qui améliore significativement la qualité du code.

## Résumé

_À compléter..._