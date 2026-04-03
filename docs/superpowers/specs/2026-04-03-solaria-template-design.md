# Solaria Template — Spec de design

## Contexte

Alexandre (CEO Solaria Advisory) a besoin d'un repo template GitHub réutilisable pour tous ses futurs projets. Le template doit fournir un environnement Claude Code complet (CLAUDE.md, settings, commands, skills, agents) et des templates GitHub, le tout agnostique en termes de stack. Chaque nouveau projet copie ce template puis le personnalise via `/project:init-project`.

## Arborescence cible

```
solaria-template/
├── CLAUDE.md
├── README.md
├── LICENSE                              # MIT
├── .gitignore                           # Multi-stack
├── .claude/
│   ├── settings.json                    # Permissions + hooks essentiels
│   ├── commands/
│   │   ├── init-project.md              # Personnalisation du template
│   │   ├── plan.md                      # Génère un plan.md structuré
│   │   ├── review.md                    # Revue de code complète
│   │   ├── deploy.md                    # Checklist pré-déploiement
│   │   └── debug.md                     # Diagnostic structuré de bugs
│   ├── agents/
│   │   └── code-reviewer.md             # Subagent review sécurité/conventions
│   └── skills/
│       └── solaria-conventions/
│           └── SKILL.md                 # Charte, ton, style Solaria
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
└── docs/                                # Vide, prêt pour les specs projet
```

## 1. CLAUDE.md

Fichier concis, suit les best practices (uniquement ce que Claude ne peut pas deviner). Sections :

- **Objectif** : placeholder `{{NOM_PROJET}}` + `{{DESCRIPTION}}`
- **Stack** : placeholder `{{À compléter via /project:init-project}}`
- **Conventions** (pré-rempli, commun à tous les projets Solaria) :
  - Langue : français (code, commits, docs)
  - Commits : conventional commits FR (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`)
  - Tests obligatoires pour toute feature/fix
  - Planification obligatoire avant implémentation (`plan.md`)
  - Commits atomiques : une feature = un commit
  - `/compact` quand le contexte dépasse 50%
- **Commandes** : placeholders build, test, lint, dev
- **Architecture** : placeholder à documenter lors de l'init
- **Vérification** : section rappelant de toujours fournir critères de vérification (tests, screenshots, commandes)

Ne PAS inclure : conventions de code standard, descriptions fichier par fichier, tutoriels.

## 2. Slash Commands

### `/project:init-project`
- Demande interactivement : nom du projet, description, stack technique, commandes build/test/lint
- Remplace les placeholders `{{...}}` dans CLAUDE.md
- Crée la structure de dossiers adaptée à la stack
- Initialise git si pas déjà fait
- Crée un premier commit

### `/project:plan`
- Accepte `$ARGUMENTS` comme description de la feature
- Génère `plan.md` à la racine avec : contexte, approche retenue, fichiers impactés, plan de tests, critères de succès, risques
- S'inspire du workflow "Explore → Plan → Implement → Commit" des best practices

### `/project:review`
- Analyse les changements (staged + unstaged)
- Vérifie : qualité du code, respect des conventions CLAUDE.md, couverture de tests, sécurité (OWASP top 10), cohérence avec le plan.md si existant
- Produit un rapport structuré avec sévérité (bloquant/warning/info)

### `/project:deploy`
- Checklist pré-déploiement interactive :
  - [ ] Tests passent
  - [ ] Build réussit
  - [ ] Pas de TODO/FIXME critiques
  - [ ] Variables d'environnement documentées
  - [ ] Migrations à jour
  - [ ] CHANGELOG mis à jour
  - [ ] Version bumped si applicable
- Bloque si un item critique échoue

### `/project:debug`
- Accepte `$ARGUMENTS` comme description du bug
- Processus structuré : reproduction → localisation → analyse root cause → fix → vérification
- Utilise subagents pour investigation (préserve le contexte principal)
- Crée un test de non-régression

## 3. settings.json

### Permissions allow
```
Read(*), Edit(*), Write(*), Grep(*), Glob(*),
WebSearch(*), WebFetch(*), Bash(*), Skill(*)
```

### Permissions deny
**Commandes destructives :**
```
Bash(rmdir *), Bash(sudo *), Bash(su *),
Bash(git push --force *), Bash(git push -f *),
Bash(git reset --hard *), Bash(git clean *),
Bash(git checkout . *), Bash(git checkout -- . *),
Bash(git restore . *), Bash(git branch -D *),
Bash(dd if=*), Bash(mkfs*), Bash(shred *),
Bash(truncate *), Bash(chmod 777 *), Bash(chown *),
Bash(shutdown *), Bash(reboot *), Bash(kill -9 *), Bash(killall *)
```

**Fichiers sensibles :**
```
Read(*.env), Read(.env*), Read(*/.env), Read(**/.env), Read(**/.env.*),
Read(~/.ssh/**), Read(~/.aws/**), Read(**/*.pem), Read(**/*.key),
Edit(*.env), Edit(.env*), Edit(**/.env), Edit(**/.env.*),
Write(*.env), Write(.env*), Write(**/.env), Write(**/.env.*)
```

### Hooks PreToolUse (Bash uniquement)
1. **Blocage destructif** : sudo, dd, mkfs, shred, truncate, chmod 777, chown
2. **Blocage pipe-to-shell** : `curl|bash`, `wget|sh`
3. **Blocage git destructif** : push --force, reset --hard, clean, checkout ., restore .
4. **Warnings** (non-bloquants) : git push, git merge/rebase, rm

## 4. Subagent code-reviewer

Fichier `.claude/agents/code-reviewer.md` :
- Outils autorisés : Read, Grep, Glob, Bash
- Focus : vulnérabilités sécurité (injection, XSS, auth), conventions Solaria, edge cases, qualité des tests
- Produit un rapport avec références de lignes et suggestions de fix
- Rédigé en français

## 5. Skill solaria-conventions

Fichier `.claude/skills/solaria-conventions/SKILL.md` :
- Charte visuelle : coral `#F4815A`, fond parchment `#FDF6EC`, police Outfit
- Ton éditorial : crédible, sobre, jamais startup-hype, pas de langue de bois
- Jamais de statistiques inventées
- Registre professionnel
- Chargé à la demande (pas dans CLAUDE.md = contexte économisé)

## 6. Templates GitHub

### Bug report (`.github/ISSUE_TEMPLATE/bug_report.md`)
Sections : description, étapes de reproduction, comportement attendu, comportement observé, environnement, captures d'écran

### Feature request (`.github/ISSUE_TEMPLATE/feature_request.md`)
Sections : problème, solution proposée, alternatives considérées, contexte additionnel

### PR template (`.github/PULL_REQUEST_TEMPLATE.md`)
Sections : description, type de changement, checklist (tests, lint, docs, review, breaking changes)

Tous en français, ton Solaria.

## 7. Fichiers racine

### README.md
- Présentation du template Solaria
- Instructions d'utilisation (comment créer un nouveau projet)
- Structure du repo expliquée
- Référence aux slash commands disponibles

### LICENSE
MIT, copyright Solaria Advisory

### .gitignore
Multi-stack couvrant : Node.js, Python, Java, Go, Rust, éditeurs (VS Code, JetBrains), OS (.DS_Store, Thumbs.db), environnement (.env, .venv), build (dist, build, out)

## Vérification

1. Initialiser git et créer le premier commit
2. Vérifier que `claude` charge bien le CLAUDE.md au démarrage
3. Tester `/project:init-project` avec un projet fictif
4. Vérifier que les permissions deny bloquent bien `git push --force` (test manuel)
5. Vérifier que le subagent code-reviewer est détecté par Claude Code
6. Confirmer que le skill solaria-conventions se charge quand pertinent
7. Activer "Use this template" sur GitHub après push
