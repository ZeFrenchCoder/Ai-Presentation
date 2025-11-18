# Planifier et prioriser avec l'aide de l'AI

**ID:** PO-01  
**Plateforme:** GitHub Enterprise + Planification  
**Statut:** Actif

## Type d'audience
Scrum Master / Product Owner

## AI utilisé
GitHub Enterprise

## Niveau Connaissance AI
Débutant

## Résumé Technique
L'AI aide à découper les stories, estimer les efforts et prioriser selon la valeur métier.

## Contenu

### Exemple pratique : Feature "Système de notifications personnalisables"

**Feature à développer :**
Notre application e-commerce a besoin d'un système permettant aux utilisateurs de configurer leurs préférences de notifications (email, SMS, push) pour différents événements (commandes, promotions, livraisons).

### Requête AI pour le découpage et la priorisation

```
En tant que Scrum Master/Product Owner, j'ai la feature suivante à planifier :

**Feature :** Système de notifications personnalisables pour une application e-commerce

**Description :** Les utilisateurs doivent pouvoir configurer leurs préférences de notifications (email, SMS, push) pour différents types d'événements (confirmation de commande, statut de livraison, promotions, rappels de panier abandonné).

**Contraintes :**
- Équipe de 5 développeurs
- Sprint de 2 semaines
- Intégration avec les systèmes existants (email, SMS gateway, push notifications)
- Respect du RGPD

Peux-tu m'aider à :
1. Découper cette feature en user stories priorisées
2. Estimer les efforts en story points pour chaque story
3. Proposer une priorisation basée sur la valeur métier
4. Identifier les dépendances techniques
5. Suggérer un plan de livraison progressive (MVP puis améliorations)

Pour chaque story, indique :
- Le titre et la description (format "En tant que... je veux... afin de...")
- L'estimation en story points (échelle fibonacci : 1, 2, 3, 5, 8, 13)
- La valeur métier (Haute, Moyenne, Faible)
- Les critères d'acceptation principaux
- Les dépendances éventuelles
```

### Exemple de réponse AI structurée

L'IA répondrait avec une structure comme :

**Epic :** Système de notifications personnalisables

**MVP - Sprint 1 (13 points)**
1. **US-001** - Configuration de base des notifications email (5 pts, Valeur Haute)
2. **US-002** - Notifications de confirmation de commande (3 pts, Valeur Haute)  
3. **US-003** - Interface utilisateur de gestion des préférences (5 pts, Valeur Haute)

**Améliorations - Sprint 2 (16 points)**
4. **US-004** - Notifications SMS (8 pts, Valeur Moyenne)
5. **US-005** - Notifications push mobile (5 pts, Valeur Moyenne)
6. **US-006** - Notifications de livraison (3 pts, Valeur Haute)

**Features avancées - Sprint 3+ (21 points)**
7. **US-007** - Notifications promotionnelles ciblées (8 pts, Valeur Moyenne)
8. **US-008** - Rappels de panier abandonné (5 pts, Valeur Faible)
9. **US-009** - Historique et analytics des notifications (8 pts, Valeur Faible)

### Bénéfices de cette approche

- **Gain de temps :** Découpage initial en 15 minutes au lieu de 2-3 heures d'atelier
- **Objectivité :** Priorisation basée sur des critères métier clairs
- **Completude :** L'IA identifie des aspects souvent oubliés (RGPD, analytics)
- **Cohérence :** Format standardisé pour toutes les stories

### Conseils d'utilisation

1. **Affinez les estimations :** Utilisez les suggestions AI comme base, puis ajustez avec l'équipe
2. **Validez la priorisation :** Confrontez les priorités AI avec les objectifs business
3. **Itérez :** Utilisez l'AI pour re-prioriser en cours de développement

## Résumé

Cette méthode permet aux Scrum Masters et Product Owners d'utiliser l'IA comme assistant de planification intelligent. En fournissant le contexte métier et les contraintes techniques, l'IA génère un découpage structuré avec estimations et priorisation, servant de base solide pour les discussions d'équipe et la planification des sprints.