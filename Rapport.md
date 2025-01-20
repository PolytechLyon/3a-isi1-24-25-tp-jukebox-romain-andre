# Compte Rendu TP Jukebox

## Binôme
- Aillaud Romain
- da Conceição André

## Choix de conception et de réalisation

Recommandation : utiliser mozilla firefox pour un meilleur rendu graphique des CSS

Nous avons décidé de séparer l'application en plusieurs vues :

- `AudioController.vue`
- `Playlist.vue`
- `PlaylistItem.vue`
- `AddMusicForm.vue`

La vue principale `App.vue` permet d'importer et d'utiliser toutes ces vues.


Les sons défectueux sont marqués par une couleur d'arrière plan rouge sur le son.

## Difficultés rencontrées (optionnel)

L'utilisation des ref() réactive à été l'une des principales difficultés rencontrés. 


## Extensions réalisées (optionnel)

- Les musiques ajoutées par URL sont conservées après chaque rechargement.