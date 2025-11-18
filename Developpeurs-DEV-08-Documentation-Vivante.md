# Documentation vivante grâce à l'AI

**ID:** DEV-08  
**Plateforme:** ChatGPT + GitHub Wiki  

## Type d'audience
Développeurs

## AI utilisé
ChatGPT/MS Copilot

## Niveau Connaissance AI
Avancé

## Résumé Technique
L'AI crée et met à jour la documentation technique à partir des commits et du code.

## Contenu

### 🧠 Introduction

La **documentation technique** est souvent en retard sur le code ou incomplète. Les développeurs écrivent du code mais négligent la documentation, créant des problèmes de maintenance et d'onboarding.

**L'IA peut automatiser** la création de documentation :
- **Documenter les fonctions** directement dans le code
- **Expliquer les tests** avec références aux tickets
- **Générer la doc système** complète
- **Créer les guides** de démarrage

**Avantage** : Documentation toujours à jour et synchronisée avec le code.

### 🧪 Exemple 1 — Documenter une fonction dans le code

#### Situation
Tu as une fonction dans ton API .NET et tu veux la documenter proprement.

#### Ce que tu fais

1. **Ta fonction sans doc** :
```csharp
// Controllers/UsersController.cs
public async Task<ActionResult<UserDto>> GetUserById(int id)
{
    var user = await _userService.GetUserByIdAsync(id);
    if (user == null)
        return NotFound($"User with ID {id} not found");
    
    return Ok(_mapper.Map<UserDto>(user));
}
```

2. **Demande à Copilot** :
```
@workspace Documente cette fonction C# avec :
- Résumé de ce qu'elle fait
- Paramètres et leur validation
- Retours possibles avec codes HTTP
- Exemple d'utilisation

Format XML standard .NET
```

3. **Copilot génère la documentation** :
```csharp
// Controllers/UsersController.cs

/// <summary>
/// Récupère un utilisateur spécifique par son identifiant unique.
/// </summary>
/// <param name="id">L'identifiant unique de l'utilisateur (doit être positif)</param>
/// <returns>
/// Les informations de l'utilisateur au format UserDto si trouvé,
/// sinon retourne NotFound (404)
/// </returns>
/// <response code="200">Utilisateur trouvé et retourné avec succès</response>
/// <response code="404">Aucun utilisateur trouvé avec cet ID</response>
/// <response code="400">ID invalide (négatif ou zéro)</response>
/// <example>
/// GET /api/users/123
/// Retourne : { "id": 123, "name": "John Doe", "email": "john@example.com" }
/// </example>
/// <remarks>
/// Cette méthode utilise le service UserService pour accéder aux données.
/// Le mapping vers UserDto exclut les informations sensibles comme le mot de passe.
/// </remarks>
[HttpGet("{id}")]
public async Task<ActionResult<UserDto>> GetUserById(int id)
{
    var user = await _userService.GetUserByIdAsync(id);
    if (user == null)
        return NotFound($"User with ID {id} not found");
    
    return Ok(_mapper.Map<UserDto>(user));
}
```

### 🧪 Exemple 2 — Documenter des tests avec référence ticket

#### Situation
Tu écris des tests unitaires pour une story Jira et tu veux documenter le contexte.

#### Ce que tu fais

1. **Ton test sans documentation** :
```csharp
// Tests/UsersControllerTests.cs
[Test]
public async Task GetUserById_ReturnsUser_WhenUserExists()
{
    var userId = 123;
    var user = new User { Id = userId, Name = "Test User" };
    _userService.Setup(x => x.GetUserByIdAsync(userId)).ReturnsAsync(user);

    var result = await _controller.GetUserById(userId);
    
    Assert.IsInstanceOf<OkObjectResult>(result.Result);
}
```

2. **Demande à Copilot** :
```
@workspace Documente ce test avec :
- Référence au ticket Jira US-456
- Contexte métier du test
- Scénario testé 
- Critères d'acceptation validés

Format standard avec Given/When/Then
```

3. **Copilot documente le test** :
```csharp
// Tests/UsersControllerTests.cs

/// <summary>
/// Test de récupération d'utilisateur - Cas de succès
/// 
/// Ticket: US-456 - "En tant qu'admin, je veux consulter le profil d'un utilisateur 
/// pour vérifier ses informations personnelles"
/// 
/// Contexte métier: 
/// Les administrateurs doivent pouvoir accéder aux profils utilisateurs pour 
/// le support client et la gestion des comptes.
/// 
/// Scénario: Consultation réussie d'un profil utilisateur existant
/// 
/// Critères d'acceptation validés:
/// - ✅ AC1: L'API retourne les données utilisateur quand l'ID existe
/// - ✅ AC2: Le format de réponse respecte le contrat UserDto
/// - ✅ AC3: Le code de retour HTTP est 200 OK
/// </summary>
/// <remarks>
/// Given: Un utilisateur existe avec l'ID 123 dans la base
/// When: L'admin fait une requête GET /api/users/123  
/// Then: L'API retourne 200 OK avec les données au format UserDto
/// 
/// Référence: https://jira.company.com/browse/US-456
/// </remarks>
[Test]
public async Task GetUserById_ReturnsUser_WhenUserExists()
{
    // Arrange - Given: Un utilisateur existe dans le système
    var userId = 123;
    var user = new User { Id = userId, Name = "Test User", Email = "test@example.com" };
    _userService.Setup(x => x.GetUserByIdAsync(userId)).ReturnsAsync(user);

    // Act - When: L'admin demande les infos de cet utilisateur
    var result = await _controller.GetUserById(userId);
    
    // Assert - Then: L'API retourne les données avec succès
    Assert.IsInstanceOf<OkObjectResult>(result.Result);
    var okResult = result.Result as OkObjectResult;
    var userDto = okResult.Value as UserDto;
    Assert.AreEqual(userId, userDto.Id);
    Assert.AreEqual("Test User", userDto.Name);
}
```

### 🧪 Exemple 3 — Documenter le système complet

#### Situation
Tu veux générer une documentation complète du système dans `./docs/system.md`.

#### Ce que tu fais

1. **Demande à Copilot** :
```
@workspace Génère une documentation système complète dans ./docs/system.md pour notre API .NET

Inclus :
- Architecture générale
- APIs disponibles avec exemples
- Base de données et entités
- Services et dépendances
- Configuration et déploiement

Termine par la date, ticket US-789 et utilisateur andre.theriault@cgi.com
```

2. **Copilot génère** `./docs/system.md` :
```markdown
# Documentation Système - UserManagement API

## 🏗️ Architecture Générale

Cette API .NET Core 6.0 fournit un système de gestion d'utilisateurs avec authentification JWT et base de données SQL Server.

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Client Web    │────│   API Gateway   │────│  UserMgmt API   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                                               ┌─────────────────┐
                                               │  SQL Server DB  │
                                               └─────────────────┘
```

## 📡 APIs Disponibles

### Gestion des Utilisateurs
```http
GET    /api/users           # Liste tous les utilisateurs
GET    /api/users/{id}      # Récupère un utilisateur par ID
POST   /api/users           # Crée un nouvel utilisateur
PUT    /api/users/{id}      # Met à jour un utilisateur
DELETE /api/users/{id}      # Supprime un utilisateur
```

### Authentification
```http
POST   /api/auth/login      # Connexion utilisateur
POST   /api/auth/logout     # Déconnexion
POST   /api/auth/refresh    # Renouvellement token JWT
```

### Exemple d'utilisation
```bash
# Créer un utilisateur
curl -X POST https://api.company.com/api/users \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {token}" \
  -d '{
    "name": "John Doe",
    "email": "john.doe@company.com",
    "role": "User"
  }'

# Réponse
{
  "id": 456,
  "name": "John Doe", 
  "email": "john.doe@company.com",
  "role": "User",
  "createdAt": "2025-10-13T10:30:00Z"
}
```

## 🗄️ Base de Données

### Entité User
```sql
CREATE TABLE Users (
    Id int IDENTITY(1,1) PRIMARY KEY,
    Name nvarchar(100) NOT NULL,
    Email nvarchar(255) NOT NULL UNIQUE,
    PasswordHash nvarchar(255) NOT NULL,
    Role nvarchar(50) NOT NULL DEFAULT 'User',
    CreatedAt datetime2 NOT NULL DEFAULT GETDATE(),
    UpdatedAt datetime2 NOT NULL DEFAULT GETDATE(),
    IsActive bit NOT NULL DEFAULT 1
);
```

### Relations
- Un utilisateur peut avoir plusieurs sessions (table UserSessions)
- Un utilisateur peut avoir plusieurs rôles (table UserRoles)

## 🔧 Services et Dépendances

### Services Principaux
- **UserService**: Logique métier des utilisateurs
- **AuthService**: Gestion authentification JWT
- **EmailService**: Envoi notifications email
- **AuditService**: Traçabilité des actions

### Dépendances NuGet
```xml
<PackageReference Include="Microsoft.AspNetCore.Authentication.JwtBearer" Version="6.0.0" />
<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="6.0.0" />
<PackageReference Include="AutoMapper" Version="12.0.0" />
<PackageReference Include="FluentValidation" Version="11.0.0" />
<PackageReference Include="Serilog" Version="2.12.0" />
```

## ⚙️ Configuration

### Variables d'environnement
```bash
# Base de données
ConnectionStrings__DefaultConnection=Server=localhost;Database=UserMgmtDB;Trusted_Connection=true;

# JWT
JwtSettings__Secret=your-super-secret-key-min-256-bits
JwtSettings__Issuer=UserMgmtAPI
JwtSettings__ExpiryInHours=24

# Email
EmailSettings__SmtpServer=smtp.company.com
EmailSettings__Port=587
EmailSettings__Username=noreply@company.com
EmailSettings__Password=smtp-password
```

### Déploiement
```bash
# Build
dotnet build --configuration Release

# Tests
dotnet test

# Publication
dotnet publish --configuration Release --output ./publish

# Docker
docker build -t usermgmt-api .
docker run -p 8080:80 usermgmt-api
```

## 📊 Monitoring

### Endpoints de santé
- `GET /health` - Statut général de l'API
- `GET /health/db` - Statut base de données
- `GET /health/ready` - API prête à recevoir du trafic

### Logs
- **Serilog** configuré avec rotation quotidienne
- Logs stockés dans `/logs/` et envoyés vers Seq
- Niveaux: Debug, Info, Warning, Error, Fatal

## 🚀 Performance

### Métriques cibles
- **Temps de réponse** : < 200ms (95e percentile)
- **Throughput** : > 1000 req/sec
- **Disponibilité** : 99.9% SLA
- **Base de données** : < 50ms par requête

---

*Documentation générée le 13 octobre 2025*  
*Ticket: US-789*  
*Utilisateur: andre.theriault@cgi.com*


### 🧪 Exemple 4 — Guide de démarrage du système

#### Situation
Nouveau développeur qui rejoint l'équipe et a besoin d'un guide pour démarrer le projet.

#### Ce que tu fais

1. **Demande à Copilot** :
```
@workspace Crée un guide de démarrage dans ./docs/getting-started.md

Pour un nouveau dev qui veut :
- Cloner et setup le projet
- Installer les dépendances
- Configurer la base de données
- Lancer l'application
- Faire ses premiers tests

Étapes claires avec commandes exactes. Termine par date, ticket DEV-123 et utilisateur.
```

2. **Copilot crée** `./docs/getting-started.md` :
```markdown
# Guide de Démarrage - UserManagement API

## 🚀 Setup Initial

### Prérequis
- .NET 6.0 SDK ou plus récent
- SQL Server (LocalDB suffit pour le développement)
- Visual Studio 2022 ou VS Code
- Git

### Vérification des prérequis
```bash
# Vérifier .NET
dotnet --version
# Doit afficher 6.0.x ou plus récent

# Vérifier SQL Server LocalDB
sqllocaldb info
# Doit lister les instances disponibles


## 📥 Cloner le Projet

```bash
# Cloner le repository
git clone https://github.com/company/usermanagement-api.git
cd usermanagement-api

# Créer ta branche de développement
git checkout -b feature/ton-nom-setup

...
...
...
```

## Résumé

La **Documentation Vivante avec l'IA** transforme la maintenance documentaire en automatisant :

### ✅ Bénéfices pratiques
- **Documentation synchronisée** avec le code en temps réel
- **Standards respectés** (XML .NET, références tickets, exemples concrets)
- **Guides complets** générés automatiquement
- **Traçabilité** avec dates, tickets et utilisateurs

### 🎯 Types de documentation automatisée
1. **Fonctions** : Documentation XML dans le code avec exemples
2. **Tests** : Contexte métier avec références Jira/DevOps
3. **Système** : Architecture complète avec APIs et déploiement
4. **Guides** : Procédures step-by-step pour nouveaux devs

### 🚀 En pratique
- **Code auto-documenté** avec contexte métier
- **Tests explicites** liés aux user stories
- **Architecture à jour** avec exemples d'usage
- **Onboarding facilité** avec guides détaillés

L'IA maintient une documentation **vivante** qui évolue avec le code, éliminant le décalage traditionnel entre code et documentation.