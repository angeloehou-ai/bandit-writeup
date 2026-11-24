# 04 — Cron, setuid, brute-force (niveaux 19 → 25)

## Niveau 19 → 20 : setuid
- `ls -la` : repérer le binaire avec `s` dans les permissions (`-rwsr-x---`).
- `./binaire` sans argument → mode d'emploi.
- `./binaire cat /etc/bandit_pass/bandit20` : exécute `cat` avec les droits du propriétaire.
- **Notion** : setuid = exécution avec les droits du **propriétaire** du binaire.

## Niveau 20 → 21 : client/serveur
- `nc -lvnp 1234` : serveur en écoute.
- `./binaire 1234` : client setuid qui se connecte au port.
- Envoyer le secret au serveur → le binaire compare et renvoie le suivant.
- **Notion** : job control (`&`, `jobs`, `fg`, `bg`, `Ctrl+Z`).

## Niveau 21 → 22 : cron
- `ls /etc/cron.d/` : tâches planifiées.
- `cat /etc/cron.d/<fichier>` : commande exécutée et utilisateur.
- `cat /usr/bin/<script>.sh` : logique du script.
- **Format cron** : `* * * * *` = chaque minute (minute, heure, jour, mois, jour de semaine).

## Niveau 22 → 23 : nom de fichier dérivé
- Le script calcule un nom via `whoami` + `md5sum`.
- **Piège** : exécuter le script soi-même change `whoami` → mauvais hash.
- Recalculer : `echo "I am user bandit23" | md5sum`.

## Niveau 23 → 24 : écrire son propre script
- Créer un script dans /tmp qui lit /etc/bandit_pass/bandit24 et l'écrit dans un fichier lisible.
- `chmod +x` le script, `chmod 777` le dossier de sortie, `cp` dans le dossier cron.
- **Notions** : script supprimé après exécution → garder une copie ; `nano` peut échouer sans `~/.local` → heredoc.

## Niveau 24 → 25 : brute-force
- `seq -w 0000 9999` : 10000 PIN à largeur fixe.
- Pipe vers `nc` : **une seule** connexion.
- `grep -v "Wrong"` : filtrer les échecs.
- **Notion** : brute-force = essayer toutes les combinaisons ; coûteux en réel.
