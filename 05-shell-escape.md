# 05 — Évasion de shell (niveaux 25 → 26, 32 → 33)

## Niveau 25 → 26 : more → vim → shell
- `/etc/passwd` : le shell de bandit26 est `showtext` (pas bash).
- `showtext` lance `more ~/text.txt`.
- **Astuce** : réduire la fenêtre à 3-4 lignes → `more` reste interactif (`--More--`).
- `v` dans `more` → `vim` ; `:set shell=/bin/bash` puis `:shell` → bash complet.
- **Notions** : évasion de shell restreint via pager/éditeur ; `stty rows 4` pour forcer la hauteur.

## Niveau 32 → 33 : UPPERCASE SHELL
- Le shell convertit l'entrée en MAJUSCULES → `ls` devient `LS` → échec.
- `$0` : variable spéciale = nom du shell → relance un shell normal.
- `whoami` → `bandit33` (binaire setuid).
- **Notion** : un filtre naïf ne bloque pas les expansions de variables.
