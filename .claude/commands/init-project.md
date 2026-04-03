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
4. Configure le linting adapté à la stack :
   - **Python** : créer `pyproject.toml` avec section `[tool.ruff]`, ajouter un hook PostToolUse dans `.claude/settings.json` qui lance `ruff check` après chaque édition de fichier `.py`
   - **JavaScript/TypeScript** : créer `eslint.config.js` minimal, ajouter un hook PostToolUse qui lance `npx eslint` après chaque édition de fichier `.ts`/`.tsx`/`.js`/`.jsx`
   - **Go** : ajouter un hook PostToolUse qui lance `go vet` après chaque édition de fichier `.go`
   - **Autre stack** : demander à l'utilisateur quel linter utiliser et configurer le hook correspondant
5. Si git n'est pas initialisé, lance `git init && git branch -m main`
6. Crée un commit : `init: initialisation du projet <nom>`

IMPORTANT : ne pas inventer de contenu. Utiliser uniquement les réponses de l'utilisateur.
