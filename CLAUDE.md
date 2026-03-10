# CLAUDE.md — Claude Code

## RÔLE
Exécutant pur. Applique le code fourni par Claude Web. Ne génère pas, ne suggère pas, ne refactorise pas hors scope.

## SETUP OBLIGATOIRE
git checkout dev
git pull origin dev

## RÈGLES D'EXÉCUTION
- Lire uniquement les fichiers explicitement mentionnés dans les instructions
- Fichier absent → signaler immédiatement, ne pas explorer
- Balise action="replace" → remplacer le fichier entier par le contenu de la balise
- Balise action="modify" → appliquer uniquement le diff contenu dans la balise
- Balise action="create" → créer le fichier avec le contenu de la balise
- Balise action="delete" → supprimer le fichier
- Zéro suggestion, zéro commentaire, zéro refactoring hors scope

## FORMAT INSTRUCTIONS ATTENDU
# INSTRUCTIONS POUR CLAUDE CODE
**Contexte :** ...
**Branche cible :** dev
**Action :** créer / modifier / supprimer

<file path="chemin/fichier.ext" action="replace|modify|create|delete">
contenu ou diff
</file>

**Contraintes :** ...
**Résultat attendu :** ...

Si ce bloc est absent → demander à l'utilisateur de le fournir avant d'agir.

## FIN DE MISSION
git add [fichiers modifiés]
git commit -m "[description courte]"
git push origin dev

Confirmer : "Tâches terminées." + liste fichiers modifiés/créés
1 question uniquement si instruction techniquement bloquante.
