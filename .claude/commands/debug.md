Diagnostic structuré pour le bug : $ARGUMENTS

Processus :

1. **Comprendre** — Analyse la description du bug. Pose des questions si le contexte est insuffisant.
2. **Reproduire** — Identifie les étapes de reproduction. Si possible, écris un test qui reproduit le bug (le test doit échouer).
3. **Localiser** — Utilise des subagents pour investiguer le code pertinent sans polluer le contexte principal. Identifie le fichier et la ligne responsables.
4. **Analyser** — Identifie la root cause (pas juste le symptôme). Explique pourquoi le bug se produit.
5. **Corriger** — Implémente le fix minimal. Pas de refactoring opportuniste.
6. **Vérifier** — Lance le test de reproduction : il doit maintenant passer. Lance la suite de tests complète pour vérifier l'absence de régression.
7. **Documenter** — Commit avec un message `fix: <description>` qui explique la root cause.

IMPORTANT :
- Toujours créer un test de non-régression AVANT de corriger.
- Utiliser des subagents pour l'investigation large (préserve le contexte).
- Ne pas corriger plus que nécessaire — un fix, pas un refactoring.
