# DEVLOG — claude-workflow

## Session 3 — Consolidation DEVLOG + workflow multi-session

**Décisions :**
- Remplacement des fichiers `contexte-conversation_*.md` par un unique `DEVLOG.md` consolidé
- Workflow : DEVLOG.md régénéré en fin de chaque session + livré à Claude Code pour commit/push
- Instructions projet mises à jour avec section "Fin de session"

**TODO :** aucun.

---

## Session 4 — Séparation Partie 1 / Partie 2 dans CLAUDE_WEB.md

**Décisions :**
- CLAUDE_WEB.md restructuré en deux parties : Partie 1 (bonnes pratiques génériques) / Partie 2 (specs techniques projet)
- Incident : instructions Claude Code transmises au mauvais projet → rollback `git reset --hard HEAD~1 --force`

**TODO :** aucun.

---

## Session 5 — Exploration GitHub via API + création CLAUDE_WEB.md

**Décisions :**
- Exploration GitHub via API publique : Claude génère l'URL, l'utilisateur la colle une fois, Claude fetche librement ensuite
- `REPO.md` abandonné → remplacé par l'approche API à la demande
- Création `CLAUDE_WEB.md` : instructions architecte séparées de `CLAUDE.md`
- Règle : `CLAUDE.md` = Claude Code uniquement
- Reformatage dense/machine pour lecture agent

**TODO :** aucun.

---

## Session 6 — Extraction workflow générique → repo claude-workflow

**Décisions :**
- Création du repo `claude-workflow` pour centraliser la Partie 1 générique — réutilisable sur tous les projets futurs
- Chaque projet ne conserve que la Partie 2 specs dans son `CLAUDE_WEB.md`
- `CLAUDE.md` générique centralisé ici, chaque projet ajoute ses commandes spécifiques

**TODO :** aucun.

---

## Session 7 — Correction incident + règle fetch clarifiée

**Décisions :**
- Incident session 6 : Claude Code avait pushé les fichiers claude-workflow sur main de dan-immersive → corrigé via `git reset --hard HEAD~1` + force push sur dev et main
- Règle fetch clarifiée : l'utilisateur colle une URL du repo une fois en début de session → Claude fetche librement toutes les URLs dérivées sans redemander
- Règle ajoutée dans CLAUDE_WEB.md section "RÈGLE EXPLORATION GITHUB"

**TODO :** aucun.

---

## Session 7 — Correction incident git + règle fetch clarifiée

**Décisions :**
- Diagnostic incident : commits corrompus sur main et dev de dan-immersive → `git reset --hard` + force push
- Règle fetch clarifiée : l'utilisateur colle une URL du repo une fois en début de session → Claude fetche librement toutes les URLs dérivées sans redemander
- Règle ajoutée dans CLAUDE_WEB.md section "RÈGLE EXPLORATION GITHUB"
- Livrable DEVLOG : diff uniquement (bloc à ajouter), pas le fichier entier régénéré → ajouté dans CLAUDE_WEB.md section "FIN DE SESSION — DEVLOG"

**TODO :** aucun.

---

## Session 9 — Format livrable XML + versioning PART1

**Décisions :**
- PART1_VERSION ajouté en tête de CLAUDE_WEB.md (semver, ex: 1.0) — permet de vérifier la sync entre référence claude-workflow et instructions projet sur claude.ai
- Format livrable Claude Code migré vers balises XML : <file path="..." action="replace|modify|create|delete"> — élimine les conflits de délimiteurs markdown pour tout type de fichier (.md, .html, .js, etc.)
- Règles GitHub clarifiées : Claude ne peut pas accéder seul à un repo — URL fournie par l'utilisateur via widget Q&R (minimum 2 options pour affichage)
- Workflow session mis à jour : confirmation sync git + annonce PART1_VERSION en SETUP
- Avant livrable : Claude demande confirmation repo + branche active en local
- Comportement face aux questionnements : Claude étudie et justifie avant de valider ou maintenir sa position
- Branche dev créée sur claude-workflow
- CLAUDE.md mis à jour avec le nouveau format XML

**Paramètres modifiés :** CLAUDE_WEB.md, CLAUDE.md

**Bugs résolus :** Widget Q&R avec une seule option ne s'affiche pas — ajouter option "Annuler" comme fallback

**TODO :** aucun.

---

## Session 10 — Restructuration CLAUDE_WEB.md + glossaire entités

**Décisions :**
- CLAUDE_WEB.md restructuré en 6 sections avec sous-sections — logique : contexte → rôle → comportements → règles → workflow → format livrable
- Ajout section 1. CONTEXTE : glossaire 11 entités métier + flux de mise à jour
- Ajout section 3. COMPORTEMENTS & EXPRESSIONS : communication, compréhension du besoin, rigueur analytique, interactions GitHub
- GITHUB_USERNAME remplace URL_REFERENCE — Claude construit les URLs à partir du username
- Suppression des endpoints utiles — surcharge de contexte inutile
- Workflow session enrichi : étape 5.2 DÉFINITION DU BESOIN ajoutée — la génération du livrable est la dernière étape
- PART1_VERSION passée à 1.1

**Paramètres modifiés :** CLAUDE_WEB.md

**Bugs résolus :** aucun

**TODO :** aucun

---

## Session 11 — Refonte workflow SETUP + fiabilité fetch GitHub

**Décisions :**
- Le fetch GitHub depuis claude.ai est non fiable en raison du cache CDN — `raw.githubusercontent.com` retourne une version obsolète indépendamment du cache-busting par query string
- L'API GitHub (`api.github.com`) retourne le bon contenu mais en base64, ce qui représente un coût token 5x supérieur au contenu brut — écarté
- Le canal retenu pour lire les fichiers GitHub est le collage du contenu par l'utilisateur — Claude fournit l'URL à copier-coller
- Claude peut lire `PART1_VERSION` directement depuis le system prompt actif — la règle inverse présente dans la version 1.0 repo était incorrecte
- Le SETUP intègre désormais une demande de confirmation de synchronisation des fichiers du projet claude.ai via le bouton de synchronisation GitHub natif
- La section 3.4 Interactions GitHub (widget Q&R pour les URLs) est supprimée — remplacée par la fourniture d'URLs en texte brut pour faciliter le copier-coller
- Le widget Q&R ne peut pas servir à transmettre une URL pour `web_fetch` — l'URL doit être présente en texte brut dans le chat au moment du fetch

**Paramètres modifiés :** CLAUDE_WEB.md (PART1_VERSION 1.1 → 1.2), sections 3.4 supprimée, 4.3 reformulée, 5.1 restructurée

**Bugs résolus :** Fausse alerte désynchronisation PART1_VERSION en début de session causée par le cache CDN GitHub

**TODO :** aucun
