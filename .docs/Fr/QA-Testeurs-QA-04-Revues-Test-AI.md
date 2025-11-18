# Améliorer la qualité logicielle grâce aux revues de test AI

**ID:** QA-04  
**Plateforme:** ChatGPT + GitHub PR  

## Type d'audience
QA / Testeurs

## AI utilisé
ChatGPT/MS Copilot

## Niveau Connaissance AI
Intermédiaire

## Résumé Technique
Comment ChatGPT peut t'aider à relire et commenter les plans de test ou résultats d'exécution.

Supposons que la documentation contient ces informations sur la structure d'information d'un client :

### Propriétés du modèle Client

| Nom    | Type                               | Obligatoire | Exemple             | Description                                       |
| ------ | ---------------------------------- | ----------: | ------------------- | ------------------------------------------------- |
| id     | string (UUID)                      |           ✅ | `c_7f2b9a`          | Identifiant unique du client                      |
| prenom | string                             |           ✅ | `Marie`             | Prénom légal                                      |
| nom    | string                             |           ✅ | `Tremblay`          | Nom de famille                                    |
| email  | string (email)                     |           ✅ | `marie@exemple.com` | Courriel principal, unique                        |
| statut | enum(`prospect`,`actif`,`inactif`) |           ✅ | `actif`             | État du client                                    |
| solde  | number(decimal)                    |             | `-25.50`            | Solde du compte (positif = dû; négatif = crédit) |

### Actions disponibles
| Action                | Paramètres                      | Retour                             | Notes                                                  |
| --------------------- | ------------------------------- | ---------------------------------- | ------------------------------------------------------ |
| creerClient           | `payload: {prenom, nom, email}` | `Client`                           | Initialise `statut="prospect"`.                        |
| activerClient         | `id`                            | `Client`                           | Passe `statut` à `actif` (idempotent).                 |
| mettreAJourEmail      | `id, email`                     | `Client`                           | Valide unicité et format email.                        |
| verifierPlafondCredit | `id, montant`                   | `{autorise:boolean, reste:number}` | Vérifie `solde + montant <= limiteClient` (si défini)  |

### Prompt à utiliser avec l'IA

```
À partir de la doc ci-dessus (propriétés et actions du modèle Client), 
génère 6 cas de test unitaires couvrant les scénarios suivants : 
création de client valide, email invalide, activation idempotente, 
mise à jour d'email en doublon, vérification de plafond de crédit 
autorisée et refusée. 

Pour chaque cas, fournis préconditions, entrée, étapes, résultat attendu. 
Je suis un QA, je n'ai pas de formation technique. 

Format souhaité pour chaque test :
- Titre
- Description
- Step by Step
- Résultat attendu
- Résultat obtenu
```

### Résultat généré par l'IA
---

#### **Test 1 : Création de client valide**

**Description **
Précondition : aucun client n’existe avec l’email **[marie@exemple.com](mailto:marie@exemple.com)**. On vérifie qu’un client peut être créé avec des informations valides.

**Step by Step**

1. Ouvrir le site **BackOffice Clients** et se connecter.
2. Menu **Clients** → bouton **Nouveau client**.
3. Remplir : *Prénom* = `Marie`, *Nom* = `Tremblay`, *Email* = `marie@exemple.com`.
4. Cliquer **Enregistrer**.
5. Observer la fiche client qui s’affiche.

**Résultat attendu**

* Un message de succès s’affiche « Client créé ».
* La fiche montre `Statut = prospect`, `Prénom = Marie`, `Nom = Tremblay`, `Email = marie@exemple.com`.
* Un identifiant (ID) est visible et non vide.

**Résultat obtenu**
À compléter lors de l’exécution.

---

#### **Test 2 : Email invalide (validation d'entrée)**

**Titre :** Création refusée — email invalide

**Description **
Précondition : aucune contrainte particulière. On vérifie que le système refuse un email au mauvais format.

**Step by Step**

1. Ouvrir **BackOffice Clients** → **Nouveau client**.
2. Remplir : *Prénom* = `Alex`, *Nom* = `Dubois`, *Email* = `alex@@exemple..com`.
3. Cliquer **Enregistrer**.

**Résultat attendu**

* Aucune fiche n’est créée.
* Un message d’erreur apparaît près du champ email : « Adresse courriel invalide ».

**Résultat obtenu**
À compléter lors de l’exécution.

---

#### **Test 3 : Idempotence d'activation**

**Titre :** Activation idempotente (2e clic sans effet)

**Description **
Précondition : un client existe avec `Email = prospect@exemple.com` et `Statut = prospect`. On vérifie qu’activer deux fois ne produit pas d’effet supplémentaire.

**Step by Step**

1. Chercher `prospect@exemple.com` via **Clients → Rechercher** et ouvrir la fiche.
2. Cliquer **Activer** → confirmer si demandé.
3. Vérifier que le `Statut` est passé à `actif`.
4. Cliquer **Activer** à nouveau (2e fois).

**Résultat attendu**

* Après le 1er clic : message « Client activé », `Statut = actif`.
* Au 2e clic : soit aucun changement, soit message informatif « Client déjà actif » (pas d’erreur).
* L’historique ne duplique pas l’événement d’activation (1 seule entrée).

**Résultat obtenu**
À compléter lors de l’exécution.

---

#### **Test 4 : Contrainte d'unicité d'email**

**Titre :** Mise à jour d'email en doublon (refus)

**Description **
Précondition : deux clients existent — **C1** avec `unique1@exemple.com` et **C2** avec `unique2@exemple.com`. On vérifie que l’email doit rester unique lors d’une modification.

**Step by Step**

1. Ouvrir la fiche du client **C2** (`unique2@exemple.com`).
2. Cliquer **Modifier**.
3. Remplacer *Email* par `unique1@exemple.com`.
4. Cliquer **Enregistrer**.

**Résultat attendu**

* Sauvegarde refusée.
* Message d’erreur : « Adresse courriel déjà utilisée ».
* L’email de **C2** reste `unique2@exemple.com`.

**Résultat obtenu**
À compléter lors de l’exécution.

---

#### **Test 5 : Logique métier - Crédit autorisé**

**Titre :** Vérification du plafond de crédit — autorisée

**Description **
Précondition : client **C3** avec `Solde = 200,00` et `Limite de crédit = 1 000,00`. On vérifie qu’un achat de `300,00` est autorisé.

**Step by Step**

1. Ouvrir la fiche du client **C3**.
2. Cliquer **Nouvelle commande**.
3. Saisir *Montant* = `300,00`.
4. Cliquer **Vérifier crédit** (ou **Soumettre** s’il y a une vérification automatique).

**Résultat attendu**

* Validation acceptée : message « Autorisé ».
* Le système indique le **reste disponible** ≈ `500,00` (1 000,00 − (200,00 + 300,00)).
* La commande peut continuer.

**Résultat obtenu**
À compléter lors de l’exécution.

---

#### **Test 6 : Cas limite - Crédit refusé**

**Titre :** Vérification du plafond de crédit — refusée

**Description **
Précondition : client **C4** avec `Solde = 350,00` et `Limite de crédit = 400,00`. On vérifie qu’un achat de `100,00` est refusé (dépassement).

**Step by Step**

1. Ouvrir la fiche du client **C4**.
2. Cliquer **Nouvelle commande**.
3. Saisir *Montant* = `100,00`.
4. Cliquer **Vérifier crédit** (ou **Soumettre**).

**Résultat attendu**

* Validation refusée : message « Crédit insuffisant ».
* Le système peut afficher **reste** = `-50,00` (400,00 − (350,00 + 100,00)).
* La commande est bloquée (pas de passage à l’étape suivante).

**Résultat obtenu**
À compléter lors de l'exécution.

---

### Analyse de la valeur ajoutée de l'IA

#### **Points forts de la génération automatique :**

1. **Structure standardisée** : Tous les cas suivent le même format (Titre, Description, Steps, Résultats)
2. **Couverture complète** : L'IA identifie automatiquement les scénarios critiques à tester
3. **Langage accessible** : Terminologie adaptée aux QA non-techniques 
4. **Contexte réaliste** : Utilisation d'un "BackOffice Clients" imaginaire mais crédible
5. **Cas positifs et négatifs** : Équilibre entre tests de succès et d'échec

#### **Ce que l'IA apporte aux QA :**

- **Gain de temps** : Génération instantanée vs rédaction manuelle
- **Couverture exhaustive** : L'IA n'oublie pas les cas limites
- **Cohérence** : Format uniforme facilite la maintenance
- **Inspiration** : Suggestions de scénarios auxquels on n'aurait pas pensé

#### **Bonnes pratiques identifiées :**

✅ **Documentation source structurée** : Plus la doc est claire, meilleurs sont les tests  
✅ **Prompt précis** : Spécifier le format et l'audience cible  
✅ **Exemples concrets** : Utiliser des valeurs réalistes  
✅ **Validation humaine** : Réviser et adapter selon le contexte

### Étapes pour reproduire cette approche

1. **Préparer la documentation** : Structurer les propriétés et actions du système
2. **Formuler le prompt** : Préciser format, audience et scénarios souhaités
3. **Générer les cas** : Utiliser l'IA pour créer la première version
4. **Réviser et adapter** : Ajuster selon le contexte spécifique du projet
5. **Intégrer dans le processus** : Incorporer dans les outils de gestion de test

### Templates réutilisables

#### **Template de prompt pour génération de tests :**
```
À partir de la documentation ci-dessous pour [SYSTÈME/MODULE], 
génère [NOMBRE] cas de test couvrant : [LISTE_SCENARIOS]

Format requis pour chaque test :
- Titre descriptif
- Description (contexte + objectif)
- Étapes détaillées
- Résultat attendu précis
- Résultat obtenu (à compléter)

Audience : QA [niveau technique]
Interface : [Web/API/Mobile/Desktop]
```

#### **Checklist de couverture de test :**
- [ ] Cas nominal (happy path)
- [ ] Validation des entrées (format, obligatoire)
- [ ] Contraintes métier (unicité, limites)
- [ ] Gestion d'erreurs
- [ ] Cas limites (boundaries)
- [ ] Opérations idempotentes



## Contenu

### Objectifs
- Utiliser l'IA pour améliorer la qualité des plans de test
- Générer automatiquement des cas de test structurés à partir de documentation technique
- Faciliter la création de tests pour les QA non-techniques
- Accélérer la couverture de test en transformant des spécifications en cas d'usage concrets

### Méthodologie : De la documentation technique aux cas de test

#### 1. Préparation de la documentation source
L'IA a besoin d'une documentation structurée pour générer des tests de qualité. Dans l'exemple présenté, nous avons :

**Documentation du modèle Client :**
- **Propriétés** : Structure des données avec types, contraintes et exemples
- **Actions** : Opérations disponibles avec paramètres et retours attendus

#### 2. Prompt structuré pour l'IA

**Template de demande :**
```
À partir de la doc ci-dessus (propriétés et actions du modèle [NOM]), 
génère [NOMBRE] cas de test unitaires couvrant les scénarios suivants : 
[LISTE DES SCÉNARIOS À COUVRIR]

Pour chaque cas, fournis :
- Titre
- Description   
- Step by Step
- Résultat attendu
- Résultat obtenu (à compléter)

Format adapté pour QA sans formation technique.
```

#### 3. Exemple concret : Modèle Client

**Documentation technique fournie à l'IA :**

**Propriétés du Client :**

## Résumé

L'IA révolutionne la création de cas de test en transformant la documentation technique en plans de test structurés et accessibles. 

**Processus démontré :**
1. **Documentation technique** → Propriétés et actions du modèle Client
2. **Prompt structuré** → Demande de 6 cas couvrant différents scénarios
3. **Génération automatique** → Tests formatés pour QA non-techniques
4. **Résultat** → Couverture complète avec cas positifs, négatifs et limites

**Bénéfices mesurables :**
- **Gain de temps** : 6 cas de test générés en quelques secondes vs plusieurs heures manuellement
- **Qualité supérieure** : Couverture exhaustive incluant cas limites souvent oubliés
- **Standardisation** : Format uniforme facilite maintenance et exécution
- **Accessibilité** : Langage adapté aux QA sans formation technique approfondie

**Types de tests couverts automatiquement :**
- ✅ Validation d'entrées (format email, champs obligatoires)
- 🔄 Comportements métier (idempotence, contraintes d'unicité)
- 📊 Logique applicative (calculs de plafond, règles de gestion)
- ⚠️ Cas limites et gestion d'erreurs

Cette approche transforme la création de tests d'une tâche fastidieuse en processus créatif assisté par l'IA, permettant aux QA de se concentrer sur l'analyse et l'amélioration plutôt que sur la rédaction répétitive.