# Changelog

## 1.6.0-beta

Première version de la Carte Enedis Linky V2, reprise de content-card-linky 1.5.6.

### Features

- Type de carte `custom:content-card-linky-v2`, installable à côté de la carte d'origine.
- Période annuelle personnalisée (`annual_period_start`) et camembert Tempo en 6 parts (`showTempoPieChart`).

### Bug Fixes

- EcoWatt : heures lues dans les deux formats d'export, `00 h` (V1) et `0h 00min` (V2). Les cases de 0 h à 9 h et la ligne des heures s'affichent.
- EcoWatt : niveau `0` (production décarbonée chez RTE) affiché en vert.
- Tempo : jours restants affichés au format `restants / quota` avec l'export V2.
