Génère un plan d'implémentation structuré pour : $ARGUMENTS

Processus :

1. **Explorer** — Lis les fichiers pertinents du projet pour comprendre le contexte. Utilise des subagents si l'exploration est large.
2. **Analyser** — Identifie les fichiers à modifier, les dépendances, et les risques.
3. **Rédiger** — Crée `plan.md` à la racine avec cette structure :

```
# Plan : <titre>

## Contexte
Pourquoi ce changement est nécessaire.

## Approche
Description de la solution retenue et pourquoi.

## Fichiers impactés
- `chemin/fichier.ext` — description du changement

## Plan de tests
- Tests unitaires à écrire
- Tests d'intégration si applicable
- Commandes de vérification

## Critères de succès
- [ ] Critère 1
- [ ] Critère 2

## Risques
- Risque identifié → mitigation
```

4. **Valider** — Présente le plan à l'utilisateur pour approbation avant toute implémentation.

IMPORTANT : pas d'implémentation dans cette commande. Uniquement le plan.
