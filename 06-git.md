# 06 — Git (niveaux 27 → 32)

## Niveau 27 → 28 : clone
- `git clone ssh://user@host:2220/chemin/repo` : le port est **dans l'URL**.
- `cd repo`, `ls -la`, `cat README`.
- **Piège** : cloner **depuis sa machine locale**, pas depuis le serveur.

## Niveau 28 → 29 : historique
- README caviardé (`********`).
- `git log` : commits ; `git show <hash>` : diff (`-` retiré, `+` ajouté).
- `git log -p` : historique avec diffs.
- **Notion** : un secret supprimé **reste** dans l'historique.

## Niveau 29 → 30 : branches
- `git branch -a` : branches locales et distantes.
- `git checkout <branche>` : changer de branche ; relire `README.md`.
- `git log --all` : historique de toutes les branches.
- **Notion** : un secret peut être sur une branche « oubliée ».

## Niveau 30 → 31 : tags
- `git tag` : liste des tags.
- `git show <tag>` : message du tag (annoté) + contenu.
- `git show-ref`, `git cat-file -p <hash>`, `git fsck --lost-found` : objets non référencés.
- **Notion** : un tag annoté peut contenir un secret dans son message.

## Niveau 31 → 32 : push
- `git clone ... repo31`, `cat README.md` : fichier/contenu/branche à pousser.
- `.gitignore` (`*.txt`) → `git add -f key.txt` pour forcer.
- `git config --global user.name/user.email` : requis pour commiter.
- `git commit -m "..."`, `git push origin master`.
- **Notion** : hook `post-receive` côté serveur → réponse après push.
