# Créer des procédures efficaces avec l'aide de l'AI

**ID:** GEN-06  
**Plateforme:** ChatGPT + MS Copilot + GitHub Copilot Enterprise  
**Statut:** Actif

## Type d'audience
Tous / Transversal

## AI utilisé
ChatGPT / MS Copilot / GitHub Copilot Enterprise

## Niveau Connaissance AI
Débutant à Intermédiaire

## Résumé Technique
Utiliser l'IA pour créer, structurer et optimiser des procédures opérationnelles, techniques et métier. L'IA aide à transformer les connaissances tacites en documentation claire et actionnable.

## Contenu

## Contenu

### 🎯 Objectifs
- Transformer les connaissances tacites en procédures structurées
- Créer des fichiers d'instructions clairs et exploitables
- Standardiser les processus métier avec l'IA
- Permettre la réplication de tâches complexes
- Optimiser l'efficacité opérationnelle

### 📝 Exemple complet : Procédure de comparaison de CV

#### Contexte de l'exemple
Créer une procédure complète pour analyser et comparer des CV selon un mandat spécifique, en utilisant l'IA comme assistant de recrutement.

#### Step 1 : Création du fichier d'instruction avec ChatGPT

**Prompt de création :**
```
Je veux que tu me créer un fichier d'instruction (procédure) en texte.

Ce fichier te sera fourni afin de suivre la procédure.

Le but de la procédure est de comparer des CV selon un mandat précis

Je veux que les instructions permettent de : 

##CUEILLETTE DE DONNÉES##
1- Demander la description du mandat.
2- Demander la ou les CV à comparer. 
3- Demander s'il y a d'autres instructions supplémentaires à vérifier sur les CV. 
(poser les questions une a une, demander en boucle les CV, jusqu'à ce que l'utilisateur dise qu'il n'a plus de CV a fournir)

##ANALYSE DE CV##
- Analyser les CV selon les expériences et compétences.
- S'assurer de vérifier les requis du poste pour qualifier les CV
- Ne pas discriminer sur l'âge, provenance, le nom, statut personnelle
- Vérifier les instructions supplémentaires si l'utilisateur a fourni des instructions supplémentaires

##SORTIE##
- Fournir un tableau des candidats les mieux adaptés pour ce mandat. Titre : Top 5
- Fournir une explication pour chacun des tops 5 sur l'analyse de leur CV :
  -- Raison, point fort, point faible, conseils à apporter au CV
- Pour les autres CV qui ne sont pas dans le top, fournir une explication pourquoi ils n'ont pas été sélectionnés. Écrire une phrase avec une énumération.
```

#### Résultat généré par l'IA

**Fichier d'instruction : Procédure_Analyse_CV.txt**

```
PROCÉDURE D'ANALYSE ET COMPARAISON DE CV
========================================

OBJECTIF : Analyser et comparer des CV selon un mandat spécifique

ÉTAPE 1 : CUEILLETTE DE DONNÉES
-------------------------------

1.1 Description du mandat
- Demander : "Pouvez-vous me fournir la description complète du poste ?"
- Attendre la réponse complète
- Valider : "Y a-t-il des compétences techniques spécifiques requises ?"

1.2 Collecte des CV
- Demander : "Veuillez me fournir le premier CV à analyser."
- Traiter le CV reçu
- Répéter : "Avez-vous d'autres CV à analyser ?"
- Continuer jusqu'à réponse négative
- Confirmer : "Confirmez-vous que tous les CV ont été fournis ?"

1.3 Instructions supplémentaires
- Demander : "Y a-t-il des critères d'évaluation spécifiques ou des instructions supplémentaires ?"
- Noter toutes les instructions additionnelles
- Valider la compréhension des critères

ÉTAPE 2 : ANALYSE DE CV
-----------------------

2.1 Critères d'analyse
- Expériences professionnelles pertinentes
- Compétences techniques requises
- Compétences transversales
- Formation et certifications
- Adéquation avec les exigences du poste

2.2 Principes d'évaluation
- OBJECTIVITÉ : Évaluer uniquement sur les compétences et expériences
- NON-DISCRIMINATION : Ignorer l'âge, l'origine, le nom, le statut personnel
- ÉQUITÉ : Appliquer les mêmes critères à tous les candidats
- CONFORMITÉ : Respecter les instructions supplémentaires fournies

2.3 Grille d'évaluation
- Adéquation poste : /10
- Expérience pertinente : /10
- Compétences techniques : /10
- Formation : /5
- Potentiel d'évolution : /5
- TOTAL : /40

ÉTAPE 3 : SORTIE ET RECOMMANDATIONS
-----------------------------------

3.1 Tableau Top 5
Créer un tableau avec colonnes :
- Rang
- Candidat (anonymisé si nécessaire)
- Score total
- Points forts
- Points d'amélioration

3.2 Analyse détaillée Top 5
Pour chaque candidat du Top 5 :
- Raisons de la sélection
- Points forts identifiés
- Points faibles ou manques
- Conseils d'amélioration du CV
- Recommandations pour l'entretien

3.3 Candidats non retenus
Pour les autres candidats :
- Phrase explicative concise
- Énumération des raisons principales :
  * Manque d'expérience dans [domaine]
  * Compétences techniques insuffisantes
  * Formation non alignée
  * Autres critères non remplis

VALIDATION FINALE
-----------------
- Vérifier l'objectivité de l'analyse
- Confirmer le respect des critères de non-discrimination
- Valider la cohérence des recommandations
- S'assurer de la complétude de l'analyse
```
- Confirmer le respect des critères de non-discrimination
- Valider la cohérence des recommandations
- S'assurer de la complétude de l'analyse
```

#### Step 2 : Sauvegarde du fichier texte

**Action à effectuer :**
1. Copier le contenu généré par l'IA
2. Créer un fichier `Procédure_Analyse_CV.txt`
3. Sauvegarder le fichier dans le répertoire de travail

#### Step 3 : Utilisation du fichier d'instruction

**Prompt d'utilisation :**
```
Je te fournis un fichier d'instruction à suivre scrupuleusement.

Voici le fichier d'instruction :
[Coller ici le contenu du fichier Procédure_Analyse_CV.txt]

Peux-tu maintenant suivre cette procédure étape par étape ? 
Commence par l'étape 1.1 : demande-moi la description du mandat.
```

### 🔄 Processus complet d'utilisation

#### Étape 1 : Création de la procédure
- L'utilisateur définit le processus à automatiser
- ChatGPT génère le fichier d'instruction structuré
- Le fichier est sauvegardé pour réutilisation

#### Étape 2 : Exécution de la procédure
- Le fichier d'instruction est fourni à l'IA
- L'IA suit scrupuleusement les étapes définies
- Le processus est exécuté de manière standardisée

#### Étape 3 : Amélioration continue
- Les retours d'expérience sont collectés
- La procédure est ajustée et optimisée
- Les nouvelles versions sont documentées

### 🎯 Avantages de cette méthode

#### Standardisation
- **Consistance** : Même approche à chaque utilisation
- **Qualité** : Respect des bonnes pratiques
- **Traçabilité** : Documentation des processus
- **Formation** : Facilite l'onboarding

#### Efficacité
- **Gain de temps** : Automatisation des tâches répétitives
- **Réduction d'erreurs** : Procédures détaillées et validées
- **Réutilisabilité** : Fichiers d'instruction réutilisables
- **Évolutivité** : Amélioration continue des processus

### 🛠️ Templates d'application

#### Pour créer d'autres procédures
```
Je veux créer un fichier d'instruction pour [PROCESSUS À AUTOMATISER].

Le but de la procédure est de [OBJECTIF PRINCIPAL].

Les étapes principales sont :
1. [PHASE DE PRÉPARATION]
2. [PHASE D'EXÉCUTION] 
3. [PHASE DE VALIDATION]

Crée un fichier d'instruction détaillé que je pourrai fournir à l'IA pour qu'elle suive cette procédure.
```

#### Pour utiliser une procédure existante
```
Voici un fichier d'instruction que tu dois suivre scrupuleusement :

[CONTENU DU FICHIER PROCÉDURE]

Commence maintenant par la première étape et guide-moi dans le processus.
```

### 💡 Bonnes pratiques

#### Création de procédures efficaces
- **Clarté** : Instructions sans ambiguïté
- **Séquencement** : Étapes logiques et numérotées
- **Validation** : Points de contrôle réguliers
- **Flexibilité** : Gestion des cas particuliers
- **Documentation** : Objectifs et contexte clairs

#### Utilisation optimale
- **Test initial** : Valider la procédure sur un cas simple
- **Feedback** : Collecter les retours d'amélioration
- **Versioning** : Maintenir les différentes versions
- **Formation** : Former les utilisateurs à la méthode
- **Monitoring** : Suivre l'efficacité des procédures

## Résumé
Niveau de détail : [préciser selon l'audience]
```

**Optimisation du style et clarté**
```
Améliore cette procédure pour la rendre plus claire :

[Texte de la procédure actuelle]

Critères d'amélioration :
- Langage simple et direct
- Étapes numérotées clairement
- Suppression des ambiguïtés
- Ajout d'exemples concrets
- Format visuel (listes, tableaux)
- Temps estimé par étape

Adapte pour [type d'utilisateur spécifique].
```

#### Phase 3 : Enrichissement et validation
**Ajout de cas d'usage et exemples**
```
Enrichis cette procédure avec des exemples concrets :

Procédure de base : [texte existant]

Ajoute :
- 2-3 exemples pratiques par étape critique
- Captures d'écran simulées (descriptions textuelles)
- Cas d'erreurs communes et solutions
- Tips et bonnes pratiques
- Checklist de vérification finale

Format : [selon ton standard]
```

**Création de FAQ associée**
```
Génère une FAQ pour cette procédure :

Procédure : [titre et contenu]

Catégories de questions :
- Questions techniques courantes
- Problèmes de droits/accès
- Gestion des erreurs
- Variations selon les contextes
- Escalade et support

Objectif : Réduire les demandes de support de 80%.
```

### 🛠️ Templates de prompts par type

#### Procédures IT/Techniques
```
Crée une procédure technique pour [installation/configuration/maintenance] :

Environnement :
- Système d'exploitation : [Windows/Linux/macOS]
- Versions logicielles : [spécifications]
- Prérequis techniques : [hardware/software]
- Droits nécessaires : [admin/user/spécifique]

Structure attendue :
1. Prérequis et vérifications
2. Préparation de l'environnement
3. Installation/configuration step-by-step
4. Tests de validation
5. Troubleshooting courant
6. Rollback si nécessaire

Inclus les commandes exactes et captures d'écran descriptives.
```

#### Procédures métier/RH
```
Développe une procédure RH pour [processus métier] :

Contexte organisationnel :
- Départements impliqués : [liste]
- Systèmes utilisés : [SIRH, outils métier]
- Réglementations : [conformité requise]
- Délais standards : [timeframes]

Format procédure :
1. Déclencheurs du processus
2. Acteurs et responsabilités
3. Workflow détaillé
4. Documents et formulaires
5. Contrôles et validations
6. Archivage et suivi
7. Indicateurs de performance

Inclus templates de communication et emails types.
```

#### Procédures de sécurité/qualité
```
Élabore une procédure de sécurité pour [incident/processus] :

Cadre réglementaire :
- Normes applicables : [ISO, SOX, GDPR, etc.]
- Niveaux de criticité : [classification]
- Délais de réponse : [SLA requis]
- Reporting obligatoire : [autorités, management]

Structure sécurisée :
1. Détection/signalement
2. Évaluation initiale
3. Escalade selon criticité
4. Actions correctives
5. Communication interne/externe
6. Post-mortem et amélioration
7. Documentation et compliance

Inclus matrice de décision et contacts d'urgence.
```

### 📋 Outils de validation et amélioration

#### Test d'utilisabilité
```
Simule l'utilisation de cette procédure par [type d'utilisateur] :

Procédure à tester : [contenu]

Critères d'évaluation :
- Temps d'exécution réaliste
- Points de blocage potentiels
- Clarté des instructions
- Complétude des informations
- Gestion des cas d'erreur

Joue le rôle d'un [débutant/expert] et identifie les améliorations.
```

#### Optimisation continue
```
Analyse cette procédure pour l'optimiser :

Procédure actuelle : [texte]
Métriques actuelles : [temps, erreurs, questions support]
Feedback utilisateurs : [retours reçus]

Propose des améliorations pour :
- Réduire le temps d'exécution
- Minimiser les erreurs
- Simplifier les étapes complexes
- Automatiser les tâches répétitives
- Améliorer l'expérience utilisateur

Priorise les améliorations par impact/effort.
```

### 🎨 Formats et présentations

#### Procédure interactive
```
Transforme cette procédure linéaire en format interactif :

Procédure source : [contenu]

Format cible :
- Arbre de décision selon les situations
- Branches conditionnelles (Si... alors...)
- Points de choix utilisateur
- Retours et boucles possibles
- Navigation non-linéaire

Objectif : Adapter le parcours selon le contexte utilisateur.
```

#### Procédure multi-formats
```
Adapte cette procédure en plusieurs formats :

Contenu source : [procédure complète]

Formats à générer :
1. Checklist rapide (1 page)
2. Guide détaillé (format complet)
3. Aide-mémoire (format pocket)
4. Présentation formation (slides)
5. Vidéo script (storyboard textuel)

Adapte le niveau de détail à chaque format.
```

### 📊 Maintenance et évolution

#### Versioning des procédures
```
Crée un système de gestion des versions pour nos procédures :

Besoins :
- Tracking des modifications
- Approbation des changements
- Communication des mises à jour
- Archivage des versions précédentes
- Impact analysis des modifications

Propose :
- Modèle de versioning
- Workflow d'approbation
- Template de changelog
- Processus de communication
- Métriques de suivi
```

#### Audit et amélioration
```
Audite l'efficacité de nos procédures existantes :

Procédures à évaluer : [liste]
Métriques disponibles : [temps, erreurs, satisfaction]
Problématiques identifiées : [feedback terrain]

Analyse :
- Procédures obsolètes ou redondantes
- Manques et gaps identifiés
- Opportunités d'automatisation
- Besoins de mise à jour
- Priorisation des améliorations

Recommandations concrètes avec planning.
```

### 🚀 Automatisation et intégration

#### Génération automatique
```
Crée un système de génération automatique de procédures :

Sources d'information :
- Logs système/applications
- Workflows existants
- Documentation technique
- Retours d'expérience
- Best practices internes

Processus :
1. Extraction automatique des étapes
2. Génération du draft initial
3. Validation par expert métier
4. Enrichissement et finalisation
5. Publication et distribution

Template de sortie standardisé.
```

#### Intégration avec les outils
```
Intègre la création de procédures dans nos outils quotidiens :

Écosystème actuel :
- [Confluence/SharePoint/Wiki interne]
- [Systèmes de tickets/ITSM]
- [Outils de formation/LMS]
- [Plateformes de collaboration]

Objectifs d'intégration :
- Création directe depuis les outils
- Synchronisation automatique
- Notifications de mise à jour
- Tracking d'utilisation
- Feedback intégré

Propose l'architecture technique et les APIs nécessaires.
```

### 💡 Bonnes pratiques

#### Rédaction efficace
- **Langage simple** : Éviter le jargon technique
- **Structure claire** : Numérotation et hiérarchie
- **Actions concrètes** : Verbes d'action précis
- **Validation** : Points de contrôle réguliers
- **Flexibilité** : Gestion des exceptions

#### Maintenance continue
- **Reviews régulières** : Calendrier de mise à jour
- **Feedback utilisateurs** : Canaux de retour
- **Métriques d'usage** : Suivi d'efficacité
- **Évolution contextuelle** : Adaptation aux changements
- **Formation associée** : Support à l'adoption

### 🎯 Cas d'usage concrets

#### Exemple 1 : Procédure de déploiement
**Situation :** Équipe DevOps qui veut standardiser les déploiements

**Prompt de création :**
```
Crée une procédure de déploiement pour notre application web :

Environnements : Dev → Test → Préprod → Prod
Stack technique : [détails]
Outils CI/CD : [pipeline existant]
Contraintes : [downtime, rollback, tests]

Format : Checklist avec validations automatiques et manuelles
```

#### Exemple 2 : Procédure d'onboarding
**Situation :** RH qui veut améliorer l'intégration des nouveaux employés

**Prompt de création :**
```
Optimise notre processus d'onboarding nouveau collaborateur :

Durée cible : 2 semaines
Départements impliqués : RH, IT, Manager, Équipe
Systèmes à configurer : [liste des accès]
Formation requise : [modules obligatoires]

Objectif : Autonomie opérationnelle en 10 jours
```

## Résumé

Cette méthode révolutionne la création de procédures en permettant de transformer n'importe quel processus métier en fichier d'instruction exploitable par l'IA. 

**Bénéfices clés :**
- **Standardisation** : Processus uniformes et reproductibles
- **Efficacité** : Automatisation des tâches répétitives  
- **Qualité** : Respect systématique des bonnes pratiques
- **Formation** : Documentation vivante et actionnable
- **Évolution** : Amélioration continue des processus

**L'exemple de comparaison de CV** démontre comment créer une procédure complète en 3 étapes simples, permettant d'obtenir des analyses objectives et structurées à chaque utilisation.

**Next step :** Identifie un processus répétitif dans ton équipe et crée ta première procédure avec ChatGPT cette semaine en suivant cette méthodologie.