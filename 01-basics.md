# 01 — Bases du shell (niveaux 0 → 13)

## Niveau 0 → 1 : ssh, ls, cat
- `ssh user@host -p 2220` : connexion distante (port 2220).
- `ls` : lister ; `cat fichier` : afficher le contenu.

## Niveau 1 → 2 : fichier nommé `-`
- Un fichier nommé `-` est interprété comme stdin par `cat`.
- **Solution** : `cat ./-` (préfixer par `./`).

## Niveau 2 → 3 : espaces dans le nom
- `cat "fichier avec espaces"` ou `cat fichier\ avec\ espaces`.

## Niveau 3 → 4 : fichier caché
- `ls -a` affiche les fichiers commençant par `.`.

## Niveau 4 → 5 : fichier lisible
- `file ./*` : identifier le type de chaque fichier.
- Repérer celui qui est « ASCII text ».

## Niveau 5 → 6 : find
- `find . -type f -size 1033c ! -executable`
- `-type f` fichier, `-size 1033c` taille exacte en octets, `! -executable` non exécutable.

## Niveau 6 → 7 : find dans tout le système
- `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`
- `2>/dev/null` masque les erreurs de permission.

## Niveau 7 → 8 : grep
- `grep "motif" fichier` : filtrer les lignes contenant le motif.

## Niveau 8 → 9 : sort | uniq -u
- `sort fichier | uniq -u` : lignes uniques.
- **Piège** : `uniq` ne détecte que les doublons **adjacents** → `sort` d'abord.

## Niveau 9 → 10 : strings
- `strings fichier | grep "=="` : extraire le texte lisible d'un binaire.

## Niveau 10 → 11 : base64
- `base64 -d fichier` : décoder.
- **Notion** : l'encodage n'est **pas** du chiffrement (aucune clé).

## Niveau 11 → 12 : ROT13
- `tr 'A-Za-z' 'N-ZA-Mn-za-m'` : ROT13.
- **Notion** : substitution, aucune clé → ce n'est pas un vrai chiffrement.

## Niveau 12 → 13 : archives multiples
- `mktemp -d` : dossier temporaire.
- `xxd -r` : convertir un hexdump en binaire.
- Boucle : `file` → `gzip -d` / `bzip2 -d` / `tar xf`.
- **Pièges** : renommer avec la bonne extension pour gzip/bzip2 ; `tar tf` pour lister avant d'extraire.
