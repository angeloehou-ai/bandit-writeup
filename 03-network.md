# 03 — Réseau (niveaux 14 → 17)

## Niveau 14 → 15 : nc
- `nc localhost 30000` : client TCP brut.
- Envoyer le secret, lire la réponse.

## Niveau 15 → 16 : TLS
- `openssl s_client -connect localhost:30001` : client TLS.
- Handshake → taper le secret.
- **CONNECTED COMMANDS** : `DONE`, `Q`, `R`, `K` agissent sur la connexion, pas sur le serveur.

## Niveau 16 → 17 : scan et tri
- `nmap -p 31000-32000 localhost` : ports ouverts.
- Trier TLS/non-TLS avec `s_client`.
- **Écho** : réponse = envoi → leurre.
- **Bon serveur** : réponse différente (`Correct!`).

## Notions
- `localhost` / `127.0.0.1` : la machine elle-même.
- Port : identifie un service.
- TLS : chiffrement de la connexion.
