# QA + Copilot : créer des données de test réalistes

**ID:** QA-05  
**Plateforme:** GitHub Enterprise + Copilot  

## Type d'audience
QA / Testeurs

## AI utilisé
GitHub Enterprise / ChatGPT

## Niveau Connaissance AI
Intermédiaire

## Résumé Technique
Génération de jeux de données pertinents et cohérents pour les tests automatisés.

## Contenu

### Créer des données de test à partir d’un modèle « Client » (et les exporter)###

> **Résumé** : Un exemple minimal de modèle **Client** (quelques champs + validations), un **prompt prêt-à-copier** pour générer automatiquement des jeux de données (valides et invalides, avec explication), puis des **exemples d’export** en CSV, XLSX, JSON et Markdown.

**Auteur** : Vous
**Date** : 2025-10-14
**Public cible** : QA, PO, équipes produit
**Objectif** : Documenter un modèle succinct et accélérer la génération de données de test réalistes.

---

#### 1) Exemple de modèle « Client » (extrait de documentation)

##### 1.1 Propriétés (exemples)

| Nom          | Type                               | Obligatoire | Exemple             | Description                                       |
| ------------ | ---------------------------------- | ----------: | ------------------- | ------------------------------------------------- |
| id           | string (UUID)                      |           ✅ | `c_7f2b9a`          | Identifiant unique (généré par le système).       |
| prenom       | string                             |           ✅ | `Marie`             | Prénom légal.                                     |
| nom          | string                             |           ✅ | `Tremblay`          | Nom de famille.                                   |
| email        | string (email)                     |           ✅ | `marie@exemple.com` | Courriel principal **unique**.                    |
| statut       | enum(`prospect`,`actif`,`inactif`) |           ✅ | `actif`             | État du client.                                   |
| solde        | number(decimal)                    |             | `-25.50`            | Solde du compte (positif = dû; négatif = crédit). |
| limiteCredit | number(decimal)                    |             | `1000.00`           | Plafond d’achat autorisé.                         |
| langue       | enum(`fr`,`en`)                    |           ✅ | `fr`                | Langue préférée.                                  |

> **Remarque** : Ce n’est qu’un extrait; adaptez selon votre système.

 1.2 Validations (à vérifier)

* **email** : format valide + **unicité** (pas de doublons).
* **statut** : doit appartenir à {`prospect`,`actif`,`inactif`} ; transitions contrôlées par le métier.
* **langue** : doit appartenir à {`fr`,`en`}.
* **limiteCredit** : ≥ 0 ; décimal (2–4 décimales).
* **solde** : dérivé/calculé par le système (non modifiable directement via l’UI publique).
* **prenom / nom** : longueur 1–100, caractères autorisés (lettres, tirets, apostrophes).

---

#### 2) Prompt prêt-à-copier pour générer un jeu de données

> **Objectif** : Demander à une IA de produire une **liste de clients** avec des cas **valides** et **invalides**, en expliquant **pourquoi** chaque ligne est valide ou invalide.

#### Prompt (copiez-collez)

```
Tu es un générateur de données de test. Utilise le modèle « Client » ci-dessous et crée un jeu de données réaliste.

Modèle « Client » (extrait) :
- id: string(UUID) — généré par le système (peut être vide dans l’entrée si non pertinent)
- prenom: string (1–100)
- nom: string (1–100)
- email: string (format email), UNIQUE
- statut: enum {prospect, actif, inactif}
- solde: number(decimal)
- limiteCredit: number(decimal ≥ 0)
- langue: enum {fr, en}

Validations clés : email format + unicité ; statut dans l’énum ; langue dans l’énum ; limiteCredit ≥ 0 ; prenom/nom longueur 1–100.

TÂCHE :
1) Génère 20 lignes de données « Client » variées (prénoms, noms, emails, langues, statuts, limites de crédit et soldes variés). 
2) Pour chaque ligne, indique si la ligne est **valide** ou **invalide**, et si invalide, **donne une raison claire** (ex. « email en double », « langue non supportée », « limiteCredit négative », « email mal formé », etc.).
3) Assure-toi d’inclure plusieurs erreurs différentes, dont au moins :
   - email invalide (mauvais format)
   - email en doublon
   - langue non supportée
   - statut hors énum
   - limiteCredit négative
   - nom trop court (vide) ou trop long
4) Génère des emails cohérents avec prénoms/noms, mais introduis des variations contrôlées pour créer des doublons/erreurs.
5) **Format de sortie** : JSON (une liste d’objets). Schéma de sortie exact :
   [
     {
       "prenom": "...",
       "nom": "...",
       "email": "...",
       "statut": "prospect|actif|inactif|autre",
       "solde": 0,
       "limiteCredit": 0,
       "langue": "fr|en|autre",
       "valide": true|false,
       "raison": "...explication si invalide, sinon chaîne vide..."
     },
     ... (20 objets)
   ]
6) Ne fournis aucun autre texte hors du JSON pour que l’export soit direct.
```

> **Astuce QA** : si vous préférez un format table (CSV/Markdown), demandez explicitement « **Format de sortie : CSV** » ou « **Format de sortie : Markdown** ».

---

#### 3) Exemples d’export (CSV, XLSX, JSON, Markdown)

##### 3.1 Export CSV (exemple)

```csv
prenom,nom,email,statut,solde,limiteCredit,langue,valide,raison
Marie,Tremblay,marie@exemple.com,actif,0,1000,fr,true,
Alex,Dubois,alex@@exemple..com,prospect,0,500,fr,false,Adresse courriel invalide
Nina,Lopez,nina@exemple.com,actif,200,400,en,true,
Sam,Chen,nina@exemple.com,actif,0,800,en,false,Adresse courriel déjà utilisée
```

**Comment l’obtenir ?**

* Si l’IA a produit du **JSON**, utilisez un convertisseur (outil interne, script, ou tableur) pour mapper les champs puis « **Enregistrer sous… CSV** ».

##### 3.2 Export XLSX (exemple)

* Ouvrez le CSV dans Excel/Sheets → **Fichier > Enregistrer sous… > .xlsx**.
* Ou demandez directement à l’IA : « **Donne le résultat en tableau Markdown** » → copiez-collez dans Sheets → **Fichier > Télécharger > Microsoft Excel (.xlsx)**.

##### 3.3 Export JSON (exemple)

```json
[
  {
    "prenom": "Marie",
    "nom": "Tremblay",
    "email": "marie@exemple.com",
    "statut": "actif",
    "solde": 0,
    "limiteCredit": 1000,
    "langue": "fr",
    "valide": true,
    "raison": ""
  },
  {
    "prenom": "Alex",
    "nom": "Dubois",
    "email": "alex@@exemple..com",
    "statut": "prospect",
    "solde": 0,
    "limiteCredit": 500,
    "langue": "fr",
    "valide": false,
    "raison": "Adresse courriel invalide"
  }
]
```

##### 3.4 Export Markdown (.md) — tableau prêt pour un wiki

```md
| prenom | nom | email | statut | solde | limiteCredit | langue | valide | raison |
|---|---|---|---|---:|---:|---|:---:|---|
| Marie | Tremblay | marie@exemple.com | actif | 0 | 1000 | fr | ✅ | |
| Alex | Dubois | alex@@exemple..com | prospect | 0 | 500 | fr | ❌ | Adresse courriel invalide |
```

---

## Annexes (optionnel)

* **Variantes de prompt** :

  * *Sortie CSV* : « Ajoute une première ligne d’en-tête et retourne uniquement le CSV. »
  * *Données massives* : « Génère 500 lignes en t’assurant d’environ 20% d’entrées invalides. »
  * *Contrainte de langue* : « 70% `fr`, 30% `en`. »
* **Contrôles QA rapides** : vérifier absence de doublons email dans les lignes marquées `valide=true`; vérifier que chaque `raison` correspond bien à une validation.

## Résumé

Ce guide présente une méthode structurée pour générer des données de test réalistes à l'aide de l'IA, en prenant l'exemple d'un modèle "Client". Il couvre :

1. **Modélisation des données** : Définition claire des propriétés, types, contraintes et validations d'un modèle métier
2. **Prompt optimisé** : Template prêt-à-copier pour demander à l'IA de générer des jeux de données variés avec cas valides et invalides
3. **Exports multiformats** : Exemples de conversion en CSV, XLSX, JSON et Markdown pour s'adapter aux différents outils de test
4. **Contrôle qualité** : Génération de données avec explications des erreurs pour faciliter les tests de validation

Cette approche permet aux équipes QA de créer rapidement des datasets cohérents et pertinents, incluant des cas d'erreur spécifiques pour tester les validations métier, tout en documentant clairement les raisons des échecs attendus.