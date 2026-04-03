Exécute la checklist pré-déploiement pour ce projet.

Pour chaque item, exécute la vérification et rapporte le résultat :

## Checklist

1. **Tests** — Lance la commande de test du CLAUDE.md. Vérifie que tous passent.
2. **Build** — Lance la commande de build. Vérifie qu'il réussit sans erreur.
3. **Lint** — Lance la commande de lint. Vérifie zéro erreur.
4. **TODO/FIXME** — Recherche les TODO et FIXME critiques dans le code source. Signale ceux qui bloquent le déploiement.
5. **Variables d'environnement** — Vérifie que toutes les variables utilisées dans le code sont documentées (dans .env.example ou README).
6. **Migrations** — Si le projet utilise des migrations DB, vérifie qu'elles sont à jour.
7. **CHANGELOG** — Vérifie que le CHANGELOG est à jour avec les derniers changements.
8. **Version** — Vérifie que la version a été bumped si applicable.

## Rapport

```
# Checklist pré-déploiement

| Item | Statut | Détail |
|------|--------|--------|
| Tests | OK/KO | ... |
| Build | OK/KO | ... |
| ... | ... | ... |

## Verdict
PRÊT / NON PRÊT — <raison si non prêt>
```

Si un item critique échoue (Tests, Build, Lint), le verdict est NON PRÊT.
