# Recruter avec l'AI sans biais

**ID:** HR-02  
**Plateforme:** Azure AI Search + HR Tools  

## Type d'audience
RH / Recrutement Tech

## AI utilisé
ChatGPT/MS Copilot

## Niveau Connaissance AI
Intermédiaire

## Résumé Technique
Comment utiliser l'AI pour accélérer le tri de CV tout en préservant l'équité et la diversité.

## Contenu

### Étapes de mise en œuvre

1. **Préparation des documents**
   - Téléverser les CV dans un environnement de chat sécurisé
   - Copier la description complète du poste et des critères de sélection

2. **Prompt structuré pour l'AI**
   ```
   Voici [X] CV de candidats et la description du poste ci-joint.
   
   Mission : Analyser objectivement ces candidatures en te basant uniquement sur :
   - Les compétences techniques requises
   - L'expérience professionnelle pertinente
   - Les réalisations quantifiables
   
   Ignore complètement : nom, âge, genre, origine, photo, adresse, situation familiale.
   ```

3. **Demandes spécifiques à l'AI**
   - **Classement objectif** : Liste ordonnée des candidats avec score de correspondance (1-10)
   - **Justification transparente** : Explication détaillée des critères de classement
   - **Points de vigilance** : Pour chaque candidat retenu :
     - Questions spécifiques à poser en entrevue
     - Compétences à approfondir
     - Zones d'amélioration potentielles

### Bonnes pratiques anti-biais

- **Anonymisation** : Masquer les informations personnelles avant analyse
- **Critères objectifs** : Se concentrer sur les compétences mesurables
- **Validation croisée** : Faire analyser par plusieurs AI ou équipes
- **Documentation** : Tracer les décisions pour audit de diversité


## Résumé

Cette approche permet aux équipes RH de traiter efficacement de gros volumes de candidatures tout en maintenant l'équité dans le processus de sélection. L'AI agit comme un premier filtre objectif, se concentrant uniquement sur les compétences et l'expérience pertinentes.

**Avantages clés :**
- **Gain de temps** : Traitement rapide de centaines de CV
- **Réduction des biais** : Analyse basée sur les compétences uniquement
- **Consistance** : Critères d'évaluation uniformes pour tous les candidats
- **Traçabilité** : Documentation claire des décisions de sélection

**Points d'attention :**
- Nécessite une description de poste précise et des critères objectifs
- L'AI complète mais ne remplace pas le jugement humain final
- Importance de valider régulièrement l'absence de biais dans les résultats