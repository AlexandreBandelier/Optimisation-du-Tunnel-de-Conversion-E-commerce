# Documentation des Scénarios de Test - Moteur de Recommandation

Ce document répertorie les scénarios de test critiques utilisés pour valider la logique du moteur de recommandation. L'objectif est de garantir le respect des contraintes métiers (exclusions strictes) et la fiabilité des mécanismes de secours (*fallback*).

## 1. Logique d'Exclusion Stricte

| ID | Scénario | Comportement Attendu | Priorité |
| :--- | :--- | :--- | :--- |
| **TS-01** | **Segment Enfant** | Si l'option "Enfant" est "OUI", le système doit filtrer **exclusivement** les produits tagués enfant. Aucune référence adulte ne doit apparaître, même en cas de score élevé. | Critique |
| **TS-02** | **Étanchéité des Usages** | Un utilisateur sélectionnant l'**Usage A** ne peut recevoir de recommandations pour l'**Usage B**, et inversement. Ce filtre est binaire et prioritaire sur le scoring. | Haute |
| **TS-03** | **Genre et Coupe** | La sélection "Homme" doit exclure les modèles identifiés comme "Coupe Femme". La sélection "Femme" affiche tous les modèles compatibles. | Haute |

## 2. Algorithme de Scoring et Proximité

| ID | Scénario | Comportement Attendu | Statut |
| :--- | :--- | :--- | :--- |
| **TS-04** | **Gestion du "No Match"** | Si aucun produit ne correspond à 100%, l'algorithme calcule un score de proximité et affiche les 3 meilleures alternatives avec une mention des écarts. | Validé |
| **TS-05** | **Neutralité des Données** | Les produits possédant la valeur `INCONNU` sur un critère optionnel ne sont pas pénalisés. Ils restent éligibles au scoring de base pour maximiser le catalogue. | Validé |
| **TS-06** | **Nudges Techniques** | Application de bonus de points (+4 à +8) sur des critères secondaires (Sensation, Réversibilité) pour départager deux produits de rang équivalent. | Validé |

## 3. Cas Particulier : Mode Polyvalent

| ID | Scénario | Logique de Fallback |
| :--- | :--- | :--- |
| **TS-07** | **Recherche Polyvalente** | Le moteur privilégie les équipements hybrides. Si le stock est insuffisant, il propose des équipements Typés (A ou B) en précisant leur spécialisation d'origine pour guider l'utilisateur. |

---
*Dernière mise à jour : Avril 2026*
*Validé par : Système de Test Automatisé & Contrôle Qualité Données*
