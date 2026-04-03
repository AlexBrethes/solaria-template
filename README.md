# Solaria Template

Template de projet réutilisable pour tous les projets Solaria Advisory. Inclut un environnement Claude Code pré-configuré avec conventions, commandes, et garde-fous.

## Utilisation

1. Cliquer **"Use this template"** sur GitHub (ou copier le repo)
2. Cloner le nouveau repo
3. Lancer Claude Code et exécuter `/project:init-project`
4. Suivre les instructions interactives pour personnaliser le projet

## Structure

```
├── CLAUDE.md                    # Conventions projet (à personnaliser)
├── .editorconfig                # Formatage universel (indentation, line endings)
├── .claude/
│   ├── settings.json            # Permissions et hooks de sécurité
│   ├── commands/                # Slash commands Claude Code
│   ├── agents/                  # Subagents spécialisés
│   └── skills/                  # Skills à la demande
├── .github/                     # Templates issues et PR
└── docs/                        # Specs et plans
```

## Slash Commands

| Commande | Usage |
|---|---|
| `/project:init-project` | Personnaliser le template pour un nouveau projet |
| `/project:plan` | Générer un plan d'implémentation structuré |
| `/project:review` | Lancer une revue de code complète |
| `/project:deploy` | Checklist pré-déploiement |
| `/project:debug` | Diagnostic structuré d'un bug |

## Conventions

- Langue : français (code, commits, docs)
- Commits : conventional commits FR (`feat:`, `fix:`, `docs:`)
- Tests obligatoires pour toute feature ou fix
- Planification avant implémentation

## Licence

MIT — Solaria Advisory
