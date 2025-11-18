# Améliorer les stories et critères d'acceptation avec ChatGPT

**ID:** PO-02  
**Plateforme:** ChatGPT + Agile  
**Statut:** Terminé

## Type d'audience
Scrum Master / Product Owner

## AI utilisé
ChatGPT/MS Copilot

## Niveau Connaissance AI
Débutant

## Résumé Technique
Génère des user stories claires et des critères d'acceptation précis automatiquement.

## Objectif
Utiliser l'IA pour améliorer la qualité des user stories et générer des critères d'acceptation complets et précis, garantissant une meilleure compréhension des besoins par l'équipe de développement.

## Contenu

### 1. Exemple de User Story bien structurée

#### User Story exemple
**Contexte :** Application e-commerce, amélioration de l'expérience d'achat

**User Story :**
"En tant qu'utilisateur inscrit sur le site e-commerce, je veux pouvoir sauvegarder des produits dans une liste de souhaits afin de pouvoir les retrouver facilement lors de mes prochaines visites et planifier mes achats futurs."

### 2. Génération des critères d'acceptation

#### Requête exemple pour générer des critères d'acceptation

```
Pour la user story suivante :
"En tant qu'utilisateur inscrit sur le site e-commerce, je veux pouvoir sauvegarder des produits dans une liste de souhaits afin de pouvoir les retrouver facilement lors de mes prochaines visites et planifier mes achats futurs."

Peux-tu me proposer des critères d'acceptation complets en utilisant le format Given/When/Then ?

Assure-toi de couvrir :
- Les cas d'usage normaux
- Les cas limites
- Les validations nécessaires
- L'expérience utilisateur
- La performance attendue
- La compatibilité multi-appareils

Format souhaité :
**Critère 1 :** [Titre descriptif]
- Given : [Conditions initiales]
- When : [Action utilisateur]
- Then : [Résultat attendu]

Ajoute aussi des considérations techniques si pertinentes.
```

#### Exemple de réponse attendue

**Critère 1 :** Ajouter un produit à la liste de souhaits
- **Given :** Je suis connecté et je consulte un produit
- **When :** Je clique sur l'icône "♡" ou "Ajouter aux souhaits"
- **Then :** Le produit est ajouté à ma liste de souhaits et l'icône devient "♥" (remplie)

**Critère 2 :** Accéder à ma liste de souhaits
- **Given :** J'ai au moins un produit dans ma liste de souhaits
- **When :** Je clique sur l'icône "Liste de souhaits" dans le menu
- **Then :** Je vois tous mes produits sauvegardés avec leurs informations principales (nom, prix, disponibilité)

**Critère 3 :** Retirer un produit de la liste
- **Given :** Je consulte ma liste de souhaits contenant des produits
- **When :** Je clique sur "Supprimer" ou l'icône "×" d'un produit
- **Then :** Le produit est retiré de la liste et un message de confirmation s'affiche

**Critère 4 :** Gestion des produits indisponibles
- **Given :** Un produit de ma liste de souhaits devient indisponible
- **When :** Je consulte ma liste de souhaits
- **Then :** Le produit est clairement marqué comme "Indisponible" avec une option pour être notifié de son retour

**Critère 5 :** Limite de la liste de souhaits
- **Given :** Ma liste de souhaits contient déjà 100 produits (limite système)
- **When :** Je tente d'ajouter un nouveau produit
- **Then :** Un message m'informe de la limite atteinte et me propose de supprimer d'anciens produits

### 3. Prompts avancés pour l'amélioration continue

#### Révision de stories existantes
```
Analyse cette user story et propose des améliorations :
[Coller la story existante]

Vérifie si elle respecte les critères INVEST :
- Independent (Indépendante)
- Negotiable (Négociable)
- Valuable (Valeur ajoutée)
- Estimable (Estimable)
- Small (Petite)
- Testable (Testable)

Propose une version améliorée si nécessaire.
```

#### Découpage de stories trop importantes
```
Cette user story semble trop importante pour un sprint :
[Coller la story]

Peux-tu me proposer un découpage en plusieurs stories plus petites tout en :
- Conservant la valeur métier de chaque partie
- Maintenant l'indépendance entre les stories
- Assurant une progression logique pour l'utilisateur
- Permettant des livraisons incrementales
```

### 4. Conseils d'utilisation

#### Bonnes pratiques
- **Contexte riche :** Fournissez toujours le contexte projet/utilisateur à l'IA
- **Itération :** N'hésitez pas à demander des variantes ou améliorations
- **Validation équipe :** Toujours faire valider les résultats par l'équipe de développement
- **Adaptation :** Ajustez les critères selon les standards de votre organisation

#### Pièges à éviter
- Ne pas utiliser les résultats sans révision humaine
- Éviter les critères trop techniques sans valeur utilisateur
- Ne pas oublier les aspects non-fonctionnels (performance, sécurité)

## Résumé

Cette approche permet aux Scrum Masters et Product Owners de :
- **Accélérer** la création de user stories bien structurées
- **Améliorer** la qualité des critères d'acceptation
- **Réduire** les ambiguïtés et malentendus en équipe
- **Standardiser** le format des stories dans l'organisation
- **Gagner du temps** sur la préparation des sprints

L'IA devient un assistant précieux pour transformer les besoins métier en spécifications claires et actionnables, tout en maintenant l'aspect humain essentiel dans la validation et l'adaptation au contexte spécifique du projet.