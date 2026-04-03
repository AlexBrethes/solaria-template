# Solaria Template — Plan d'implémentation

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Créer un repo template GitHub réutilisable avec un environnement Claude Code complet (CLAUDE.md, settings, commands, skills, agents) et des templates GitHub.

**Architecture:** Repo statique sans dépendances. Tous les fichiers sont du Markdown ou du JSON. Les slash commands sont des prompts Markdown dans `.claude/commands/`. Le skill et le subagent sont des fichiers Markdown dans `.claude/skills/` et `.claude/agents/`.

**Tech Stack:** Git, Markdown, JSON — aucune dépendance externe.

---

## File Structure

```
solaria-template/
├── CLAUDE.md                                    # Conventions projet (concis)
├── README.md                                    # Guide d'utilisation du template
├── LICENSE                                      # MIT Solaria Advisory
├── .gitignore                                   # Multi-stack
├── .claude/
│   ├── settings.json                            # Permissions + hooks sécurité
│   ├── commands/
│   │   ├── init-project.md                      # Slash command init
│   │   ├── plan.md                              # Slash command plan
│   │   ├── review.md                            # Slash command review
│   │   ├── deploy.md                            # Slash command deploy
│   │   └── debug.md                             # Slash command debug
│   ├── agents/
│   │   └── code-reviewer.md                     # Subagent review
│   └── skills/
│       └── solaria-conventions/
│           └── SKILL.md                         # Charte Solaria
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md                        # Template issue bug
│   │   └── feature_request.md                   # Template issue feature
│   └── PULL_REQUEST_TEMPLATE.md                 # Template PR
└── docs/                                        # Prêt pour specs/plans projet
```

---

### Task 1: Initialiser le repo Git et créer les fichiers racine

**Files:**
- Create: `.gitignore`
- Create: `LICENSE`
- Create: `README.md`

- [ ] **Step 1: Initialiser git**

```bash
cd C:/Users/alexa/Desktop/SolariaApps/solaria-template
git init
git branch -m main
```

Expected: `Initialized empty Git repository`

- [ ] **Step 2: Créer .gitignore**

Create `.gitignore`:

```gitignore
# === OS ===
.DS_Store
Thumbs.db
Desktop.ini

# === Éditeurs ===
.vscode/
!.vscode/settings.json
!.vscode/extensions.json
.idea/
*.swp
*.swo
*~

# === Node.js ===
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
.npm
.yarn/cache
.pnp.*

# === Python ===
__pycache__/
*.py[cod]
*$py.class
*.egg-info/
dist/
build/
.venv/
venv/
.pytest_cache/
.ruff_cache/
.mypy_cache/

# === Java / Kotlin ===
*.class
*.jar
target/

# === Go ===
bin/

# === Rust ===
target/
Cargo.lock

# === Build / Output ===
dist/
build/
out/
.next/
.nuxt/

# === Environnement ===
.env
.env.*
!.env.example

# === Logs ===
*.log
logs/

# === Coverage ===
coverage/
htmlcov/
.coverage
```

- [ ] **Step 3: Créer LICENSE**

Create `LICENSE`:

```
MIT License

Copyright (c) 2026 Solaria Advisory

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

- [ ] **Step 4: Créer README.md**

Create `README.md`:

```markdown
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
```

- [ ] **Step 5: Commit initial**

```bash
git add .gitignore LICENSE README.md
git commit -m "init: initialisation du repo template Solaria"
```

---

### Task 2: Créer CLAUDE.md

**Files:**
- Create: `CLAUDE.md`

- [ ] **Step 1: Créer CLAUDE.md**

Create `CLAUDE.md`:

```markdown
# {{NOM_PROJET}}

> {{DESCRIPTION}}

## Stack

{{À compléter via /project:init-project}}

## Conventions

- Langue : français (code, commits, docs, commentaires)
- Commits : conventional commits FR (feat:, fix:, docs:, refactor:, test:)
- Tests obligatoires pour toute feature ou fix — ne jamais skipper
- IMPORTANT : toujours planifier avant de coder (plan.md via /project:plan)
- Commits atomiques : une feature = un commit
- Utiliser /compact quand le contexte dépasse 50%

## Commandes

- Build : `{{À compléter}}`
- Test : `{{À compléter}}`
- Test unitaire : `{{À compléter}}`
- Lint : `{{À compléter}}`
- Dev : `{{À compléter}}`

## Architecture

{{À documenter via /project:init-project}}

## Vérification

Toujours fournir des critères de vérification pour chaque changement :
- Tests automatisés couvrant le cas nominal et les edge cases
- Commande de vérification exécutable (lint, build, test)
- Pour les changements UI : capture d'écran avant/après
```

- [ ] **Step 2: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: ajout du CLAUDE.md template avec placeholders"
```

---

### Task 3: Créer .claude/settings.json

**Files:**
- Create: `.claude/settings.json`

- [ ] **Step 1: Créer le fichier settings.json**

Create `.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "Read(*)",
      "Edit(*)",
      "Write(*)",
      "Grep(*)",
      "Glob(*)",
      "WebSearch(*)",
      "WebFetch(*)",
      "Bash(*)",
      "Skill(*)"
    ],
    "deny": [
      "Bash(rmdir *)",
      "Bash(sudo *)",
      "Bash(su *)",
      "Bash(su -*)",
      "Bash(git push --force *)",
      "Bash(git push -f *)",
      "Bash(git push origin --delete *)",
      "Bash(git reset --hard *)",
      "Bash(git clean *)",
      "Bash(git checkout . *)",
      "Bash(git checkout -- . *)",
      "Bash(git restore . *)",
      "Bash(git branch -D *)",
      "Bash(dd if=*)",
      "Bash(mkfs*)",
      "Bash(shutdown *)",
      "Bash(reboot *)",
      "Bash(halt *)",
      "Bash(poweroff *)",
      "Bash(chmod 777 *)",
      "Bash(chown *)",
      "Bash(shred *)",
      "Bash(truncate *)",
      "Bash(kill -9 *)",
      "Bash(killall *)",
      "Read(*.env)",
      "Read(.env*)",
      "Read(*/.env)",
      "Read(*/.env.*)",
      "Read(**/.env)",
      "Read(**/.env.*)",
      "Read(~/.ssh/**)",
      "Read(~/.aws/**)",
      "Read(**/*.pem)",
      "Read(**/*.key)",
      "Read(**/*id_rsa*)",
      "Edit(*.env)",
      "Edit(.env*)",
      "Edit(*/.env)",
      "Edit(**/.env)",
      "Edit(**/.env.*)",
      "Write(*.env)",
      "Write(.env*)",
      "Write(*/.env)",
      "Write(**/.env)",
      "Write(**/.env.*)"
    ]
  },
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "bash -c 'CMD=$(echo \"$TOOL_INPUT\" | jq -r \".command // empty\" 2>/dev/null); if [ -z \"$CMD\" ]; then exit 0; fi; if echo \"$CMD\" | grep -qE \"(\\bsudo\\s+|\\bsu\\s+|\\bdd\\s+if=|\\bmkfs|\\bshred|\\btruncate|\\bchmod\\s+777|\\bchown\\s+)\"; then echo \"BLOQUE: Commande destructive: $CMD\" >&2; exit 2; fi; if echo \"$CMD\" | grep -qE \"(curl|wget).*\\|\\s*(sh|bash|zsh)\"; then echo \"BLOQUE: Pipe-to-shell detecte: $CMD\" >&2; exit 2; fi; if echo \"$CMD\" | grep -qE \"git\\s+push\\s+(--force|-f)|git\\s+reset\\s+--hard|git\\s+clean|git\\s+checkout\\s+\\.|git\\s+restore\\s+\\.\"; then echo \"BLOQUE: Operation git destructive: $CMD\" >&2; exit 2; fi; exit 0'"
          }
        ]
      },
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "bash -c 'CMD=$(echo \"$TOOL_INPUT\" | jq -r \".command // empty\" 2>/dev/null); if [ -z \"$CMD\" ]; then exit 0; fi; if echo \"$CMD\" | grep -qE \"^git\\s+push\"; then echo \"ATTENTION: Push vers le remote: $CMD\"; fi; if echo \"$CMD\" | grep -qE \"^git\\s+(merge|rebase)\"; then echo \"ATTENTION: Operation de branche: $CMD\"; fi; if echo \"$CMD\" | grep -qE \"\\brm\\b\"; then echo \"ATTENTION: Suppression detectee: $CMD\"; fi; exit 0'"
          }
        ]
      }
    ]
  }
}
```

- [ ] **Step 2: Commit**

```bash
git add .claude/settings.json
git commit -m "feat: ajout settings.json avec permissions et hooks de securite"
```

---

### Task 4: Créer les 5 slash commands

**Files:**
- Create: `.claude/commands/init-project.md`
- Create: `.claude/commands/plan.md`
- Create: `.claude/commands/review.md`
- Create: `.claude/commands/deploy.md`
- Create: `.claude/commands/debug.md`

- [ ] **Step 1: Créer init-project.md**

Create `.claude/commands/init-project.md`:

```markdown
Initialise ce projet à partir du template Solaria.

Pose les questions suivantes une par une avec l'outil AskUserQuestion :

1. Nom du projet
2. Description en une phrase
3. Stack technique (langage, framework, base de données)
4. Commandes : build, test, test unitaire, lint, dev

Ensuite :

1. Remplace tous les placeholders `{{...}}` dans CLAUDE.md avec les réponses
2. Documente l'architecture de base dans la section Architecture de CLAUDE.md
3. Crée les dossiers pertinents pour la stack (ex: src/, tests/, etc.)
4. Si git n'est pas initialisé, lance `git init && git branch -m main`
5. Crée un commit : `init: initialisation du projet <nom>`

IMPORTANT : ne pas inventer de contenu. Utiliser uniquement les réponses de l'utilisateur.
```

- [ ] **Step 2: Créer plan.md**

Create `.claude/commands/plan.md`:

```markdown
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
```

- [ ] **Step 3: Créer review.md**

Create `.claude/commands/review.md`:

```markdown
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
```

- [ ] **Step 4: Créer deploy.md**

Create `.claude/commands/deploy.md`:

```markdown
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
| Tests | ✅/❌ | ... |
| Build | ✅/❌ | ... |
| ... | ... | ... |

## Verdict
PRÊT / NON PRÊT — <raison si non prêt>
```

Si un item critique échoue (Tests, Build, Lint), le verdict est NON PRÊT.
```

- [ ] **Step 5: Créer debug.md**

Create `.claude/commands/debug.md`:

```markdown
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
```

- [ ] **Step 6: Commit**

```bash
git add .claude/commands/
git commit -m "feat: ajout des 5 slash commands (init, plan, review, deploy, debug)"
```

---

### Task 5: Créer le subagent code-reviewer

**Files:**
- Create: `.claude/agents/code-reviewer.md`

- [ ] **Step 1: Créer code-reviewer.md**

Create `.claude/agents/code-reviewer.md`:

```markdown
---
name: code-reviewer
description: Revue de code spécialisée sécurité, conventions et edge cases
tools: Read, Grep, Glob, Bash
---

Tu es un ingénieur sécurité senior. Analyse le code pour détecter :

## Sécurité
- Injections (SQL, XSS, commandes shell)
- Failles d'authentification et d'autorisation
- Secrets ou credentials en dur dans le code
- Gestion non sécurisée des données utilisateur

## Conventions Solaria
- Langue française dans les commentaires et docs
- Conventional commits respectés
- Tests présents pour chaque changement
- Code DRY et YAGNI

## Qualité
- Edge cases non gérés
- Gestion d'erreurs manquante aux frontières système (input utilisateur, API externes)
- Race conditions ou problèmes de concurrence
- Ressources non libérées (fichiers, connexions)

## Format du rapport

Pour chaque problème trouvé, indique :
- **Fichier et ligne** : `chemin/fichier.ext:42`
- **Sévérité** : BLOQUANT / WARNING / INFO
- **Description** : explication claire du problème
- **Suggestion** : code corrigé ou approche recommandée

Termine par un verdict : APPROUVÉ ou CHANGEMENTS REQUIS.
```

- [ ] **Step 2: Commit**

```bash
git add .claude/agents/code-reviewer.md
git commit -m "feat: ajout du subagent code-reviewer"
```

---

### Task 6: Créer le skill solaria-conventions

**Files:**
- Create: `.claude/skills/solaria-conventions/SKILL.md`

- [ ] **Step 1: Créer SKILL.md**

Create `.claude/skills/solaria-conventions/SKILL.md`:

```markdown
---
name: solaria-conventions
description: Charte visuelle et éditoriale Solaria Advisory — couleurs, typographie, ton
---

# Conventions Solaria Advisory

## Charte visuelle

| Élément | Valeur |
|---------|--------|
| Couleur primaire | Coral `#F4815A` |
| Couleur de fond | Parchment `#FDF6EC` |
| Police principale | Outfit (Google Fonts) |
| Import | `@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700&display=swap');` |

## Ton éditorial

- **Crédible et sobre** — jamais startup-hype, pas de superlatifs gratuits
- **Professionnel** — registre soutenu sans être pompeux
- **Pas de langue de bois** — dire les choses directement
- **Jamais de statistiques inventées** — toute donnée chiffrée doit avoir une source
- **Pas d'emojis** sauf demande explicite de l'utilisateur

## Application

- Utiliser ces conventions pour tout contenu visible par des utilisateurs finaux (UI, emails, docs publiques)
- Les documents internes (specs, plans) suivent le ton mais pas nécessairement la charte visuelle
- En cas de doute sur le ton, relire et supprimer tout ce qui sonne "marketing générique"
```

- [ ] **Step 2: Commit**

```bash
git add .claude/skills/solaria-conventions/
git commit -m "feat: ajout du skill solaria-conventions (charte visuelle et editoriale)"
```

---

### Task 7: Créer les templates GitHub

**Files:**
- Create: `.github/ISSUE_TEMPLATE/bug_report.md`
- Create: `.github/ISSUE_TEMPLATE/feature_request.md`
- Create: `.github/PULL_REQUEST_TEMPLATE.md`

- [ ] **Step 1: Créer bug_report.md**

Create `.github/ISSUE_TEMPLATE/bug_report.md`:

```markdown
---
name: Rapport de bug
about: Signaler un comportement inattendu
title: "[BUG] "
labels: bug
assignees: ""
---

## Description

Description claire et concise du bug.

## Étapes de reproduction

1. Aller sur '...'
2. Cliquer sur '...'
3. Observer '...'

## Comportement attendu

Ce qui devrait se passer.

## Comportement observé

Ce qui se passe réellement.

## Environnement

- OS : [ex: Windows 11, macOS 14]
- Navigateur : [ex: Chrome 120]
- Version : [ex: 1.0.0]

## Captures d'écran

Si applicable, ajouter des captures d'écran.

## Contexte additionnel

Toute information complémentaire utile.
```

- [ ] **Step 2: Créer feature_request.md**

Create `.github/ISSUE_TEMPLATE/feature_request.md`:

```markdown
---
name: Demande de fonctionnalité
about: Proposer une nouvelle fonctionnalité ou amélioration
title: "[FEATURE] "
labels: enhancement
assignees: ""
---

## Problème

Description du problème ou besoin à adresser.

## Solution proposée

Description de la solution envisagée.

## Alternatives considérées

Autres approches envisagées et pourquoi elles n'ont pas été retenues.

## Contexte additionnel

Maquettes, exemples, références utiles.
```

- [ ] **Step 3: Créer PULL_REQUEST_TEMPLATE.md**

Create `.github/PULL_REQUEST_TEMPLATE.md`:

```markdown
## Description

Résumé des changements et motivation.

Fixes #(numéro d'issue)

## Type de changement

- [ ] Bug fix
- [ ] Nouvelle fonctionnalité
- [ ] Refactoring (pas de changement fonctionnel)
- [ ] Documentation
- [ ] Breaking change

## Checklist

- [ ] Mon code suit les conventions du projet (CLAUDE.md)
- [ ] J'ai écrit des tests couvrant mes changements
- [ ] Les tests existants passent toujours
- [ ] Le lint passe sans erreur
- [ ] J'ai mis à jour la documentation si nécessaire
- [ ] J'ai vérifié l'absence de secrets dans le code
```

- [ ] **Step 4: Commit**

```bash
git add .github/
git commit -m "feat: ajout des templates GitHub (issues bug/feature, PR)"
```

---

### Task 8: Vérification finale

- [ ] **Step 1: Vérifier l'arborescence complète**

```bash
find . -not -path './.git/*' -not -path './.git' | sort
```

Expected output doit contenir tous les fichiers listés dans la spec.

- [ ] **Step 2: Vérifier le contenu de CLAUDE.md**

```bash
cat CLAUDE.md
```

Vérifier que les placeholders `{{...}}` sont présents et que les conventions sont pré-remplies.

- [ ] **Step 3: Vérifier que settings.json est du JSON valide**

```bash
cat .claude/settings.json | python -m json.tool > /dev/null && echo "JSON valide" || echo "JSON invalide"
```

Expected: `JSON valide`

- [ ] **Step 4: Vérifier l'historique git**

```bash
git log --oneline
```

Expected: 7 commits atomiques, un par task, en conventional commits FR.

- [ ] **Step 5: Commit de vérification (si ajustements nécessaires)**

Si des ajustements ont été faits pendant la vérification :

```bash
git add -A
git commit -m "fix: corrections post-verification du template"
```
