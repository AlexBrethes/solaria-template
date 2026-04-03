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
