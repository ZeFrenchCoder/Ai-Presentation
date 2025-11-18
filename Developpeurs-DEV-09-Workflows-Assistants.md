# Se créer des WorkFlow ou Assistant de création

**ID:** DEV-09  
**Plateforme:** GitHub Enterprise + Custom Workflows  

## Type d'audience
Développeurs

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Avancé

## Résumé Technique
Créer des workflows personnalisés et des assistants de création pour automatiser les tâches répétitives et standardiser les processus de développement avec GitHub Copilot Enterprise.

## Contenu

### 🧠 Introduction

Les développeurs font souvent les **mêmes tâches répétitives** : créer des classes, des controllers, des tests, etc. Au lieu de refaire les mêmes questions à l'IA à chaque fois, tu peux créer des **workflows assistés** avec des fichiers JSON.

**L'idée** : L'IA utilise un fichier de configuration pour te poser les bonnes questions dans le bon ordre et générer exactement ce dont tu as besoin.

**Avantage** :
- **Standardisation** : Même processus pour toute l'équipe
- **Rapidité** : L'IA sait quoi demander  
- **Qualité** : Rien n'est oublié
- **Réutilisabilité** : Un workflow pour plusieurs projets

### 🛠️ Comment ça fonctionne

1. **Tu crées** un fichier JSON de configuration dans `./workflows/`
2. **L'IA lit** le workflow et suit les étapes
3. **L'IA te pose** chaque question une par une
4. **L'IA génère** le code final avec tes réponses

### 🧪 Exemple 1 — Workflow création de classe

#### Demande initiale : Créer le workflow

**Utilisateur** demande à l'IA :
> "Je veux créer un fichier de configuration JSON pour un workflow assistant qui m'aide à créer des classes.
> 
> Le workflow doit me poser ces questions :
> 1. Quel est le nom de la classe ?
> 2. Quelles sont les propriétés de la classe ?
> 3. Des validations sur la classe ?
> 4. Des calculs sur la classe ?
> 5. Des actions spéciales ?
> 6. Quel format de sortie (C#, VB.NET, Python, Java, Documentation) ?
> 
> Crée le fichier `./workflows/create-class-workflow.json` avec toute la structure nécessaire."

#### Étape 1 : L'IA crée le fichier workflow

L'IA génère `./workflows/create-class-workflow.json` :

```json
{
  "name": "Créateur de Classe",
  "description": "Assistant pour créer une classe avec propriétés, validations et méthodes",
  "version": "1.0",
  "steps": [
    {
      "id": "class_name",
      "question": "Quel est le nom de la classe ?",
      "type": "string",
      "required": true,
      "validation": "^[A-Z][a-zA-Z0-9]*$",
      "example": "Client, Product, Order"
    },
    {
      "id": "properties",
      "question": "Quelle est la liste des propriétés ? (Format: nom:type:description)",
      "type": "array",
      "required": true,
      "example": [
        "Id:int:Identifiant unique",
        "Name:string:Nom complet du client", 
        "Email:string:Adresse email",
        "DateCreated:DateTime:Date de création"
      ]
    },
    {
      "id": "validations",
      "question": "Des validations sur la classe ? (Format: propriété:règle:message)",
      "type": "array",
      "required": false,
      "example": [
        "Name:Required:Le nom est obligatoire",
        "Email:EmailAddress:Format email invalide",
        "Id:Range(1,int.MaxValue):L'ID doit être positif"
      ]
    },
    {
      "id": "calculations",
      "question": "Des calculs sur la classe ? (Format: nom:formule:description)",
      "type": "array", 
      "required": false,
      "example": [
        "Age:DateTime.Now.Year - DateOfBirth.Year:Calcule l'âge",
        "IsActive:LastLoginDate > DateTime.Now.AddDays(-30):Client actif si connexion récente"
      ]
    },
    {
      "id": "special_actions",
      "question": "Des actions spéciales ? (méthodes personnalisées)",
      "type": "array",
      "required": false,
      "example": [
        "SendWelcomeEmail():Envoie un email de bienvenue",
        "GenerateReport():Génère un rapport client",
        "UpdateLastActivity():Met à jour la dernière activité"
      ]
    },
    {
      "id": "output_format",
      "question": "Quel est le format pour écrire ?",
      "type": "choice",
      "required": true,
      "options": ["C#", "VB.NET", "Python", "Java", "Documentation"],
      "default": "C#"
    }
  ],
  "output": {
    "template": "class_template.txt",
    "file_extension": {
      "C#": ".cs",
      "VB.NET": ".vb", 
      "Python": ".py",
      "Java": ".java",
      "Documentation": ".md"
    }
  }
}
```

#### Étape 2 : L'utilisateur fait sa demande

**Utilisateur** : 
> "Je veux créer une Classe Client."

#### Étape 3 : L'IA active le workflow

**IA** lit le fichier `./workflows/create-class-workflow.json` et répond :

> J'ai détecté que tu veux créer une classe. Je vais utiliser mon workflow assisté pour t'aider. 
> 
> **Question 1/6** : Quel est le nom de la classe ?  
> *(Exemple: Client, Product, Order)*

**Utilisateur** : `Client`

**IA** :
> Parfait ! **Client** est un nom valide.
>
> **Question 2/6** : Quelle est la liste des propriétés ? (Format: nom:type:description)  
> *(Exemple: Id:int:Identifiant unique, Name:string:Nom complet)*

**Utilisateur** : 
```
Id:int:Identifiant unique
Name:string:Nom complet du client
Email:string:Adresse email
Phone:string:Numéro de téléphone
DateCreated:DateTime:Date de création du compte
IsActive:bool:Indique si le client est actif
```

**IA** :
> Excellent ! 6 propriétés enregistrées.
>
> **Question 3/6** : Des validations sur la classe ? (Format: propriété:règle:message)  
> *(Optionnel - appuie sur Entrée pour ignorer)*

**Utilisateur** :
```
Name:Required:Le nom est obligatoire
Email:EmailAddress:Format email invalide
Email:Required:L'email est obligatoire
Phone:Phone:Format de téléphone invalide
Id:Range(1,int.MaxValue):L'ID doit être positif
```

**IA** :
> 5 validations ajoutées.
>
> **Question 4/6** : Des calculs sur la classe ? (Format: nom:formule:description)  
> *(Optionnel - appuie sur Entrée pour ignorer)*

**Utilisateur** :
```
AccountAge:DateTime.Now.Subtract(DateCreated).Days:Âge du compte en jours
IsRecentClient:DateCreated > DateTime.Now.AddMonths(-3):Client récent (moins de 3 mois)
```

**IA** :
> 2 calculs ajoutés.
>
> **Question 5/6** : Des actions spéciales ? (méthodes personnalisées)  
> *(Optionnel - appuie sur Entrée pour ignorer)*

**Utilisateur** :
```
SendWelcomeEmail():Envoie un email de bienvenue au client
DeactivateAccount():Désactive le compte client
GetOrderHistory():Récupère l'historique des commandes
UpdateContactInfo(email, phone):Met à jour les infos de contact
```

**IA** :
> 4 actions spéciales ajoutées.
>
> **Question 6/6** : Quel est le format pour écrire ?  
> **Choix** : C# | VB.NET | Python | Java | Documentation

**Utilisateur** : `C#`

#### Étape 4 : L'IA génère le code

**IA** :
> Parfait ! Je génère ta classe **Client** en C# avec toutes les spécifications...

```csharp
using System;
using System.ComponentModel.DataAnnotations;
using System.Linq;

namespace YourProject.Models
{
    /// <summary>
    /// Représente un client du système avec ses informations personnelles et méthodes associées
    /// Généré automatiquement le 13 octobre 2025
    /// </summary>
    public class Client
    {
        // Propriétés de base
        
        /// <summary>
        /// Identifiant unique
        /// </summary>
        [Required]
        [Range(1, int.MaxValue, ErrorMessage = "L'ID doit être positif")]
        public int Id { get; set; }
        
        /// <summary>
        /// Nom complet du client
        /// </summary>
        [Required(ErrorMessage = "Le nom est obligatoire")]
        public string Name { get; set; }
        
        /// <summary>
        /// Adresse email
        /// </summary>
        [Required(ErrorMessage = "L'email est obligatoire")]
        [EmailAddress(ErrorMessage = "Format email invalide")]
        public string Email { get; set; }
        
        /// <summary>
        /// Numéro de téléphone
        /// </summary>
        [Phone(ErrorMessage = "Format de téléphone invalide")]
        public string Phone { get; set; }
        
        /// <summary>
        /// Date de création du compte
        /// </summary>
        public DateTime DateCreated { get; set; }
        
        /// <summary>
        /// Indique si le client est actif
        /// </summary>
        public bool IsActive { get; set; }
        
        // Propriétés calculées
        
        /// <summary>
        /// Âge du compte en jours
        /// </summary>
        public int AccountAge => DateTime.Now.Subtract(DateCreated).Days;
        
        /// <summary>
        /// Client récent (moins de 3 mois)
        /// </summary>
        public bool IsRecentClient => DateCreated > DateTime.Now.AddMonths(-3);
        
        // Constructeur
        
        public Client()
        {
            DateCreated = DateTime.Now;
            IsActive = true;
        }
        
        // Actions spéciales
        
        /// <summary>
        /// Envoie un email de bienvenue au client
        /// </summary>
        public void SendWelcomeEmail()
        {
            // TODO: Implémenter l'envoi d'email de bienvenue
            Console.WriteLine($"Email de bienvenue envoyé à {Email}");
        }
        
        /// <summary>
        /// Désactive le compte client
        /// </summary>
        public void DeactivateAccount()
        {
            IsActive = false;
            Console.WriteLine($"Compte {Name} désactivé");
        }
        
        /// <summary>
        /// Récupère l'historique des commandes
        /// </summary>
        /// <returns>Liste des commandes du client</returns>
        public List<Order> GetOrderHistory()
        {
            // TODO: Implémenter la récupération des commandes
            return new List<Order>();
        }
        
        /// <summary>
        /// Met à jour les infos de contact
        /// </summary>
        /// <param name="email">Nouvelle adresse email</param>
        /// <param name="phone">Nouveau numéro de téléphone</param>
        public void UpdateContactInfo(string email, string phone)
        {
            Email = email;
            Phone = phone;
            Console.WriteLine($"Informations de contact mises à jour pour {Name}");
        }
        
        public override string ToString()
        {
            return $"Client: {Name} ({Email}) - Créé le {DateCreated:dd/MM/yyyy} - {(IsActive ? "Actif" : "Inactif")}";
        }
    }
}
```

> **✅ Classe Client générée !**
>
> 📁 Fichier sauvé : `./Models/Client.cs`  
> 🎯 Format : C# avec validations DataAnnotations  
> 📊 Contenu : 6 propriétés, 5 validations, 2 calculs, 4 méthodes  
> ⏰ Généré le 13 octobre 2025

### 💡 Autres exemples de workflows

Tu peux créer d'autres workflows dans `./workflows/` :

- `create-controller-workflow.json` - Pour les controllers API
- `create-test-workflow.json` - Pour les tests unitaires  
- `create-migration-workflow.json` - Pour les migrations BD
- `create-service-workflow.json` - Pour les services métier
- `create-dto-workflow.json` - Pour les objets de transfert
- Il est aussi possible de demander de poser les questions une seule à la fois.
- Vous pouvez aussi demander a l'AI d'inscrire les étapes standard pour la création d'un projet, d'une feature, d'un bugfix, d'un billet Jira ou Devops.

### 🎯 Avantages des workflows

**Pour les développeurs** :
- ✅ **Plus d'oublis** - L'IA suit une checklist
- ✅ **Code standardisé** - Même structure pour tous
- ✅ **Gain de temps** - Pas besoin de réexpliquer à chaque fois
- ✅ **Questions pertinentes** - L'IA sait quoi demander

**Pour l'équipe** :
- ✅ **Processus uniforme** - Même workflow pour tous les devs
- ✅ **Knowledge sharing** - Les workflows sont partagés
- ✅ **Amélioration continue** - Les workflows évoluent
- ✅ **Onboarding facilité** - Les nouveaux devs suivent le processus

## Résumé

Les **Workflows Assistants** permettent de créer des processus guidés où l'IA :

### ✅ Ce que ça apporte
- **Standardise** la création de code avec des fichiers JSON de configuration
- **Guide l'utilisateur** avec des questions structurées une par une  
- **Génère automatiquement** le code avec toutes les spécifications
- **Évite les oublis** en suivant une checklist complète

### 🎯 En pratique  
1. **Créer** des workflows JSON dans `./workflows/`
2. **Utiliser** des questions structurées avec validation
3. **Laisser l'IA** guider le processus étape par étape
4. **Obtenir** du code standardisé et complet

### 🚀 Résultat
- **Code cohérent** dans toute l'équipe
- **Processus répétables** et améliorables
- **Gain de temps** significatif
- **Qualité garantie** par la structure

L'IA devient ton **assistant personnel** qui connaît tes processus et t'aide à les appliquer de manière consistante.