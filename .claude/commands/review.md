Lance une revue de code complète sur les changements en cours.

Processus :

1. **Inventaire** — `git diff` (staged + unstaged) pour lister tous les changements.
2. **Vérification plan** — Si un `plan.md` existe, vérifie la cohérence entre le plan et l'implémentation.
3. **Analyse** — Pour chaque fichier modifié, vérifie :
   - Qualité du code (lisibilité, DRY, YAGNI)
   - Respect des conventions du CLAUDE.md
   - Couverture de tests (chaque changement a-t-il un test ?)
   - Sécurité (injection SQL/XSS/commandes, auth, gestion des secrets)
   - Gestion des erreurs et edge cases
4. **Rapport** — Produit un rapport structuré :

```
# Revue de code

## Résumé
<vue d'ensemble des changements>

## Bloquants
- [fichier:ligne] Description du problème

## Warnings
- [fichier:ligne] Description du problème

## Suggestions
- [fichier:ligne] Amélioration proposée

## Verdict
APPROUVÉ / CHANGEMENTS REQUIS
```

Si des bloquants sont trouvés, propose des corrections concrètes.
