# 02 — Clés SSH et permissions (niveaux 13 → 17)

## Niveau 13 → 14 : clé privée SSH
- Une clé privée remplace un mot de passe : le serveur garde la **publique**, le client la **privée**.
- `scp -P 2220 user@host:chemin .` : copier un fichier (**-P majuscule** pour scp, **-p minuscule** pour ssh).
- `chmod 600 clé` : SSH refuse une clé lisible par d'autres.
- `ssh -i clé user@host -p 2220`.
- **Piège** : le home Bandit est en lecture seule → copier la clé **côté client**.

## Niveau 14 → 15 : nc
- `nc localhost 30000` : client TCP brut.
- Envoyer le secret, lire la réponse.
- **Piège** : `Ctrl+C` pour sortir.

## Niveau 15 → 16 : service TLS
- `openssl s_client -connect localhost:30001` : client TLS.
- Handshake affiché (certificat, cipher) → taper le secret.
- **Piège** : `DONE` / `Q` / `KEYUPDATE` sont des **CONNECTED COMMANDS** de `s_client` (ferment la connexion).

## Niveau 16 → 17 : scan + TLS
- `nmap -p 31000-32000 localhost` : ports ouverts.
- `echo | openssl s_client -connect localhost:PORT 2>&1 | grep -E "Cipher is|no peer certificate"` : tri TLS/non-TLS.
- **Notion** : un port ouvert n'est pas forcément TLS ; un serveur « écho » renvoie l'entrée.

## Niveau 17 → 18 : diff
- `diff passwords.old passwords.new` : différences ligne par ligne.
- `42c42` = ligne changée ; `<` = 1er fichier, `>` = 2e fichier.
- **Piège** : l'ordre des arguments décide de quel côté est le secret.
