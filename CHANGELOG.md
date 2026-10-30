# Changelog

## 0.3.0

Version stable : regroupe 0.3.0-beta et 0.3.0-beta.2. Notes complètes dans `.github/release-notes/v0.3.0.md` et sur la page de la release.

## 0.3.0-beta.2

### Bug Fixes

- Camembert Tempo sur sa propre ligne, sous les évolutions, avec une légende sur deux colonnes : les textes des évolutions ne sont plus écrasés.

## 0.3.0-beta

### Features

- Page de démonstration (`docs/demo.html`) : la vraie carte avec des données simulées, exports V1 et V2, modes de calcul des prix, Tempo et EcoWatt, thème clair ou sombre.
- Camembert Tempo avec l'export V2 : répartition calculée sur l'historique publié (31 jours) quand les attributs `tempo_percentage_*` sont absents.
- Captures réelles dans le README.

### Bug Fixes

- Camembert Tempo sans données : cercle gris et « Données indisponibles » au lieu d'un cercle entièrement rouge à 0 %.
- Titres des lignes de l'historique (Prix HC, Prix HP…) jamais coupés : les lignes ne se décalent plus quand le camembert réduit la largeur.

## 0.2.0

Première version stable : regroupe les versions 1.6.0-beta à 1.6.0-beta.6. Notes complètes dans `.github/release-notes/v0.2.0.md` et sur la page de la release.

## 1.6.0-beta.6

### Bug Fixes

- Éditeur visuel : les listes déroulantes (nombre de jours, format des jours, calcul des prix) changent de nouveau de valeur. Elles utilisent maintenant `ha-selector`.
- Éditeur visuel rechargé après chaque mise à jour de la carte : le navigateur ne garde plus l'ancienne version en cache.

## 1.6.0-beta.5

### Features

- Éditeur visuel en français, organisé en sections : Général, EcoWatt, Tempo, Prix, Affichage, Évolutions, Historique, EcoWatt et Tempo.
- Réglages de prix dans l'éditeur visuel : calcul des prix (`priceMode`), prix Base, heures creuses et heures pleines (nombre ou entité).
- Interrupteur du camembert Tempo dans l'éditeur visuel.

### Bug Fixes

- Éditeur visuel : le capteur « Tempo informations » choisi s'affiche de nouveau.
- Prix saisis avec une virgule (`0,2016`) acceptés.

## 1.6.0-beta.4

### Features

- Prix calculés par la carte quand l'export ne les fournit pas : formules Base (`kWhPrice`), HC/HP (`kWhPriceHC`, `kWhPriceHP`) et Tempo (prix de la couleur du jour, lus dans `sensor.myelectricaldata_tempo_price_*`). Prix en nombre ou en entité. Option `priceMode` : `auto`, `base`, `hchp`, `tempo` ou `export`.

### Bug Fixes

- `kWhPrice` : le prix par jour de l'historique n'est plus `NaN`.
- Offre Tempo avec l'export V2 : coût du jour en en-tête et lignes Prix, Prix HC et Prix HP renseignés au lieu de 0.00 € et ⚠.

## 1.6.0-beta.3

### Bug Fixes

- Historique : l'unité (`showInTableUnit`) reste sur la même ligne que la valeur, en plus petit. Les lignes du tableau ne se décalent plus quand les colonnes sont étroites.
- EcoWatt : la ligne des heures (01 à 23) s'affiche même quand RTE n'a pas encore publié J+2.
- EcoWatt : un jour pas encore publié par RTE s'affiche en cases grises au lieu d'une barre vide.

## 1.6.0-beta.2

### Bug Fixes

- Type de carte renommé `custom:content-card-linky-classic` : `custom:content-card-linky-v2` est déjà réservé par la carte Linky New, qui s'affichait à la place quand elle est installée.

## 1.6.0-beta

Première version de la Carte Enedis Linky V2, reprise de content-card-linky 1.5.6.

### Features

- Type de carte `custom:content-card-linky-v2`, installable à côté de la carte d'origine.
- Période annuelle personnalisée (`annual_period_start`) et camembert Tempo en 6 parts (`showTempoPieChart`).

### Bug Fixes

- EcoWatt : heures lues dans les deux formats d'export, `00 h` (V1) et `0h 00min` (V2). Les cases de 0 h à 9 h et la ligne des heures s'affichent.
- EcoWatt : niveau `0` (production décarbonée chez RTE) affiché en vert.
- Tempo : jours restants affichés au format `restants / quota` avec l'export V2.
