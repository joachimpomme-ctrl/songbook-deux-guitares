# Songbook Deux Guitares — règles de contribution

Site statique en un fichier (`index.html`), publié par GitHub Pages depuis `main`.
PWA : `sw.js`, `manifest.webmanifest`, `icon.svg`.

## Règles sur les morceaux (impératives)

1. **Grilles complètes** : chaque morceau ajouté doit couvrir toutes ses sections
   (couplet, refrain, pont, coda…), pas seulement une boucle. Pour les standards
   de jazz, une section A seule est tolérée uniquement si la `note:` le dit
   explicitement.
2. **Grilles vérifiées** : toute grille nouvelle ou modifiée doit être vérifiée
   contre au moins une source (recherche web de la partition/tablature), jamais
   écrite de mémoire seule. Mentionner les sources dans la réponse à l'utilisateur.
3. **Format** (le rendu casse en silence sinon) :
   - Exactement **4 mesures par système** (`grid` CSS en `repeat(4,1fr)`).
   - Tout accord d'une grille doit figurer dans le tableau `chords:` du morceau
     **et** dans le dictionnaire `CHORDS`.
   - Séparateur de deux accords dans une mesure : point médian ` · ` entouré d'espaces.
   - Pas de `/` dans un nom d'accord sauf vraie basse étrangère (le générateur de
     basse lit `tok.split("/")[1]` comme note de basse).
   - Toute nouvelle `zone` doit avoir son entrée dans `GROOVE_DEFAULTS`.
4. **Groove et basse** : ajouter une entrée `GROOVE_BY_TITLE` si le morceau n'est
   pas un 4/4 standard de sa zone ; forcer `BASS_FEEL` si le feel déduit est faux
   (ex. ballade jazz → `root5` pour éviter la walking).
5. **Pas de doublon de grille** : deux morceaux à grille identique doivent être
   soit différenciés (tonalité réelle), soit explicitement croisés dans leurs tips.

## Validation avant tout commit

Extraire le `<script>` dans un fichier Node avec un stub `document`/`localStorage`,
puis vérifier : nombre de cartes = nombre de morceaux = bandeaux rythmiques =
blocs « Ligne de basse » ; 0 `undefined` ; 0 case de tablature à deux chiffres ;
0 système ≠ 4 mesures ; 0 accord manquant/non listé ; 0 titre en double ;
0 orphelin dans `GROOVE_BY_TITLE`/`BASS_FEEL`. Contrôler aussi la page dans un
navigateur (0 erreur console, pas de débordement horizontal à 320 px).

## Publication

Travailler sur la branche `claude/...` désignée, puis fast-forward `main`
(`git checkout main && git merge --ff-only <branche> && git push origin main`)
— le site sert `main`. Revenir ensuite sur la branche de travail.
